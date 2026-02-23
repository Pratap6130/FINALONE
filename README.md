# RecruitX 

AI-powered mock interview platform built with Next.js, Firebase, Vapi voice calls, and Gemini-based evaluation.

## Overview

RecruitX helps users practice job interviews end-to-end:

- generate tailored interview questions by role, level, and tech stack,
- take a real-time AI voice interview,
- get structured feedback with category scores, strengths, and improvement areas,
- review interview history on a personalized dashboard.

## Features

- Email/password authentication with Firebase Auth
- Server-side session cookies via Firebase Admin
- AI interview question generation via Gemini (`app/api/vapi/generate`)
- Real-time voice interview flow using Vapi Web SDK
- AI feedback generation from interview transcript
- Dashboard with:
	- Your completed interviews
	- Community/latest interviews (excluding your own)
- Detailed feedback page with:
	- overall score,
	- per-category breakdown,
	- strengths,
	- areas for improvement,
	- final assessment

## Tech Stack

- **Framework:** Next.js 15 (App Router), React 19, TypeScript
- **Styling/UI:** Tailwind CSS v4, Radix primitives, Sonner toasts
- **Validation & Forms:** Zod, React Hook Form
- **Auth & Database:** Firebase (client SDK + Admin SDK), Firestore
- **AI:** Vercel AI SDK + Google Gemini (`gemini-2.0-flash-001`)
- **Voice Interview:** Vapi (`@vapi-ai/web`)

## Project Structure

```text
app/
	(auth)/                 # Sign in / sign up routes
	(root)/                 # Protected app routes (dashboard, interview flow)
	api/vapi/generate/      # API route to generate interview questions
components/
	Agent.tsx               # Voice interview/generation call experience
firebase/
	client.ts               # Firebase web SDK init
	admin.ts                # Firebase Admin SDK init
lib/actions/
	auth.action.ts          # Auth/session server actions
	general.action.ts       # Interview/feedback server actions
constants/
	index.ts                # Interview assistant config + feedback schema
```

## Prerequisites

- Node.js 20+
- npm

## Installation & Running Locally

```bash
npm install
npm run dev
```

Then open [http://localhost:3000](http://localhost:3000).

## Available Scripts

- `npm run dev` – start development server (Turbopack)
- `npm run build` – create production build
- `npm run start` – run production server
- `npm run lint` – run Next.js lint checks

## Data Model (Firestore)

Main collections used:

- `users`
	- `name`, `email`
- `interviews`
	- `role`, `type`, `level`, `techstack[]`, `questions[]`, `userId`, `finalized`, `coverImage`, `createdAt`
- `feedback`
	- `interviewId`, `userId`, `totalScore`, `categoryScores[]`, `strengths[]`, `areasForImprovement[]`, `finalAssessment`, `createdAt`

## How the Flow Works

1. User signs up / signs in.
2. Session cookie is created on the server.
3. User starts interview generation (voice workflow via Vapi).
4. App stores generated interview data in Firestore.
5. User takes interview with AI interviewer voice assistant.
6. Transcript is sent to Gemini-based evaluator.
7. Structured feedback is saved and shown on feedback page.

## Deployment

You can deploy on Vercel (recommended for Next.js):

1. Push this repo to GitHub.
2. Import project in Vercel.
3. Configure your project settings and required integrations.
4. Deploy.

## Notes

- `next.config.ts` currently ignores TypeScript and ESLint errors during builds. For stricter production quality, remove:
	- `typescript.ignoreBuildErrors: true`
	- `eslint.ignoreDuringBuilds: true`

## License

This project currently has no license file in the repository.
