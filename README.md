# Chore Tracker

A small web app that helps a parent and child build a habit of doing household chores.

The parent creates recurring chores tied to days of the week (e.g. *Saturday: vacuum the room*, *Sunday: change the bed sheets*). The child logs in each day, sees today's chores and checks them off. The parent sees a history of what was done and when.

> 🚧 Work in progress. Built as a learning project for Supabase (auth, Postgres, Row Level Security).

## Tech stack

- [Next.js](https://nextjs.org) (App Router) + TypeScript
- [Tailwind CSS](https://tailwindcss.com)
- [Supabase](https://supabase.com): authentication, Postgres, Row Level Security
- [Vercel](https://vercel.com) for hosting
- PWA, installable on a phone's home screen

## Data model (draft)

| Table         | Purpose                                                        |
| ------------- | -------------------------------------------------------------- |
| `profiles`    | User id and role (`parent` or `child`)                         |
| `tasks`       | Title, `weekdays` (`int[]`, e.g. `[6]` = Saturday), `active`   |
| `completions` | `task_id`, date, `completed_at`, optional parent approval      |

### Access rules (RLS)

- **Child:** can read tasks; can create and read their own completions.
- **Parent:** can create and edit tasks; can see all completions.

Permissions are enforced in the database with Row Level Security, not only in the UI.

## Roadmap

**MVP**
- [ ] Login
- [ ] Parent creates chores per weekday
- [ ] Child sees today's chores and checks them off
- [ ] Parent sees completion history

**Extras**
- [ ] Parent approval ("really done?")
- [ ] Streaks / points
- [ ] Push reminders via PWA

## Getting started

```bash
npm install
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

Supabase environment variables will be documented here once the integration is in place.
