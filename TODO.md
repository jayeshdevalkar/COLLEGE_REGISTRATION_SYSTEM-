# College Event Registration System — Delivery Checklist

## Public discovery and responsive shell
- [ ] Visitors can open the landing page, see the project name and introduction, browse featured event cards, see event categories, use Explore Events, and understand how the platform works.
- [ ] Visitors can browse published upcoming events publicly; the navigation remains usable on desktop, tablet, and mobile with readable contrast, labels, keyboard-friendly controls, loading states, success/error messages, and useful empty states.

## Account creation and sessions
- [ ] Students can create an account with full name, email, college name, password, and confirm password; required fields, email format, password confirmation, and duplicate accounts are validated; passwords are never stored in plaintext.
- [ ] Students can log in and log out securely, keep their session across refreshes, and are redirected to login before protected actions with an intended destination preserved.

## Student dashboard and event discovery
- [ ] Authenticated students see a personalized dashboard with a welcome message, upcoming events, search, category filters, upcoming-date filtering, registration statistics, events they created, and events they joined.
- [ ] Event cards show title, category, date, time, venue, organizer, description, registration status, and available seats where appropriate; no-match states explain what to do next.

## Event lifecycle and ownership
- [ ] Any authenticated student can publish an event with title, detailed description, category, future date, start time, venue, positive capacity, optional organizer contact, and optional poster reference; the saved event is associated with the creator and appears in public listings without auto-registering the creator.
- [ ] Event details show poster when present, description, category, date, time, venue, organizer, capacity, available seats, registration status, and a clear Register Now action.
- [ ] Students can edit or cancel only events they created; other students cannot alter them; cancelled events communicate their status clearly.

## Registration integrity
- [ ] A logged-in student registers with one click using the authenticated account ID, persists the registration timestamp, updates counts and available seats, shows a confirmation only after saving, and changes the action to Registered/Already Registered.
- [ ] Duplicate student-event registrations are rejected by a database uniqueness constraint; capacity is enforced in a transaction so simultaneous requests cannot overbook; full, cancelled, and past events reject new registrations safely.
- [ ] My Registrations lists the current student's events and allows cancellation only when allowed; cancellation is confirmed, restores availability, and cannot affect another student's registration.

## Profile and admin
- [ ] Students can view and safely edit name and college while the authentication email remains consistent; private registration information is not exposed to other users.
- [ ] An actual server-enforced admin role allows approved administrators to review events, cancel inappropriate events, and view registration statistics; ordinary students cannot access admin procedures or self-promote.

## Data, security, and handover
- [ ] The persistent schema includes users/profiles, events, registrations, sessions, relationships, indexes, timestamps, status fields, and unique ownership/registration constraints; critical data is not stored only in browser localStorage.
- [ ] Backend validation and authorization protect every protected operation; secrets remain server-side; uploaded poster references are validated and stored safely.
- [ ] The application runs type checks and production builds, reports what was and was not tested, and provides beginner-friendly setup, admin bootstrap, publish, GitHub/Vercel, and teacher-demo instructions.
