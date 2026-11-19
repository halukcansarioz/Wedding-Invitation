# 💍 Wedding Invitation
### (Interactive Digital Wedding Invitation Web Application Built with React, Vite & Supabase)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![React](https://img.shields.io/badge/React-20232A?style=flat&logo=react&logoColor=61DAFB)](#)
[![Vite](https://img.shields.io/badge/Vite-646CFF?style=flat&logo=vite&logoColor=white)](#)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white)](#)
[![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=flat&logo=supabase&logoColor=white)](#)
[![Vercel](https://img.shields.io/badge/Vercel-000000?style=flat&logo=vercel&logoColor=white)](#)
[![Playwright](https://img.shields.io/badge/Playwright-2EAD33?style=flat&logo=playwright&logoColor=white)](#)

This project is an **interactive digital wedding invitation web application** built with React, Vite, TypeScript, and Supabase. Deployed live at [`wedding-invitation-halook.vercel.app`](https://wedding-invitation-halook.vercel.app), it combines a mobile-first **Progressive Web App (PWA)** frontend with real-time RSVP management, Supabase Edge Functions, automated unit/E2E testing, and production-ready Vercel security headers.

---

## 📚 Table of Contents
- [About the Project](#about-the-project)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Installation & Usage](#installation--usage)
- [Project Structure](#project-structure)
- [Available Scripts](#available-scripts)
- [Security & Operational Notes](#security--operational-notes)
- [Development Process](#development-process)
- [Contributing](#contributing)
- [Contact](#contact)
- [License](#license)

---

## About the Project
Sharing wedding details, collecting guest RSVPs, and managing event updates across mobile devices requires a fast, reliable, and visually refined experience. This application delivers a full-stack digital invitation covering **Event Details**, **Interactive RSVP**, **Media & PWA Caching**, **Automated Notifications**, and **Production CI/CD** backed by Supabase PostgreSQL and Vercel.

- **Developer:** Haluk Can SARIÖZ
- **Live Demo:** [wedding-invitation-halook.vercel.app](https://wedding-invitation-halook.vercel.app)

---

## Features
- **Mobile-First PWA Experience** — Responsive invitation design with Progressive Web App support and runtime image caching (`dev-dist` / `vite.config.js`) so heavy images are never precached unnecessarily.
- **Supabase PostgreSQL & RLS** — Idempotent database schema (`src/supabase/supabase-setup.sql`) with Row-Level Security (RLS) policies that preserve existing production data.
- **Supabase Edge Functions & CORS** — Serverless backend functions restricted via the `ALLOWED_ORIGINS` secret for production domain security.
- **Automated Testing Suite** — Unit tests powered by **Vitest** (`vitest.config.js`) and end-to-end browser tests powered by **Playwright** (`playwright.config.js`).
- **Linting & Performance Auditing** — Static analysis with **Oxlint** and **webhint**, plus a custom mobile performance audit script (`.performance-audit.mjs`) reporting JSON metrics.
- **GitHub Actions CI Pipeline** — Automated linting, production dependency audit, unit/E2E testing, and build verification on every push and pull request.
- **Notification Helpers** — Includes standalone email (`send-email.js`) and WhatsApp (`whatsapp_bot.py`) automation scripts for guest outreach.
- **Vercel Security & Monitoring** — Production security headers configured in `vercel.json` with optional **Sentry** (`VITE_SENTRY_DSN`) error tracking.

---

## Technologies Used
- **React, Vite & TypeScript** — Component-based frontend architecture, fast HMR builds, PostCSS styling, and PWA packaging.
- **Supabase (PostgreSQL & Edge Functions)** — Relational database, Row-Level Security (RLS) policies, and serverless backend endpoints.
- **Vitest & Playwright** — Automated unit, coverage, and end-to-end (E2E) browser testing.
- **Oxlint, webhint & GitHub Actions** — Code quality checks, performance auditing, and continuous integration.
- **Vercel, Node.js & Python** — Production hosting (`vercel.json`) and notification helper scripts (`send-email.js`, `whatsapp_bot.py`).

---

## Installation & Usage

### Option A: Local Development

#### 1. Clone the Repository
```bash
git clone https://github.com/halukcansarioz/wedding-invitation.git
```

#### 2. Navigate to the Project Directory
```bash
cd wedding-invitation
```

#### 3. Install Dependencies
```bash
npm install
```

#### 4. Configure Environment Variables & Launch
Create a `.env` file in the root directory with your Supabase credentials:
```env
VITE_SUPABASE_URL=your_supabase_project_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
VITE_SENTRY_DSN=your_optional_sentry_dsn
```

Then start the local Vite development server:
```bash
npm run dev
```

### Option B: Production Deployment (Vercel & Supabase)

#### 1. Apply the Supabase Database Schema
Open the Supabase SQL Editor and run `src/supabase/supabase-setup.sql` to apply idempotent tables and RLS policies.

#### 2. Configure Supabase Edge Function Secrets
Set `ALLOWED_ORIGINS` to your production domain(s):
```env
ALLOWED_ORIGINS=https://your-domain.example,https://www.your-domain.example
```

#### 3. Deploy to Vercel
Add `VITE_SUPABASE_URL`, `VITE_SUPABASE_ANON_KEY`, and (optionally) `VITE_SENTRY_DSN` in Vercel Environment Variables and deploy the `dist/` build output.

> ⚠️ **Note:** Never expose the Supabase `service_role` key in frontend environment variables—keep it strictly inside Supabase Edge Function secrets.

---

## Project Structure
```text
wedding-invitation/
├── .github/workflows/       # GitHub Actions CI workflows (lint, audit, test, build)
├── public/                  # Static public assets
├── src/                     # React + TypeScript source code & Supabase SQL setup
├── supabase/                # Supabase Edge Functions & backend configuration
├── tests/                   # Vitest unit tests & Playwright E2E test suites
├── .performance-audit.mjs   # Mobile resource and image performance audit script
├── index.html               # Application HTML entry point
├── package.json             # Dependencies and npm scripts
├── vite.config.js           # Vite & PWA configuration
├── vitest.config.js         # Vitest unit test configuration
├── playwright.config.js     # Playwright E2E test configuration
├── vercel.json              # Vercel routing and security headers
├── send-email.js            # Email notification helper script
├── whatsapp_bot.py          # WhatsApp notification helper script
└── README.md                # Project documentation
```

---

## Available Scripts
| Command | Action |
| :--- | :--- |
| `npm run dev` | Start the local Vite development server |
| `npm run build` | Build the production bundle into `dist/` |
| `npm run lint` | Run Oxlint static analysis checks |
| `npm run test:unit` | Run Vitest unit tests |
| `npm run test:e2e` | Run Playwright end-to-end tests |
| `npm run test:coverage` | Generate unit test coverage report |
| `npm test` | Run unit and E2E tests sequentially |
| `npm run audit:performance` | Audit mobile resource and image metrics against a running Vite server |

---

## Security & Operational Notes
Camera, microphone, and geolocation features require **HTTPS** and explicit user permission. Production database schemas and RLS policies are managed inside Supabase; never drop existing production schemas when applying updates.

---

## Development Process

### 1. Fork the Repository
Start by forking the project to your own GitHub account.

### 2. Create a New Branch
```bash
git checkout -b feature/invitation-improvement
```

### 3. Push Your Code
```bash
git push origin feature/invitation-improvement
```

---

## Contributing
1. **Fork** this repository.
2. Create a **Branch** (`git checkout -b feature/NewFeature`).
3. Make your changes and **Commit** (`git commit -m 'Add: New feature'`).
4. **Push** your code (`git push origin feature/NewFeature`).
5. Open a **Pull Request**.

---

<a name="contact"></a>
## Contact
**Haluk Can Sarıöz**
- GitHub: [@halukcansarioz](https://github.com/halukcansarioz)
- Email: [halukcansarioz19@gmail.com](mailto:halukcansarioz19@gmail.com)
- LinkedIn: [Haluk Can Sarıöz](https://www.linkedin.com/in/halukcansarioz)

**Project Link:** [https://github.com/halukcansarioz/wedding-invitation](https://github.com/halukcansarioz/wedding-invitation)

---

## License
This project is licensed under the [MIT License](LICENSE).
