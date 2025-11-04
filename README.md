# 10xCards Flashcard Assistant

![version](https://img.shields.io/badge/version-0.0.1-blue.svg)
![status](https://img.shields.io/badge/status-in%20development-yellow.svg)
![node](https://img.shields.io/badge/node-22.14.0-43853d.svg)
![license](https://img.shields.io/badge/license-TBD-lightgrey.svg)

## Table of Contents
- [Project Description](#project-description)
- [Tech Stack](#tech-stack)
- [Getting Started Locally](#getting-started-locally)
- [Available Scripts](#available-scripts)
- [Project Scope](#project-scope)
- [Project Status](#project-status)
- [License](#license)

## Project Description
10xCards is a web-based flashcard creation and review tool that helps students turn study notes into high-quality decks in minutes. The MVP pairs AI-assisted drafting with guardrails that keep learners in control, ensures cards can be edited before saving, and feeds accepted cards into a built-in spaced repetition schedule. The experience targets university students and lifelong learners who already embrace flashcards but need a faster, more reliable creation workflow. For deeper context, review the [Product Requirements Document](.ai/prd.md).

## Tech Stack
- **Frontend:** Astro 5, React 19, TypeScript 5, Tailwind CSS 4, Shadcn/ui component primitives.
- **Backend:** Supabase (PostgreSQL, auth, storage) delivering backend-as-a-service capabilities.
- **AI Integration:** OpenRouter.ai for connecting to multiple large-language models with configurable rate limits.
- **Tooling & Infrastructure:** npm, Node.js 22.14.0, GitHub Actions for CI/CD pipelines, Docker images deployed to DigitalOcean.

## Getting Started Locally
### Prerequisites
- Node.js `22.14.0` (enforced via `.nvmrc`)
- npm (ships with Node.js) or another Node package manager

### Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/lawsaw/10x-cards.git
   cd 10x-cards
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Start the development server:
   ```bash
   npm run dev
   ```
4. Build the production bundle:
   ```bash
   npm run build
   ```
5. Preview the production build locally:
   ```bash
   npm run preview
   ```
6. Lint and format the codebase:
   ```bash
   npm run lint
   npm run lint:fix
   npm run format
   ```

> ℹ️ Supabase and AI credentials have not yet been defined. Add the necessary environment variables before connecting to external services.

## Available Scripts
- `npm run dev` — Start Astro in development mode with hot-module replacement.
- `npm run build` — Produce an optimized production build.
- `npm run preview` — Serve the production build locally for smoke testing.
- `npm run lint` — Run ESLint against the entire workspace.
- `npm run lint:fix` — Run ESLint with auto-fix enabled.
- `npm run format` — Format files using Prettier.

## Project Scope
**In scope**
- Web application optimized for desktop with responsive support for mobile browsers.
- AI-assisted card generation from plain-text input up to 2000 characters with live limits, loading states, and retry handling.
- Inline review flows for accepting, editing, or discarding AI-generated cards, including thumbs-up/down feedback capture.
- Manual card authoring, editing, duplication, and deletion within the same management view.
- Integration with an existing spaced repetition algorithm for scheduling and updating review queues.
- Email/password authentication, password reset, logout, and GDPR-aligned account deletion.
- Event logging for core actions: AI generation, acceptance, edits, deletions, review completion.

**Out of scope**
- Custom spaced repetition algorithms beyond configuring the selected open-source implementation.
- Rich media or document imports beyond the 2000-character text entry.
- Multi-user collaboration, sharing, or external LMS/calendar integrations.
- Native mobile or desktop applications.
- Expanded feedback mechanisms beyond thumbs-up/thumbs-down ratings.

## Project Status
- **Current focus:** MVP planning and foundational setup (version `0.0.1`).
- **Team capacity:** One developer and one designer working ~20 hours per week.
- **Timeline:** Target launch window of 3–4 weeks from project start.
- **Near-term milestones:** Implement authentication flows, integrate AI generation via OpenRouter, and wire Supabase-backed spaced repetition storage.
- **Risks & mitigation:** AI failure states require robust retry UX; reliability tracked via event instrumentation and uptime monitoring goals (<5% generation errors, 99% uptime).

## License
The project license is not yet defined. All rights reserved until a formal license is published.
