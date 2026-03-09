# Premium Tools & B2B Monetization Plan
## API Access for Developers + White-Label for Agencies

---

## Overview

Expand beyond B2C subscriptions into **B2B revenue streams** with two premium offerings:

1. **API Access for Developers** - Monetize your content database and platform features via paid API tiers
2. **White-Label for Agencies** - License your platform to agencies who want to run their own branded adult content networks

**Revenue Potential:**
- API: $500-$5,000/month per developer/company
- White-Label: $2,000-$50,000/month per agency + revenue share

---

## Part 1: Developer API Access

### 1.1 API Tier Structure

```javascript
const apiTiers = {
    free: {
        name: 'Free Tier',
        price: 0,
        limits: {
            requestsPerDay: 100,
            requestsPerMinute: 10,
            endpoints: ['read_only'],
            features: [
                'Search public posts',
                'Get user profiles (public)',
                'Basic post metadata',
                'No commercial use'
            ]
        }
    },
    
    developer: {
        name: 'Developer',
        price: 49,
        priceUnit: 'month',
        limits: {
            requestsPerDay: 10000,
            requestsPerMinute: 100,
            endpoints: ['read_only', 'webhooks'],
            features: [
                'All public content access',
                'Advanced search & filters',
                'Webhook notifications',
                'Commercial use allowed',
                'Email support'
            ]
        }
    },
    
    business: {
        name: 'Business',
        price: 299,
        priceUnit: 'month',
        limits: {
            requestsPerDay: 100000,
            requestsPerMinute: 500,
            endpoints: ['read_only', 'write', 'webhooks', 'analytics'],
            features: [
                'Everything in Developer',
                'Write access (post on behalf)',
                'Analytics API',
                'Bulk operations',
                'Priority support',
                '99.9% SLA'
            ]
        }
    },
    
    enterprise: {
        name: 'Enterprise',
        price: 'custom',
        limits: {
            requestsPerDay: 'unlimited',
            requestsPerMinute: 2000,
            endpoints: ['all'],
            features: [
                'Everything in Business',
                'Custom rate limits',
                'Dedicated support',
                'Custom integrations',
                'On-premise options',
                'Legal review assistance'
            ]
        }
    }
};
```

### 1.2 Database Schema for API Access

```sql
-- API Applications (developer projects)
CREATE TABLE api_applications (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    user_id BIGINT NOT NULL,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    tier ENUM('free', 'developer', 'business', 'enterprise') DEFAULT 'free',
    status ENUM('active', 'suspended', 'cancelled') DEFAULT 'active',
    api_key VARCHAR(64) UNIQUE NOT NULL,
    api_secret VARCHAR(128) NOT NULL,
    webhook_url VARCHAR(512),
    webhook_secret VARCHAR(128),
    allowed_origins TEXT, -- JSON array of allowed CORS origins
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id),
    INDEX idx_api_key (api_key)
);

-- API Subscriptions
CREATE TABLE api_subscriptions (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    application_id BIGINT NOT NULL,
    tier VARCHAR(50) NOT NULL,
    status ENUM('active', 'expired', 'cancelled') DEFAULT 'active',
    price_monthly DECIMAL(10,2) NOT NULL,
    billing_cycle ENUM('monthly', 'annual') DEFAULT 'monthly',
    started_at TIMESTAMP NOT NULL,
    expires_at TIMESTAMP,
    payment_provider VARCHAR(50),
    payment_provider_subscription_id VARCHAR(255),
    FOREIGN KEY (application_id) REFERENCES api_applications(id)
);

-- API Usage Tracking
CREATE TABLE api_usage_logs (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    application_id BIGINT NOT NULL,
    endpoint VARCHAR(255) NOT NULL,
    method VARCHAR(10) NOT NULL,
    status_code INT NOT NULL,
    response_time_ms INT,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    ip_address VARCHAR(45),
    user_agent TEXT,
    FOREIGN KEY (application_id) REFERENCES api_applications(id),
    INDEX idx_app_timestamp (application_id, timestamp),
    INDEX idx_timestamp (timestamp)
);

-- API Rate Limiting (in-memory cache for performance)
CREATE TABLE api_rate_limits (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    application_id BIGINT NOT NULL,
    window_start TIMESTAMP NOT NULL,
    window_type ENUM('minute', 'hour', 'day') NOT NULL,
    request_count INT DEFAULT 0,
    UNIQUE KEY (application_id, window_start, window_type),
    FOREIGN KEY (application_id) REFERENCES api_applications(id)
);

-- API Quotas Summary (aggregated)
CREATE TABLE api_usage_summary (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    application_id BIGINT NOT NULL,
    date DATE NOT NULL,
    total_requests INT DEFAULT 0,
    successful_requests INT DEFAULT 0,
    failed_requests INT DEFAULT 0,
    avg_response_time_ms INT,
    bandwidth_bytes BIGINT DEFAULT 0,
    UNIQUE KEY (application_id, date),
    FOREIGN KEY (application_id) REFERENCES api_applications(id)
);
```

### 1.3 API Authentication & Rate Limiting

**File**: `api/middleware/apiAuth.js`

```javascript
const crypto = require('crypto');
const redis = require('redis').createClient();

// API Key authentication
async function authenticateApiKey(req, res, next) {
    const apiKey = req.headers['x-api-key'];
    
    if (!apiKey) {
        return res.status(401).json({ 
            error: 'API key required',
            message: 'Include X-API-Key header with your request'
        });
    }
    
    // Check cache first
    let app = await redis.get(`api_app:${apiKey}`);
    
    if (!app) {
        // Load from database
        app = await getApiApplicationByKey(apiKey);
        
        if (!app) {
            return res.status(401).json({ error: 'Invalid API key' });
        }
        
        // Cache for 5 minutes
        await redis.setex(`api_app:${apiKey}`, 300, JSON.stringify(app));
    } else {
        app = JSON.parse(app);
    }
    
    if (app.status !== 'active') {
        return res.status(403).json({ 
            error: 'API access suspended',
            message: 'Please contact support'
        });
    }
    
    // Check subscription status
    const subscription = await getApiSubscription(app.id);
    if (!subscription || subscription.status !== 'active') {
        return res.status(402).json({ 
            error: 'Subscription required',
            message: 'Please upgrade your API plan'
        });
    }
    
    req.apiApp = app;
    req.apiSubscription = subscription;
    next();
}

// Rate limiting middleware
async function rateLimitApi(req, res, next) {
    const app = req.apiApp;
    const tier = req.apiSubscription.tier;
    const limits = apiTiers[tier].limits;
    
    // Check per-minute limit
    const minuteKey = `ratelimit:${app.id}:minute:${Math.floor(Date.now() / 60000)}`;
    const minuteCount = await redis.incr(minuteKey);
    await redis.expire(minuteKey, 60);
    
    if (minuteCount > limits.requestsPerMinute) {
        return res.status(429).json({
            error: 'Rate limit exceeded',
            limit: limits.requestsPerMinute,
            window: 'per minute',
            retryAfter: 60
        });
    }
    
    // Check per-day limit
    const today = new Date().toISOString().split('T')[0];
    const dayKey = `ratelimit:${app.id}:day:${today}`;
    const dayCount = await redis.incr(dayKey);
    await redis.expire(dayKey, 86400);
    
    if (limits.requestsPerDay !== 'unlimited' && dayCount > limits.requestsPerDay) {
        return res.status(429).json({
            error: 'Daily quota exceeded',
            limit: limits.requestsPerDay,
            window: 'per day',
            resetAt: new Date(new Date().setHours(24, 0, 0, 0))
        });
    }
    
    // Add rate limit headers
    res.setHeader('X-RateLimit-Limit-Minute', limits.requestsPerMinute);
    res.setHeader('X-RateLimit-Remaining-Minute', limits.requestsPerMinute - minuteCount);
    res.setHeader('X-RateLimit-Limit-Day', limits.requestsPerDay);
    res.setHeader('X-RateLimit-Remaining-Day', limits.requestsPerDay - dayCount);
    
    next();
}

// Endpoint access control
function requireApiEndpoint(endpointType) {
    return (req, res, next) => {
        const allowedEndpoints = apiTiers[req.apiSubscription.tier].limits.endpoints;
        
        if (!allowedEndpoints.includes(endpointType) && !allowedEndpoints.includes('all')) {
            return res.status(403).json({
                error: 'Endpoint not available in your tier',
                currentTier: req.apiSubscription.tier,
                requiredEndpoint: endpointType,
                upgradeUrl: '/api/developer/upgrade'
            });
        }
        
        next();
    };
}
```

### 1.4 Developer API Endpoints

**File**: `api/v1/developer/endpoints.js`

```javascript
// Developer Portal - Manage API Apps
const developerPortalEndpoints = {
    // GET /api/developer/applications
    listApplications: async (req, res) => {
        const apps = await getApiApplicationsByUser(req.user.id);
        res.json(apps);
    },
    
    // POST /api/developer/applications
    createApplication: async (req, res) => {
        const { name, description } = req.body;
        
        // Generate API credentials
        const apiKey = 'bdslr_' + crypto.randomBytes(32).toString('hex');
        const apiSecret = crypto.randomBytes(64).toString('hex');
        
        const app = await createApiApplication({
            userId: req.user.id,
            name,
            description,
            apiKey,
            apiSecret: hashSecret(apiSecret), // Store hashed
            tier: 'free'
        });
        
        // Return secret only once
        res.json({
            ...app,
            apiSecret, // Show only on creation
            warning: 'Save this secret - it will not be shown again'
        });
    },
    
    // GET /api/developer/applications/:appId/usage
    getUsageStats: async (req, res) => {
        const { appId } = req.params;
        const { startDate, endDate } = req.query;
        
        const usage = await getApiUsageSummary(appId, startDate, endDate);
        const currentLimits = await getCurrentRateLimits(appId);
        
        res.json({
            usage,
            limits: currentLimits,
            tier: req.apiSubscription.tier
        });
    },
    
    // POST /api/developer/applications/:appId/subscribe
    upgradeApiTier: async (req, res) => {
        const { appId } = req.params;
        const { tier, paymentMethodId } = req.body;
        
        const pricing = apiTiers[tier];
        
        // Create Stripe subscription
        const stripeSubscription = await stripe.subscriptions.create({
            customer: req.user.stripeCustomerId,
            items: [{ 
                price_data: {
                    currency: 'usd',
                    product: process.env.STRIPE_API_PRODUCT_ID,
                    recurring: { interval: 'month' },
                    unit_amount: pricing.price * 100
                }
            }],
            default_payment_method: paymentMethodId,
            metadata: {
                applicationId: appId,
                tier
            }
        });
        
        // Create API subscription record
        const subscription = await createApiSubscription({
            applicationId: appId,
            tier,
            status: 'active',
            priceMonthly: pricing.price,
            paymentProvider: 'stripe',
            paymentProviderSubscriptionId: stripeSubscription.id,
            expiresAt: new Date(stripeSubscription.current_period_end * 1000)
        });
        
        res.json({ subscription });
    },
    
    // POST /api/developer/applications/:appId/regenerate-key
    regenerateApiKey: async (req, res) => {
        const { appId } = req.params;
        
        const newApiKey = 'bdslr_' + crypto.randomBytes(32).toString('hex');
        
        await updateApiApplication(appId, { apiKey: newApiKey });
        
        res.json({ 
            apiKey: newApiKey,
            message: 'Update your applications with the new key'
        });
    }
};
```

### 1.5 Public API Endpoints for Developers

**File**: `api/v1/public/content.js`

```javascript
// Public API that developers will call
const publicApiEndpoints = {
    // GET /api/v1/posts/search
    searchPosts: [authenticateApiKey, rateLimitApi, async (req, res) => {
        const { query, tags, creator, limit = 20, offset = 0 } = req.query;
        
        // Log API usage
        await logApiRequest(req.apiApp.id, req);
        
        const results = await searchPosts({
            query,
            tags: tags?.split(','),
            creatorId: creator,
            limit: Math.min(limit, 100), // Cap at 100
            offset,
            visibility: 'public' // Only public content via API
        });
        
        res.json({
            results: results.map(post => formatPostForApi(post)),
            pagination: {
                limit,
                offset,
                total: results.total
            }
        });
    }],
    
    // GET /api/v1/posts/:postId
    getPost: [authenticateApiKey, rateLimitApi, async (req, res) => {
        const { postId } = req.params;
        
        await logApiRequest(req.apiApp.id, req);
        
        const post = await getPost(postId);
        
        if (!post || post.visibility !== 'public') {
            return res.status(404).json({ error: 'Post not found' });
        }
        
        res.json(formatPostForApi(post));
    }],
    
    // GET /api/v1/users/:userId
    getUser: [authenticateApiKey, rateLimitApi, async (req, res) => {
        const { userId } = req.params;
        
        await logApiRequest(req.apiApp.id, req);
        
        const user = await getUser(userId);
        
        if (!user) {
            return res.status(404).json({ error: 'User not found' });
        }
        
        res.json(formatUserForApi(user));
    }],
    
    // POST /api/v1/posts (Business tier+)
    createPost: [
        authenticateApiKey, 
        rateLimitApi, 
        requireApiEndpoint('write'),
        async (req, res) => {
            const { title, content, tags, media } = req.body;
            
            await logApiRequest(req.apiApp.id, req);
            
            // Create post on behalf of the API app owner
            const post = await createPost({
                creatorId: req.apiApp.user_id,
                title,
                content,
                tags,
                media,
                source: 'api',
                apiApplicationId: req.apiApp.id
            });
            
            res.status(201).json(formatPostForApi(post));
        }
    ],
    
    // GET /api/v1/analytics/posts/:postId (Business tier+)
    getPostAnalytics: [
        authenticateApiKey,
        rateLimitApi,
        requireApiEndpoint('analytics'),
        async (req, res) => {
            const { postId } = req.params;
            const { startDate, endDate } = req.query;
            
            await logApiRequest(req.apiApp.id, req);
            
            // Verify ownership
            const post = await getPost(postId);
            if (post.creator_id !== req.apiApp.user_id) {
                return res.status(403).json({ error: 'Not your post' });
            }
            
            const analytics = await getContentAnalytics(postId, startDate, endDate);
            
            res.json(analytics);
        }
    ]
};

// Format post for API response (remove sensitive data)
function formatPostForApi(post) {
    return {
        id: post.id,
        title: post.title,
        content: post.content,
        creator: {
            id: post.creator_id,
            username: post.creator_username,
            avatar: post.creator_avatar
        },
        media: post.media.map(m => ({
            type: m.type,
            url: m.public_url,
            thumbnail: m.thumbnail_url
        })),
        tags: post.tags,
        stats: {
            views: post.views_count,
            likes: post.likes_count,
            comments: post.comments_count
        },
        created_at: post.created_at,
        updated_at: post.updated_at
    };
}
```

### 1.6 Webhooks for Developers

**File**: `api/v1/webhooks/delivery.js`

```javascript
// Send webhooks to developer applications
async function sendWebhook(applicationId, event, data) {
    const app = await getApiApplication(applicationId);
    
    if (!app.webhook_url) return;
    
    const payload = {
        event,
        data,
        timestamp: new Date().toISOString(),
        applicationId
    };
    
    // Create signature
    const signature = crypto
        .createHmac('sha256', app.webhook_secret)
        .update(JSON.stringify(payload))
        .digest('hex');
    
    try {
        const response = await fetch(app.webhook_url, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
                'X-BDSLR-Signature': signature,
                'X-BDSLR-Event': event
            },
            body: JSON.stringify(payload)
        });
        
        await logWebhookDelivery({
            applicationId,
            event,
            statusCode: response.status,
            success: response.ok
        });
        
    } catch (error) {
        await logWebhookDelivery({
            applicationId,
            event,
            error: error.message,
            success: false
        });
    }
}

// Webhook events developers can subscribe to
const webhookEvents = {
    'post.created': (postId) => sendWebhook(appId, 'post.created', { postId }),
    'post.updated': (postId) => sendWebhook(appId, 'post.updated', { postId }),
    'post.deleted': (postId) => sendWebhook(appId, 'post.deleted', { postId }),
    'user.followed': (userId, followerId) => sendWebhook(appId, 'user.followed', { userId, followerId }),
    'comment.created': (commentId, postId) => sendWebhook(appId, 'comment.created', { commentId, postId })
};
```

---

## Part 2: White-Label Platform for Agencies

### 2.1 White-Label Tier Structure

```javascript
const whiteLabelTiers = {
    starter: {
        name: 'Starter',
        price: 1999,
        priceUnit: 'month',
        setup_fee: 5000,
        features: [
            'Up to 10,000 users',
            'Custom domain',
            'Basic branding (logo, colors)',
            'Standard features',
            'Email support',
            'Revenue share: 15%'
        ],
        limits: {
            maxUsers: 10000,
            maxStorage: '500GB',
            customization: 'basic'
        }
    },
    
    professional: {
        name: 'Professional',
        price: 4999,
        priceUnit: 'month',
        setup_fee: 10000,
        features: [
            'Up to 100,000 users',
            'Multiple custom domains',
            'Full branding customization',
            'All features',
            'Custom features (limited)',
            'Priority support',
            'Revenue share: 10%'
        ],
        limits: {
            maxUsers: 100000,
            maxStorage: '5TB',
            customization: 'advanced'
        }
    },
    
    enterprise: {
        name: 'Enterprise',
        price: 'custom',
        setup_fee: 'custom',
        features: [
            'Unlimited users',
            'White-glove onboarding',
            'Complete customization',
            'Custom feature development',
            'Dedicated infrastructure',
            '24/7 phone support',
            'SLA guarantees',
            'Revenue share: negotiable'
        ],
        limits: {
            maxUsers: 'unlimited',
            maxStorage: 'unlimited',
            customization: 'unlimited'
        }
    }
};
```

### 2.2 Database Schema for White-Label

```sql
-- White-label instances
CREATE TABLE whitelabel_instances (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    agency_user_id BIGINT NOT NULL,
    name VARCHAR(255) NOT NULL,
    slug VARCHAR(100) UNIQUE NOT NULL,
    tier ENUM('starter', 'professional', 'enterprise') NOT NULL,
    status ENUM('active', 'suspended', 'trial', 'setup') DEFAULT 'setup',
    
    -- Domain configuration
    primary_domain VARCHAR(255) UNIQUE,
    custom_domains JSON, -- Array of additional domains
    ssl_enabled BOOLEAN DEFAULT true,
    
    -- Branding
    brand_name VARCHAR(255),
    logo_url VARCHAR(512),
    favicon_url VARCHAR(512),
    color_primary VARCHAR(7),
    color_secondary VARCHAR(7),
    custom_css TEXT,
    
    -- Features
    enabled_features JSON, -- Array of feature flags
    custom_settings JSON,
    
    -- Billing
    monthly_price DECIMAL(10,2),
    revenue_share_percentage DECIMAL(5,2),
    
    -- Limits
    max_users INT,
    max_storage_gb INT,
    current_users INT DEFAULT 0,
    current_storage_gb DECIMAL(10,2) DEFAULT 0,
    
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    launched_at TIMESTAMP,
    
    FOREIGN KEY (agency_user_id) REFERENCES users(id)
);

-- White-label users (isolated per instance)
CREATE TABLE whitelabel_users (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    instance_id BIGINT NOT NULL,
    username VARCHAR(100) NOT NULL,
    email VARCHAR(255) NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    
    -- Same user/post/subscription structure as main platform
    -- but scoped to instance_id
    
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    
    UNIQUE KEY (instance_id, username),
    UNIQUE KEY (instance_id, email),
    FOREIGN KEY (instance_id) REFERENCES whitelabel_instances(id)
);

-- White-label revenue tracking
CREATE TABLE whitelabel_revenue (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    instance_id BIGINT NOT NULL,
    month VARCHAR(7) NOT NULL, -- "2026-02"
    
    gross_revenue DECIMAL(10,2) DEFAULT 0,
    platform_share DECIMAL(10,2) DEFAULT 0,
    agency_share DECIMAL(10,2) DEFAULT 0,
    
    subscription_revenue DECIMAL(10,2) DEFAULT 0,
    creator_revenue DECIMAL(10,2) DEFAULT 0,
    
    total_users INT DEFAULT 0,
    active_creators INT DEFAULT 0,
    total_transactions INT DEFAULT 0,
    
    payout_status ENUM('pending', 'paid') DEFAULT 'pending',
    payout_date TIMESTAMP,
    
    UNIQUE KEY (instance_id, month),
    FOREIGN KEY (instance_id) REFERENCES whitelabel_instances(id)
);

-- White-label customization assets
CREATE TABLE whitelabel_assets (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    instance_id BIGINT NOT NULL,
    asset_type ENUM('logo', 'favicon', 'banner', 'email_template', 'css', 'javascript'),
    file_url VARCHAR(512),
    file_size_kb INT,
    uploaded_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (instance_id) REFERENCES whitelabel_instances(id)
);
```

### 2.3 White-Label Instance Management

**File**: `api/whitelabel/management.js`

```javascript
const whiteLabelEndpoints = {
    // POST /api/whitelabel/request-demo
    requestDemo: async (req, res) => {
        const { companyName, email, phone, expectedUsers } = req.body;
        
        // Create lead in CRM
        await createWhiteLabelLead({
            companyName,
            email,
            phone,
            expectedUsers,
            status: 'demo_requested'
        });
        
        // Send to sales team
        await notifySalesTeam({ email, companyName });
        
        res.json({ message: 'Demo request received. Our team will contact you within 24 hours.' });
    },
    
    // POST /api/whitelabel/instances (Admin only)
    createInstance: async (req, res) => {
        const {
            agencyUserId,
            name,
            slug,
            tier,
            primaryDomain
        } = req.body;
        
        // Generate isolated database schema
        await createInstanceDatabase(slug);
        
        // Create instance record
        const instance = await createWhiteLabelInstance({
            agencyUserId,
            name,
            slug,
            tier,
            primaryDomain,
            status: 'setup',
            monthlyPrice: whiteLabelTiers[tier].price,
            revenueSharePercentage: parseRevenueShare(whiteLabelTiers[tier].features)
        });
        
        // Set up infrastructure
        await provisionInstanceInfrastructure(instance);
        
        res.json(instance);
    },
    
    // GET /api/whitelabel/instances/:instanceId
    getInstance: async (req, res) => {
        const { instanceId } = req.params;
        
        const instance = await getWhiteLabelInstance(instanceId);
        
        // Check ownership
        if (instance.agency_user_id !== req.user.id && !req.user.isAdmin) {
            return res.status(403).json({ error: 'Access denied' });
        }
        
        const stats = await getInstanceStats(instanceId);
        const revenue = await getInstanceRevenue(instanceId);
        
        res.json({
            instance,
            stats,
            revenue
        });
    },
    
    // PUT /api/whitelabel/instances/:instanceId/branding
    updateBranding: async (req, res) => {
        const { instanceId } = req.params;
        const {
            brandName,
            logoUrl,
            faviconUrl,
            colorPrimary,
            colorSecondary,
            customCss
        } = req.body;
        
        await updateWhiteLabelInstance(instanceId, {
            brand_name: brandName,
            logo_url: logoUrl,
            favicon_url: faviconUrl,
            color_primary: colorPrimary,
            color_secondary: colorSecondary,
            custom_css: customCss
        });
        
        // Rebuild CSS for instance
        await rebuildInstanceStyles(instanceId);
        
        res.json({ message: 'Branding updated' });
    },
    
    // POST /api/whitelabel/instances/:instanceId/launch
    launchInstance: async (req, res) => {
        const { instanceId } = req.params;
        
        const instance = await getWhiteLabelInstance(instanceId);
        
        // Verify setup complete
        const setupChecks = await verifyInstanceSetup(instanceId);
        if (!setupChecks.complete) {
            return res.status(400).json({
                error: 'Setup incomplete',
                missing: setupChecks.missing
            });
        }
        
        // Configure DNS
        await configureDNS(instance.primary_domain, instanceId);
        
        // Issue SSL certificate
        await provisionSSL(instance.primary_domain);
        
        // Update status
        await updateWhiteLabelInstance(instanceId, {
            status: 'active',
            launched_at: new Date()
        });
        
        res.json({ message: 'Instance launched successfully' });
    }
};
```

### 2.4 Multi-Tenancy Architecture

**File**: `api/middleware/multitenancy.js`

```javascript
// Detect which white-label instance the request is for
async function detectInstance(req, res, next) {
    const hostname = req.hostname;
    
    // Check if main platform or white-label
    if (hostname === 'bdsmlr.com' || hostname === 'www.bdsmlr.com') {
        req.instanceId = null; // Main platform
        req.isWhiteLabel = false;
    } else {
        // Look up white-label instance by domain
        const instance = await getInstanceByDomain(hostname);
        
        if (!instance) {
            return res.status(404).json({ error: 'Site not found' });
        }
        
        if (instance.status !== 'active') {
            return res.status(503).json({ error: 'Site temporarily unavailable' });
        }
        
        req.instanceId = instance.id;
        req.instance = instance;
        req.isWhiteLabel = true;
    }
    
    next();
}

// Database query scoping for multi-tenancy
function scopeQuery(query, instanceId) {
    if (!instanceId) return query; // Main platform - no scoping
    
    // Add instance_id filter to all queries
    return query.where('instance_id', instanceId);
}

// Example usage in controllers
async function getPosts(req) {
    let query = db.select('*').from('posts');
    
    // Automatically scope to instance if white-label
    query = scopeQuery(query, req.instanceId);
    
    return await query;
}
```

### 2.5 White-Label Revenue Sharing

**File**: `api/whitelabel/revenue.js`

```javascript
// Calculate monthly revenue for white-label instance
async function calculateInstanceRevenue(instanceId, month) {
    // Get all transactions for the month
    const transactions = await getInstanceTransactions(instanceId, month);
    
    const instance = await getWhiteLabelInstance(instanceId);
    const revenueSharePct = instance.revenue_share_percentage;
    
    let grossRevenue = 0;
    let subscriptionRevenue = 0;
    let creatorRevenue = 0;
    
    for (const transaction of transactions) {
        grossRevenue += parseFloat(transaction.amount);
        
        if (transaction.type === 'subscription') {
            subscriptionRevenue += parseFloat(transaction.amount);
        } else if (transaction.type === 'post_purchase' || transaction.type === 'creator_subscription') {
            creatorRevenue += parseFloat(transaction.amount);
        }
    }
    
    // Calculate shares
    const platformShare = grossRevenue * (revenueSharePct / 100);
    const agencyShare = grossRevenue - platformShare;
    
    // Save revenue record
    await createWhiteLabelRevenue({
        instanceId,
        month,
        grossRevenue,
        platformShare,
        agencyShare,
        subscriptionRevenue,
        creatorRevenue,
        totalUsers: await countInstanceUsers(instanceId),
        activeCreators: await countInstanceCreators(instanceId),
        totalTransactions: transactions.length
    });
    
    return {
        grossRevenue,
        platformShare,
        agencyShare
    };
}

// Monthly payout to white-label agencies
async function processWhiteLabelPayouts() {
    const lastMonth = getLastMonth(); // "2026-01"
    
    const revenues = await getWhiteLabelRevenuePending(lastMonth);
    
    for (const revenue of revenues) {
        const instance = await getWhiteLabelInstance(revenue.instance_id);
        
        if (revenue.agency_share >= 100) { // Minimum payout $100
            // Create Stripe transfer to agency's connected account
            await stripe.transfers.create({
                amount: Math.round(revenue.agency_share * 100),
                currency: 'usd',
                destination: instance.stripe_connected_account_id,
                description: `Revenue share for ${instance.name} - ${lastMonth}`
            });
            
            await updateWhiteLabelRevenue(revenue.id, {
                payout_status: 'paid',
                payout_date: new Date()
            });
        }
    }
}
```

---

## Part 3: Developer Documentation Portal

### 3.1 Auto-Generated API Documentation

**File**: `docs/api/generator.js`

```javascript
// Generate OpenAPI/Swagger documentation
const apiDocs = {
    openapi: '3.0.0',
    info: {
        title: 'BDSMLR API',
        version: '1.0.0',
        description: 'Access BDSMLR content programmatically'
    },
    servers: [
        { url: 'https://api.bdsmlr.com/v1', description: 'Production' },
        { url: 'https://sandbox-api.bdsmlr.com/v1', description: 'Sandbox' }
    ],
    security: [
        { ApiKeyAuth: [] }
    ],
    components: {
        securitySchemes: {
            ApiKeyAuth: {
                type: 'apiKey',
                in: 'header',
                name: 'X-API-Key'
            }
        },
        schemas: {
            Post: {
                type: 'object',
                properties: {
                    id: { type: 'integer' },
                    title: { type: 'string' },
                    content: { type: 'string' },
                    creator: { $ref: '#/components/schemas/User' },
                    media: {
                        type: 'array',
                        items: { $ref: '#/components/schemas/Media' }
                    },
                    created_at: { type: 'string', format: 'date-time' }
                }
            }
            // ... more schemas
        }
    },
    paths: {
        '/posts/search': {
            get: {
                summary: 'Search posts',
                parameters: [
                    { name: 'query', in: 'query', schema: { type: 'string' } },
                    { name: 'limit', in: 'query', schema: { type: 'integer', default: 20 } }
                ],
                responses: {
                    200: {
                        description: 'Search results',
                        content: {
                            'application/json': {
                                schema: {
                                    type: 'object',
                                    properties: {
                                        results: {
                                            type: 'array',
                                            items: { $ref: '#/components/schemas/Post' }
                                        }
                                    }
                                }
                            }
                        }
                    }
                }
            }
        }
        // ... more endpoints
    }
};

// Serve at /api/docs
app.get('/api/docs', (req, res) => {
    res.json(apiDocs);
});
```

### 3.2 Interactive API Explorer

Build a developer portal at `developers.bdsmlr.com`:

- **Interactive API explorer** (like Stripe's docs)
- **Code examples** in multiple languages (JavaScript, Python, Ruby, PHP)
- **Postman collection** download
- **WebSocket examples** for real-time features
- **Rate limit simulator**
- **Sandbox environment** for testing

---

## Part 4: Implementation Checklist

### API Access Implementation

**Phase 1: Foundation**
- [ ] Create API applications database schema
- [ ] Build API key generation system
- [ ] Implement authentication middleware
- [ ] Create rate limiting system (use Redis)
- [ ] Build usage tracking
- [ ] Create developer portal UI

**Phase 2: API Endpoints**
- [ ] Implement read-only public endpoints
- [ ] Add webhook delivery system
- [ ] Create write endpoints (Business tier)
- [ ] Build analytics endpoints
- [ ] Add bulk operations

**Phase 3: Monetization**
- [ ] Create API subscription tiers
- [ ] Integrate Stripe for API billing
- [ ] Build usage limits enforcement
- [ ] Create upgrade flow
- [ ] Implement overage billing (optional)

**Phase 4: Documentation**
- [ ] Generate OpenAPI specification
- [ ] Build interactive documentation
- [ ] Create code examples
- [ ] Write integration guides
- [ ] Create video tutorials

### White-Label Implementation

**Phase 1: Multi-Tenancy**
- [ ] Design database isolation strategy
- [ ] Create instance provisioning system
- [ ] Build domain routing logic
- [ ] Implement DNS automation
- [ ] Set up SSL certificate automation

**Phase 2: Customization**
- [ ] Build branding editor
- [ ] Create CSS customization system
- [ ] Implement logo/asset upload
- [ ] Build email template editor
- [ ] Create theme preview system

**Phase 3: Instance Management**
- [ ] Build admin dashboard for instances
- [ ] Create agency portal
- [ ] Implement usage monitoring
- [ ] Build billing system
- [ ] Create automated provisioning

**Phase 4: Revenue Sharing**
- [ ] Implement revenue tracking per instance
- [ ] Build payout calculation system
- [ ] Integrate Stripe Connect for agencies
- [ ] Create revenue reports
- [ ] Automate monthly payouts

---

## Revenue Projections

### API Revenue Example
- 10 developers @ $49/month = $490/month
- 5 businesses @ $299/month = $1,495/month
- 2 enterprise @ $2,000/month = $4,000/month
**Total: $5,985/month ($71,820/year)**

### White-Label Revenue Example
- 3 Starter agencies @ $1,999/month = $5,997/month
- 1 Professional agency @ $4,999/month = $4,999/month
- Plus 10-15% revenue share from their transactions
**Total: $10,996/month base + revenue share**

If white-label instances generate $100,000/month in transactions combined:
- Your share (10-15%): $10,000-$15,000/month
**Total with revenue share: $20,996-$25,996/month**

### Combined B2B Revenue Potential
**$26,000-$32,000/month** ($312,000-$384,000/year)

This is **in addition to** your B2C subscription and creator revenue!

---

## AI Agent Prompts

### For API Implementation

```
Implement the Developer API system for BDSMLR:

1. Create database schema for API applications, subscriptions, and usage tracking
2. Build authentication middleware using API keys
3. Implement rate limiting with Redis
4. Create public API endpoints for:
   - Search posts
   - Get post details
   - Get user profiles
5. Add usage logging to track API calls
6. Build developer portal for managing API keys

Reference: PREMIUM_TOOLS_B2B_PLAN.md sections 1.1-1.4
```

### For White-Label Implementation

```
Implement White-Label Platform system for agencies:

1. Create database schema for white-label instances
2. Build multi-tenancy middleware to detect instance from domain
3. Implement instance provisioning system
4. Create branding customization system:
   - Logo upload
   - Color customization
   - Custom CSS
5. Build agency dashboard to manage their instance
6. Implement revenue tracking and sharing

Reference: PREMIUM_TOOLS_B2B_PLAN.md sections 2.1-2.5
```

---

## Next Steps

1. **Decide priority**: API Access or White-Label first?
   - API is faster to implement (2-3 weeks)
   - White-Label is more complex (6-8 weeks) but higher revenue potential

2. **Start with API if**:
   - You want quick B2B revenue
   - You have developers interested
   - Less infrastructure work

3. **Start with White-Label if**:
   - You have agencies interested
   - Willing to invest in infrastructure
   - Want higher revenue per customer

4. **Or do both in sequence**:
   - Month 1-2: API Access
   - Month 3-5: White-Label Platform

Both can be AI-implemented following this plan!
