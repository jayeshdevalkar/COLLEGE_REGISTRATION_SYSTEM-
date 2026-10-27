# College Event Registration System — Implementation Plan

## Implementation approach

Build a single React + Express + tRPC application on the managed Webdev starter. Use the managed MySQL-compatible database through Drizzle ORM for durable users, profiles, events, registrations, and sessions. Implement email/password authentication server-side with Node's built-in `scrypt` password hashing and a database-backed session cookie; preserve the starter's Manus OAuth callback for platform compatibility, while the project UI uses the explicit email/password flow requested in the brief. All protected mutations use tRPC protected/admin procedures and validate ownership on the server.

Events are public to browse. Authenticated users can create and manage their own events, register once per event, cancel their own registration, and edit their profile. Registration is protected by a database unique constraint and an atomic transaction that locks the event row before checking capacity. Available seats are computed from active registrations so counts cannot drift. The first user whose email matches `ADMIN_EMAIL` at sign-up/login is promoted to admin; the server never accepts role changes from the browser.

## Project structure

- `client/src/App.tsx`: route map, public shell, auth screens, dashboard pages, event detail/create/edit, registrations, profile, and admin views.
- `client/src/index.css`: visual system, responsive layout, cards, forms, badges, and interaction states.
- `client/src/lib/trpc.ts`: typed API client.
- `server/routers.ts`: auth, events, registrations, profile, and admin procedures.
- `server/db.ts`: Drizzle queries and transactional registration/cancellation logic.
- `server/_core/context.ts`: resolves Manus OAuth or the database-backed college event session.
- `drizzle/schema.ts` and `drizzle/*.sql`: persistent data model and indexes/constraints.
- `public/manus-routes.json`: page route manifest for the managed platform.

## Design direction

Three candidate styles:

1. **Campus Signal / editorial bulletin** — probability 0.07.
2. **Neo-library / quiet academic** — probability 0.06.
3. **Festival control room / kinetic utility** — probability 0.05.

Chosen: **Campus Signal / editorial bulletin**.

- **Design Movement:** A contemporary university bulletin board translated into a polished digital product: strong editorial blocks, oversized type, crisp borders, and deliberate asymmetry.
- **Core Principles:** Scan first, act quickly, show operational truth, keep student energy visible without clutter.
- **Color Philosophy:** Ink navy grounds the experience like a campus noticeboard; warm paper surfaces make the content approachable; electric cyan marks active routes and status; acid lime is reserved for positive action and availability.
- **Layout Paradigm:** A two-column editorial frame with a narrow utility rail and a wide event stream; mobile collapses into stacked sections without losing hierarchy.
- **Signature Elements:** Numbered event cards, compact status pills, and a small diagonal “signal” motif in hero/dashboard surfaces.
- **Interaction Philosophy:** Every action has a visible state: available seats, registered, cancelled, saved, or error. Forms are short and direct; destructive actions require an explicit confirmation.
- **Animation:** Use quick 160–220ms transitions for cards, buttons, and filters; no decorative motion that competes with event details. Loading uses skeleton shimmer and a subtle signal pulse.
- **Typography System:** `Space Grotesk` for display/UI labels and `DM Sans` for body copy; uppercase eyebrow labels with tight tracking, generous line-height for descriptions, and tabular numerals for statistics.
- **Brand Essence:** The student-run signal for what is happening next on campus. Personality: capable, bright, grounded.
- **Brand Voice:** Headlines are direct and specific (“Find your next room to be in.”). CTAs are active and human (“Save my seat”, “Publish event”).
- **Wordmark & Logo:** A compact square mark made from three offset signal bars, paired with a stacked “Campus / Signal” wordmark.
- **Signature Brand Color:** Electric cyan `#2DD4D8`, used as the ownable navigation and focus color.

## Delivery notes

Use only relative browser URLs so the app works in Preview and production. Keep secrets server-side. Publish after checks pass; explain the actual managed React/Express/tRPC/Drizzle stack, the managed MySQL database, custom email/password session flow, admin bootstrap rule, and any manual production configuration that remains.
