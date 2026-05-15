# Password Authentication: How It Works for Existing BDSMLR Users

**Date:** May 14, 2026  
**Question:** "I don't really understand how this will work. For example, I've been a user of bdsmlr for a long time. What happens when I click the Upgrade button? We uploaded the database to WordPress before launching the project"

---

## **Scenario 1: Pre-Import Users (What Akira Has Ready)**

**Before Launch: Import all BDSMLR users to WordPress**

```sql
-- One-time migration before launch
INSERT INTO wp_users (user_login, user_email, user_registered, user_pass)
SELECT 
    username,
    email,
    created_at,
    '$P$B...'  -- WordPress password hash (PROBLEM: We can't copy BDSMLR passwords!)
FROM bdsmlr_users;
```

**The Problem:**
- BDSMLR uses Laravel bcrypt: `$2y$10$...`
- WordPress uses phpass: `$P$B...`
- **We can't decrypt and re-encrypt passwords** (impossible!)
- So imported users **don't have valid passwords** in WordPress

**When User Clicks "Upgrade" on BDSMLR:**

```
Step 1: User clicks "Upgrade" on BDSMLR
        ↓
Step 2: Redirect to relayos.com/login
        ↓
Step 3: User sees login form:
        ┌──────────────────────────────────┐
        │ Sign in to RelayOS               │
        │                                  │
        │ Email: user@example.com          │
        │ Password: [their BDSMLR password]│
        │                                  │
        │ [Sign In]                        │
        └──────────────────────────────────┘
        ↓
Step 4: User enters their BDSMLR password
        ↓
Step 5: WordPress checks password:
        - First: Try WordPress password hash ❌ (doesn't match - we couldn't import it)
        - Second: Call BDSMLR API to verify ✅ (password correct!)
        ↓
Step 6: WordPress UPDATES the user's password:
        - Now store WordPress-compatible hash
        - User logged in
        ↓
Step 7: Proceed to checkout
```

**Code:**
```php
// WordPress plugin
add_filter('authenticate', 'relayos_bdsmlr_password_bridge', 30, 3);

function relayos_bdsmlr_password_bridge($user, $username, $password) {
    // Try normal WordPress auth first
    $wp_user = wp_authenticate_username_password(null, $username, $password);
    if (!is_wp_error($wp_user)) {
        return $wp_user;  // WordPress password works, done!
    }
    
    // WordPress password failed, try BDSMLR
    $email = $username;  // Could be email or username
    $user_obj = get_user_by('email', $email);
    
    if (!$user_obj) {
        return $user;  // User doesn't exist
    }
    
    // Check if this user was imported from BDSMLR
    $source = get_user_meta($user_obj->ID, '_source', true);
    if ($source !== 'bdsmlr') {
        return $user;  // Not a BDSMLR user
    }
    
    // Verify password with BDSMLR API
    $bdsmlr_api = 'https://api.bdsmlr.com/auth/verify';
    $response = wp_remote_post($bdsmlr_api, [
        'body' => json_encode(['email' => $email, 'password' => $password]),
        'headers' => ['Content-Type' => 'application/json']
    ]);
    
    if ($response['status'] === 'valid') {
        // Password correct in BDSMLR!
        // Update WordPress password so next login is faster
        wp_set_password($password, $user_obj->ID);
        
        // Mark as password migrated
        update_user_meta($user_obj->ID, '_password_migrated', true);
        
        // Return authenticated user
        return $user_obj;
    }
    
    return $user;  // Password invalid
}
```

**Result:**
- ✅ First login: WordPress checks BDSMLR API (slow, 200-500ms)
- ✅ Stores WordPress password hash
- ✅ Second login: WordPress native auth (fast, no API call)
- ✅ User doesn't know anything happened

---

## **Scenario 2: Lazy Migration (No Pre-Import)**

**Before Launch: Don't import users**

**When User Clicks "Upgrade" on BDSMLR:**

```
Step 1: User clicks "Upgrade" on BDSMLR
        ↓
Step 2: Redirect to relayos.com/login
        (Maybe pre-fill email via URL parameter)
        ↓
Step 3: User sees login form:
        ┌──────────────────────────────────┐
        │ Sign in to RelayOS               │
        │                                  │
        │ Email: user@example.com          │
        │ Password: [their BDSMLR password]│
        │                                  │
        │ [Sign In]                        │
        │                                  │
        │ Don't have an account? [Register]│
        └──────────────────────────────────┘
        ↓
Step 4: User enters BDSMLR credentials
        ↓
Step 5: WordPress checks:
        - User doesn't exist in WordPress yet
        - Call BDSMLR API: "Is this a valid user?"
        - BDSMLR API: "Yes, valid!"
        ↓
Step 6: WordPress CREATES user automatically:
        - username: from BDSMLR
        - email: from BDSMLR
        - password: store WordPress hash
        - meta: _source = 'bdsmlr'
        ↓
Step 7: User logged in automatically
        ↓
Step 8: Proceed to checkout
```

**Code:**
```php
add_filter('authenticate', 'relayos_lazy_bdsmlr_migration', 30, 3);

function relayos_lazy_bdsmlr_migration($user, $username, $password) {
    // Try normal WordPress auth first
    $wp_user = wp_authenticate_username_password(null, $username, $password);
    if (!is_wp_error($wp_user)) {
        return $wp_user;  // User exists and password correct
    }
    
    // User doesn't exist or password wrong
    // Check BDSMLR API
    $bdsmlr_api = 'https://api.bdsmlr.com/auth/verify';
    $response = wp_remote_post($bdsmlr_api, [
        'body' => json_encode(['username' => $username, 'password' => $password]),
        'headers' => ['Content-Type' => 'application/json']
    ]);
    
    if ($response['status'] === 'valid') {
        $bdsmlr_user = $response['user'];
        
        // User exists in BDSMLR! Create WordPress account
        $user_id = wp_create_user(
            $bdsmlr_user['username'],
            $password,  // Store WordPress-hashed password
            $bdsmlr_user['email']
        );
        
        // Store metadata
        update_user_meta($user_id, '_source', 'bdsmlr');
        update_user_meta($user_id, '_bdsmlr_id', $bdsmlr_user['id']);
        
        // If they had premium before, give badge
        if ($bdsmlr_user['premium']) {
            update_user_meta($user_id, 'subscriber_badge', 'early_supporter');
        }
        
        // Return newly created user
        return get_user_by('id', $user_id);
    }
    
    return $user;  // Invalid credentials
}
```

---

## **Which Approach is Better?**

### **Scenario 1: Pre-Import (What You Mentioned)**

**Pros:**
- ✅ All users exist in WordPress from day 1
- ✅ WordPress → Anope IRC sync happens immediately (triggers fire)
- ✅ Easier to manage user list

**Cons:**
- ⚠️ 3M users in WordPress immediately (PayPal might notice)
- ⚠️ First login requires BDSMLR API call (password bridge)
- ⚠️ Need to handle users who never upgrade (wasted database rows)

**PayPal Risk:** MEDIUM-HIGH (sudden 3M user spike)

---

### **Scenario 2: Lazy Migration (My Original Recommendation)**

**Pros:**
- ✅ Organic growth (100 users, then 500, then 1000...)
- ✅ Only create accounts for users who actually upgrade
- ✅ No wasted database rows
- ✅ Looks natural to PayPal

**Cons:**
- ⚠️ Every first login requires BDSMLR API call
- ⚠️ IRC nicknames not reserved until user registers

**PayPal Risk:** LOW (looks like normal growth)

---

## **My Updated Recommendation: Hybrid Approach**

**Combine both strategies:**

### **Pre-Import: Only Active Users**

```sql
-- Import only users who logged in recently (active users)
INSERT INTO wp_users (...)
SELECT ...
FROM bdsmlr_users
WHERE last_login > DATE_SUB(NOW(), INTERVAL 90 DAY)  -- Active in last 90 days
LIMIT 100000;  -- Cap at 100K users
```

**Why:**
- ✅ Most likely to convert
- ✅ Reasonable initial size (100K not 3M)
- ✅ IRC nicknames reserved for active users
- ✅ Lazy migration handles everyone else

**Then:**
- Active users (100K): Use Scenario 1 (password bridge)
- Inactive users (2.9M): Use Scenario 2 (lazy migration if they come back)

---

## **Clearer User Flow: Step by Step**

**As an existing BDSMLR user, here's what you experience:**

```
1. You're browsing BDSMLR
   ↓
2. You see: "Get BDSMLR Premium - Collections, Downloads, Ad-Free"
   ↓
3. You click [Upgrade]
   ↓
4. Browser redirects to: relayos.com/login?email=your@email.com
   ↓
5. You see:
   ┌───────────────────────────────────────┐
   │ Sign in to RelayOS                    │
   │                                       │
   │ Email: your@email.com (pre-filled)    │
   │ Password: _______________             │
   │                                       │
   │ [Sign In]                             │
   │                                       │
   │ New to RelayOS? [Create Account]      │
   └───────────────────────────────────────┘
   ↓
6. You type your BDSMLR password (same one you use on BDSMLR)
   ↓
7. You click [Sign In]
   ↓
8. Backend magic happens:
   - WordPress checks: "Is password correct in WordPress DB?" 
     → No (first login) or Yes (subsequent logins)
   - If No: "Let me check BDSMLR API..."
   - BDSMLR API: "Yes, password correct!"
   - WordPress: "Great! I'll save this password now"
   ↓
9. You're logged in! (You didn't notice the API call, took 300ms)
   ↓
10. Redirect to: relayos.com/checkout
   ↓
11. You see WooCommerce checkout:
   ┌───────────────────────────────────────┐
   │ RelayOS Premium - $12/month           │
   │                                       │
   │ [ PayPal Checkout ]                   │
   └───────────────────────────────────────┘
   ↓
12. You complete payment
   ↓
13. Done! You have:
    - RelayOS IRC access (WordPress → Anope synced automatically)
    - BDSMLR premium features (API checks WordPress subscription)
```

**From your perspective:**
- ✅ Used your existing BDSMLR password
- ✅ Didn't create a new account manually
- ✅ Seamless experience

**Behind the scenes:**
- ✅ WordPress account created/updated
- ✅ IRC nickname registered (Anope triggers)
- ✅ BDSMLR API will check subscription status going forward

---

**Does this clarify how Option 1 works?**
