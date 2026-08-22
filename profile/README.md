<div align="center">

# Innobox R&R

**A product engineering studio that ships commercial software — desktop, web, mobile and AI.**

Founded and led by **[Homero Raúl Vargas Cruz](https://github.com/hrauvc)** · Toluca, México 🇲🇽

[![GitHub](https://img.shields.io/badge/@hrauvc-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/hrauvc)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/hraulvc)
[![Email](https://img.shields.io/badge/homero.vargascruz@gmail.com-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:homero.vargascruz@gmail.com)

`14+ years shipping software` · `272 repositories` · `14 organizations` · `12 commercial desktop products` · `40+ open-source packages`

</div>

---

## 👋 Who is behind this

I'm **Homero Raúl Vargas Cruz** — Founder & Principal Software Engineer at Innobox R&R.

I started as a full-stack web developer and spent a decade building enterprise systems in **PHP/Laravel + Vue**. Today I design and ship **complete products end to end**: a desktop application framework of my own, a catalog of licensed commercial apps built on top of it, the licensing/billing infrastructure that sells them, the mobile clients, and the AI layer that makes them useful.

I don't just write features. **I build the platform the features stand on.**

> 🎓 M.Sc. in Innovation and Educational Technology · B.Eng. in Systems Engineering · B.A. in Psychology
> 🌍 Spanish (native) · English (advanced) · Open to remote and relocation

---

## 🏗️ The platform: `@innoboxrr/forge`

The centerpiece of everything here. **Forge is a TypeScript framework I built for offline-first, license-sold Electron desktop applications** — the same way Laravel is a framework for web apps, but for software you install, sell and update on a customer's machine.

```
src/kernel        Application lifecycle, service container, bootstrapping
src/database      Migrations, query layer, pluggable drivers, two-way sync
src/auth          Authentication with swappable adapters (local / Supabase / OAuth)
src/licensing     License validation, activation, entitlement enforcement
src/http          Embedded Fastify server bridging renderer ↔ backend
src/jobs          Background job queue
src/events        Event bus and listeners
src/updater       Signed auto-update channel (electron-updater)
src/install       First-run provisioning
src/integrations  Third-party adapters (payments, CFDI, storage, messaging)
src/mcp           Model Context Protocol server — apps expose tools to AI agents
src/interop       Cross-app communication inside the Innobox ecosystem
src/workspace     Multi-tenant workspaces
src/console       CLI tooling and code generation
src/ui            Shared React design system
```

**Interchangeable backends by design:** the exact same application runs against **local SQLite** (fully offline), **Supabase**, or **PostgreSQL** — chosen by configuration, not by rewriting the app.

| | |
|---|---|
| **Runtime** | Electron · Node.js · Fastify · better-sqlite3 |
| **Language** | TypeScript (strict), 100% typed surface |
| **UI** | React 18 · Vite · Lucide |
| **Testing** | Vitest · typecheck gates on every release |
| **Distribution** | electron-builder · code-signed installers · delta auto-updates |
| **AI** | Native MCP server — every app is an agent-callable tool |

Current release: **v0.19.3** — and **12 shipping products depend on it.**

---

## 📦 The catalog — commercial desktop apps built on Forge

Every one of these is a real, versioned, installer-distributed, license-gated product with its own auto-update release channel.

| Product | What it does | Notable engineering |
|---|---|---|
| **[Innobox Hub](https://github.com/innoboxrr/innobox-hub)** `v0.1.44` | Central app manager — one account, installs / updates / sells the entire catalog | Storefront + package manager + SSO in a desktop shell |
| **[LeadOps](https://github.com/innoboxrr/leadops)** `v0.2.20` | Lead generation & prospecting workstation | **Anthropic Claude SDK** for enrichment/qualification · Puppeteer scraping · Leaflet geospatial mapping |
| **[Aprendiz](https://github.com/innoboxrr/aprendiz)** | *"Teach it once and it repeats by itself, on any page or program."* — desktop RPA | Puppeteer-driven task recording & replay, JSDOM-tested |
| **[Clipia](https://github.com/innoboxrr/clipia)** `v0.1.16` | Programmatic video generation studio | **Remotion** render pipeline · FFmpeg/FFprobe · Zustand state |
| **[Facturalista](https://github.com/innoboxrr/facturalista)** `v0.1.18` | Invoicing for the Mexican market | Mexican **CFDI** electronic stamping (Facturama + managed/self-service billing modes) |
| **[Chispa](https://github.com/innoboxrr/chispa)** `v0.1.19` | Children's educational software — buy once, works offline, the child's data never leaves the computer | See engine below |
| **[Chispa · Lectura](https://github.com/innoboxrr/chispa-lectura)** | Reading title in the Chispa vertical | OpenDyslexic & Andika typography, accessibility-first |
| **[Cobraya](https://github.com/innoboxrr/cobraya)** `v0.1.17` | Collections & receivables | Offline-first ledger with sync |
| **[Timegrid](https://github.com/innoboxrr/timegrid)** `v0.3.0` | Scheduling & appointments | Conflict-free slot engine |
| **[Rayita](https://github.com/innoboxrr/rayita)** `v0.1.10` | Catalog productivity app | Full Forge integration (Hub, licensing, interop) |
| **[Tipster](https://github.com/innoboxrr/tipster)** | Web + mobile product | Laravel API + React Native client |
| **[Caso Culpable](https://github.com/innoboxrr/crime)** | Deductive crime-fiction game — *live at [casoculpable.com](https://casoculpable.com)* | **Hexagonal architecture monorepo**: a zero-dependency pure domain, a deterministic *fair-play solver* that proves every case is logically solvable before publication, blind-reader validation, Stripe billing, architecture & secret-scanning CI gates |

### 🧠 `@innoboxrr/chispa` — the learning engine

A pedagogy engine that sits **on top of** Forge: learner profiles, **per-node mastery modeling**, **spaced repetition**, an adaptive session planner, and auto-generated progress material for parents. Built with the **Anthropic SDK** for content generation. `v0.11.3`.

---

## ☁️ The infrastructure that sells it

Building the product is half the job. These are the systems that turn it into a business:

- **[innobox-licensing](https://github.com/innoboxrr/innobox-licensing)** — central multi-product license & sales server. **Supabase Edge Functions (Deno)** + Postgres schema + admin CLI, tested against **PGlite**. Every product in the catalog validates against it.
- **[innobox-gateway](https://github.com/innoboxrr/innobox-gateway)** — managed gateway fronting **S3/R2 storage and AI inference**, with entitlement checks and **credit-based metering**.
- **[innobox-community](https://github.com/innoboxrr/innobox-community)** — the ecosystem's support forum, on isolated Supabase infrastructure.
- **[innobox-factory](https://github.com/innoboxrr/innobox-factory)** / **[innobox-forge](https://github.com/innoboxrr/innobox-forge)** — scaffolding and code generation: a new licensed product goes from zero to installable in hours.
- **Release channels** — a dedicated public repo per product (`*-releases`) serving signed installers and auto-update manifests.

---

## 🤖 AI & Machine Learning

- **Anthropic Claude SDK** integrated in production across LeadOps, Chispa Engine and Caso Culpable.
- **Model Context Protocol (MCP)** — a first-class Forge module: desktop apps expose their capabilities as tools that AI agents can call.
- **[xtts_local](https://github.com/innoboxrr/xtts_local)** — a **Python voice-cloning desktop application**: Coqui XTTS v2 + PyTorch + Transformers, GUI, packaged with **PyInstaller** (custom scipy/transformers hooks) and an **Inno Setup** Windows installer with its own license client. ML that ships as a product, not a notebook.
- **[narrator-xtts](https://github.com/narrator-xtts)** — audio review tooling for the TTS pipeline.
- **AI agents in production platforms** — multi-tenant real estate platform with autonomous agents, AI landing-page generation at scale (**BrandAI**, 20+ generated properties), conversational assistants.
- **Automation** — Puppeteer fleets, WhatsApp automation servers, government-form fillers (**RVOE**), scrapers on AWS Lambda.

---

## 📱 Mobile

**[Tipster Mobile](https://github.com/innoboxrr/tipster-mobile)** — production **React Native 0.81 + Expo (SDK 54)** application:

`expo-router` · `expo-iap` in-app purchases · `expo-notifications` push · `expo-secure-store` · `expo-auth-session` OAuth · `@tanstack/react-query` · `react-hook-form` + Zod · `nativewind` · `i18next` full localization · Reanimated · TypeScript throughout.

Plus a decade of **hybrid and PWA** delivery for the enterprise platforms below.

---

## 🌐 Web platforms — the enterprise track record

Over a decade of multi-tenant, business-critical systems in **Laravel + Vue.js**:

- **[SeguroPro](https://github.com/seguropro)** — a complete CRM for the insurance industry: core engine, landing-page manager, embeddable widgets, campaign infrastructure.
- **[ActualSales](https://github.com/actualsales)** — enterprise sales platform: core services, webhook infrastructure, the *Olympus* backend, and a visual Vue builder. RESTful API design, GitLab CI/CD, legacy-to-modern migrations.
- **[iTec School](https://github.com/itecschool)** — multi-tenant school management: academic control, payment gateways, video processing, audit trails, multi-page app architecture.
- **[EBAT — Escuela de Bellas Artes de Toluca](https://github.com/ebatoluca)** — I founded and led their Technology Department with a team of 8, and built the systems for administration, finance, social service, procedures and R&D.
- **[SiConsulta](https://github.com/siconsulta)** — medical practice platform.
- **[ProfeMX](https://github.com/profemx)** — education platform with **RVOE** regulatory automation.
- **[iTec Systems](https://github.com/itec-systems)** — 70+ conversion-focused React/TypeScript landing pages and micro-SaaS products.
- **[Laravelers Academy](https://github.com/laravelers-academy)** — 25 open teaching repositories. I teach what I build.
- **LMS for Tecnológico de Monterrey** — learning management system with multimedia and assessment.

---

## 🧰 Open source — 40+ published packages

Reusable infrastructure extracted from real production work, on **Packagist** and **npm**:

**Laravel / PHP** — [`larapack-generator`](https://github.com/innoboxrr/larapack-generator) · [`laravel-auth`](https://github.com/innoboxrr/laravel-auth) · [`laravel-audit`](https://github.com/innoboxrr/laravel-audit) · [`omni-billing`](https://github.com/innoboxrr/omni-billing) (+ [Stripe](https://github.com/innoboxrr/omni-billing-stripe) / [PayPal](https://github.com/innoboxrr/omni-billing-paypal) drivers) · [`s3-resumable-uploads`](https://github.com/innoboxrr/s3-resumable-uploads) · [`video-processor`](https://github.com/innoboxrr/video-processor) · [`search-surge`](https://github.com/innoboxrr/search-surge) · [`domain-manager`](https://github.com/innoboxrr/domain-manager) · [`laravel-options`](https://github.com/innoboxrr/laravel-options) · [`twilio-sdk`](https://github.com/innoboxrr/twilio-sdk) · [`zoom-sdk`](https://github.com/innoboxrr/zoom-sdk) · [`google-calendar`](https://github.com/innoboxrr/google-calendar) · [`laravel-tel-input`](https://github.com/innoboxrr/laravel-tel-input) · [`make-bridge`](https://github.com/innoboxrr/make-bridge) · [`composer-deploy-tool`](https://github.com/innoboxrr/composer-deploy-tool) · [`laravel-env-editor`](https://github.com/innoboxrr/laravel-env-editor) · [`wirecomments`](https://github.com/innoboxrr/wirecomments) · [`routes-to-json`](https://github.com/innoboxrr/routes-to-json)

**JavaScript / Vue** — [`form-elements`](https://github.com/innoboxrr/form-elements) · [`vue-datatable`](https://github.com/innoboxrr/vue-datatable) · [`js-validator`](https://github.com/innoboxrr/js-validator) · [`multipart-uploader`](https://github.com/innoboxrr/innoboxrr-multipart-uploader) · [`locale-generator`](https://github.com/innoboxrr/innoboxrr-locale-generator) · [`http-request`](https://github.com/innoboxrr/innoboxrr-http-request) · [`laravel-setup`](https://github.com/innoboxrr/laravel-setup) · [`feedback-visual`](https://github.com/innoboxrr/feedback-visual)

---

## 🛠️ Tech stack

<div align="center">

**Languages**

![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![PHP](https://img.shields.io/badge/PHP-777BB4?style=flat-square&logo=php&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat-square&logo=postgresql&logoColor=white)
![Bash](https://img.shields.io/badge/Bash-4EAA25?style=flat-square&logo=gnubash&logoColor=white)

**Frontend & Desktop**

![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)
![Electron](https://img.shields.io/badge/Electron-47848F?style=flat-square&logo=electron&logoColor=white)
![Vue.js](https://img.shields.io/badge/Vue.js-4FC08D?style=flat-square&logo=vuedotjs&logoColor=white)
![React Native](https://img.shields.io/badge/React_Native-61DAFB?style=flat-square&logo=react&logoColor=black)
![Expo](https://img.shields.io/badge/Expo-000020?style=flat-square&logo=expo&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-646CFF?style=flat-square&logo=vite&logoColor=white)
![Tailwind](https://img.shields.io/badge/Tailwind-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)

**Backend**

![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white)
![Fastify](https://img.shields.io/badge/Fastify-000000?style=flat-square&logo=fastify&logoColor=white)
![Laravel](https://img.shields.io/badge/Laravel-FF2D20?style=flat-square&logo=laravel&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=flat-square&logo=express&logoColor=white)
![Deno](https://img.shields.io/badge/Deno_Edge-000000?style=flat-square&logo=deno&logoColor=white)

**Data**

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3FCF8E?style=flat-square&logo=supabase&logoColor=white)

**Cloud, AI & DevOps**

![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonaws&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Anthropic](https://img.shields.io/badge/Claude_API-D97757?style=flat-square&logo=anthropic&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)
![GitLab CI](https://img.shields.io/badge/GitLab_CI-FC6D26?style=flat-square&logo=gitlab&logoColor=white)
![Stripe](https://img.shields.io/badge/Stripe-635BFF?style=flat-square&logo=stripe&logoColor=white)

</div>

**AWS in production:** EC2 · S3 · Lambda · IAM · Route 53 · SES · CloudWatch · CodeDeploy · CloudTrail
**Practices:** hexagonal architecture · offline-first & sync · monorepos · migrations as code · CI architecture/secret gates · signed releases & delta updates · multi-tenancy · RESTful & SOAP APIs · i18n/l10n · accessibility

---

## 🎯 What I'm good at

**I take a product from idea to a customer's machine, alone or leading a team.** That means: designing the architecture, building the framework, writing the domain logic, shipping the UI, wiring the payments, signing the installer, running the update channel, and keeping it maintainable enough that twelve products can share one codebase.

- **Platform & framework engineering** — Forge is the proof: 20+ modules, adapter-based, 12 dependent products.
- **Desktop application engineering at scale** — Electron, native modules, code signing, auto-update, offline-first data with sync.
- **Full-stack product delivery** — React/TypeScript, Vue, Laravel, Node, React Native.
- **AI-native software** — LLM integration, MCP tooling, local ML inference, autonomous agents.
- **Monetization infrastructure** — licensing servers, entitlements, metered billing, Stripe/PayPal, CFDI.
- **Technical leadership** — founded and ran a technology department (team of 8), and I teach publicly through Laravelers Academy.

---

<div align="center">

## 📫 Let's talk

I'm open to **senior / staff / principal engineering** roles, **technical leadership**, and **consulting** — remote worldwide or relocation.

[![LinkedIn](https://img.shields.io/badge/Connect_on_LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/hraulvc)
[![GitHub](https://img.shields.io/badge/Follow_@hrauvc-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/hrauvc)
[![Email](https://img.shields.io/badge/Email_me-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:homero.vargascruz@gmail.com)

📱 WhatsApp: [+52 729 447 0019](https://wa.me/527294470019)

> *"To build software that is efficient and human-centered — and to keep pushing the boundary of what one engineer can ship."*

</div>
