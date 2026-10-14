# Chore Tracker

A web app that helps families build a habit of doing household chores.

A parent signs up, creates a family and invites kids (and other adults, like grandparents) with a one-time code. Parents create recurring chores tied to days of the week (e.g. *Saturday: vacuum the room*, *Sunday: change the bed sheets*) and assign them to a specific child. Each child logs in daily, sees only their own chores for today and checks them off. Parents see a history of what was done and when.

> 🚧 Work in progress. Built as a learning project for Supabase (auth, Postgres, Row Level Security).

## Tech stack

- [Next.js](https://nextjs.org) (App Router) + TypeScript
- [Tailwind CSS](https://tailwindcss.com)
- [Supabase](https://supabase.com): authentication, Postgres, Row Level Security
- [Vercel](https://vercel.com) for hosting
- PWA, installable on a phone's home screen

## Roles

| Role       | Can do                                                                         |
| ---------- | ------------------------------------------------------------------------------ |
| **Owner**  | Everything a parent can, plus invite parents, remove members, transfer ownership |
| **Parent** | Create and assign chores, invite kids, see history, approve completions        |
| **Child**  | See and check off their own chores for today                                   |

## Data model

| Table         | Purpose                                                                     |
| ------------- | --------------------------------------------------------------------------- |
| `families`    | Name, timezone, owner                                                       |
| `profiles`    | User id, family, role (`parent` or `child`), display name                   |
| `invites`     | One-time code (expires after 48h) to join a family as a child or parent     |
| `tasks`       | Title, `weekdays` (ISO, `1` = Monday … `7` = Sunday), assigned child, active |
| `completions` | Task, child, date, completion time, optional parent approval                |

### Access rules

- **Families are fully isolated:** nobody can see or change another family's data.
- **Kids are isolated from each other:** a child sees only their own chores and completions.
- A child can check off only today's chores (in the family's timezone) and can't approve their own work.
- Profiles are created only through database functions (create family / accept invite), so nobody can grant themselves a role.

Permissions are enforced in the database with Row Level Security and explicit grants, not only in the UI.

## Roadmap

**MVP**
- [ ] Sign up and log in
- [ ] Create a family
- [ ] Invite a child with a one-time code
- [ ] Parents create chores per weekday and assign them to a child
- [ ] Child sees today's chores and checks them off
- [ ] Parents see completion history

**Extras**
- [ ] Parent approval ("really done?")
- [ ] Invite additional parents
- [ ] Remove members
- [ ] Transfer ownership
- [ ] Account deletion
- [ ] Streaks / points
- [ ] Push reminders via PWA

## Getting started

```bash
npm install
cp .env.example .env.local   # fill in your Supabase project URL and publishable key
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).
