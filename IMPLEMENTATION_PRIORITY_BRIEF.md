# Implementation Priority Brief

**Date:** May 14, 2026  
**Focus:** Cut corners in theorizing - concrete, actionable steps only

---

## 1. Product Framing Strategy (Prioritized)

### **What PayPal Sees (Front)**
```
Product: "RelayOS Premium IRC" - $12/month
Description: "Private IRC chat with persistent connections and message history"
Domain: relayos.com (neutral, clean)
Business: Forward Handle LLC (existing account)
```

### **What Actually Happens (Behind)**
```
Week 1-2: WordPress + WooCommerce setup
Week 2-3: User authentication (password bridge)
Week 3-4: BDSMLR API checks WordPress subscription by email
Week 4+: Features unlock based on subscription status
```

### **Traffic Flow (Breaking Referrer Chain)**
```
BDSMLR user clicks "Upgrade"
  ↓
Redirect to: relayos.com (homepage, NOT checkout)
  ↓
User browses, clicks "Get Started"
  ↓
Login/Register (email pre-filled)
  ↓
Checkout via PayPal
```

**PayPal sees:** relayos.com → PayPal (NOT bdsmlr.com → PayPal)

---

## 2. User Authentication Setup (Prioritized Steps)

### **Week 1: Pre-Import Active Users**
```sql
-- Import last 90 days active users only (~100K users, not 3M)
INSERT INTO wp_users (user_login, user_email, user_registered, user_pass)
SELECT username, email, created_at, '$P$Btemp...'  -- Temporary password
FROM bdsmlr_users
WHERE last_login > DATE_SUB(NOW(), INTERVAL 90 DAY)
LIMIT 100000;

-- Tag them
UPDATE wp_usermeta SET meta_key='_source', meta_value='bdsmlr';
```

**Result:** WordPress → Anope IRC sync happens automatically (triggers already exist)

---

### **Week 2: Build Password Bridge Plugin**
```php
// WordPress plugin: 50 lines
// File: wp-content/plugins/relayos-auth/auth.php

add_filter('authenticate', 'relayos_bdsmlr_bridge', 30, 3);

function relayos_bdsmlr_bridge($user, $username, $password) {
    // 1. Try WordPress auth first
    $wp_user = wp_authenticate_username_password(null, $username, $password);
    if (!is_wp_error($wp_user)) return $wp_user;
    
    // 2. Try BDSMLR API
    $response = wp_remote_post('https://api.bdsmlr.com/auth/verify', [
        'body' => json_encode(['email' => $username, 'password' => $password])
    ]);
    
    if ($response['status'] === 'valid') {
        $wp_user = get_user_by('email', $username);
        
        if (!$wp_user) {
            // Lazy create for inactive users
            $user_id = wp_create_user($response['user']['username'], $password, $username);
            update_user_meta($user_id, '_source', 'bdsmlr');
            $wp_user = get_user_by('id', $user_id);
        } else {
            // Update password for pre-imported users
            wp_set_password($password, $wp_user->ID);
        }
        
        return $wp_user;
    }
    
    return $user;
}
```

**Result:** BDSMLR users log in with existing credentials

---

### **Week 3: BDSMLR API Checks Subscription**
```python
# bdsmlr-api/v2/services/subscription_service.py (NEW)

import requests
from functools import lru_cache

@lru_cache(maxsize=2000, ttl=300)
def check_subscription(email: str) -> dict:
    response = requests.get(
        f"{WORDPRESS_API}/subscription-status?email={email}",
        headers={"X-Internal-Token": INTERNAL_TOKEN},
        timeout=2
    )
    return response.json() if response.status_code == 200 else {}

# Update identity_decorations.py (ADD 3 LINES):
sub_data = check_subscription(viewer_email)
subscriber_status = sub_data.get("subscriber_status")
subscriber_badge = sub_data.get("subscriber_badge")

# Rest of code unchanged - decorations already work!
```

**Result:** 💙 badge appears on BDSMLR for subscribers

---

## **Priority Timeline**

| Week | Task | Deliverable |
|------|------|-------------|
| **1** | Pre-import 100K active users | Users exist in WordPress |
| **1-2** | WooCommerce + PayPal setup | Can accept payments |
| **2** | Password bridge plugin (50 lines) | Users can log in |
| **3** | BDSMLR API subscription check | Badges appear |
| **4-6** | Premium features (collections, downloads) | Full feature set |

---

**Total to Launch: 3 weeks (auth working) + 3 weeks (features) = 6 weeks**
