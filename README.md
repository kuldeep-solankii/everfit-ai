# Everfit AI

An AI-powered fitness web application that helps users create personalized workout routines and diet plans. The project combines a Next.js interface with Clerk authentication, Convex for backend data, Gemini for AI-generated plans, and Vapi for voice interactions.

> **Live demo:** https://everfit-ai.vercel.app/  
> **Repository:** https://github.com/kuldeep-solankii/everfit-ai

## Features

- **Authentication:** Sign up and sign in using Clerk.
- **Personalized fitness plans:** Collect fitness preferences and generate workout and diet recommendations with Google Gemini.
- **Saved plans and profile:** Store and retrieve user-related fitness information with Convex.
- **Voice assistant integration:** Uses Vapi Web to support voice-based interaction.
- **Responsive interface:** Built with Next.js, React, Tailwind CSS, and reusable UI components.

*Available features depend on the current deployment configuration and the credentials you provide.*

## Tech stack

- **Framework:** Next.js 15 (App Router)
- **UI:** React 19, TypeScript, Tailwind CSS 4
- **Authentication:** Clerk
- **Backend and data:** Convex
- **AI:** Google Gemini (`@google/generative-ai`)
- **Voice:** Vapi Web SDK
- **Icons and UI primitives:** Lucide React, Radix UI
- **Deployment:** Vercel (live deployment)

## Getting started

### Prerequisites

- Node.js (use a currently supported LTS release)
- npm
- Accounts and credentials for Clerk, Convex, Google Gemini, and Vapi if you want to run the corresponding integrations locally

### 1. Clone the repository

```bash
git clone https://github.com/kuldeep-solankii/everfit-ai.git
cd everfit-ai
```

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment variables

Create a `.env.local` file in the project root for the variables required by your local setup. Do not commit this file.

The source code references the following variables; configure the ones required by the feature you are running:

```dotenv
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=
CLERK_SECRET_KEY=
NEXT_PUBLIC_CONVEX_URL=
GEMINI_API_KEY=
CLERK_WEBHOOK_SECRET=
NEXT_PUBLIC_VAPI_API_KEY=
NEXT_PUBLIC_VAPI_WORKFLOW_ID=
```

**Important:** These names are a starting checklist, not a guarantee that every variable is used under exactly this name in the current code. Check the Clerk, Convex, Gemini, and Vapi setup in the source and their dashboards, and use the exact names expected by the project. Never put secret keys in variables prefixed with `NEXT_PUBLIC_`; values with that prefix can be exposed to the browser. Do not share or commit real credentials.

Configure Clerk and Convex according to their official documentation, and make sure the Convex deployment has the required environment variables configured as well. If the project uses Clerk webhooks, configure the webhook endpoint and secret.

### 4. Start the development server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### 5. Create a production build

```bash
npm run build
```

Resolve any build errors before deploying. The app's third-party integrations also need valid environment configuration to work end to end.

## Project structure

```text
src/
  app/                  Next.js routes and pages
    (auth)/             Sign-in and sign-up pages
    generate-program/   Fitness plan generation flow
    profile/            User profile and saved-plan area
  components/           Shared page and UI components
  constants/            Application constants and prompt-related data
  lib/                  Shared utilities and Vapi setup
  middleware.ts         Route/authentication middleware
  providers/            Clerk and Convex providers
convex/
  schema.ts             Database schema
  users.ts              User-related backend functions
  plans.ts              Fitness plan functions
  http.ts               HTTP actions and integrations
public/                 Static images and assets
```

## How it works (high level)

1. A user signs in through Clerk.
2. The interface collects fitness-related preferences.
3. Backend logic calls Gemini to generate workout and diet suggestions.
4. Convex stores and retrieves user and plan data.
5. The app displays the user's profile and fitness plans; Vapi provides voice functionality where configured.

## Security notes

- Keep API keys and webhook secrets out of source control.
- Validate incoming request data on the server.
- Do not trust a user ID supplied by the browser without verifying it against the authenticated identity.
- Check ownership and authorization in every query or mutation that reads or changes private user data.
- Add appropriate rate limiting and abuse protection to public AI-generation endpoints.
- Treat AI-generated fitness guidance as general information, not a substitute for advice from a qualified health professional.

## Current limitations / future improvements

Potential next steps for the project:

- Add automated tests for core UI and backend flows.
- Validate AI output against a defined schema and handle malformed responses gracefully.
- Improve loading, empty, and error states.
- Document exact environment variables and setup steps after verifying the current deployment configuration.
- Review authorization for all Convex queries, mutations, and HTTP actions.
- Add screenshots or a short demo GIF to help visitors understand the app quickly.

## Contributing

This is a personal learning and portfolio project. Suggestions and bug reports are welcome. Before submitting changes, run the production build and test the relevant user flows.

## Acknowledgements

Built with Next.js, React, Clerk, Convex, Google Gemini, Vapi, and the open-source packages listed in `package.json`.
