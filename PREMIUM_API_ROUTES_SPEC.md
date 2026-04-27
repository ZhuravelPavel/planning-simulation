# BDSMLR Premium API Routes Specification
**Version:** 1.0  
**Date:** April 27, 2026  
**Status:** Draft for Developer Review

---

## Overview

This document specifies new API routes required for **Product B: BDSMLR Premium** features (collections, downloads, bookmarks, ad-free).

**Base URL:** `https://api-dev.bdsmlr.com` (dev), `https://api-prod.bdsmlr.com` (prod)

**Authentication:** All premium routes require:
- Valid session token (existing auth)
- Active premium subscription (WordPress subscription check)

---

## Authentication Flow

### Premium Status Check

**Endpoint:** `GET /subscription/status`

**Purpose:** Check if current user has active premium subscription

**Request:**
```http
GET /subscription/status
Authorization: Bearer {session_token}
```

**Response (FREE user):**
```json
{
  "user_id": "12345",
  "blog_name": "nonnudecuties",
  "subscription": {
    "active": false,
    "plan": "free",
    "capabilities": []
  }
}
```

**Response (PREMIUM user):**
```json
{
  "user_id": "12345",
  "blog_name": "nonnudecuties",
  "subscription": {
    "active": true,
    "plan": "bdsmlr_premium",
    "price": "$10/month",
    "payment_processor": "ccbill",
    "expires_at": "2026-05-27T16:50:00Z",
    "capabilities": [
      "collections",
      "downloads",
      "bookmarks",
      "ad_free",
      "search_advanced",
      "search_unlimited"
    ]
  }
}
```

**Error (401 Unauthorized):**
```json
{
  "error": "unauthorized",
  "message": "Valid session required"
}
```

---

## Collections

**Feature:** Users can create collections (folders) to organize saved posts

### List Collections

**Endpoint:** `GET /collections`

**Auth:** Premium subscription required

**Request:**
```http
GET /collections
Authorization: Bearer {session_token}
```

**Response (200 OK):**
```json
{
  "collections": [
    {
      "id": "coll_123abc",
      "name": "Favorites",
      "description": "My favorite posts",
      "post_count": 45,
      "created_at": "2026-01-15T10:30:00Z",
      "updated_at": "2026-04-20T14:22:00Z",
      "thumbnail": "https://cdn.bdsmlr.com/thumb/coll_123abc.jpg"
    },
    {
      "id": "coll_456def",
      "name": "Inspiration",
      "description": null,
      "post_count": 12,
      "created_at": "2026-02-10T08:15:00Z",
      "updated_at": "2026-04-25T11:05:00Z",
      "thumbnail": null
    }
  ],
  "total": 2
}
```

**Error (403 Forbidden - Not Premium):**
```json
{
  "error": "premium_required",
  "message": "Collections require BDSMLR Premium subscription",
  "upgrade_url": "https://bdsmlr.com/premium"
}
```

---

### Get Collection Details

**Endpoint:** `GET /collections/:id`

**Auth:** Premium subscription required

**Request:**
```http
GET /collections/coll_123abc
Authorization: Bearer {session_token}
```

**Query Params (optional):**
- `limit` (int, default: 50, max: 100) - Posts per page
- `offset` (int, default: 0) - Pagination offset
- `sort` (string, default: "added_desc") - Sort order
  - `added_desc` - Most recently added first
  - `added_asc` - Oldest added first
  - `popular` - Most liked/reblogged first

**Response (200 OK):**
```json
{
  "id": "coll_123abc",
  "name": "Favorites",
  "description": "My favorite posts",
  "post_count": 45,
  "created_at": "2026-01-15T10:30:00Z",
  "updated_at": "2026-04-20T14:22:00Z",
  "posts": [
    {
      "post_id": "521053899",
      "added_at": "2026-04-20T14:22:00Z",
      "post_data": {
        "id": "521053899",
        "blog_name": "example-blog",
        "content": "...",
        "media": [...],
        "created_at": "2026-04-15T12:00:00Z"
      }
    }
  ],
  "pagination": {
    "limit": 50,
    "offset": 0,
    "total": 45,
    "has_more": false
  }
}
```

**Error (404 Not Found):**
```json
{
  "error": "not_found",
  "message": "Collection not found"
}
```

---

### Create Collection

**Endpoint:** `POST /collections`

**Auth:** Premium subscription required

**Request:**
```http
POST /collections
Authorization: Bearer {session_token}
Content-Type: application/json

{
  "name": "New Collection",
  "description": "Optional description"
}
```

**Response (201 Created):**
```json
{
  "id": "coll_789ghi",
  "name": "New Collection",
  "description": "Optional description",
  "post_count": 0,
  "created_at": "2026-04-27T16:50:00Z",
  "updated_at": "2026-04-27T16:50:00Z",
  "thumbnail": null
}
```

**Error (400 Bad Request):**
```json
{
  "error": "validation_error",
  "message": "Collection name is required",
  "field": "name"
}
```

---

### Update Collection

**Endpoint:** `PATCH /collections/:id`

**Auth:** Premium subscription required, must own collection

**Request:**
```http
PATCH /collections/coll_123abc
Authorization: Bearer {session_token}
Content-Type: application/json

{
  "name": "Updated Name",
  "description": "Updated description"
}
```

**Response (200 OK):**
```json
{
  "id": "coll_123abc",
  "name": "Updated Name",
  "description": "Updated description",
  "post_count": 45,
  "created_at": "2026-01-15T10:30:00Z",
  "updated_at": "2026-04-27T16:55:00Z",
  "thumbnail": "https://cdn.bdsmlr.com/thumb/coll_123abc.jpg"
}
```

---

### Delete Collection

**Endpoint:** `DELETE /collections/:id`

**Auth:** Premium subscription required, must own collection

**Request:**
```http
DELETE /collections/coll_123abc
Authorization: Bearer {session_token}
```

**Response (204 No Content):**
```
(empty body)
```

**Note:** Deleting a collection does NOT delete the posts, only the collection itself.

---

### Add Post to Collection

**Endpoint:** `POST /collections/:id/posts`

**Auth:** Premium subscription required, must own collection

**Request:**
```http
POST /collections/coll_123abc/posts
Authorization: Bearer {session_token}
Content-Type: application/json

{
  "post_id": "521053899"
}
```

**Response (201 Created):**
```json
{
  "collection_id": "coll_123abc",
  "post_id": "521053899",
  "added_at": "2026-04-27T16:58:00Z"
}
```

**Error (409 Conflict - Already in collection):**
```json
{
  "error": "already_exists",
  "message": "Post already in this collection"
}
```

---

### Remove Post from Collection

**Endpoint:** `DELETE /collections/:id/posts/:post_id`

**Auth:** Premium subscription required, must own collection

**Request:**
```http
DELETE /collections/coll_123abc/posts/521053899
Authorization: Bearer {session_token}
```

**Response (204 No Content):**
```
(empty body)
```

---

## Downloads

**Feature:** Users can download posts (images, videos) for offline viewing

### List Downloads

**Endpoint:** `GET /downloads`

**Auth:** Premium subscription required

**Request:**
```http
GET /downloads
Authorization: Bearer {session_token}
```

**Query Params (optional):**
- `limit` (int, default: 50, max: 100)
- `offset` (int, default: 0)
- `sort` (string, default: "downloaded_desc")
  - `downloaded_desc` - Most recently downloaded first
  - `downloaded_asc` - Oldest downloaded first

**Response (200 OK):**
```json
{
  "downloads": [
    {
      "post_id": "521053899",
      "downloaded_at": "2026-04-27T10:30:00Z",
      "file_count": 3,
      "total_size_bytes": 15728640,
      "post_data": {
        "id": "521053899",
        "blog_name": "example-blog",
        "content": "...",
        "media": [...]
      }
    }
  ],
  "pagination": {
    "limit": 50,
    "offset": 0,
    "total": 1,
    "has_more": false
  },
  "stats": {
    "total_downloads": 1,
    "total_size_bytes": 15728640,
    "total_size_human": "15 MB"
  }
}
```

---

### Download Post

**Endpoint:** `POST /downloads`

**Auth:** Premium subscription required

**Request:**
```http
POST /downloads
Authorization: Bearer {session_token}
Content-Type: application/json

{
  "post_id": "521053899"
}
```

**Response (200 OK):**
```json
{
  "post_id": "521053899",
  "download_url": "https://cdn.bdsmlr.com/downloads/521053899.zip?token=xyz&expires=1619537400",
  "expires_at": "2026-04-27T17:10:00Z",
  "files": [
    {
      "filename": "image1.jpg",
      "size_bytes": 5242880,
      "url": "https://cdn.bdsmlr.com/downloads/521053899/image1.jpg?token=xyz"
    },
    {
      "filename": "image2.jpg",
      "size_bytes": 5242880,
      "url": "https://cdn.bdsmlr.com/downloads/521053899/image2.jpg?token=xyz"
    },
    {
      "filename": "video.mp4",
      "size_bytes": 5242880,
      "url": "https://cdn.bdsmlr.com/downloads/521053899/video.mp4?token=xyz"
    }
  ],
  "total_size_bytes": 15728640,
  "total_size_human": "15 MB"
}
```

**Note:** 
- `download_url` is a ZIP file containing all media from the post
- Individual file URLs are also provided
- URLs expire after 10 minutes (for security)

**Error (404 Not Found - Post deleted):**
```json
{
  "error": "not_found",
  "message": "Post not found or has been deleted"
}
```

---

### Delete Download Record

**Endpoint:** `DELETE /downloads/:post_id`

**Auth:** Premium subscription required

**Request:**
```http
DELETE /downloads/521053899
Authorization: Bearer {session_token}
```

**Response (204 No Content):**
```
(empty body)
```

**Note:** This only removes the download record (history), not the actual files on user's device.

---

## Bookmarks

**Feature:** Quick-save posts for later viewing (simpler than collections)

### List Bookmarks

**Endpoint:** `GET /bookmarks`

**Auth:** Premium subscription required

**Request:**
```http
GET /bookmarks
Authorization: Bearer {session_token}
```

**Query Params (optional):**
- `limit` (int, default: 50, max: 100)
- `offset` (int, default: 0)
- `sort` (string, default: "bookmarked_desc")
  - `bookmarked_desc` - Most recently bookmarked first
  - `bookmarked_asc` - Oldest bookmarked first

**Response (200 OK):**
```json
{
  "bookmarks": [
    {
      "post_id": "521053899",
      "bookmarked_at": "2026-04-27T11:00:00Z",
      "post_data": {
        "id": "521053899",
        "blog_name": "example-blog",
        "content": "...",
        "media": [...]
      }
    }
  ],
  "pagination": {
    "limit": 50,
    "offset": 0,
    "total": 1,
    "has_more": false
  }
}
```

---

### Add Bookmark

**Endpoint:** `POST /bookmarks`

**Auth:** Premium subscription required

**Request:**
```http
POST /bookmarks
Authorization: Bearer {session_token}
Content-Type: application/json

{
  "post_id": "521053899"
}
```

**Response (201 Created):**
```json
{
  "post_id": "521053899",
  "bookmarked_at": "2026-04-27T17:00:00Z"
}
```

**Error (409 Conflict - Already bookmarked):**
```json
{
  "error": "already_exists",
  "message": "Post already bookmarked"
}
```

---

### Remove Bookmark

**Endpoint:** `DELETE /bookmarks/:post_id`

**Auth:** Premium subscription required

**Request:**
```http
DELETE /bookmarks/521053899
Authorization: Bearer {session_token}
```

**Response (204 No Content):**
```
(empty body)
```

---

### Check if Post is Bookmarked

**Endpoint:** `GET /bookmarks/:post_id`

**Auth:** Premium subscription required

**Request:**
```http
GET /bookmarks/521053899
Authorization: Bearer {session_token}
```

**Response (200 OK - Bookmarked):**
```json
{
  "bookmarked": true,
  "post_id": "521053899",
  "bookmarked_at": "2026-04-27T11:00:00Z"
}
```

**Response (200 OK - Not Bookmarked):**
```json
{
  "bookmarked": false,
  "post_id": "521053899"
}
```

---

## Ad-Free Experience

**Feature:** Premium users don't see ads

**Implementation:** Client-side check

**Frontend Logic:**
```javascript
// React frontend checks subscription status
const { subscription } = await fetch('/subscription/status');

if (subscription.capabilities.includes('ad_free')) {
  // Don't render ad components
  return null;
} else {
  // Render ads for free users
  return <AdComponent />;
}
```

**No new API routes needed** - uses existing `/subscription/status` endpoint.

---

## Premium Search Gating

**Feature:** Advanced search filters for premium users

**Existing Routes (from CSV):**
- `/search?q=query&sort=popular` (PAID)
- `/search?q=query&sort=liked` (PAID)
- `/search?q=query&sort=reblogged` (PAID)
- `/search?q=query&sort=commented` (PAID)

**Implementation:** API checks subscription status before allowing advanced sorts

**FREE users request:**
```http
GET /search?q=bikini&sort=popular
Authorization: Bearer {free_user_token}
```

**Response (403 Forbidden):**
```json
{
  "error": "premium_required",
  "message": "Advanced search sorting requires BDSMLR Premium",
  "upgrade_url": "https://bdsmlr.com/premium",
  "allowed_sorts": ["newest", "oldest"],
  "premium_sorts": ["popular", "liked", "reblogged", "commented"]
}
```

**PREMIUM users request:**
```http
GET /search?q=bikini&sort=popular
Authorization: Bearer {premium_user_token}
```

**Response (200 OK):**
```json
{
  "results": [...],
  "pagination": {...}
}
```

---

## Premium Search - Unlimited Results

**Feature:** Free users limited to 50 results, premium users get unlimited

**FREE users request (>50 results):**
```http
GET /search?q=bikini&limit=100
Authorization: Bearer {free_user_token}
```

**Response (200 OK with limit override):**
```json
{
  "results": [...50 results...],
  "pagination": {
    "limit": 50,
    "offset": 0,
    "total": 1500,
    "has_more": true,
    "message": "Free tier limited to 50 results. Upgrade to Premium for unlimited results.",
    "upgrade_url": "https://bdsmlr.com/premium"
  }
}
```

**PREMIUM users request:**
```http
GET /search?q=bikini&limit=1000
Authorization: Bearer {premium_user_token}
```

**Response (200 OK):**
```json
{
  "results": [...1000 results...],
  "pagination": {
    "limit": 1000,
    "offset": 0,
    "total": 1500,
    "has_more": true
  }
}
```

---

## Database Schema (for Developer Reference)

### Collections Table
```sql
CREATE TABLE collections (
  id VARCHAR(255) PRIMARY KEY,
  user_id VARCHAR(255) NOT NULL,
  blog_name VARCHAR(255) NOT NULL,
  name VARCHAR(255) NOT NULL,
  description TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  INDEX idx_user_id (user_id),
  INDEX idx_blog_name (blog_name)
);
```

### Collection Posts Table (Join Table)
```sql
CREATE TABLE collection_posts (
  collection_id VARCHAR(255) NOT NULL,
  post_id VARCHAR(255) NOT NULL,
  added_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (collection_id, post_id),
  FOREIGN KEY (collection_id) REFERENCES collections(id) ON DELETE CASCADE,
  INDEX idx_collection_id (collection_id),
  INDEX idx_post_id (post_id)
);
```

### Downloads Table
```sql
CREATE TABLE downloads (
  user_id VARCHAR(255) NOT NULL,
  blog_name VARCHAR(255) NOT NULL,
  post_id VARCHAR(255) NOT NULL,
  downloaded_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (user_id, post_id),
  INDEX idx_user_id (user_id),
  INDEX idx_blog_name (blog_name),
  INDEX idx_downloaded_at (downloaded_at)
);
```

### Bookmarks Table
```sql
CREATE TABLE bookmarks (
  user_id VARCHAR(255) NOT NULL,
  blog_name VARCHAR(255) NOT NULL,
  post_id VARCHAR(255) NOT NULL,
  bookmarked_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (user_id, post_id),
  INDEX idx_user_id (user_id),
  INDEX idx_blog_name (blog_name),
  INDEX idx_bookmarked_at (bookmarked_at)
);
```

---

## Error Codes Reference

| Code | HTTP Status | Meaning |
|------|-------------|---------|
| `unauthorized` | 401 | No valid session token |
| `premium_required` | 403 | Feature requires premium subscription |
| `forbidden` | 403 | User doesn't own this resource |
| `not_found` | 404 | Resource doesn't exist |
| `already_exists` | 409 | Duplicate resource (e.g., already bookmarked) |
| `validation_error` | 400 | Invalid input data |
| `rate_limit_exceeded` | 429 | Too many requests |
| `internal_error` | 500 | Server error |

---

## Rate Limiting

**Premium users:** 1000 requests/hour  
**Free users:** 100 requests/hour

**Exceeded:**
```json
{
  "error": "rate_limit_exceeded",
  "message": "Rate limit exceeded. Try again in 15 minutes.",
  "retry_after": 900,
  "limit": 100,
  "reset_at": "2026-04-27T18:00:00Z"
}
```

---

## Next Steps

1. **Developer Review:** Review this spec for technical feasibility
2. **Database Setup:** Create tables for collections, downloads, bookmarks
3. **WordPress Integration:** Implement `/subscription/status` endpoint that checks WordPress subscriptions
4. **Route Implementation:** Build the premium routes (Week 10-12)
5. **Testing:** Test all routes on api-dev before deploying to api-prod
6. **Frontend Integration:** React frontend consumes these routes (Week 10-12)

---

**Questions or Concerns:** Contact Product Owner (Pavel) or Network Ops Manager (Allen Day)
