# 🎬 LUMIQ — Production AI Video Generation Platform

> **Live**: [lumiq.asia](https://lumiq.asia) · **API Docs**: [docs.lumiq.asia](https://docs.lumiq.asia)  
> Solo-built · Serving paying customers · Multi-AI pipeline

---

## ⚠️ Source Code Notice

This is a **showcase repository** documenting the LUMIQ platform.  
**Source code is proprietary and not published here.**  
For technical discussions, code samples, or work references, please [contact me](#contact).

---

## 🚀 What is LUMIQ?

LUMIQ is a production SaaS platform that transforms user-uploaded photos and videos into AI-generated content — face swap avatars, sports fan videos, and cinematic scenes. Built and operated solo, currently handling real payments and paying customers.

**Try it live**: [lumiq.asia](https://lumiq.asia)

---

## ✨ Core Features

### 🎭 AI Avatar Generator
Transform any video into your AI digital human.
- **Face swap** via Kling Motion Control 3.0
- **Voice cloning** via ElevenLabs (7 languages)
- **Innovation**: Demucs-based vocal separation to preserve original background audio while replacing the speaker's voice
- Selectable durations: 10s / 20s / 30s
- Supports aspect ratios: 9:16 / 16:9 / 1:1 / 4:5

### ⚽ Football Fan 2026
Places users in World Cup crowd scenes.
- 48-team support
- GPT-image-2 for hero photo generation
- Claude Sonnet for prompt engineering
- Kling 3.0 for video animation

### 🏆 FIFA Pro
Cinematic 15s football match videos.
- Multi-step AI pipeline
- ByteDance Seedance 2.0 via kie.ai
- User-selectable teams (48 nations)

### 💎 Credit System (Business Logic)
- **FIFO batch tracking** with 30-day expiry
- **Automatic cron-based expiration** (`expire_credits.py`)
- **Refund verification**: Only refunds credits AFTER verifying no upstream API cost was incurred
- **Pro Member status** for paying users
- Multi-tier: Regular users / Admin accounts / Shareholder accounts

### 🔌 Public API
- REST endpoints for programmatic access
- Rate limiting: 30 req/min per key
- Webhook callbacks on completion
- API key management dashboard
- Full documentation at [docs.lumiq.asia](https://docs.lumiq.asia)

---

## 🏗️ Tech Stack

| Layer | Technologies |
|-------|--------------|
| **Backend** | Python · Flask · SQLite |
| **Payments** | Stripe (Checkout + Webhooks) |
| **Auth** | Google OAuth 2.0 · Custom admin auth |
| **AI Integrations** | Anthropic Claude Sonnet 4.6 · OpenAI GPT-image-2 · Kling 3.0 · ElevenLabs · Demucs · ByteDance Seedance 2.0 |
| **Infrastructure** | Ubuntu VPS · Nginx (reverse proxy + SSL) · Let's Encrypt · systemd services · Cron jobs |
| **DNS / Email** | GoDaddy · Cloudflare · Resend |
| **Frontend** | Vanilla JavaScript · Server-rendered HTML · Mobile-first |

---

## 🔧 Engineering Highlights

### Zero-Downtime Domain Migration
Migrated production from `lumiq.my` to `lumiq.asia`, including:
- DNS A records (GoDaddy)
- SSL certificate re-signing (Let's Encrypt with certbot)
- Nginx reverse proxy reconfiguration
- Google OAuth 2.0 redirect URI updates
- Stripe webhook endpoint migration
- Full codebase URL replacement via `sed`
- **Zero user-visible downtime**

### Multi-Tier Authentication System
- **User accounts**: Google OAuth with 8-hour session persistence
- **Admin accounts** (`/admin789xyz`): Password-based, separate credit pool
- **Shareholder pricing**: Discounted admin top-ups
- **API keys**: Public API access with rate limiting

### Robust Error Handling
- Content moderation detection (APIYI content policy rejection → auto-refund)
- Timeout recovery (Nginx 1800s proxy_read_timeout for long AI jobs)
- Automatic stuck-task recovery (background cron scans processing tasks > 15min)
- Refunds only trigger after verifying no upstream API cost was actually incurred

### Multi-Language Support
Voice cloning pipeline supports:
- 🇺🇸 English · 🇨🇳 Chinese · 🇪🇸 Spanish · 🇫🇷 French  
- 🇸🇦 Arabic · 🇵🇹 Portuguese · 🇷🇺 Russian

### Business Logic: Credit Batches
Non-trivial FIFO credit expiry system:
- Each purchase creates a `credit_batch` with 30-day expiry
- Deductions use FIFO ordering (soonest-to-expire first)
- Nightly cron marks expired batches and syncs `users.credits`
- Admin accounts get `expires_at = NULL` (lifetime)
- Refunds create new batches (30-day reset)

---

## 📊 System Scale

- **Live production** with paying customers via Stripe
- **6 credit packages** (from $1.99 to $74.99)
- **Multi-domain setup**: `lumiq.asia` + `docs.lumiq.asia`
- **Uptime**: 99.9% via systemd auto-restart + Nginx failover
- **Payment processing**: Stripe with signed webhooks (HMAC verification)

---

## 🎯 Solo-Built Scope

Everything you see was designed, coded, deployed, and maintained by me:

- ✅ Full-stack architecture & implementation
- ✅ AI API integration & error handling (6+ providers)
- ✅ Payment processing & webhook signature verification
- ✅ DNS / SSL / Nginx / systemd / cron configuration
- ✅ Custom admin panel with real-time credit analytics
- ✅ Credit batch system with auto-expiry & FIFO deduction
- ✅ Public REST API + rate limiting + docs portal
- ✅ Content moderation edge case handling
- ✅ Multi-language voice pipeline (Demucs vocal separation)
- ✅ Domain migration playbook (executed with zero downtime)

---

## 📸 Screenshots

_Screenshots coming soon — see [lumiq.asia](https://lumiq.asia) for live demo._

<!--
Add screenshots here once you have them:
![Homepage](screenshots/01-homepage.png)
![Avatar Generator](screenshots/02-avatar.png)
![My Videos](screenshots/03-my-videos.png)
![Admin Dashboard](screenshots/04-admin.png)
![Pricing](screenshots/05-pricing.png)
-->

---

## 🌐 Live Demo

**Best way to see it**: Visit [lumiq.asia](https://lumiq.asia)

- Sign in with Google (new users get 50 free credits)
- Try the Avatar Generator or Football Fan
- Explore the Pricing page and Public API dashboard

**API Documentation**: [docs.lumiq.asia](https://docs.lumiq.asia)

---

## 💼 About This Project

- **Duration**: 6+ months of active development
- **Role**: Founder · Full-stack engineer · Solo operator
- **Status**: Production · Actively maintained · Growing

---

## 📬 Contact

- 📧 Email: [contact me via lumiq.asia](https://lumiq.asia)
- 🌐 Portfolio: [github.com/kelvin-builds](https://github.com/kelvin-builds)
- 📍 Kuala Lumpur, Malaysia 🇲🇾

---

## 🔒 Copyright

© 2026 LUMIQ. All rights reserved. Source code is proprietary and not released under this repository.

This showcase repository is for portfolio and reference purposes only.
