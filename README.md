# MediLearn AI

MediLearn AI is an AI-powered study platform for medical students and professionals. It generates personalized quizzes, provides feedback, and tracks learning progress.

## Core Features

- Personalized quiz generation by topic and context
- AI-powered grading and feedback
- User profiles and leaderboard
- Email/password authentication with secure HttpOnly session cookies
- MongoDB Atlas-backed persistence for users and quiz results

## Tech Stack

- Framework: Next.js (App Router)
- Language: TypeScript
- Generative AI: Google Gemini via Genkit
- UI: React, shadcn/ui, Tailwind CSS
- Auth + Data: MongoDB Atlas + custom session routes

## Getting Started

### Prerequisites

- Node.js 18+
- npm
- MongoDB Atlas cluster

### Installation

1. Install dependencies:

```bash
npm install
```

1. Create and configure .env.local:

```env
GEMINI_API_KEY=YOUR_GEMINI_API_KEY
MONGODB_URI=mongodb+srv://<username>:<password>@<cluster-url>/medilearn?retryWrites=true&w=majority
MONGODB_DB_NAME=medilearn
AUTH_JWT_SECRET=YOUR_LONG_RANDOM_SECRET
```

1. Run the app:

```bash
npm run dev
```

Open <http://localhost:3000>.

## MongoDB Atlas Setup

1. Create a cluster in Atlas.
2. Add your development IP to Network Access.
3. Create a database user with readWrite permissions.
4. Copy the SRV URI and place it in MONGODB_URI.

## Notes

- Authentication APIs live under src/app/api/auth.
- Leaderboard API is at src/app/api/leaderboard.
- Quiz score persistence API is at src/app/api/quiz/complete.

## License

MIT
