# HisabAI — المحاسبة الذكية 🧾🤖

> **AI-Powered Accounting Platform for Moroccan SMBs**
> منصة محاسبة ذكية للمقاولات المغربية الصغيرة

---

## 🖼️ Homepage Preview

![HisabAI Homepage](./hisabai-frontend/public/logo.png)

> Full RTL Arabic landing page with dark navy background (`#050D1A`) — includes Navbar, Hero, Stats Bar, Features, Fintech News, How It Works, Dashboard Preview, Pricing, Testimonials, CTA Banner, and Footer.

---

## 📌 What is HisabAI?

**HisabAI** is a full-stack SaaS accounting platform built for small and medium Moroccan businesses. It combines traditional double-entry bookkeeping with AI-powered financial insights, anomaly detection, invoice management, tax tracking, and multi-channel integrations (WhatsApp, Gmail, OCR).

---

## 🗂️ Monorepo Structure

```
New folder/
├── hisabai-frontend/        # Next.js 14 frontend (TypeScript)
└── server project/
    └── hisabai-api/         # Express.js REST API (Node.js)
```

---

## 🏗️ Architecture

```
Browser (Next.js :3000)
        │
        ▼
  /api/proxy/* (Next.js API route — reverse proxy)
        │
        ▼
Express API (Node.js :3001)
        │
        ├── Supabase (PostgreSQL) ── data storage & auth
        ├── Anthropic Claude ──────── AI financial assistant
        ├── OpenRouter ────────────── alternative AI models
        └── Twilio ────────────────── WhatsApp messaging
```

---

## ✨ Features

| Feature | Description |
|---|---|
| 📊 Dashboard | KPI cards (revenue, expenses, net profit, TVA due), revenue charts, recent invoices |
| 🧾 Invoices | Create, validate, pay, cancel invoices with PDF generation & digital signature |
| 📒 Accounting | Double-entry journal entries with validation |
| 🏦 Bank | Bank accounts management & transaction reconciliation |
| 👥 Contacts | Clients & suppliers directory |
| 💰 Taxes | TVA declarations & tax deadlines tracking |
| 🔔 Smart Alerts | AI-generated financial alerts & notifications |
| 🤖 AI Assistant | Chat-based financial Q&A powered by Claude / OpenRouter |
| 🔍 Anomaly Detection | AI scans transactions for unusual patterns |
| 📧 Gmail Integration | Extract financial data from Gmail |
| 📷 OCR | Scan invoices & receipts via image recognition |
| 💬 WhatsApp | Send financial reports & alerts via WhatsApp (Twilio) |
| 📰 Fintech News | Live fintech news feed |
| ⚙️ Settings | Company profile, logo upload, preferences |

---

## 🛠️ Full Tech Stack

| Layer | Technology |
|---|---|
| Frontend Framework | Next.js 14 (App Router) |
| Language | TypeScript (frontend) / JavaScript (backend) |
| Styling | Tailwind CSS + Radix UI |
| Charts | Recharts |
| Animations | Framer Motion |
| Forms | React Hook Form + Zod |
| Backend Framework | Express.js 5 |
| Database | Supabase (PostgreSQL) |
| Auth | Supabase Auth + JWT |
| AI | Anthropic Claude, OpenRouter, Ollama |
| PDF | pdf-lib |
| Messaging | Twilio (WhatsApp / SMS) |
| HTTP Client | Axios |
| Security | Helmet.js + CORS |
| Notifications | react-hot-toast |

---

# 🖥️ Frontend — `hisabai-frontend`

### Folder Structure

```
hisabai-frontend/
├── app/
│   ├── (auth)/              # Login & Register pages
│   ├── (dashboard)/         # All dashboard pages
│   │   ├── dashboard/       # Main KPI dashboard
│   │   ├── invoices/        # Invoice list & creation
│   │   ├── accounting/      # Journal entries
│   │   ├── bank/            # Bank accounts & transactions
│   │   ├── contacts/        # Clients & suppliers
│   │   ├── taxes/           # TVA declarations & deadlines
│   │   ├── alerts/          # Smart alerts
│   │   ├── ai-assistant/    # AI chat assistant
│   │   ├── apps/            # Integrations (Gmail, OCR, WhatsApp)
│   │   ├── news/            # Fintech news
│   │   └── settings/        # Company settings
│   ├── api/                 # Next.js API routes (proxy + AI)
│   └── page.tsx             # Landing page
├── components/
│   ├── landing/             # Landing page sections
│   ├── dashboard/           # KPI cards, charts, widgets
│   ├── ai/                  # Anomaly banner, AI feedback
│   ├── signature/           # Draw / type / upload signature
│   ├── layout/              # Sidebar & Header
│   └── ui/                  # Shared UI components
├── hooks/                   # Custom React hooks
├── lib/
│   ├── api.ts               # Axios API client + all API functions
│   ├── supabase.ts          # Supabase client
│   ├── openrouter.ts        # OpenRouter AI client
│   └── utils.ts             # Utility helpers
└── public/                  # Static assets & logos
```

### Next.js API Routes

| Route | Method | Description |
|---|---|---|
| `/api/proxy/[...path]` | ALL | Reverse proxy to backend API |
| `/api/ai-chat` | POST | AI chat completions |
| `/api/anomaly` | POST | Anomaly detection scan |
| `/api/smart-alerts` | POST | Generate smart alerts |
| `/api/auth/login` | POST | User authentication |
| `/api/invoices/sign` | POST | Sign invoice PDF |
| `/api/ocr` | POST | OCR document scanning |
| `/api/gmail-extract` | POST | Extract data from Gmail |
| `/api/whatsapp/send` | POST | Send WhatsApp message |
| `/api/whatsapp/webhook` | POST | Receive WhatsApp messages |
| `/api/fintech-news` | GET | Fetch fintech news |
| `/api/upload-logo` | POST | Upload company logo |
| `/api/realtime-ai` | GET | Realtime AI stream |

### Environment Variables (`.env.local`)

```env
NEXT_PUBLIC_API_URL=http://127.0.0.1:3001/api
NEXT_PUBLIC_SUPABASE_URL=<your_supabase_url>
NEXT_PUBLIC_SUPABASE_ANON_KEY=<your_supabase_anon_key>
NEXT_PUBLIC_COMPANY_ID=<your_default_company_id>
NEXT_PUBLIC_APP_URL=http://127.0.0.1:3000

# AI
ANTHROPIC_API_KEY=<your_anthropic_api_key>
OLLAMA_API_KEY=<your_ollama_api_key>
OLLAMA_MODEL=mistral-large-3:675b-cloud
OLLAMA_URL=https://ollama.com/api/chat

# WhatsApp / Twilio
TWILIO_ACCOUNT_SID=<your_twilio_account_sid>
TWILIO_AUTH_TOKEN=<your_twilio_auth_token>
TWILIO_WHATSAPP_NUMBER=whatsapp:+<your_number>
```

### Run Frontend

```bash
cd hisabai-frontend
npm install
npm run dev        # http://localhost:3000
npm run build      # production build
npm start          # production server
```

---

# ⚙️ Backend — `hisabai-api`

### Folder Structure

```
hisabai-api/
├── src/
│   ├── app.js                  # Express app entry point
│   ├── config/
│   │   └── supabase.js         # Supabase client config
│   ├── middleware/
│   │   ├── auth.js             # JWT authentication
│   │   ├── errorHandler.js     # Global error handler
│   │   └── validate.js         # Request validation
│   ├── routes/
│   │   ├── index.js            # Route aggregator
│   │   ├── companies.js
│   │   ├── users.js
│   │   ├── contacts.js
│   │   ├── invoices.js
│   │   ├── invoiceLines.js
│   │   ├── journalEntries.js
│   │   ├── bankAccounts.js
│   │   ├── bankTransactions.js
│   │   ├── taxes.js
│   │   ├── alerts.js
│   │   ├── ai.js
│   │   └── whatsapp.js
│   └── services/
│       ├── aiService.js        # Anthropic Claude logic
│       ├── contextService.js   # Financial context builder
│       ├── invoiceService.js   # Invoice business logic
│       ├── journalService.js   # Journal automation
│       ├── sessionService.js   # AI conversation sessions
│       ├── taxService.js       # Tax calculations
│       └── whatsappService.js  # Twilio WhatsApp
├── seed.js                     # Database seeder
├── seed2.js                    # Additional seed data
└── whatsapp_migration.sql      # WhatsApp schema migration
```

### API Endpoints

#### 🏢 Companies
| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/companies` | List all companies |
| GET | `/api/companies/:id` | Get company by ID |
| POST | `/api/companies` | Create company |
| PUT | `/api/companies/:id` | Update company |

#### 👥 Contacts
| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/contacts` | List contacts |
| POST | `/api/contacts` | Create contact |
| PUT | `/api/contacts/:id` | Update contact |
| DELETE | `/api/contacts/:id` | Delete contact |

#### 🧾 Invoices
| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/invoices` | List invoices |
| POST | `/api/invoices` | Create invoice + lines |
| PUT | `/api/invoices/:id/validate` | Validate (creates journal entry) |
| PUT | `/api/invoices/:id/pay` | Mark as paid |
| DELETE | `/api/invoices/:id` | Delete invoice |

#### 📒 Journal
| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/journal` | List journal entries |
| POST | `/api/journal` | Create entry |
| PUT | `/api/journal/:id/validate` | Validate entry |

#### 🏦 Bank
| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/bank-accounts` | List bank accounts |
| POST | `/api/bank-accounts` | Create account |
| GET | `/api/bank-transactions` | List transactions |
| POST | `/api/bank-transactions` | Create transaction |
| PUT | `/api/bank-transactions/:id/reconcile` | Reconcile transaction |

#### 💰 Taxes
| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/taxes/tva` | List TVA declarations |
| POST | `/api/taxes/tva` | Create declaration |
| GET | `/api/taxes/deadlines` | List deadlines |
| POST | `/api/taxes/deadlines` | Create deadline |
| PUT | `/api/taxes/deadlines/:id/pay` | Mark as paid |

#### 🔔 Alerts
| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/alerts` | List alerts |
| POST | `/api/alerts` | Create alert |
| PUT | `/api/alerts/:id/read` | Mark as read |
| DELETE | `/api/alerts/:id` | Delete alert |

#### 🤖 AI
| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/ai/chat` | AI financial Q&A |
| POST | `/api/ai/ocr` | OCR extraction |

#### 💬 WhatsApp
| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/whatsapp/send` | Send message |
| POST | `/api/whatsapp/webhook` | Receive messages |
| GET | `/api/whatsapp/poll` | Poll new messages |

#### ❤️ Health
| Method | Endpoint | Description |
|---|---|---|
| GET | `/health` | Server health check |

### Environment Variables (`.env`)

```env
PORT=3001

# Supabase
SUPABASE_URL=<your_supabase_url>
SUPABASE_SERVICE_KEY=<your_supabase_service_role_key>

# AI
OPENROUTER_API_KEY=<your_openrouter_api_key>
OPENROUTER_MODEL=<model_name>
ANTHROPIC_API_KEY=<your_anthropic_api_key>

# WhatsApp / Twilio
TWILIO_ACCOUNT_SID=<your_twilio_account_sid>
TWILIO_AUTH_TOKEN=<your_twilio_auth_token>
TWILIO_WHATSAPP_NUMBER=whatsapp:+<your_number>
```

### Run Backend

```bash
cd "server project/hisabai-api"
npm install
npm run dev        # http://localhost:3001 (with nodemon)
npm start          # production
```

### Seed Database

```bash
node seed.js       # initial seed
node seed2.js      # additional data
```

---

## 🚀 Running the Full Stack

```bash
# Terminal 1 — Backend
cd "server project/hisabai-api"
npm install && npm run dev

# Terminal 2 — Frontend
cd hisabai-frontend
npm install && npm run dev
```

Then open [http://localhost:3000](http://localhost:3000)

---

## 🌍 Localization

- Full **RTL** (Right-to-Left) layout
- Arabic UI with `lang="ar"` and `dir="rtl"`
- Font: **Tajawal** (Arabic-optimized)
- Aligned with **Moroccan tax regulations** (TVA system)

---

## 📄 License

Private — All rights reserved © HisabAI
