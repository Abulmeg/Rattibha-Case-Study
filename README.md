# Rattibha / رتّبها

Rattibha is a web and mobile platform built for students at Jordan University of Science and Technology (JUST).

It started as a schedule builder. The web app focuses on finding courses and building schedules, while the mobile app brings schedules, academic services, eLearning, degree-plan tools, tasks, and notifications into one place.

**Live website:** https://www.rattibha.online/

## Web

The web app helps students search the university schedule, choose sections, build schedules, save them, and check registration information without moving between multiple university pages.

### Main features

- Course and section search
- Schedule builder with section selection
- Saved schedules
- Arabic and English interfaces
- Light and dark themes
- Schedule export
- Registration helper
- Admin tools for schedule data review and updates

### Stack

<p>
<img src="https://img.shields.io/badge/Next.js-20232a?style=flat-square&logo=nextdotjs&logoColor=white" />
<img src="https://img.shields.io/badge/TypeScript-20232a?style=flat-square&logo=typescript&logoColor=3178C6" />
<img src="https://img.shields.io/badge/React-20232a?style=flat-square&logo=react&logoColor=61DAFB" />
<img src="https://img.shields.io/badge/Supabase-20232a?style=flat-square&logo=supabase&logoColor=3FCF8E" />
<img src="https://img.shields.io/badge/PostgreSQL-20232a?style=flat-square&logo=postgresql&logoColor=4169E1" />
<img src="https://img.shields.io/badge/Vercel-20232a?style=flat-square&logo=vercel&logoColor=white" />
</p>

## Schedule data sync

Rattibha uses the official JUST course schedule as its source for course and section data.

The current sync flow is operator-controlled:

```text
JUST course schedule
        ↓
Browser sync extension
        ↓
Admin preview and validation
        ↓
Supabase
        ↓
Rattibha web and mobile
```

The browser extension reads schedule data that has already been loaded in the administrator's browser. Rattibha validates the imported snapshot before updating the database.

This avoids depending on unattended scraping, since automated access to the university schedule can be unreliable because of site protections and request limits.

No private university endpoints, credentials, tokens, or internal sync details are included in this public repository.

## Mobile

Rattibha Mobile extends the project beyond schedule building.

### Main features

- Registered courses and weekly schedule
- Degree-plan progress
- Next-semester course availability
- Official academic data from JUST services
- eLearning course content
- Exams and tasks
- Academic notifications and reminders
- Arabic and English support
- Admin overview

### Stack

<p>
<img src="https://img.shields.io/badge/React%20Native-20232a?style=flat-square&logo=react&logoColor=61DAFB" />
<img src="https://img.shields.io/badge/Expo-20232a?style=flat-square&logo=expo&logoColor=white" />
<img src="https://img.shields.io/badge/TypeScript-20232a?style=flat-square&logo=typescript&logoColor=3178C6" />
<img src="https://img.shields.io/badge/Supabase-20232a?style=flat-square&logo=supabase&logoColor=3FCF8E" />
<img src="https://img.shields.io/badge/PostgreSQL-20232a?style=flat-square&logo=postgresql&logoColor=4169E1" />
</p>

## Mobile data flow

The mobile app does not call sensitive university integrations directly from the UI.

University service requests are routed through the Rattibha backend, which keeps service details and server-side logic outside the client application.

The app combines several sources:

```text
JUST Student Services ──→ Rattibha backend ──→ Mobile app
Official schedule data ─→ Supabase ──────────→ Mobile app
University eLearning ───→ eLearning layer ───→ Mobile app
                                           └──→ Notifications
```

The goal is to give the student one interface while keeping the integrations separated internally.

## Screenshots

### Website

<table>
<tr>
<td width="50%"><img src="./screenshots/web/home-light.png" alt="Rattibha website home page in light mode"></td>
<td width="50%"><img src="./screenshots/web/home-dark.png" alt="Rattibha website home page in dark mode"></td>
</tr>
<tr>
<td width="50%"><img src="./screenshots/web/builder-english-light.png" alt="Schedule builder in English"></td>
<td width="50%"><img src="./screenshots/web/builder-arabic-dark.png" alt="Schedule builder in Arabic dark mode"></td>
</tr>
</table>

### Mobile

<table>
<tr>
<td width="33%"><img src="./screenshots/mobile/courses.jpeg" alt="Courses screen"></td>
<td width="33%"><img src="./screenshots/mobile/schedule-weekly.jpeg" alt="Weekly schedule"></td>
<td width="33%"><img src="./screenshots/mobile/course-elearning.jpeg" alt="Course and eLearning content"></td>
</tr>
<tr>
<td width="33%"><img src="./screenshots/mobile/next-semester.jpeg" alt="Next semester courses"></td>
<td width="33%"><img src="./screenshots/mobile/admin-overview.jpeg" alt="Admin overview"></td>
<td width="33%"><img src="./screenshots/mobile/splash.jpeg" alt="Rattibha mobile splash screen"></td>
</tr>
</table>

## Architecture

```text
                     ┌──────────────────────┐
                     │ Official JUST data   │
                     └──────────┬───────────┘
                                │
              ┌─────────────────┴─────────────────┐
              │                                   │
              ▼                                   ▼
     Schedule sync/import                Student Services
              │                                   │
              ▼                                   ▼
        ┌──────────┐                      ┌────────────────┐
        │ Supabase │                      │ Rattibha API   │
        └────┬─────┘                      └───────┬────────┘
             │                                    │
        ┌────┴──────────────┐                     │
        ▼                   ▼                     ▼
  Next.js web app     React Native mobile app ←───┘
                              │
                              ▼
                        eLearning layer
                              │
                              ▼
                         Notifications
```

## Source code

The main Rattibha web and mobile repositories are private.

This repository is a public case study. It shows the product, architecture, integrations, and engineering decisions without publishing private source code, credentials, student data, or internal service details.

## Links

- Website: https://www.rattibha.online/
- GitHub: https://github.com/Abulmeg
- LinkedIn: https://www.linkedin.com/in/abulmeg/
