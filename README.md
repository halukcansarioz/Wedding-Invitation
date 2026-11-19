# 💍 Wedding Invitation

### (Interactive Digital Wedding Invitation Web Application Built with React, Vite & Supabase)

This project is an **interactive digital wedding invitation web application** built with React, Vite, TypeScript, and Supabase. Deployed live at [`wedding-invitation-halook.vercel.app`](https://wedding-invitation-halook.vercel.app), it combines a mobile-first **Progressive Web App (PWA)** frontend with real-time RSVP management, Supabase Edge Functions, automated unit/E2E testing, and production-ready Vercel security headers.

## 📚 Table of Contents

* [About the Project](https://www.google.com/search?q=%23about-the-project)

* [Features](https://www.google.com/search?q=%23features)

* [Technologies Used](https://www.google.com/search?q=%23technologies-used)

* [Installation & Usage](https://www.google.com/search?q=%23installation--usage)

* [Project Structure](https://www.google.com/search?q=%23project-structure)

* [Available Scripts](https://www.google.com/search?q=%23available-scripts)

* [Security & Operational Notes](https://www.google.com/search?q=%23security--operational-notes)

* [Development Process](https://www.google.com/search?q=%23development-process)

* [Contributing](https://www.google.com/search?q=%23contributing)

* [Contact](https://www.google.com/search?q=%23contact)

* [License](https://www.google.com/search?q=%23license)

## About the Project

Sharing wedding details, collecting guest RSVPs, and managing event updates across mobile devices requires a fast, reliable, and visually refined experience. This application delivers a full-stack digital invitation covering **Event Details**, **Interactive RSVP**, **Media & PWA Caching**, **Automated Notifications**, and **Production CI/CD** backed by Supabase PostgreSQL and Vercel.

* **Developer:** Haluk Can SARIÖZ

* **Live Demo:** [wedding-invitation-halook.vercel.app](https://wedding-invitation-halook.vercel.app)

## Features

* **Mobile-First PWA Experience** — Responsive invitation design with Progressive Web App support and runtime image caching (`dev-dist` / `vite.config.js`) so heavy images are never precached unnecessarily.

* **Supabase PostgreSQL & RLS** — Idempotent database schema (`src/supabase/supabase-setup.sql`) with Row-Level Security (RLS) policies that preserve existing production data.

* **Supabase Edge Functions & CORS** — Serverless backend functions restricted via the `ALLOWED_ORIGINS` secret for production domain security.

* **Automated Testing Suite** — Unit tests powered by **Vitest** (`vitest.config.js`) and end-to-end browser tests powered by **Playwright** (`playwright.config.js`).

* **Linting & Performance Auditing** — Static analysis with **Oxlint** and **webhint**, plus a custom mobile performance audit script (`.performance-audit.mjs`) reporting JSON metrics.

* **GitHub Actions CI Pipeline** — Automated linting, production dependency audit, unit/E2E testing, and build verification on every push and pull request.

* **Notification Helpers** — Includes standalone email (`send-email.js`) and WhatsApp (`whatsapp_bot.py`) automation scripts for guest outreach.

* **Vercel Security & Monitoring** — Production security headers configured in `vercel.json` with optional **Sentry** (`VITE_SENTRY_DSN`) error tracking.

## Technologies Used

* **React, Vite & TypeScript** — Component-based frontend architecture, fast HMR builds, PostCSS styling, and PWA packaging.

* **Supabase (PostgreSQL & Edge Functions)** — Relational database, Row-Level Security (RLS) policies, and serverless backend endpoints.

* **Vitest & Playwright** — Automated unit, coverage, and end-to-end (E2E) browser testing.

* **Oxlint, webhint & GitHub Actions** — Code quality checks, performance auditing, and continuous integration.

* **Vercel, Node.js & Python** — Production hosting (`vercel.json`) and notification helper scripts (`send-email.js`, `whatsapp_bot.py`).

## Installation & Usage

### Option A: Local Development

#### 1. Clone the Repository

```
git clone https://github.com/halukcansarioz/wedding-invitation.git

```

#### 2. Navigate to the Project Directory

```
cd wedding-invitation

```

#### 3. Install Dependencies

```
npm install

```

#### 4. Configure Environment Variables & Launch

Create a `.env` file in the root directory with your Supabase credentials:

```
VITE_SUPABASE_URL=your_supabase_project_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
VITE_SENTRY_DSN=your_optional_sentry_dsn

```

Then start the local Vite development server:

```
npm run dev

```

### Option B: Production Deployment (Vercel & Supabase)

#### 1. Apply the Supabase Database Schema

Open the Supabase SQL Editor and run `src/supabase/supabase-setup.sql` to apply idempotent tables and RLS policies.

#### 2. Configure Supabase Edge Function Secrets

Set `ALLOWED_ORIGINS` to your production domain(s):

```
ALLOWED_ORIGINS=https://your-domain.example,https://www.your-domain.example

```

#### 3. Deploy to Vercel

Add `VITE_SUPABASE_URL`, `VITE_SUPABASE_ANON_KEY`, and (optionally) `VITE_SENTRY_DSN` in Vercel Environment Variables and deploy the `dist/` build output.

> ⚠️ **Note:** Never expose the Supabase `service_role` key in frontend environment variables—keep it strictly inside Supabase Edge Function secrets.

## Project Structure

```
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

## Available Scripts

| Command | Action | 
| ----- | ----- | 
| `npm run dev` | Start the local Vite development server | 
| `npm run build` | Build the production bundle into `dist/` | 
| `npm run lint` | Run Oxlint static analysis checks | 
| `npm run test:unit` | Run Vitest unit tests | 
| `npm run test:e2e` | Run Playwright end-to-end tests | 
| `npm run test:coverage` | Generate unit test coverage report | 
| `npm test` | Run unit and E2E tests sequentially | 
| `npm run audit:performance` | Audit mobile resource and image metrics against a running Vite server | 

## Security & Operational Notes

Camera, microphone, and geolocation features require **HTTPS** and explicit user permission. Production database schemas and RLS policies are managed inside Supabase; never drop existing production schemas when applying updates.

## Development Process

### 1. Fork the Repository

Start by forking the project to your own GitHub account.

### 2. Create a New Branch

```
git checkout -b feature/invitation-improvement

```

### 3. Push Your Code

```
git push origin feature/invitation-improvement

```

## Contributing

1. **Fork** this repository.

2. Create a **Branch** (`git checkout -b feature/NewFeature`).

3. Make your changes and **Commit** (`git commit -m 'Add: New feature'`).

4. **Push** your code (`git push origin feature/NewFeature`).

5. Open a **Pull Request**.

<a name="contact"></a>

## Contact

**Haluk Can Sarıöz**

* GitHub: [@halukcansarioz](https://github.com/halukcansarioz)

* Email: [halukcansarioz19@gmail.com](https://www.google.com/search?q=mailto%3Ahalukcansarioz19%40gmail.com)

* LinkedIn: [Haluk Can Sarıöz](https://www.linkedin.com/in/halukcansarioz)

**Project Link:** <https://github.com/halukcansarioz/wedding-invitation>

## License

This project is licensed under the [MIT License](https://www.google.com/search?q=LICENSE).