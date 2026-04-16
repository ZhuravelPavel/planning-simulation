# Observability Setup: Grafana-Centric Monitoring
## Minimum Viable Observability for 3-Person Team

**Version:** 1.0  
**Date:** April 10, 2026  
**Owner:** Network Ops Manager  
**Timeline:** Week 0-4 (setup), ongoing monitoring

---

## Philosophy: "One Dashboard to Rule Them All"

**Goal:** Manager opens Grafana once per day (5 minutes), sees everything. Alerts notify when things break.

**Principles:**
- Centralized (all data in one place)
- Automated (alerts, not manual checking)
- Simple (no overwhelming complexity)
- Free/cheap (budget-conscious)

---

## Architecture: How It All Connects

```
┌─────────────────────────────────────────────────────────────────┐
│                       YOUR SERVERS                              │
│                                                                 │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐         │
│  │  Demo IRC    │  │  ISC Chat    │  │ BDSMLR Chat  │         │
│  │  Network     │  │              │  │              │         │
│  │              │  │              │  │              │         │
│  │ - InspIRCd   │  │ - InspIRCd   │  │ - InspIRCd   │         │
│  │ - KiwiIRC    │  │ - KiwiIRC    │  │ - KiwiIRC    │         │
│  │ - KiwiBNC    │  │ - KiwiBNC    │  │ - KiwiBNC    │         │
│  │ - Jitsi      │  │ - Jitsi      │  │ - Jitsi      │         │
│  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘         │
│         │                 │                 │                  │
│         └─────────────────┴─────────────────┘                  │
│                           │                                    │
│              ┌────────────▼────────────┐                       │
│              │   Node Exporter         │                       │
│              │   (collects metrics)    │                       │
│              │   - CPU usage           │                       │
│              │   - Memory usage        │                       │
│              │   - Disk space          │                       │
│              │   - Network traffic     │                       │
│              └────────────┬────────────┘                       │
│                           │                                    │
│              ┌────────────▼────────────┐                       │
│              │      Promtail           │                       │
│              │   (collects logs)       │                       │
│              │   - Application logs    │                       │
│              │   - Web server logs     │                       │
│              │   - IRC server logs     │                       │
│              │   - System logs         │                       │
│              └────────────┬────────────┘                       │
│                           │                                    │
└───────────────────────────┼────────────────────────────────────┘
                            │
                            │ Data flows up
                            │ (every 15-60 seconds)
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│              OBSERVABILITY SERVER                               │
│              (can be same or separate server)                   │
│                                                                 │
│  ┌──────────────────────┐        ┌──────────────────────┐     │
│  │     Prometheus       │        │        Loki          │     │
│  │   (metrics storage)  │        │    (logs storage)    │     │
│  │                      │        │                      │     │
│  │ - Time-series DB     │        │ - Log aggregation    │     │
│  │ - Stores numbers     │        │ - Stores text        │     │
│  │ - 15 days retention  │        │ - 7 days retention   │     │
│  │ - Scrapes exporters  │        │ - Receives from      │     │
│  │   every 15s          │        │   Promtail           │     │
│  └──────────┬───────────┘        └──────────┬───────────┘     │
│             │                               │                  │
│             └───────────────┬───────────────┘                  │
│                             │                                  │
│                  ┌──────────▼──────────┐                       │
│                  │      Grafana        │                       │
│                  │  (visualization)    │                       │
│                  │                     │                       │
│                  │ - Dashboards        │                       │
│                  │ - Alerts            │                       │
│                  │ - Query both        │                       │
│                  │   Prometheus & Loki │                       │
│                  └──────────┬──────────┘                       │
│                             │                                  │
│                             │ Sends alerts when               │
│                             │ thresholds exceeded             │
│                             ▼                                  │
│                  ┌─────────────────────┐                       │
│                  │   Slack / Email     │                       │
│                  │   (notifications)   │                       │
│                  └─────────────────────┘                       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
                             │
                             │ Manager accesses via browser
                             ▼
                   http://monitoring.relayos.com:3000
                   (Grafana Web UI - one dashboard)
```

---

## What Grafana Shows (The One Dashboard)

### **Manager opens one URL, sees everything:**

```
┌────────────────────────────────────────────────────────────────┐
│  Grafana Dashboard: RelayOS Production Monitoring             │
│  Last updated: 2 seconds ago                    [Refresh: 5s] │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│  ROW 1: SERVICE HEALTH ────────────────────────────────────── │
│                                                                │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐          │
│  │ Demo IRC    │  │ ISC Chat    │  │ BDSMLR Chat │          │
│  │   🟢 UP     │  │   🟢 UP     │  │   🟢 UP     │          │
│  │   125 users │  │   342 users │  │   189 users │          │
│  └─────────────┘  └─────────────┘  └─────────────┘          │
│                                                                │
│  API Response Time (p95): 145ms  ✅                           │
│  Error Rate (last hour): 0.2%    ✅                           │
│                                                                │
│  ROW 2: BUSINESS METRICS ─────────────────────────────────── │
│                                                                │
│  ┌─────────────────┐  ┌─────────────────┐  ┌───────────────┐│
│  │ MRR             │  │ New Subs Today  │  │ Churn (Week)  ││
│  │ $14,850         │  │      12         │  │    3.2%       ││
│  │ ▲ +$320 vs yday │  │  ▲ +2 vs yday   │  │ ✅ Normal     ││
│  └─────────────────┘  └─────────────────┘  └───────────────┘│
│                                                                │
│  Conversion Rate (this week): 1.2%  ✅                        │
│  Active Subscribers: 1,245  (480 A + 240 B + 525 bundle)     │
│                                                                │
│  ROW 3: INFRASTRUCTURE ────────────────────────────────────── │
│                                                                │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐          │
│  │ CPU Usage   │  │ Memory      │  │ Disk Space  │          │
│  │             │  │             │  │             │          │
│  │   ▁▂▃▂▁▂▃   │  │   ▂▃▃▃▂▂▁   │  │   ▁▁▁▁▁▁▁   │          │
│  │   42%       │  │   67%       │  │   54%       │          │
│  └─────────────┘  └─────────────┘  └─────────────┘          │
│                                                                │
│  ROW 4: RECENT ACTIVITY ──────────────────────────────────── │
│                                                                │
│  📊 Subscription API calls: 342/min  ✅                       │
│  💳 Payment success rate: 97.2%      ✅                       │
│  📹 Video calls (last hour): 23                               │
│  📤 File uploads (last hour): 156                             │
│                                                                │
│  ROW 5: RECENT LOGS (last 10 lines) ─────────────────────── │
│                                                                │
│  [15:42:31] INFO  Subscription check: user_12345 -> active   │
│  [15:42:28] INFO  Payment webhook received: subscription_...  │
│  [15:42:15] INFO  User login: alice@example.com (ISC)        │
│  [15:41:52] WARN  Slow query: 520ms (collections endpoint)   │
│  [15:41:30] INFO  Video call started: channel #bdsm-chat     │
│  ...                                                           │
│                                                                │
│  [View all logs →]  [Search logs...]                          │
│                                                                │
│  ROW 6: ACTIVE ALERTS ────────────────────────────────────── │
│                                                                │
│  ✅ No active alerts (all systems operational)                │
│                                                                │
└────────────────────────────────────────────────────────────────┘
```

---

## What to Measure: Complete List

### **Layer 1: Service Health**

| Metric | Target | Alert Threshold | Check Frequency |
|--------|--------|-----------------|-----------------|
| Service uptime (demo, ISC, BDSMLR) | 99.9% | Down >5 min | Every 1 min |
| API response time (p95) | <500ms | >1000ms for >5 min | Every 15s |
| Error rate (5xx) | <1% | >5% for >5 min | Every 15s |
| Active IRC connections | Track | Drop >20% in 5 min | Every 1 min |
| Subscription API calls | Track | Spike >5x normal | Every 1 min |
| Payment success rate | >95% | <90% | Every payment |

**Tools:**
- Prometheus Blackbox Exporter (uptime checks)
- Application instrumentation (API metrics)
- Prometheus (stores all metrics)

---

### **Layer 2: Infrastructure**

| Metric | Target | Alert Threshold | Check Frequency |
|--------|--------|-----------------|-----------------|
| CPU usage | <70% | >90% for >10 min | Every 15s |
| Memory usage | <80% | >90% for >5 min | Every 15s |
| Disk space | <80% | >90% | Every 1 min |
| Network bandwidth | Track | Spike/drop | Every 15s |
| Database connections | <80% max | >95% max | Every 15s |

**Tools:**
- Node Exporter (runs on each server)
- Prometheus (scrapes Node Exporter)

---

### **Layer 3: IRC-Specific**

| Metric | What it tells you | Check Frequency |
|--------|-------------------|-----------------|
| Active connections | Users online now | Every 1 min |
| Concurrent users (peak) | Capacity planning | Every 5 min |
| Channels active | Community health | Every 5 min |
| Messages per minute | Activity level | Every 1 min |
| KiwiBNC connections | Premium feature usage | Every 5 min |
| Jitsi sessions active | Premium feature usage | Every 1 min |
| File uploads per hour | Premium feature usage | Every 5 min |

**Tools:**
- Custom exporter (parse InspIRCd logs or stats)
- Prometheus (scrapes custom exporter)

---

### **Layer 4: Business Metrics**

| Metric | Formula | Check Frequency |
|--------|---------|-----------------|
| Monthly Recurring Revenue (MRR) | Active subs × price | Daily |
| New MRR | New subs × price | Daily |
| Churned MRR | Cancelled subs × price | Daily |
| Net New MRR | New - Churned | Daily |
| Total subscribers (Product A) | Count active | Daily |
| Total subscribers (Product B) | Count active | Daily |
| Conversion rate | New subs / MAU | Weekly |
| Churn rate | Cancelled / Active | Weekly |
| MAU (Monthly Active Users) | Unique users/month | Weekly |

**Tools:**
- WordPress database queries (via Prometheus MySQL exporter)
- Google Analytics (for MAU)
- Google Sheets (for weekly reports)

---

### **Layer 5: Payment Processor**

| Metric | What it tells you | Check Frequency |
|--------|-------------------|-----------------|
| Payment attempts | Users trying to pay | Every payment |
| Payment success rate | Checkout working | Every payment |
| Payment failures | Card declined, etc. | Every payment |
| Webhook delivery | Integration working | Every webhook |
| Subscription created | New subscribers | Real-time |
| Subscription cancelled | Churn | Real-time |

**Tools:**
- Webhook logging (WordPress)
- Prometheus (count webhook events)
- Payment processor dashboards (Stripe, PayPal, CCBill) for details

---

## Tech Stack: What to Install

### **Week 0-2: Bare Minimum (Foundation)**

**Time investment:** ~2 hours  
**Cost:** $0

1. **Prometheus**
   - Download: https://prometheus.io/download/
   - Install: Extract, configure, run as service
   - Config: Add targets (servers to monitor)
   - Port: 9090

2. **Node Exporter** (on each server)
   - Download: https://prometheus.io/download/#node_exporter
   - Install: Extract, run as service
   - Exposes: CPU, RAM, disk, network metrics
   - Port: 9100

3. **Grafana**
   - Download: https://grafana.com/grafana/download
   - Install: APT/YUM package or Docker
   - Config: Add Prometheus as data source
   - Port: 3000

4. **Promtail** (on each server)
   - Download: https://github.com/grafana/loki/releases
   - Install: Extract, configure, run as service
   - Config: Tail log files, send to Loki
   - Port: N/A (client only)

5. **Loki**
   - Download: https://github.com/grafana/loki/releases
   - Install: Extract, configure, run as service
   - Config: Receive logs from Promtail
   - Port: 3100

---

### **Docker Compose Option (Easier)**

**File:** `docker-compose.yml`

```yaml
version: '3'

services:
  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
      - prometheus-data:/prometheus
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/prometheus'
      - '--storage.tsdb.retention.time=15d'
    ports:
      - "9090:9090"
    restart: unless-stopped

  loki:
    image: grafana/loki:latest
    container_name: loki
    ports:
      - "3100:3100"
    command: -config.file=/etc/loki/local-config.yaml
    restart: unless-stopped

  grafana:
    image: grafana/grafana:latest
    container_name: grafana
    ports:
      - "3000:3000"
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=your_secure_password
      - GF_USERS_ALLOW_SIGN_UP=false
    volumes:
      - grafana-data:/var/lib/grafana
    depends_on:
      - prometheus
      - loki
    restart: unless-stopped

  node-exporter:
    image: prom/node-exporter:latest
    container_name: node-exporter
    ports:
      - "9100:9100"
    command:
      - '--path.procfs=/host/proc'
      - '--path.sysfs=/host/sys'
      - '--collector.filesystem.mount-points-exclude=^/(sys|proc|dev|host|etc)($$|/)'
    volumes:
      - /proc:/host/proc:ro
      - /sys:/host/sys:ro
      - /:/rootfs:ro
    restart: unless-stopped

volumes:
  prometheus-data:
  grafana-data:
```

**Run:** `docker-compose up -d`

**Access Grafana:** http://your-server-ip:3000 (username: admin, password: your_secure_password)

---

### **Prometheus Configuration**

**File:** `prometheus.yml`

```yaml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

scrape_configs:
  # Node Exporter (server metrics)
  - job_name: 'node-exporter'
    static_configs:
      - targets: 
        - 'localhost:9100'           # Observability server
        - 'demo-irc.relayos.com:9100' # Demo IRC server
        - 'isc-chat.relayos.com:9100' # ISC server
        - 'bdsmlr-chat.relayos.com:9100' # BDSMLR server

  # Blackbox Exporter (uptime checks)
  - job_name: 'blackbox'
    metrics_path: /probe
    params:
      module: [http_2xx]
    static_configs:
      - targets:
        - https://demo.relayos.com
        - https://chat.isexychat.com
        - https://chat.bdsmlr.com
        - https://subscriptions.relayos.com
        - https://bdsmlr.com
    relabel_configs:
      - source_labels: [__address__]
        target_label: __param_target
      - source_labels: [__param_target]
        target_label: instance
      - target_label: __address__
        replacement: localhost:9115  # Blackbox exporter address

  # WordPress Subscription API
  - job_name: 'subscription-api'
    static_configs:
      - targets: ['subscriptions.relayos.com:9091']

  # Custom IRC metrics
  - job_name: 'irc-metrics'
    static_configs:
      - targets: 
        - 'demo-irc.relayos.com:9092'
        - 'isc-chat.relayos.com:9092'
        - 'bdsmlr-chat.relayos.com:9092'
```

---

## Grafana Dashboard Panels (What to Create)

### **Panel 1: Service Status (Stat Visualization)**

**Query (PromQL):**
```promql
up{job="blackbox"}
```

**Display:** 
- Green box = 1 (up)
- Red box = 0 (down)
- One box per service

---

### **Panel 2: Active IRC Connections (Graph)**

**Query (PromQL):**
```promql
irc_active_connections{instance=~"demo-irc.*|isc-chat.*|bdsmlr-chat.*"}
```

**Display:** Line graph showing connections over time

---

### **Panel 3: API Response Time (Graph)**

**Query (PromQL):**
```promql
histogram_quantile(0.95, rate(api_request_duration_seconds_bucket[5m]))
```

**Display:** Line graph showing p95 latency

---

### **Panel 4: Error Rate (Graph)**

**Query (PromQL):**
```promql
sum(rate(http_requests_total{status=~"5.."}[5m])) / sum(rate(http_requests_total[5m])) * 100
```

**Display:** Line graph showing % errors

---

### **Panel 5: CPU/Memory/Disk (Gauge)**

**Queries (PromQL):**
```promql
# CPU
100 - (avg by(instance) (irate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)

# Memory
(1 - (node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes)) * 100

# Disk
(1 - (node_filesystem_avail_bytes / node_filesystem_size_bytes)) * 100
```

**Display:** Gauge showing 0-100%

---

### **Panel 6: Revenue Metrics (Stat)**

**Query (MySQL via Prometheus MySQL Exporter):**
```sql
SELECT 
  SUM(order_total) as mrr
FROM wp_woocommerce_subscriptions 
WHERE status = 'active'
```

**Display:** Big number + sparkline

---

### **Panel 7: Recent Logs (Logs Visualization)**

**Query (LogQL for Loki):**
```logql
{job="wordpress"} |= "subscription" | json | line_format "{{.timestamp}} {{.level}} {{.message}}"
```

**Display:** Scrolling log viewer (last 100 lines)

---

## Alert Rules

### **Grafana Alert Configuration**

**Alert 1: Service Down**
- **Condition:** `up{job="blackbox"} == 0`
- **For:** 5 minutes
- **Severity:** CRITICAL
- **Channel:** Slack + Email
- **Message:** "🚨 Service DOWN: {{$labels.instance}}"

**Alert 2: High Error Rate**
- **Condition:** `(sum(rate(http_requests_total{status=~"5.."}[5m])) / sum(rate(http_requests_total[5m]))) > 0.05`
- **For:** 5 minutes
- **Severity:** HIGH
- **Channel:** Slack
- **Message:** "⚠️ Error rate >5% on {{$labels.instance}}"

**Alert 3: API Slow**
- **Condition:** `histogram_quantile(0.95, rate(api_request_duration_seconds_bucket[5m])) > 1.0`
- **For:** 10 minutes
- **Severity:** MEDIUM
- **Channel:** Slack
- **Message:** "🐌 API response time >1s (p95)"

**Alert 4: Payment Failure Spike**
- **Condition:** `(sum(rate(payment_failed_total[5m])) / sum(rate(payment_attempts_total[5m]))) > 0.10`
- **For:** 5 minutes
- **Severity:** CRITICAL
- **Channel:** Slack + Email
- **Message:** "💳 Payment failure rate >10%"

**Alert 5: Disk Space Low**
- **Condition:** `(1 - (node_filesystem_avail_bytes / node_filesystem_size_bytes)) > 0.90`
- **For:** 10 minutes
- **Severity:** HIGH
- **Channel:** Slack + Email
- **Message:** "💾 Disk space >90% on {{$labels.instance}}"

**Alert 6: Memory High**
- **Condition:** `(1 - (node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes)) > 0.90`
- **For:** 10 minutes
- **Severity:** HIGH
- **Channel:** Slack
- **Message:** "🧠 Memory usage >90% on {{$labels.instance}}"

---

## Slack Integration

### **Setup Slack Notifications:**

1. Create Slack webhook:
   - Go to https://api.slack.com/apps
   - Create app → Incoming Webhooks
   - Copy webhook URL

2. Add to Grafana:
   - Grafana → Alerting → Contact points
   - Add contact point → Type: Slack
   - Webhook URL: (paste)
   - Save

3. Create notification policy:
   - Route alerts to Slack channel (#alerts)

---

## Daily Workflow (Manager)

### **Morning Check (5 minutes):**

1. Open Grafana: http://monitoring.relayos.com:3000
2. Look at main dashboard:
   - All services green? ✅
   - Error rate normal (<1%)? ✅
   - Revenue trending up? ✅
   - CPU/Memory normal? ✅
3. If something red:
   - Click panel → See details
   - Check logs panel
   - Investigate (SSH, restart service, etc.)
4. Done.

### **If Alert Fires (Slack notification):**

1. Slack: "🚨 Demo IRC network down"
2. Open Grafana → Check logs panel
3. See error: "Connection timeout"
4. SSH into server: `ssh user@demo-irc.relayos.com`
5. Restart service: `sudo systemctl restart inspircd`
6. Grafana shows green again ✅

### **Weekly Review (30 minutes):**

1. Open Grafana revenue dashboard
2. Export metrics to Google Sheets
3. Review trends (conversion, churn, MAU)
4. Share with team
5. Check Stripe/PayPal/CCBill dashboards for payment details

---

## Cost Breakdown

| Component | Cost | Notes |
|-----------|------|-------|
| **Prometheus** | Free | Self-hosted |
| **Loki** | Free | Self-hosted |
| **Grafana** | Free | Self-hosted (or $0-49/month cloud) |
| **Node Exporter** | Free | Lightweight agent |
| **Promtail** | Free | Lightweight agent |
| **Server (observability)** | $10-20/month | 2GB RAM, 1 CPU sufficient |
| **Slack** | Free | Standard plan |
| **Sentry (errors)** | Free | 5K errors/month tier |
| **Total** | **$10-20/month** | Just server hosting cost |

---

## What's NOT in Grafana (Still Separate)

### **1. Sentry (Error Tracking)**
- **Why separate:** Full stack traces, user context, debugging tools
- **Grafana shows:** "50 errors in last hour" (count)
- **Sentry shows:** Full error details, stack trace, affected users
- **When to use:** Only when debugging specific errors (not daily)

### **2. Payment Processor Dashboards**
- **Stripe:** https://dashboard.stripe.com
- **PayPal:** https://www.paypal.com/reports
- **CCBill:** https://admin.ccbill.com
- **Why separate:** Detailed transaction data, disputes, refunds, payouts
- **Grafana shows:** Payment success rate, new subscriptions (metrics)
- **When to use:** Weekly review, investigating payment issues

### **3. WooCommerce Admin (Optional)**
- **Why separate:** Managing subscriptions (cancel, refund, edit)
- **Grafana shows:** Active subscriptions count (metric)
- **WooCommerce shows:** Individual subscription details, customer info
- **When to use:** Manual operations (rare)

---

## Timeline: When to Set Up What

### **Week 0: Bare Minimum**
- Install Prometheus
- Install Grafana
- Add Node Exporter to observability server
- Create basic dashboard (service uptime + server health)
- **Time:** 2 hours

### **Week 1-2: Production Ready**
- Add Loki + Promtail (logs)
- Add Node Exporter to all servers (demo, ISC, BDSMLR)
- Add Blackbox Exporter (uptime checks)
- Create complete dashboard (all metrics)
- Configure alerts
- Test Slack notifications
- **Time:** 4-6 hours

### **Week 4: Demo Network Launch**
- Add IRC-specific metrics (custom exporter)
- Add demo network to monitoring
- Validate: All metrics flowing correctly

### **Week 8: ISC Integration**
- Add ISC to monitoring
- Validate: ISC metrics working

### **Week 12: BDSMLR Integration**
- Add BDSMLR to monitoring
- Add Product B metrics (v2 API)
- Validate: All products monitored

### **Week 16: Launch**
- Add revenue metrics (WordPress DB queries)
- Add payment processor metrics (webhook logging)
- Full observability operational

---

## Success Criteria

### **Week 2: Observability Operational**
- ✅ Grafana dashboard accessible
- ✅ All servers reporting metrics
- ✅ Logs flowing to Loki
- ✅ Alerts configured
- ✅ Slack notifications working

### **Week 4: Demo Network Monitored**
- ✅ Demo IRC network metrics visible
- ✅ Uptime alerts working
- ✅ Manager can see all data in one dashboard

### **Week 16: Full Production Monitoring**
- ✅ All services monitored (demo, ISC, BDSMLR)
- ✅ Revenue metrics visible
- ✅ Business metrics tracked
- ✅ Manager checks dashboard daily (5 min)
- ✅ Alerts notify team when issues occur

---

## Resources & Links

**Prometheus:**
- Website: https://prometheus.io
- Documentation: https://prometheus.io/docs
- Download: https://prometheus.io/download

**Grafana:**
- Website: https://grafana.com
- Documentation: https://grafana.com/docs
- Download: https://grafana.com/grafana/download

**Loki:**
- Website: https://grafana.com/oss/loki
- Documentation: https://grafana.com/docs/loki
- Download: https://github.com/grafana/loki/releases

**Community Dashboards:**
- Grafana Dashboard Library: https://grafana.com/grafana/dashboards
- Node Exporter Dashboard: https://grafana.com/grafana/dashboards/1860

---

**Status:** Ready for implementation  
**Owner:** Network Ops Manager  
**Timeline:** Week 0-4 setup, ongoing monitoring  
**Cost:** $10-20/month (server hosting only)

---

*Created: April 10, 2026*  
*One dashboard to rule them all: Grafana-centric observability*
