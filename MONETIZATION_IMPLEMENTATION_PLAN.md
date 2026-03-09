# BDSMLR Monetization Implementation Plan
## AI Agent-Friendly Implementation Guide

---

## Overview
Transform bdsmlr.com into a monetized platform with tiered subscriptions and creator monetization, implemented through your AI-powered visual interface that connects to your existing API.

**Key Constraint**: Implementation by AI agent with minimal human team
**Architecture**: AI Visual Interface → API → Database (users, posts, reactions, etc.)

---

## Phase 1: Database Schema Enhancements

### 1.1 Subscription & User Tiers Tables

```sql
-- User subscription status
CREATE TABLE user_subscriptions (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    user_id BIGINT NOT NULL,
    tier ENUM('free', 'enthusiast', 'pro', 'creator') DEFAULT 'free',
    status ENUM('active', 'expired', 'cancelled', 'trial') DEFAULT 'active',
    started_at TIMESTAMP NOT NULL,
    expires_at TIMESTAMP,
    auto_renew BOOLEAN DEFAULT true,
    payment_provider VARCHAR(50),
    payment_provider_subscription_id VARCHAR(255),
    FOREIGN KEY (user_id) REFERENCES users(id)
);

-- Subscription pricing configuration
CREATE TABLE subscription_tiers (
    id INT PRIMARY KEY AUTO_INCREMENT,
    tier_name VARCHAR(50) UNIQUE NOT NULL,
    price_monthly DECIMAL(10,2) NOT NULL,
    daily_view_limit INT,
    monthly_download_limit INT,
    features JSON, -- Store tier features as JSON
    is_active BOOLEAN DEFAULT true
);

-- Track daily usage limits
CREATE TABLE user_daily_usage (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    user_id BIGINT NOT NULL,
    date DATE NOT NULL,
    image_views_count INT DEFAULT 0,
    downloads_count INT DEFAULT 0,
    UNIQUE KEY (user_id, date),
    FOREIGN KEY (user_id) REFERENCES users(id)
);

-- Monthly download tracking
CREATE TABLE user_monthly_downloads (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    user_id BIGINT NOT NULL,
    year_month VARCHAR(7) NOT NULL, -- Format: "2026-02"
    downloads_count INT DEFAULT 0,
    UNIQUE KEY (user_id, year_month),
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

### 1.2 Creator Monetization Tables

```sql
-- Creator configuration
CREATE TABLE creator_profiles (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    user_id BIGINT NOT NULL UNIQUE,
    is_monetized BOOLEAN DEFAULT false,
    commission_rate DECIMAL(5,2) DEFAULT 20.00, -- Platform commission %
    minimum_payout DECIMAL(10,2) DEFAULT 50.00,
    stripe_account_id VARCHAR(255),
    paypal_email VARCHAR(255),
    analytics_enabled BOOLEAN DEFAULT true,
    FOREIGN KEY (user_id) REFERENCES users(id)
);

-- Paid content configuration
CREATE TABLE post_monetization (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    post_id BIGINT NOT NULL UNIQUE,
    is_paid BOOLEAN DEFAULT false,
    price DECIMAL(10,2), -- Price for individual post purchase
    subscriber_only BOOLEAN DEFAULT false, -- Only for creator's subscribers
    preview_enabled BOOLEAN DEFAULT true, -- Show blurred preview
    purchases_count INT DEFAULT 0,
    revenue_total DECIMAL(10,2) DEFAULT 0.00,
    FOREIGN KEY (post_id) REFERENCES posts(id)
);

-- Creator subscription (fans subscribe to specific creators)
CREATE TABLE creator_subscriptions (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    creator_id BIGINT NOT NULL,
    subscriber_id BIGINT NOT NULL,
    price_monthly DECIMAL(10,2) NOT NULL,
    status ENUM('active', 'expired', 'cancelled') DEFAULT 'active',
    started_at TIMESTAMP NOT NULL,
    expires_at TIMESTAMP,
    auto_renew BOOLEAN DEFAULT true,
    payment_provider_subscription_id VARCHAR(255),
    UNIQUE KEY (creator_id, subscriber_id),
    FOREIGN KEY (creator_id) REFERENCES users(id),
    FOREIGN KEY (subscriber_id) REFERENCES users(id)
);

-- Individual post purchases
CREATE TABLE post_purchases (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    post_id BIGINT NOT NULL,
    buyer_id BIGINT NOT NULL,
    price_paid DECIMAL(10,2) NOT NULL,
    purchased_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UNIQUE KEY (post_id, buyer_id),
    FOREIGN KEY (post_id) REFERENCES posts(id),
    FOREIGN KEY (buyer_id) REFERENCES users(id)
);
```

### 1.3 Payment & Transaction Tables

```sql
-- All financial transactions
CREATE TABLE transactions (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    user_id BIGINT NOT NULL,
    type ENUM('subscription', 'post_purchase', 'creator_subscription', 'payout', 'refund'),
    amount DECIMAL(10,2) NOT NULL,
    currency VARCHAR(3) DEFAULT 'USD',
    status ENUM('pending', 'completed', 'failed', 'refunded') DEFAULT 'pending',
    payment_provider VARCHAR(50),
    payment_provider_transaction_id VARCHAR(255),
    reference_id BIGINT, -- Links to subscription_id, post_id, etc.
    metadata JSON,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
);

-- Creator earnings tracking
CREATE TABLE creator_earnings (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    creator_id BIGINT NOT NULL,
    transaction_id BIGINT NOT NULL,
    gross_amount DECIMAL(10,2) NOT NULL,
    commission_amount DECIMAL(10,2) NOT NULL,
    net_amount DECIMAL(10,2) NOT NULL,
    status ENUM('pending', 'available', 'paid_out') DEFAULT 'pending',
    payout_date TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (creator_id) REFERENCES users(id),
    FOREIGN KEY (transaction_id) REFERENCES transactions(id)
);

-- Payout requests
CREATE TABLE payouts (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    creator_id BIGINT NOT NULL,
    amount DECIMAL(10,2) NOT NULL,
    status ENUM('requested', 'processing', 'completed', 'failed') DEFAULT 'requested',
    method ENUM('stripe', 'paypal', 'bank_transfer'),
    requested_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    completed_at TIMESTAMP,
    failure_reason TEXT,
    FOREIGN KEY (creator_id) REFERENCES users(id)
);
```

### 1.4 Analytics Tables

```sql
-- Content performance analytics
CREATE TABLE content_analytics (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    post_id BIGINT NOT NULL,
    date DATE NOT NULL,
    views_count INT DEFAULT 0,
    unique_viewers INT DEFAULT 0,
    likes_count INT DEFAULT 0,
    comments_count INT DEFAULT 0,
    downloads_count INT DEFAULT 0,
    shares_count INT DEFAULT 0,
    revenue DECIMAL(10,2) DEFAULT 0.00,
    UNIQUE KEY (post_id, date),
    FOREIGN KEY (post_id) REFERENCES posts(id)
);

-- Creator analytics summary
CREATE TABLE creator_analytics_summary (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    creator_id BIGINT NOT NULL,
    period_start DATE NOT NULL,
    period_end DATE NOT NULL,
    total_views INT DEFAULT 0,
    total_followers INT DEFAULT 0,
    new_subscribers INT DEFAULT 0,
    total_revenue DECIMAL(10,2) DEFAULT 0.00,
    top_performing_posts JSON, -- Array of post IDs with metrics
    demographics JSON, -- Viewer demographics data
    FOREIGN KEY (creator_id) REFERENCES users(id)
);
```

---

## Phase 2: Backend API Implementation

### 2.1 Authentication & Authorization Middleware

**File**: `api/middleware/auth.js`

```javascript
// JWT-based authentication middleware
async function authenticateUser(req, res, next) {
    const token = req.headers.authorization?.split(' ')[1];
    if (!token) return res.status(401).json({ error: 'Unauthorized' });
    
    try {
        const decoded = jwt.verify(token, process.env.JWT_SECRET);
        req.user = await getUserById(decoded.userId);
        req.userSubscription = await getUserSubscription(decoded.userId);
        next();
    } catch (error) {
        return res.status(401).json({ error: 'Invalid token' });
    }
}

// Check user tier and feature access
function requireTier(minTier) {
    const tierHierarchy = ['free', 'enthusiast', 'pro', 'creator'];
    
    return (req, res, next) => {
        const userTier = req.userSubscription?.tier || 'free';
        const userTierLevel = tierHierarchy.indexOf(userTier);
        const requiredTierLevel = tierHierarchy.indexOf(minTier);
        
        if (userTierLevel >= requiredTierLevel) {
            next();
        } else {
            return res.status(403).json({ 
                error: 'Subscription required',
                currentTier: userTier,
                requiredTier: minTier
            });
        }
    };
}
```

### 2.2 Content Access Control API

**File**: `api/controllers/contentAccess.js`

```javascript
// Check if user can view specific content
async function checkContentAccess(userId, postId) {
    const post = await getPost(postId);
    const monetization = await getPostMonetization(postId);
    
    // Public content - always accessible
    if (!monetization || !monetization.is_paid) {
        return { 
            hasAccess: true, 
            reason: 'public',
            content: post 
        };
    }
    
    // Check if user purchased this specific post
    const purchase = await getPostPurchase(postId, userId);
    if (purchase) {
        return { 
            hasAccess: true, 
            reason: 'purchased',
            content: post 
        };
    }
    
    // Check if user is subscribed to the creator
    const subscription = await getCreatorSubscription(post.creator_id, userId);
    if (subscription && subscription.status === 'active') {
        return { 
            hasAccess: true, 
            reason: 'creator_subscription',
            content: post 
        };
    }
    
    // User doesn't have access
    return {
        hasAccess: false,
        reason: 'payment_required',
        content: {
            ...post,
            media: post.media.map(m => ({ ...m, url: m.preview_url, blurred: true })),
            price: monetization.price,
            subscriberOnly: monetization.subscriber_only
        }
    };
}

// Track content view and enforce limits
async function trackContentView(userId, postId) {
    const subscription = await getUserSubscription(userId);
    const tier = subscription?.tier || 'free';
    
    // Free tier has daily limits
    if (tier === 'free') {
        const today = new Date().toISOString().split('T')[0];
        const usage = await getUserDailyUsage(userId, today);
        
        if (usage.image_views_count >= 50) {
            throw new Error('Daily view limit reached. Upgrade to continue.');
        }
        
        await incrementDailyViews(userId, today);
    }
    
    // Track analytics
    await incrementContentAnalytics(postId, 'views_count');
}
```

### 2.3 Subscription Management API

**File**: `api/controllers/subscriptions.js`

```javascript
// Platform subscription endpoints
const subscriptionEndpoints = {
    // GET /api/subscriptions/tiers
    getTiers: async (req, res) => {
        const tiers = await getSubscriptionTiers();
        res.json(tiers);
    },
    
    // GET /api/subscriptions/current
    getCurrentSubscription: async (req, res) => {
        const subscription = await getUserSubscription(req.user.id);
        const usage = await getCurrentUsage(req.user.id);
        res.json({ subscription, usage });
    },
    
    // POST /api/subscriptions/subscribe
    subscribe: async (req, res) => {
        const { tier, paymentMethodId } = req.body;
        
        // Create Stripe subscription
        const stripeSubscription = await stripe.subscriptions.create({
            customer: req.user.stripeCustomerId,
            items: [{ price: getTierPriceId(tier) }],
            payment_behavior: 'default_incomplete',
            default_payment_method: paymentMethodId,
            expand: ['latest_invoice.payment_intent']
        });
        
        // Save to database
        const subscription = await createUserSubscription({
            userId: req.user.id,
            tier,
            status: 'active',
            paymentProvider: 'stripe',
            paymentProviderSubscriptionId: stripeSubscription.id,
            expiresAt: new Date(stripeSubscription.current_period_end * 1000)
        });
        
        res.json({ subscription, clientSecret: stripeSubscription.latest_invoice.payment_intent.client_secret });
    },
    
    // POST /api/subscriptions/cancel
    cancel: async (req, res) => {
        const subscription = await getUserSubscription(req.user.id);
        
        // Cancel on Stripe
        await stripe.subscriptions.update(subscription.payment_provider_subscription_id, {
            cancel_at_period_end: true
        });
        
        // Update database
        await updateUserSubscription(req.user.id, { 
            status: 'cancelled',
            auto_renew: false 
        });
        
        res.json({ message: 'Subscription cancelled' });
    }
};
```

### 2.4 Creator Monetization API

**File**: `api/controllers/creators.js`

```javascript
const creatorEndpoints = {
    // POST /api/creator/enable
    enableMonetization: async (req, res) => {
        const { stripeAccountId, paypalEmail } = req.body;
        
        // User must have Creator tier subscription
        if (req.userSubscription.tier !== 'creator') {
            return res.status(403).json({ error: 'Creator subscription required' });
        }
        
        const profile = await createOrUpdateCreatorProfile({
            userId: req.user.id,
            isMonetized: true,
            stripeAccountId,
            paypalEmail
        });
        
        res.json(profile);
    },
    
    // POST /api/creator/posts/:postId/monetize
    monetizePost: async (req, res) => {
        const { postId } = req.params;
        const { price, subscriberOnly } = req.body;
        
        // Verify post ownership
        const post = await getPost(postId);
        if (post.creator_id !== req.user.id) {
            return res.status(403).json({ error: 'Not your post' });
        }
        
        const monetization = await createOrUpdatePostMonetization({
            postId,
            isPaid: true,
            price,
            subscriberOnly,
            previewEnabled: true
        });
        
        res.json(monetization);
    },
    
    // POST /api/creator/subscription/set-price
    setCreatorSubscriptionPrice: async (req, res) => {
        const { priceMonthly } = req.body;
        
        await updateCreatorProfile(req.user.id, { 
            subscriptionPriceMonthly: priceMonthly 
        });
        
        res.json({ message: 'Price updated' });
    },
    
    // GET /api/creator/analytics
    getAnalytics: async (req, res) => {
        const { startDate, endDate } = req.query;
        
        const analytics = await getCreatorAnalytics(
            req.user.id, 
            startDate, 
            endDate
        );
        
        res.json(analytics);
    },
    
    // GET /api/creator/earnings
    getEarnings: async (req, res) => {
        const earnings = await getCreatorEarnings(req.user.id);
        const payouts = await getCreatorPayouts(req.user.id);
        
        const available = earnings.reduce((sum, e) => {
            return e.status === 'available' ? sum + parseFloat(e.net_amount) : sum;
        }, 0);
        
        res.json({ earnings, payouts, availableBalance: available });
    },
    
    // POST /api/creator/payout/request
    requestPayout: async (req, res) => {
        const { amount, method } = req.body;
        
        const available = await getAvailableBalance(req.user.id);
        
        if (amount > available) {
            return res.status(400).json({ error: 'Insufficient balance' });
        }
        
        if (amount < 50) {
            return res.status(400).json({ error: 'Minimum payout is $50' });
        }
        
        const payout = await createPayout({
            creatorId: req.user.id,
            amount,
            method,
            status: 'requested'
        });
        
        // Process payout async
        processPayout(payout.id);
        
        res.json(payout);
    }
};
```

### 2.5 Post Purchase API

**File**: `api/controllers/purchases.js`

```javascript
const purchaseEndpoints = {
    // POST /api/posts/:postId/purchase
    purchasePost: async (req, res) => {
        const { postId } = req.params;
        const { paymentMethodId } = req.body;
        
        const monetization = await getPostMonetization(postId);
        if (!monetization || !monetization.is_paid) {
            return res.status(400).json({ error: 'Post is not for sale' });
        }
        
        // Check if already purchased
        const existing = await getPostPurchase(postId, req.user.id);
        if (existing) {
            return res.status(400).json({ error: 'Already purchased' });
        }
        
        // Process payment
        const paymentIntent = await stripe.paymentIntents.create({
            amount: Math.round(monetization.price * 100),
            currency: 'usd',
            customer: req.user.stripeCustomerId,
            payment_method: paymentMethodId,
            confirm: true,
            metadata: {
                postId,
                userId: req.user.id
            }
        });
        
        if (paymentIntent.status === 'succeeded') {
            // Record purchase
            const purchase = await createPostPurchase({
                postId,
                buyerId: req.user.id,
                pricePaid: monetization.price
            });
            
            // Record transaction
            const transaction = await createTransaction({
                userId: req.user.id,
                type: 'post_purchase',
                amount: monetization.price,
                status: 'completed',
                paymentProvider: 'stripe',
                paymentProviderTransactionId: paymentIntent.id,
                referenceId: postId
            });
            
            // Calculate creator earnings
            const post = await getPost(postId);
            const creator = await getCreatorProfile(post.creator_id);
            const commissionRate = creator.commission_rate || 20;
            const commissionAmount = monetization.price * (commissionRate / 100);
            const netAmount = monetization.price - commissionAmount;
            
            await createCreatorEarning({
                creatorId: post.creator_id,
                transactionId: transaction.id,
                grossAmount: monetization.price,
                commissionAmount,
                netAmount,
                status: 'available'
            });
            
            res.json({ purchase, transaction });
        } else {
            res.status(400).json({ error: 'Payment failed' });
        }
    },
    
    // POST /api/creators/:creatorId/subscribe
    subscribeToCreator: async (req, res) => {
        const { creatorId } = req.params;
        const { paymentMethodId } = req.body;
        
        const creator = await getCreatorProfile(creatorId);
        if (!creator || !creator.is_monetized) {
            return res.status(400).json({ error: 'Creator not available for subscription' });
        }
        
        // Create Stripe subscription
        const stripeSubscription = await stripe.subscriptions.create({
            customer: req.user.stripeCustomerId,
            items: [{ 
                price_data: {
                    currency: 'usd',
                    product: creator.stripeProductId,
                    recurring: { interval: 'month' },
                    unit_amount: Math.round(creator.subscription_price_monthly * 100)
                }
            }],
            default_payment_method: paymentMethodId,
            expand: ['latest_invoice.payment_intent']
        });
        
        // Save to database
        const subscription = await createCreatorSubscription({
            creatorId,
            subscriberId: req.user.id,
            priceMonthly: creator.subscription_price_monthly,
            status: 'active',
            paymentProviderSubscriptionId: stripeSubscription.id,
            expiresAt: new Date(stripeSubscription.current_period_end * 1000)
        });
        
        res.json({ subscription });
    }
};
```

---

## Phase 3: Payment Integration

### 3.1 Stripe Setup

**File**: `api/services/stripe.js`

```javascript
const stripe = require('stripe')(process.env.STRIPE_SECRET_KEY);

// Initialize customer for new users
async function createStripeCustomer(user) {
    const customer = await stripe.customers.create({
        email: user.email,
        metadata: {
            userId: user.id
        }
    });
    
    await updateUser(user.id, { stripeCustomerId: customer.id });
    return customer;
}

// Webhook handler for Stripe events
async function handleStripeWebhook(event) {
    switch (event.type) {
        case 'customer.subscription.updated':
        case 'customer.subscription.deleted':
            await syncSubscriptionStatus(event.data.object);
            break;
            
        case 'invoice.payment_succeeded':
            await handleSuccessfulPayment(event.data.object);
            break;
            
        case 'invoice.payment_failed':
            await handleFailedPayment(event.data.object);
            break;
    }
}

// Sync subscription status from Stripe
async function syncSubscriptionStatus(stripeSubscription) {
    const subscription = await getUserSubscriptionByProviderId(
        stripeSubscription.id
    );
    
    if (!subscription) return;
    
    const status = stripeSubscription.status === 'active' ? 'active' : 'expired';
    
    await updateUserSubscription(subscription.user_id, {
        status,
        expiresAt: new Date(stripeSubscription.current_period_end * 1000)
    });
}
```

### 3.2 Stripe Connected Accounts (for creators)

```javascript
// Allow creators to connect their Stripe accounts
async function createStripeConnectAccount(creatorId) {
    const account = await stripe.accounts.create({
        type: 'express',
        capabilities: {
            card_payments: { requested: true },
            transfers: { requested: true }
        }
    });
    
    await updateCreatorProfile(creatorId, { 
        stripeAccountId: account.id 
    });
    
    return account;
}

// Generate onboarding link for creators
async function getStripeConnectOnboardingLink(creatorId) {
    const creator = await getCreatorProfile(creatorId);
    
    const accountLink = await stripe.accountLinks.create({
        account: creator.stripe_account_id,
        refresh_url: `${process.env.APP_URL}/creator/settings/payments/refresh`,
        return_url: `${process.env.APP_URL}/creator/settings/payments/success`,
        type: 'account_onboarding'
    });
    
    return accountLink.url;
}
```

---

## Phase 4: AI Visual Interface Integration

### 4.1 Content Rendering Logic

**AI Interface Component**: Content Blur & Paywall

```javascript
// When AI renders content, it should check access
async function renderPost(postData, currentUser) {
    // Call API to check access
    const accessCheck = await fetch(`/api/content/${postData.id}/check-access`, {
        headers: { 'Authorization': `Bearer ${currentUser.token}` }
    });
    
    const access = await accessCheck.json();
    
    if (!access.hasAccess) {
        // Render blurred version with paywall overlay
        return {
            ...postData,
            media: postData.media.map(item => ({
                ...item,
                url: item.preview_url,
                blurred: true,
                overlayType: access.content.subscriberOnly ? 'subscription' : 'purchase',
                price: access.content.price
            })),
            showPaywall: true,
            paywallData: {
                type: access.content.subscriberOnly ? 'creator_subscription' : 'post_purchase',
                price: access.content.price,
                creatorId: postData.creator_id,
                creatorName: postData.creator_name
            }
        };
    }
    
    // User has access - render full content
    return {
        ...postData,
        media: postData.media,
        showPaywall: false
    };
}
```

### 4.2 Subscription Flow in AI Interface

```javascript
// AI should present subscription options when limit reached
async function handleViewLimitReached(currentUser) {
    const tiers = await fetch('/api/subscriptions/tiers').then(r => r.json());
    
    // AI renders comparison modal
    return {
        type: 'subscription_modal',
        message: 'Daily view limit reached (50 images)',
        currentTier: 'free',
        recommendations: [
            {
                tier: 'enthusiast',
                price: 8,
                benefits: ['Unlimited views', '50 HD downloads/month'],
                ctaText: 'Upgrade to Enthusiast'
            },
            {
                tier: 'pro',
                price: 15,
                benefits: ['Everything in Enthusiast', '200 downloads/month', 'Priority support'],
                ctaText: 'Upgrade to Pro'
            }
        ]
    };
}

// Handle subscription purchase
async function initiateSubscription(tier, paymentMethod) {
    const response = await fetch('/api/subscriptions/subscribe', {
        method: 'POST',
        headers: {
            'Authorization': `Bearer ${currentUser.token}`,
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({
            tier,
            paymentMethodId: paymentMethod.id
        })
    });
    
    const result = await response.json();
    
    // Show success message and refresh
    return {
        type: 'subscription_success',
        message: `Successfully upgraded to ${tier}!`,
        subscription: result.subscription
    };
}
```

### 4.3 Creator Dashboard in AI Interface

```javascript
// AI generates analytics dashboard for creators
async function renderCreatorDashboard(creatorId) {
    const [analytics, earnings] = await Promise.all([
        fetch(`/api/creator/analytics?period=30days`).then(r => r.json()),
        fetch(`/api/creator/earnings`).then(r => r.json())
    ]);
    
    // AI renders visual dashboard
    return {
        type: 'creator_dashboard',
        sections: [
            {
                title: 'Earnings Overview',
                widgets: [
                    { type: 'balance', value: earnings.availableBalance, label: 'Available Balance' },
                    { type: 'chart', data: earnings.earnings, chartType: 'line', label: 'Revenue (30 days)' }
                ]
            },
            {
                title: 'Performance',
                widgets: [
                    { type: 'metric', value: analytics.totalViews, label: 'Total Views' },
                    { type: 'metric', value: analytics.newSubscribers, label: 'New Subscribers' },
                    { type: 'metric', value: analytics.totalRevenue, label: 'Total Revenue' }
                ]
            },
            {
                title: 'Top Performing Content',
                widgets: [
                    { type: 'post_list', posts: analytics.topPerformingPosts }
                ]
            }
        ],
        actions: [
            { type: 'button', label: 'Request Payout', action: 'request_payout', enabled: earnings.availableBalance >= 50 },
            { type: 'link', label: 'Monetize New Post', href: '/creator/posts/monetize' }
        ]
    };
}
```

### 4.4 Paywall Prompts

**AI should generate contextual paywall messages:**

```javascript
const paywallPrompts = {
    daily_limit: {
        title: '50 Daily Views Reached',
        message: 'Enjoying the content? Upgrade for unlimited access!',
        cta: 'See Plans',
        urgency: 'low'
    },
    
    paid_post_blur: {
        title: 'Premium Content',
        message: 'This creator has marked this content as premium.',
        options: [
            { label: `Buy for $${price}`, action: 'purchase_post' },
            { label: `Subscribe to ${creatorName}`, action: 'subscribe_creator' }
        ],
        urgency: 'medium'
    },
    
    download_limit: {
        title: 'Monthly Download Limit Reached',
        message: `You've used all 50 downloads this month. Upgrade to Pro for 200 downloads!`,
        cta: 'Upgrade to Pro',
        urgency: 'medium'
    },
    
    hd_quality: {
        title: 'HD Quality Available',
        message: 'Upgrade to see this image in full resolution.',
        cta: 'Upgrade Now',
        urgency: 'low'
    }
};
```

---

## Phase 5: Implementation Checklist for AI Agent

### Step 1: Database Migration
- [ ] Create all new tables (subscriptions, monetization, payments, analytics)
- [ ] Add indexes for performance (user_id, post_id, creator_id)
- [ ] Create database migration scripts
- [ ] Seed subscription_tiers table with initial data
- [ ] Add triggers for automatic analytics updates

### Step 2: Backend API Core
- [ ] Implement authentication middleware
- [ ] Implement tier checking middleware
- [ ] Create user subscription CRUD operations
- [ ] Create content access control logic
- [ ] Implement daily/monthly usage tracking

### Step 3: Payment Integration
- [ ] Set up Stripe account and API keys
- [ ] Implement Stripe customer creation
- [ ] Create subscription checkout flow
- [ ] Set up Stripe webhooks endpoint
- [ ] Implement webhook signature verification
- [ ] Handle subscription lifecycle events
- [ ] Set up Stripe Connect for creators
- [ ] Implement creator onboarding flow

### Step 4: Creator Features
- [ ] Implement creator profile creation
- [ ] Create post monetization endpoints
- [ ] Build creator subscription logic
- [ ] Implement individual post purchase
- [ ] Create earnings calculation system
- [ ] Build payout request system
- [ ] Implement analytics tracking

### Step 5: Content Access & Watermarking
- [ ] Implement image blur/preview generation
- [ ] Create watermark service for free tier downloads
- [ ] Build content access middleware
- [ ] Implement view limit tracking
- [ ] Create download tracking system

### Step 6: Analytics System
- [ ] Create analytics data collection triggers
- [ ] Build analytics aggregation jobs (daily/monthly)
- [ ] Implement creator analytics endpoints
- [ ] Create demographic tracking (optional)
- [ ] Build performance metrics dashboard data

### Step 7: AI Interface Updates
- [ ] Update content rendering to check access
- [ ] Implement blur overlays for paid content
- [ ] Create paywall modal components
- [ ] Build subscription upgrade flows
- [ ] Implement payment method collection
- [ ] Create creator dashboard views
- [ ] Build earnings & analytics displays
- [ ] Implement payout request interface

### Step 8: Testing & Validation
- [ ] Test subscription purchase flow
- [ ] Test subscription cancellation
- [ ] Test webhook handling
- [ ] Test content access controls
- [ ] Test daily view limits
- [ ] Test download limits
- [ ] Test creator monetization flow
- [ ] Test post purchases
- [ ] Test creator subscriptions
- [ ] Test payout system
- [ ] Test analytics accuracy

### Step 9: Security & Compliance
- [ ] Implement rate limiting on API endpoints
- [ ] Add CSRF protection
- [ ] Validate all payment amounts server-side
- [ ] Implement proper error handling
- [ ] Add logging for all financial transactions
- [ ] Ensure PCI compliance (use Stripe properly)
- [ ] Implement age verification (18+)
- [ ] Add terms of service acceptance
- [ ] Create privacy policy
- [ ] Implement GDPR compliance features

### Step 10: Production Deployment
- [ ] Set up production Stripe account
- [ ] Configure environment variables
- [ ] Run database migrations on production
- [ ] Deploy API changes
- [ ] Deploy AI interface updates
- [ ] Monitor error logs
- [ ] Test in production with test cards
- [ ] Enable webhooks in production
- [ ] Set up monitoring & alerts

---

## Phase 6: AI Agent Prompt Templates

### For Database Implementation

```
Create the following database schema for a content monetization platform:

[Paste relevant schema section]

Requirements:
- Use MySQL 8.0+ syntax
- Add appropriate indexes for performance
- Include foreign key constraints
- Add comments explaining complex fields
- Create migration script to add these tables to existing database
```

### For API Implementation

```
Implement the following RESTful API endpoint:

Endpoint: POST /api/subscriptions/subscribe
Purpose: Allow users to purchase a platform subscription

Requirements:
- Authenticate user with JWT
- Validate tier selection
- Integrate with Stripe for payment
- Create subscription record in database
- Return subscription details and payment client secret
- Handle errors gracefully

Context:
- User object is in req.user (from auth middleware)
- Stripe is configured and available
- Database functions: createUserSubscription(), getUserSubscription()
```

### For Stripe Integration

```
Implement Stripe webhook handler for subscription lifecycle events:

Events to handle:
- customer.subscription.updated
- customer.subscription.deleted  
- invoice.payment_succeeded
- invoice.payment_failed

Requirements:
- Verify webhook signature
- Update database based on event
- Send user notifications (email)
- Log all events
- Handle errors without throwing
```

### For AI Interface

```
Update the AI-powered content rendering to implement paywall logic:

When rendering a post:
1. Call /api/content/:postId/check-access to verify access
2. If hasAccess=false, render blurred preview with paywall overlay
3. Show appropriate call-to-action based on monetization type
4. If hasAccess=true, render full content

Requirements:
- Seamless UX - no jarring transitions
- Clear pricing display
- One-click upgrade options
- Mobile-responsive paywall modals
```

---

## Phase 7: Progressive Rollout Strategy

### Week 1-2: Foundation
1. Database schema implementation
2. Basic API structure
3. Authentication middleware
4. Stripe account setup

### Week 3-4: Platform Subscriptions
1. Subscription tier management
2. Stripe integration for subscriptions
3. Usage tracking (views, downloads)
4. Basic paywall in AI interface

### Week 5-6: Creator Monetization
1. Creator profiles
2. Post monetization
3. Individual post purchases
4. Creator subscriptions

### Week 7-8: Analytics & Payouts
1. Analytics collection
2. Creator dashboard
3. Earnings calculation
4. Payout system

### Week 9-10: Polish & Testing
1. Comprehensive testing
2. Bug fixes
3. Performance optimization
4. Security audit
5. Soft launch to beta users

---

## Cost Estimates & Considerations

### Platform Costs
- **Stripe fees**: 2.9% + $0.30 per transaction
- **Your commission**: 20% on creator earnings
- **Net platform revenue**: ~17% per creator transaction (after Stripe fees)

### Example Revenue Calculation
If a creator earns $1,000/month:
- Gross: $1,000
- Stripe fees: ~$30 (approx)
- Platform commission (20%): $200
- Creator receives: $770
- Platform net: $170

### Infrastructure Needs
- Database: Handle subscription status checks (high read volume)
- API: Payment processing endpoints (must be fast & reliable)
- Webhooks: Process Stripe events reliably (use queue system)
- Storage: Generate and store content previews/watermarks

---

## Security Best Practices

### Payment Security
1. **Never** store credit card details - use Stripe tokens only
2. Validate all amounts server-side before charging
3. Use webhook signatures to verify Stripe events
4. Implement idempotency keys for payments
5. Log all financial transactions

### Content Protection
1. Generate temporary signed URLs for paid content
2. Implement rate limiting on content endpoints
3. Watermark free downloads
4. Use CDN with access controls for media
5. Implement download tracking

### API Security
1. Use JWT with short expiration times
2. Implement rate limiting (prevent abuse)
3. Validate all inputs
4. Use HTTPS everywhere
5. Implement CORS properly

### Age Verification
1. Require age confirmation on signup
2. Store consent records
3. Implement content warnings
4. Comply with 18 U.S.C. 2257 (adult content record-keeping)

---

## Support & Maintenance Plan

### Automated Monitoring
- Webhook failure alerts
- Failed payment notifications
- Subscription expiration warnings
- Daily revenue reports
- Unusual activity detection

### Recurring Tasks
- Monthly payout processing
- Quarterly analytics review
- Subscription renewal reminders
- Failed payment retry logic
- Abandoned cart follow-ups

### Customer Support
- Automated chatbot for common issues
- Email support for payments
- Creator support priority queue
- Refund policy enforcement
- Dispute handling process

---

## Success Metrics to Track

### Platform Health
- Monthly Recurring Revenue (MRR)
- Churn rate
- Average Revenue Per User (ARPU)
- Free → Paid conversion rate
- Subscriber lifetime value (LTV)

### Creator Success
- Number of monetized creators
- Average creator earnings
- Creator retention rate
- Content monetization rate

### User Engagement
- Daily active users (DAU)
- View limit hit rate (free tier)
- Upgrade rate from limits
- Download usage patterns
- Purchase conversion rate

---

## Next Steps for AI Agent

1. **Start with Phase 1**: Implement database schema
2. **Validate schema**: Ensure it fits your existing database structure
3. **Build incrementally**: One feature at a time, test thoroughly
4. **Integrate progressively**: Connect each backend API to AI interface
5. **Test payment flows**: Use Stripe test mode extensively
6. **Gather feedback**: Beta test with small creator group first

## Prompt for AI Agent to Begin

```
I need you to implement a content monetization system for bdsmlr.com. 

Start with Phase 1: Database Schema Enhancement.

Reference the detailed plan in MONETIZATION_IMPLEMENTATION_PLAN.md.

Begin by:
1. Reviewing the existing database structure
2. Creating SQL migration scripts for all new tables
3. Adding appropriate indexes
4. Creating seed data for subscription tiers

After completing Phase 1, wait for my approval before moving to Phase 2.

Show me the migration scripts for review.
```

---

## File Structure Recommendation

```
/backend
  /api
    /controllers
      - subscriptions.js
      - creators.js
      - purchases.js
      - contentAccess.js
    /middleware
      - auth.js
      - tierCheck.js
      - rateLimiter.js
    /services
      - stripe.js
      - analytics.js
      - watermark.js
      - payouts.js
    /routes
      - index.js
  /database
    /migrations
      - 001_subscriptions.sql
      - 002_monetization.sql
      - 003_payments.sql
      - 004_analytics.sql
    /seeds
      - subscription_tiers.sql
  /jobs
    - process-payouts.js
    - aggregate-analytics.js
    - sync-subscriptions.js
  /webhooks
    - stripe.js

/frontend (AI Interface)
  /components
    - PaywallOverlay.jsx
    - SubscriptionModal.jsx
    - CreatorDashboard.jsx
    - PaymentForm.jsx
  /services
    - api.js
    - contentAccess.js
  /utils
    - formatCurrency.js
```

---

## Quick Reference: API Endpoints

### User Subscriptions
- `GET /api/subscriptions/tiers` - List available tiers
- `GET /api/subscriptions/current` - Get user's current subscription
- `POST /api/subscriptions/subscribe` - Purchase subscription
- `POST /api/subscriptions/cancel` - Cancel subscription
- `POST /api/subscriptions/update-payment` - Update payment method

### Content Access
- `GET /api/content/:postId/check-access` - Check if user can view post
- `POST /api/content/:postId/track-view` - Track content view
- `GET /api/content/:postId/download` - Download content (enforces limits)

### Creator Features
- `POST /api/creator/enable` - Enable monetization
- `POST /api/creator/posts/:postId/monetize` - Mark post as paid
- `GET /api/creator/analytics` - Get creator analytics
- `GET /api/creator/earnings` - Get earnings details
- `POST /api/creator/payout/request` - Request payout

### Purchases
- `POST /api/posts/:postId/purchase` - Buy individual post
- `POST /api/creators/:creatorId/subscribe` - Subscribe to creator
- `GET /api/purchases/history` - User's purchase history

### Admin (if needed)
- `GET /api/admin/stats` - Platform statistics
- `POST /api/admin/payouts/process` - Process pending payouts
- `GET /api/admin/transactions` - View all transactions

---

**End of Implementation Plan**

Ready to begin implementation? Start with Phase 1 and work systematically through each phase. The AI agent can implement each section independently with proper prompting.
