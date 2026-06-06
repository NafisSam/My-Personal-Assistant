# Nafis · Life OS

> A personal assistant web app built for one person — a medical doctor building AI tools in Tehran.

**One HTML file. No build step. Works offline. Syncs across devices.**

---

## What it is

A PWA (Progressive Web App) that replaces a to-do list, planner, paper tracker, and daily assistant — all in a single file you can open in Safari and add to your iPhone home screen.

Built around the reality of running 6 research papers, 3 AI projects, a medical internship, and a life — simultaneously.

---

## Features

- **Today view** — vitamins (individual, timed), tasks by date, upcoming 7 days, active no-date items
- **Alarms** — set custom time-based push notifications with repeat options (daily, once, weekdays, weekends)
- **Talk tab** — conversational AI via OpenAI; say what happened, it adds tasks and advances pipeline stages
- **Pipeline tracker** — each research paper and AI project shown as a visual stage pipeline with progress bar
- **Weekly report** — AI-generated honest review of what got done and what's stuck
- **Pushover integration** — vitamin reminders, shift warnings, deadlines, birthdays, custom alarms pushed to iPhone
- **Cross-device sync** — Supabase as backend; data stays the same on laptop and phone
- **Voice input** — Web Speech API, no external service

---

## Stack

| Layer | Tool |
|-------|------|
| Frontend | Vanilla HTML + CSS + JS (no frameworks) |
| AI | OpenAI API (gpt-4o-mini) |
| Database | Supabase (PostgreSQL via REST) |
| Push notifications | Pushover |
| Voice | Web Speech API (browser built-in) |
| Hosting | GitHub Pages |

---

## Setup

1. Fork or download `nafis-os.html`
2. Host on [GitHub Pages](https://pages.github.com/) — rename the file to `index.html`
3. Open in Safari on iPhone → Share → **Add to Home Screen**
4. Open the app → ⚙ Settings → add:
   - Supabase Project URL + Anon Key (for sync)
   - OpenAI API Key (for Talk + Report)
   - Pushover User Key + App Token (for iPhone push notifications)

**Supabase tables required** — run this in your project's SQL Editor:

```sql
create table tasks (id text primary key, title text, cat text default 'personal', date text default '', priority text default 'normal', proj text default '', done boolean default false, done_at text, created_at text);
create table vitamins (date text primary key, log jsonb default '{}');
create table pipeline (id text primary key, dtype text default 'paper', done_stages int default 0, note text default '');
create table agendas (date text primary key, content text default '');

alter table tasks    enable row level security;
alter table vitamins enable row level security;
alter table pipeline enable row level security;
alter table agendas  enable row level security;

create policy "open" on tasks    for all using (true) with check (true);
create policy "open" on vitamins for all using (true) with check (true);
create policy "open" on pipeline for all using (true) with check (true);
create policy "open" on agendas  for all using (true) with check (true);
```

---

## Customise for yourself

The data lives in three arrays at the top of the script — `INIT_TASKS`, `PAPERS_DEF`, `PROJECTS_DEF`. Edit them to reflect your own projects and tasks. The app is intentionally personal, not generic.

---

*Built with Claude · June 2026*
