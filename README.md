# YOURLS.in — Sovereign URL Shortener & Link Infrastructure

> **Infrastructure v2.5** · Fast 301/302 Engine · Branded Slugs · Click Monetization & ROI

A next-generation, self-hosted URL shortener built for creators, marketers, and businesses who demand **data sovereignty**, **real-time analytics**, and **high-converting branded links**. Convert unwieldy URLs into memorable short links, share them everywhere, and monetize every click — with sub-15ms edge redirection and zero vendor lock-in.

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Tech Stack & Architecture](#-tech-stack--architecture)
- [Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Environment Variables](#environment-variables)
  - [Running Locally](#running-locally)
- [Usage](#-usage)
- [Subscription Plans](#-subscription-plans)
- [Competitive Advantage](#-competitive-advantage)
- [Project Structure](#-project-structure)
- [Roadmap](#-roadmap)
- [FAQ](#-faq)
- [Security & Compliance](#-security--compliance)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🚀 Overview

**YOURLS.in** is a sovereign URL shortener and link management platform. Unlike third-party SaaS alternatives, it puts **you** in control of your data, your links, and your audience — while giving you a full conversion funnel built on top of every short link.

A short link isn't just a compressed URL — it's a **high-yield conversion funnel**. YOURLS.in provides the infrastructure to maximize user trust, reach, and revenue.

### The Three Pillars

| Pillar | What It Does |
|--------|--------------|
| **01 · CONVERT** | Compress messy destination URLs into memorable branded short links with custom slugs, password gates, and dynamic QR codes. |
| **02 · SHARE** | 1-tap broadcasting across WhatsApp, X/Twitter, Instagram Bio, YouTube, LinkedIn, Telegram, newsletters, and ad campaigns. |
| **03 · EARN** | Turn clicks into revenue with affiliate tracking, UTM campaign funnels, geo analytics, and real-time telemetry. |

---

## ✨ Features

### Link Conversion
- **Sub-15ms Edge Redirection** — Clustered DB indexing + lightweight execution for instant 301/302 redirects with no interstitial ads.
- **Instant Slug Engine** — Unique alphanumeric slugs up to 5 characters.
- **Custom Branded Slugs** — Use your own domain and readable paths.
- **Password Gates** — Zero-knowledge bcrypt-protected links; visitors must enter a passcode before proceeding.
- **Dynamic QR Codes** — HTML5 Canvas vector QR generator with watermark-free PNG export for print & packaging.
- **Link Expiration Auto-Disable** — Expired links return HTTP `410 Gone`.

### Sharing & Distribution
- **Multi-Channel Reach** — 1-tap social broadcaster for WhatsApp, X, Instagram, YouTube, LinkedIn, and Telegram.
- **Rich Open Graph Previews** — Clean previews across social platforms.
- **Canonical 301 Redirects** — Protects your social presence from shadowbanning of raw affiliate links.

### Analytics & Monetization
- **Real-Time Click Intelligence** — 14-day timeline charts (Chart.js), top referrer domains, and geographic breakdown.
- **Deep UTM Campaign Builder** — One-click source / medium / campaign parameters; analyze ROI in Google Analytics & CRM tools.
- **Click Monetization & ROI** — Affiliate sales tracking and geographic territory analysis.
- **CSV Telemetry Export** — Unlimited bulk import/export.

### Team & Workspace
- **Multi-Seat Team Workspaces** — Up to 5 seats on Business tier; shared link ownership and delegated permissions.
- **Centralized Analytics** — Unified dashboard across all team links.

### Platform & Security
- **100% Data Sovereignty** — Self-hosted; no third-party data mining.
- **SOC-2 Type II Aligned** — 256-bit SSL encryption.
- **GDPR & CCPA Ready** — Zero-ad guarantee.

---

## 🛠 Tech Stack & Architecture

> The stack below reflects the platform capabilities described in the YOURLS.in product spec. Adjust the versions in your implementation to match your actual deployment.

| Layer | Technology |
|-------|-----------|
| **Backend** | PHP / Node.js (interchangeable link engine) |
| **Database** | Clustered MySQL / MariaDB with indexed slug lookup |
| **Frontend** | HTML5, CSS3, Vanilla JS / framework of choice |
| **Charts** | Chart.js (14-day timeline, referrer & geo breakdown) |
| **QR Engine** | HTML5 Canvas → PNG export |
| **Auth** | Session-based portal + API keys |
| **Redirect Engine** | 301/302 edge router (<15ms) |
| **Password Gate** | bcrypt (zero-knowledge) |
| **Deployment** | Docker / bare-metal · 256-bit TLS |

### Request Lifecycle

```
[Incoming Click] → [Edge Router] → [Slug DB Lookup] → {Password Gate?}
      ├── Yes → [bcrypt Prompt] → [Redirect]
      └── No  → [301/302 Redirect] → [Telemetry Logger] → [Destination]
```

---

## 🏁 Getting Started

### Prerequisites

- PHP 8.1+ **or** Node.js 18+ (depending on your deployment choice)
- MySQL 8.0+ / MariaDB 10.6+
- Composer **or** npm
- A domain with DNS pointing to your host
- SSL certificate (Let's Encrypt recommended)

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/your-org/yourls-in.git
cd yourls-in

# 2. Install dependencies
composer install        # PHP
# or
npm install             # Node

# 3. Copy environment template
cp .env.example .env

# 4. Configure your .env (see below)

# 5. Run database migrations
php artisan migrate     # or: npm run migrate

# 6. Build frontend assets
npm run build

# 7. Start the server
php -S localhost:8000   # or: npm run dev
```

### Environment Variables

```env
# Application
APP_NAME="YOURLS.in"
APP_URL=https://yourls.in
APP_ENV=production
APP_KEY=base64:...

# Database
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=yourls
DB_USERNAME=yourls_user
DB_PASSWORD=secret

# Redirect Engine
REDIRECT_STATUS=301          # 301 | 302
REDIRECT_CACHE_TTL=300

# Security
BCRYPT_ROUNDS=12
PASSWORD_GATE_ENABLED=true

# Analytics
TELEMETRY_RETENTION_DAYS=730
UTM_BUILDER_ENABLED=true

# Billing (Free / Pro / Business)
FREE_TIER_LINKS=50
FREE_TIER_CLICKS=1000
PRO_TIER_LINKS=5000
PRO_TIER_CLICKS=100000
BUSINESS_SEATS=5
```

### Running Locally

```bash
# Start all services (web + worker + scheduler)
docker compose up -d
# or
npm run start:dev
```

Access the dashboard at **`http://localhost:8000/dashboard`**.

---

## 📖 Usage

### Shorten a Link

1. Sign in to your workspace.
2. Paste a long destination URL into the **Shorten** field.
3. *(Optional)* Expand **Advanced Options** to add a custom slug, password gate, or UTM parameters.
4. Click **Shorten & Convert Link**.
5. Copy your branded short link — e.g., `yourls.in/cvn2b`.

### Track Performance

Navigate to **My Shortened Links** → select a link → **Stats**. You'll see:

- 14-day click timeline (Chart.js)
- Top referrer domains
- Geographic breakdown
- UTM campaign performance

### Team Workspaces *(Business Tier)*

Invite up to 5 seats, assign link ownership, delegate permissions, and export centralized CSV telemetry.

---

## 💳 Subscription Plans

| Feature | **Free** | **Pro** | **Business** |
|---------|----------|---------|--------------|
| **Price** | ₹0 /mo | ₹1,000 /mo | ₹10,000 /mo |
| **Short links** | 50 | 5,000 | Unlimited |
| **Monthly clicks** | 1,000 | 100,000 | 1,000,000 |
| **Click history** | 30 days | 2 years | Full historical |
| **Custom slugs** | ❌ | ✅ | ✅ |
| **Password-protected links** | ❌ | ✅ | ✅ |
| **UTM builder** | ❌ | ✅ | ✅ |
| **Team seats** | 1 | 1 | 5 included |
| **API access** | — | Standard | Full + Priority Support |

> **Current default:** Free Tier — 1 active link / 50 quota · 0 / 1,000 monthly clicks (resets Dec 01).

---

## 🏆 Competitive Advantage

| Feature | **** | Bitly | TinyURL |
|---------|:-------------:|:-----:|:-------:|
| 100% Data Sovereignty & Privacy | ✅ Sovereign (Your Host) | ❌ Hosted 3rd Party | ❌ Hosted 3rd Party |
| Custom Branded Slugs | ✅ Included | ⚠️ Limited (Paid) | ⚠️ Limited (Paid) |
| Zero-Knowledge Password Protection | ✅ Cryptographic Lock | ❌ Not Available | ❌ Not Available |
| Link Expiration Auto-Disable | ✅ Included (HTTP 410) | ⚠️ Enterprise Only | ❌ Not Available |
| Team Collaboration (5 Seats) | ✅ ₹10,000/mo | 💰 ₹16,500+/mo | 💰 ₹8,200+/mo |
| Bulk CSV Import & Export | ✅ Unlimited | ⚠️ Restricted | ⚠️ Restricted |

**Why teams choose :** complete data sovereignty, zero vendor lock-in, cryptographic link protection, and predictable pricing.

---

## 📁 Project Structure

```
yourls-in/
├── app/
│   ├── Http/
│   │   ├── Controllers/
│   │   │   ├── LinkController.php        # Shorten, redirect, stats
│   │   │   ├── AnalyticsController.php   # Telemetry & geo breakdown
│   │   │   └── WorkspaceController.php   # Team seats & permissions
│   │   └── Middleware/
│   │       ├── PasswordGate.php          # bcrypt zero-knowledge gate
│   │       └── RedirectStatus.php        # 301 / 302 resolver
│   ├── Models/
│   │   ├── Link.php
│   │   ├── Click.php
│   │   └── Workspace.php
│   └── Services/
│       ├── SlugGenerator.php             # Max 5-char unique slugs
│       ├── QrEngine.php                  # HTML5 Canvas QR export
│       └── TelemetryService.php          # Real-time click logging
├── resources/
│   ├── views/
│   │   ├── dashboard.blade.php
│   │   ├── links/index.blade.php
│   │   └── stats/show.blade.php
│   ├── js/
│   │   ├── charts.js                     # Chart.js 14-day timeline
│   │   └── broadcaster.js                # 1-tap social sharing
│   └── css/
├── database/
│   └── migrations/                       # Links, clicks, workspaces
├── routes/
│   ├── web.php                           # Dashboard & portal
│   └── api.php                           # Developer API
├── docker/
│   └── docker-compose.yml
├── .env.example
├── README.md
└── LICENSE
```

---

## 🗺 Roadmap

- [x] Fast 301/302 redirect engine
- [x] Branded custom slugs (max 5 chars)
- [x] Zero-knowledge password gates
- [x] Real-time click telemetry & geo breakdown
- [x] UTM campaign builder
- [x] Instant vector QR engine
- [x] Multi-seat team workspaces (5 seats)
- [x] CSV bulk import/export
- [ ] Public developer API v1 (Business tier)
- [ ] Webhook event subscriptions
- [ ] Custom domain mapping (bring your own domain)
- [ ] A/B destination testing

---

## ❓ FAQ

**Can I use my own domain?**
Yes —  is self-hosted and sovereign. Point your DNS at your deployment and use branded slugs immediately.

**How fast are redirects?**
Sub-15ms on clustered nodes with no interstitial ads.

**Are password-protected links truly private?**
Yes. Passwords are hashed with bcrypt; the plaintext is never stored.

**What happens when a link expires?**
Expired links return HTTP `410 Gone` automatically.

**Is my click data mined or sold?**
Never. Zero-ad guarantee. GDPR & CCPA ready.

**Can my team collaborate?**
Yes — Business tier includes 5 seats with shared ownership and centralized analytics.

---

## 🔒 Security & Compliance

- **SOC-2 Type II Aligned**
- **256-bit SSL Encryption**
- **Zero-Ad Guarantee**
- **GDPR & CCPA Ready**
- **bcrypt password gates** (12+ rounds)
- **100% Data Sovereignty** — self-hosted, no third-party mining

---

## 🤝 Contributing

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/amazing-feature`.
3. Commit your changes: `git commit -m "feat: add amazing feature"`.
4. Push the branch: `git push origin feature/amazing-feature`.
5. Open a Pull Request.

Please follow the [Conventional Commits](https://www.conventionalcommits.org/) spec and include tests where applicable.

---

## 📄 License

Distributed under the **MIT License**. See [`LICENSE`](./LICENSE) for details.

---

<p align="center">
  <strong></strong> · Next-generation link infrastructure & real-time click telemetry engine.<br/>
  <em>All cluster nodes operational · Completely Independent & Sovereign Platform</em><br/>
  © 2026  Link Infrastructure · Proudly Made in India 🇮🇳
</p>
