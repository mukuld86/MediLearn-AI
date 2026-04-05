# MediLearn AI MongoDB Database Setup

This document describes the MongoDB Atlas configuration used by MediLearn AI.

## Collections

- users
- quizResults

## users schema

- _id: ObjectId
- email: string (unique, lowercase)
- passwordHash: string
- displayName: string
- username: string
- photoURL: string | null
- createdAt: Date
- quizCount: number
- totalScore: number
- averageRating: number

## quizResults schema

- _id: ObjectId
- userId: ObjectId
- score: number
- category: string | null
- difficulty: string | null
- totalQuestions: number | null
- metadata: object | null
- createdAt: Date

## Required Indexes

- users.email unique
- users.averageRating descending

Indexes are created by server code on signup.

## Required Environment Variables

```env
MONGODB_URI=mongodb+srv://<username>:<password>@<cluster-url>/medilearn?retryWrites=true&w=majority
MONGODB_DB_NAME=medilearn
AUTH_JWT_SECRET=YOUR_LONG_RANDOM_SECRET
```

## Atlas Checklist

1. Create Atlas cluster.
2. Add application IP to Network Access.
3. Create DB user with readWrite permissions.
4. Paste connection string into MONGODB_URI.

## API Surface

- POST /api/auth/signup
- POST /api/auth/signin
- POST /api/auth/signout
- GET /api/auth/me
- GET /api/leaderboard
- POST /api/quiz/complete
