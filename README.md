# 🚀 FlyRank — Front-End AI Engineering Capstone

<p align="center">
  <strong>Next-Generation Search Ranking Intelligence & Semantic SERP Analytics Powered by Generative AI</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Next.js-14+-black?style=for-the-badge&logo=next.js&logoColor=white" alt="Next.js" />
  <img src="https://img.shields.io/badge/TypeScript-5.x-blue?style=for-the-badge&logo=typescript&logoColor=white" alt="TypeScript" />
  <img src="https://img.shields.io/badge/Tailwind_CSS-3.4+-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white" alt="Tailwind CSS" />
  <img src="https://img.shields.io/badge/AI_SDK-Vercel-black?style=for-the-badge&logo=vercel&logoColor=white" alt="Vercel AI SDK" />
  <img src="https://img.shields.io/badge/Conventional_Commits-1.0.0-FE5196?style=for-the-badge&logo=conventionalcommits&logoColor=white" alt="Conventional Commits" />
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License" />
</p>

---

## 📖 Table of Contents

- [Project Overview](#-project-overview)
- [Key Features](#-key-features)
- [Front-End AI Engineering Highlights](#-front-end-ai-engineering-highlights)
- [Tech Stack](#-tech-stack)
- [Repository Structure](#-repository-structure)
- [Getting Started](#-getting-started)
- [Environment Variables](#-environment-variables)
- [Development Scripts](#-development-scripts)
- [Commit Conventions](#-commit-conventions)
- [Capstone Milestones](#-capstone-milestones)
- [License & Author](#-license--author)

---

## 🌟 Project Overview

**FlyRank** is an intelligent, high-performance web platform built as a **Front-End AI Engineering Capstone Project**. Traditional search ranking and SEO analytics dashboards often present massive, static tables of metrics without contextual insights or actionable guidance. 

FlyRank bridges this gap by marrying modern front-end web engineering with generative AI streaming:
- It processes search engine result page (SERP) metrics, ranking volatility, and keyword intelligence.
- It leverages large language models (LLMs) via streaming interfaces to synthesize complex ranking shifts into immediate, human-readable competitive insights.
- It delivers a state-of-the-art user experience featuring optimistic UI updates, streaming response rendering, responsive data visualization, and accessible interface design.

---

## ✨ Key Features

- **⚡ Real-Time Streaming AI Copilot**: Instantaneous SERP diagnostics, anomaly explanations, and ranking recommendations with token-by-token streaming and zero layout shifts.
- **📊 Interactive Ranking Dashboards**: Dynamic charts tracking keyword position fluctuations, search volume, click-through estimates, and competitor movement.
- **🔍 Semantic Keyword & Gap Analysis**: AI-assisted keyword grouping, search intent classification, and content optimization recommendations.
- **🎨 Modern, Adaptive Design**: Fully responsive interface crafted with Tailwind CSS, supporting seamless light and dark mode switching with WCAG 2.1 AA accessibility.
- **🛡️ End-to-End Type Safety**: Robust schema validation using Zod coupled with strict TypeScript contracts for runtime and compile-time reliability.
- **🏎️ Next.js App Router Architecture**: Hybrid rendering using React Server Components (RSC) for fast initial paint and selective Client Components for rich interactivity.

---

## 🧠 Front-End AI Engineering Highlights

This capstone project incorporates leading architectural patterns in front-end AI engineering:

1. **Streaming UI & Perceived Latency Optimization**:
   - Integrates the Vercel AI SDK with Next.js route handlers to stream model responses.
   - Employs smooth auto-scrolling containers and skeleton states to ensure zero cumulative layout shift (CLS).
2. **Schema-Driven Structured Outputs**:
   - Enforces deterministic JSON outputs from language models using Zod schemas for automated UI rendering of ranking cards, tables, and tag badges.
3. **Human-in-the-Loop Interactivity**:
   - Rich interactive controls including response cancellation, regeneration, clipboard copying, and user feedback loops.
4. **Resilient Error Recovery & Rate Limiting**:
   - Built-in graceful degradation, exponential backoff handling, and informative UI banners for API rate limits and connection interruptions.
5. **Security & Key Management**:
   - Server-side isolation of API credentials; client components never handle private LLM API tokens.

---

## 🛠️ Tech Stack

| Category | Technology | Purpose |
| :--- | :--- | :--- |
| **Framework** | [Next.js](https://nextjs.org/) (App Router) | Server Components, hybrid rendering, and streaming API routes |
| **Language** | [TypeScript](https://www.typescriptlang.org/) | End-to-end static type safety and strict compiler rules |
| **Styling** | [Tailwind CSS](https://tailwindcss.com/) | Utility-first CSS, responsive styling, and design system variables |
| **AI Integration** | [Vercel AI SDK](https://sdk.vercel.ai/) | Client hooks (`useChat`, `useCompletion`) and streaming utilities |
| **AI Providers** | OpenAI / Anthropic APIs | Foundation models for semantic SERP and ranking synthesis |
| **UI Primitives** | Radix UI / Shadcn UI | Accessible, unstyled UI primitives and interactive components |
| **Icons** | [Lucide React](https://lucide.dev/) | Consistent, lightweight SVG icon system |
| **Validation** | [Zod](https://zod.dev/) | Runtime validation for API payloads, forms, and AI outputs |
| **State & Fetching** | React Server Components & SWR | Efficient client cache synchronization and server-side fetching |
| **Code Quality** | ESLint, Prettier, Husky | Automated linting, code formatting, and git commit hooks |
| **Commit Standard**| Conventional Commits | Structured, semantic git history for automated release workflows |

---

## 📁 Repository Structure

```plaintext
flyrank-frontend-ai-capstone/
├── app/                          # Next.js App Router root
│   ├── (auth)/                   # Authentication route group (login, register)
│   ├── (dashboard)/              # Authenticated user dashboard & analytics
│   │   ├── analytics/            # Detailed ranking & SERP analytics views
│   │   ├── keywords/             # Keyword tracking & gap exploration
│   │   └── page.tsx              # Primary dashboard overview
│   ├── api/                      # Server-side API route handlers
│   │   ├── ai/                   # Streaming AI endpoints (chat, SERP synthesis)
│   │   └── ranking/              # Search ranking metric endpoints
│   ├── favicon.ico               # Application favicon
│   ├── globals.css               # Base styles & Tailwind directives
│   ├── layout.tsx                # Global root layout with theme providers
│   └── page.tsx                  # Marketing / landing hero page
├── components/                   # Modular React component architecture
│   ├── ai/                       # AI-specific components (ChatWidget, StreamViewer)
│   ├── charts/                   # Data visualizers (RankingTrends, VolumeBarChart)
│   ├── layout/                   # Structural components (Navbar, Sidebar, Footer)
│   └── ui/                       # Reusable UI primitives (Button, Card, Modal, Input)
├── hooks/                        # Custom reusable React hooks
├── lib/                          # Shared libraries and server utilities
│   ├── ai/                       # LLM client setup, prompt templates, and streaming helpers
│   ├── utils.ts                  # Class merge utility (cn) and formatting helpers
│   └── validators/               # Zod schemas for runtime validation
├── types/                        # Shared TypeScript types, interfaces, and DTOs
├── public/                       # Static public assets (images, logos, fonts)
├── .env.example                  # Template for environment configuration
├── .gitignore                    # Git ignored patterns and build artifacts
├── CLAUDE.md                     # Agent coding rules & development specifications
├── LICENSE                       # Project license (MIT)
├── package.json                  # Dependencies, scripts, and package metadata
├── tailwind.config.ts            # Tailwind styling tokens and theme configuration
├── tsconfig.json                 # TypeScript compiler configuration
└── README.md                     # Capstone project documentation
```

---

## 🚀 Getting Started

### Prerequisites

Ensure you have the following installed on your development machine:
- **Node.js**: `v18.18.0` or higher (LTS recommended)
- **npm**: `v9.x` or higher (or `pnpm` / `yarn`)
- **Git**

### Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/OnikTechHub/flyrank-frontend-ai-capstone.git
   cd flyrank-frontend-ai-capstone
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Configure environment variables**:
   ```bash
   cp .env.example .env.local
   ```
   Open `.env.local` and add your respective API keys.

4. **Launch the development server**:
   ```bash
   npm run dev
   ```
   Open [http://localhost:3000](http://localhost:3000) in your browser to view the application.

---

## 🔐 Environment Variables

Create a `.env.local` file in the root directory. Required variables include:

```env
# Application
NEXT_PUBLIC_APP_URL=http://localhost:3000

# AI Provider API Keys (Server-side only, never expose with NEXT_PUBLIC_)
OPENAI_API_KEY=your_openai_api_key_here
ANTHROPIC_API_KEY=your_anthropic_api_key_here

# Optional: SERP Data Provider (e.g., ValueSERP, SerpAPI)
SERP_API_KEY=your_serp_provider_api_key_here
```

---

## 💻 Development Scripts

The following commands are configured for development, quality assurance, and building:

| Command | Description |
| :--- | :--- |
| `npm run dev` | Starts the Next.js development server with hot-reloading |
| `npm run build` | Compiles the production-ready build |
| `npm run start` | Serves the production build locally |
| `npm run lint` | Runs ESLint to verify code quality and rule adherence |
| `npm run lint:fix` | Automatically fixes autofixable ESLint issues |
| `npm run type-check` | Runs `tsc --noEmit` to validate all TypeScript types |
| `npm run format` | Formats all code with Prettier |
| `npm run format:check` | Verifies code conforms to Prettier formatting rules |
| `npm test` | Executes unit and integration test suites |

---

## 📝 Commit Conventions

This project enforces the **Conventional Commits** standard to maintain clean, readable git histories and support automated versioning.

Format:
```plaintext
<type>(<scope>): <short description>
```

### Commit Types
- `feat`: A new feature (e.g., `feat(ai): add streaming SERP summary generator`)
- `fix`: A bug fix (e.g., `fix(ui): correct dark mode contrast on ranking badge`)
- `docs`: Documentation updates (e.g., `docs(readme): add installation guide`)
- `style`: Code style/formatting changes without logic alterations
- `refactor`: Refactoring code without changing behavior or fixing bugs
- `perf`: Performance improvements
- `test`: Adding or updating unit/integration tests
- `build`: Dependency or build tool updates
- `ci`: CI/CD workflow configuration updates
- `chore`: Repository maintenance and housekeeping

---

## 🗺️ Capstone Milestones

- [x] **Milestone 1: Project Setup & Engineering Architecture**
  - Project configuration, TypeScript strict rules, Tailwind system tokens.
  - Standardized development rules (`CLAUDE.md`) and documentation (`README.md`).
- [ ] **Milestone 2: Design System & Core Dashboard Layout**
  - Implement navigation, shell layout, and responsive metric cards.
  - Integrate interactive chart components for ranking trajectory and keyword volume.
- [ ] **Milestone 3: Real-Time AI Copilot & Streaming Intelligence**
  - Deploy server-side AI route handlers with token streaming.
  - Implement chat widget with optimistic feedback, stop/regenerate, and markdown rendering.
- [ ] **Milestone 4: SERP Ingestion & Semantic Gap Explorer**
  - Connect search ranking data ingestion pipeline.
  - Provide AI-driven semantic gap audits with exportable reports.
- [ ] **Milestone 5: Production Hardening, Testing & Deployment**
  - End-to-end integration tests, WCAG 2.1 AA accessibility audit, and Vercel edge deployment.

---

## 📄 License & Author

- **Author**: [Onik Das](https://github.com/OnikTechHub)
- **License**: Distributed under the **MIT License**. See [LICENSE](file:///h:/PGH%20Project/flyrank-frontend-ai-capstone/LICENSE) for complete details.