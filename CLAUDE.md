# FlyRank - Front-End AI Engineering Capstone

Welcome to **FlyRank**, a modern Front-End AI Engineering capstone project designed to deliver intelligent, real-time search ranking analysis, semantic SERP intelligence, and AI-driven insights.

This file serves as the definitive reference for AI coding assistants and developers working within this codebase. Adhere strictly to the guidelines, architectures, and conventions detailed below.

---

## 🛠️ Tech Stack & Core Dependencies

- **Framework**: [Next.js](https://nextjs.org/) (App Router, React Server Components)
- **Language**: [TypeScript](https://www.typescriptlang.org/) (Strict Mode)
- **Styling**: [Tailwind CSS](https://tailwindcss.com/) with PostCSS & CSS Variables
- **AI Integration**: [Vercel AI SDK](https://sdk.vercel.ai/) (`ai`, `@ai-sdk/react`), OpenAI / Anthropic APIs
- **UI Components & Icons**: Radix UI / Shadcn UI patterns, [Lucide React](https://lucide.dev/)
- **State & Data Fetching**: React Server Components, SWR / TanStack Query, Zustand
- **Validation**: [Zod](https://zod.dev/) for runtime schema validation & type inference
- **Quality & Tooling**: ESLint, Prettier, Husky, lint-staged, Conventional Commits

---

## 🚀 Common Commands

### Development & Build
```bash
# Install dependencies
npm install

# Start local development server (default port 3000)
npm run dev

# Build production bundle
npm run build

# Start production server
npm run start
```

### Code Quality & Validation
```bash
# Run ESLint check
npm run lint

# Automatically fix lint issues
npm run lint:fix

# Run TypeScript compiler checks without emitting files
npm run type-check

# Format code with Prettier
npm run format

# Verify formatting without modifying files
npm run format:check

# Run unit / integration test suite
npm test

# Run tests in watch mode
npm run test:watch
```

---

## 📁 Project Architecture & Conventions

### Directory Layout
```plaintext
flyrank-frontend-ai-capstone/
├── app/                      # Next.js App Router (pages, layouts, route handlers)
│   ├── (auth)/               # Route group for authentication flows
│   ├── (dashboard)/          # Route group for authenticated workspace & metrics
│   ├── api/                  # API route handlers (server-side only, streaming AI)
│   │   ├── ai/               # AI generation & chat streaming endpoints
│   │   └── ranking/          # Search ranking & analytics ingestion endpoints
│   ├── layout.tsx            # Root application layout
│   ├── page.tsx              # Landing / hero page
│   └── globals.css           # Global stylesheet & Tailwind directives
├── components/               # Modular React components
│   ├── ai/                   # AI-specific components (ChatBox, StreamText, PromptInput)
│   ├── charts/               # Ranking charts & analytics visualizers
│   ├── layout/               # Navigation, Sidebar, Footer, Header
│   └── ui/                   # Reusable atom-level UI primitives (Button, Card, Input)
├── hooks/                    # Custom React hooks (UI & AI helpers)
├── lib/                      # Core utility functions and server integrations
│   ├── ai/                   # AI provider configurations, system prompts, models
│   ├── utils.ts              # Common utility functions (e.g., cn helper)
│   └── validators/           # Zod validation schemas
├── types/                    # Shared TypeScript interfaces and type definitions
├── public/                   # Static assets (images, icons, fonts)
├── .env.example              # Sample environment variables
├── CLAUDE.md                 # Agent and development rules (this file)
├── package.json              # Project metadata, scripts, and dependencies
├── tailwind.config.ts        # Tailwind CSS configuration
├── tsconfig.json             # TypeScript compiler settings
└── README.md                 # Project documentation & overview
```

---

## ⚡ Next.js Guidelines

1. **App Router Standard**:
   - Use the `app/` directory paradigm exclusively.
   - Keep page (`page.tsx`) and layout (`layout.tsx`) files lean. Extract logic into focused component modules in `components/`.

2. **Server vs. Client Components**:
   - Favor **React Server Components (RSC)** by default for data fetching, static rendering, and server-side logic.
   - Use `'use client'` strictly when necessary:
     - Interactive client state (`useState`, `useReducer`).
     - Effects and lifecycles (`useEffect`).
     - Browser-only APIs (DOM access, localStorage).
     - Streaming AI interactions using client hooks (`useChat`, `useCompletion`).
   - Never import server-only code (e.g., private API keys, direct database clients) into Client Components.

3. **API & AI Route Handlers**:
   - Place all API endpoints under `app/api/.../route.ts`.
   - Never expose LLM API keys (`OPENAI_API_KEY`, `ANTHROPIC_API_KEY`) to the client. Keep them securely in server route handlers or server actions.
   - Leverage `StreamingTextResponse` or `createDataStreamResponse` from the Vercel AI SDK for smooth, non-blocking UI streaming.

4. **Performance & Optimization**:
   - Always utilize `next/image` for image assets with explicit width/height or `fill` with `sizes`.
   - Use dynamic imports (`next/dynamic`) with loading fallbacks for heavy interactive charts or client-only widgets.
   - Define loading states with `loading.tsx` and resilient error states with `error.tsx`.

---

## 🔷 TypeScript Configuration & Rules

1. **Strict Type Safety**:
   - Enable and respect `"strict": true` in `tsconfig.json`.
   - Prohibit the usage of `any`. If a type is genuinely dynamic or unknown, use `unknown` accompanied by type guards or Zod parsing.
   - Do not use `@ts-ignore` or `@ts-nocheck` without explicit justification and documentation.

2. **Type Definitions & Interfaces**:
   - Standardize on `interface` for object models and component props.
   - Use `type` for unions, intersections, primitives, and utility types.
   - Place shared, cross-module data structures inside the `types/` directory.

3. **Schema-First AI & Data Contracts**:
   - Use **Zod** to validate all external inputs: API query parameters, body payloads, environment variables, and structured AI outputs.
   - Derive TypeScript types directly from schemas using `z.infer<typeof Schema>`:
     ```typescript
     import { z } from 'zod';

     export const RankingMetricSchema = z.object({
       keyword: z.string().min(1),
       position: z.number().int().positive(),
       previousPosition: z.number().int().positive(),
       searchVolume: z.number().nonnegative(),
       difficultyScore: z.number().min(0).max(100),
     });

     export type RankingMetric = z.infer<typeof RankingMetricSchema>;
     ```

4. **Explicit Return Types**:
   - Provide explicit return types on utility functions, server actions, and API handlers to prevent unintended type regressions.

---

## 🎨 Tailwind CSS Rules & Styling Standards

1. **Utility-First & Class Merging**:
   - Use Tailwind CSS utility classes directly within JSX.
   - Use a centralized `cn()` helper (`clsx` + `tailwind-merge`) when conditionally applying or overriding classes:
     ```typescript
     import { clsx, type ClassValue } from 'clsx';
     import { twMerge } from 'tailwind-merge';

     export function cn(...inputs: ClassValue[]) {
       return twMerge(clsx(inputs));
     }
     ```

2. **Design Tokens & Theme Consistency**:
   - Always reference design tokens configured in `tailwind.config.ts` (colors, border radii, shadows, font families) rather than hardcoded hex codes.
   - Support dark and light modes through semantic CSS variables (e.g., `bg-background`, `text-foreground`, `border-border`, `bg-muted`).
   - Avoid arbitrary magic values (e.g., avoid `w-[327px]`, use standard scale `w-80` or design tokens).

3. **Responsive & Accessible Design**:
   - Build mobile-first: start with baseline classes and scale up (`sm:`, `md:`, `lg:`, `xl:`).
   - Ensure interactive elements feature accessible focus rings:
     `focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2`.
   - Maintain high contrast ratios for text in both dark and light themes (WCAG 2.1 AA standard).

4. **Component Encapsulation**:
   - Encapsulate reusable variants with `class-variance-authority` (cva) for consistent component APIs (buttons, badges, cards).

---

## 🤖 Front-End AI Engineering Best Practices

1. **Streaming UI & Perceived Performance**:
   - Render AI output incrementally using token streaming to minimize Time to First Token (TTFT).
   - Prevent layout shifts during streaming by reserving space or using smooth auto-scrolling containers.
   - Display animated skeleton loaders or pulsing status indicators while waiting for AI generation.

2. **Error Recovery & Rate Limiting**:
   - Handle provider timeouts and API errors gracefully with user-friendly error banners and retry buttons.
   - Implement client-side debounce and optimistic feedback on submission.

3. **Prompt & Context Management**:
   - Maintain system prompts and persona definitions in structured server modules (`lib/ai/prompts.ts`), never in client code.
   - Keep token payloads minimal and sanitize user queries before forwarding them to AI endpoints.

4. **Human-in-the-Loop Controls**:
   - Provide intuitive UI controls for AI responses: Stop generating, Copy text, Regenerate answer, and Feedback rating (thumbs up/down).

5. **AI Pair Programming & Prompt Governance**:
   - Cache static system prompts and use concise prompt templates to minimize token overhead.
   - Separate reasoning prompts from presentation schemas to avoid markdown formatting anomalies.
   - Ensure all AI-generated code conforms strictly to the TypeScript, Next.js App Router, and Conventional Commits standards defined in this guide.

---

## 📝 Conventional Commits Specification

All commit messages in this repository must adhere to the **Conventional Commits** standard to ensure automated versioning and transparent changelogs.

### Structure
```plaintext
<type>(<scope>): <description>

[optional body]

[optional footer(s)]
```

### Commit Types
| Type | Description | Example |
| :--- | :--- | :--- |
| `feat` | A new feature or capability | `feat(ai): add streaming response handler for ranking insights` |
| `fix` | A bug fix | `fix(dashboard): resolve layout shift in metric cards on mobile` |
| `docs` | Documentation changes only | `docs(readme): update tech stack and local setup instructions` |
| `style` | Formatting, missing semi-colons, no code logic change | `style(components): organize tailwind utility classes` |
| `refactor` | Code change that neither fixes a bug nor adds a feature | `refactor(lib): simplify Zod validation logic for serp data` |
| `perf` | A code change that improves performance | `perf(charts): memoize data aggregation for keyword trends` |
| `test` | Adding missing tests or correcting existing tests | `test(ai): add unit tests for prompt formatting utility` |
| `build` | Changes to build configuration or dependencies | `build(deps): update next from 14.1.0 to 14.2.0` |
| `ci` | Changes to CI/CD workflows and deployment scripts | `ci(github): add automated type-check and lint workflow` |
| `chore` | Routine tasks, maintenance, tool configurations | `chore(husky): configure commit-msg git hook` |
| `revert` | Reverts a previous commit | `revert: revert "feat(ai): enable experimental model"` |

### Rules & Formatting
- **Subject line**:
  - Use imperative, present tense: `"add"` instead of `"added"` or `"adds"`.
  - Do NOT capitalize the first letter of the subject: `feat(ui): add search bar` (not `feat(ui): Add search bar`).
  - Do NOT place a period (`.`) at the end of the subject line.
  - Limit the subject line to 72 characters.
- **Breaking Changes**:
  - Indicate breaking changes with a `!` after the type/scope (e.g., `feat(api)!: migrate to v2 ranking schema`) or include `BREAKING CHANGE: <explanation>` in the commit footer.
- **Valid Scopes**:
  - `ai`, `api`, `ui`, `dashboard`, `auth`, `charts`, `ranking`, `hooks`, `types`, `config`, `deps`.

---

## 🔒 Security & Best Practices

- **Secrets**: Never commit `.env` or files containing live API keys. Always use `.env.local` for local secrets and configure `.env.example` with dummy values.
- **Sanitization**: Sanitize any dynamic markdown or HTML generated by LLMs using DOMPurify or equivalent before rendering to prevent XSS.
- **Accessibility**: Ensure keyboard navigation and ARIA landmarks exist across all interactive AI components.
