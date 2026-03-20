# ⚡ SportzLive
> *A real-time cyberpunk sports dashboard — where live data meets high-end glassmorphism.*

[![React](https://img.shields.io/badge/React-18+-61DAFB?style=flat-square&logo=react)](https://react.dev)
[![Vite](https://img.shields.io/badge/Vite-5+-646CFF?style=flat-square&logo=vite)](https://vitejs.dev)
[![Node.js](https://img.shields.io/badge/Node.js-20+-339933?style=flat-square&logo=node.js)](https://nodejs.org)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Neon-4169E1?style=flat-square&logo=postgresql)](https://neon.tech)
[![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)](LICENSE)

---

## 🧠 Overview

**SportzLive** is a full-stack, real-time sports intelligence platform built for speed, aesthetics, and live data precision. Powered by WebSockets and a PostgreSQL backbone, it streams live scores, commentary deltas, and tournament updates to every connected client — instantly.

The UI is built around a **Cyberpunk Sports Dashboard** theme: deep darks, neon sport-specific accents, glassmorphism panels, and GSAP-driven micro-animations that make data feel alive.

---

## ✨ Key Features

- ⚡ **Live Neural Stream** — Global WebSocket broadcast via the `ws` library; score deltas and live commentary pushed to all clients in real time
- 🎨 **Cyberpunk Glassmorphism UI** — Dark `#050810` base, frosted-glass panels, sport-specific neon color schemes (🟢 Neon Green for Soccer · 🟠 Orange for Basketball · 🔴 Red for Cricket)
- 🎬 **GSAP Animations** — Buttery-smooth entrance animations, staggered reveals, and icon transitions with `force3D` hardware acceleration
- 🔍 **Neural Search Bar** — Real-time filtering of active tournaments by team name, sport type, or match status — zero latency, zero round-trips
- 🛡️ **Error Boundary Recovery** — Custom React Error Boundary renders a "System Breach" failover screen and gracefully recovers without a full page reload
- 🗄️ **Drizzle ORM + Neon PostgreSQL** — Type-safe schema definitions, migration support, and a serverless-ready Postgres connection via Neon
- 🚀 **Vite + React** — Lightning-fast HMR dev environment with optimized production builds
- 🎯 **Performance-Tuned** — `will-change` CSS properties and GSAP's `force3D` flag eliminate paint jitter on Chrome; tested for 60fps across all animated panels

---

## 🏗️ Tech Stack

### Frontend
| Technology | Purpose |
|---|---|
| React 18+ (Vite) | UI framework & build tooling |
| Tailwind CSS | Utility-first styling |
| GSAP | Animation engine |
| Lucide React | Icon system |

### Backend
| Technology | Purpose |
|---|---|
| Node.js + Express | REST API & WebSocket server |
| `ws` library | Real-time WebSocket broadcasting |
| Drizzle ORM | Type-safe database access layer |
| PostgreSQL (Neon) | Serverless cloud database |

---

## 📦 Installation

### Prerequisites

- Node.js `v20+`
- A [Neon](https://neon.tech) PostgreSQL database (free tier works)
- npm `v9+`

---

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/sportzlive.git
cd sportzlive
```

---

### 2. Backend Setup

```bash
cd backend
npm install
```

Create a `.env` file in the `backend/` directory:

```env
# PostgreSQL connection string from Neon dashboard
DATABASE_URL=postgresql://user:password@host/dbname?sslmode=require

# Port for the Express server
PORT=4000

# WebSocket heartbeat interval in ms (optional)
WS_HEARTBEAT_INTERVAL=30000
```

Run database migrations:

```bash
npm run db:push
```

---

### 3. Frontend Setup

```bash
cd ../frontend
npm install
```

Create a `.env` file in the `frontend/` directory:

```env
# Base URL of your Express backend
VITE_API_URL=http://localhost:4000

# WebSocket endpoint
VITE_WS_URL=ws://localhost:4000
```

---

## 🚀 Getting Started

### Run the Backend

```bash
cd backend
npm run dev
```

The Express server starts on `http://localhost:4000`. WebSocket connections are accepted on the same port.

---

### Run the Frontend

```bash
cd frontend
npm run dev
```

The Vite dev server starts on `http://localhost:5173`. Open it in Chrome for the best animation performance.

---

### Seed Live Data

Populate the database with tournaments, teams, and initial scores:

```bash
cd backend
npm run seed
```

This seeds:
- Active tournaments across Soccer, Basketball, and Cricket
- Sample team rosters and match schedules
- Initial score states for WebSocket delta broadcasting

---

## 🎨 Design Philosophy

SportzLive is built on the belief that **sports data should feel electric**.

Every UI decision is intentional:

- **Cyberpunk Aesthetic** — The `#050810` deep-space background and 40×40 CSS grid overlay create a command-center feel. Glassmorphism panels (backdrop blur + low-opacity borders) layer depth without noise.
- **Sport-Specific Color Identity** — Each sport owns a neon accent: Soccer pulses Neon Green (`#00E676`), Basketball burns Orange (`#FF6D00`), Cricket runs Red (`#E53935`). These colors cascade through icons, progress bars, glow effects, and WebSocket notification pulses.
- **Motion as Meaning** — GSAP animations are never decorative for decoration's sake. Score updates trigger targeted timeline tweens. New data streaming in has staggered reveals. The loader cycles sport icons with `back.out` easing to signal readiness — not just loading.
- **Micro-Interactions** — Hover states, focus rings, and active transitions are all handled at the component level, keeping the experience responsive and tactile.
- **Performance First** — `will-change: transform` is applied to all animated layers. GSAP's `force3D: true` flag pushes compositing to the GPU, ensuring 60fps even on data-dense views.

---

## 📁 Project Structure

```
sportzlive/
├── backend/
│   ├── src/
│   │   ├── db/          # Drizzle schema & migrations
│   │   ├── routes/      # Express REST endpoints
│   │   ├── ws/          # WebSocket broadcaster
│   │   └── index.ts     # Server entry point
│   ├── .env
│   └── package.json
│
└── frontend/
    ├── src/
    │   ├── components/  # UI components (Dashboard, SearchBar, ScoreCard...)
    │   ├── hooks/       # useWebSocket, useLiveScore, useGSAP
    │   ├── lib/         # API client, WS client, color maps
    │   └── main.tsx     # App entry point
    ├── .env
    └── package.json
```

---

## 🛡️ Error Handling

SportzLive wraps the dashboard tree in a custom React Error Boundary. If a component throws — due to a malformed WebSocket payload, a failed API response, or an unexpected state — the boundary catches it and renders a **"System Breach"** recovery screen with a one-click reset, without losing the WebSocket connection.

---

## 📄 License

MIT © 2025 SportzLive

Permission is hereby granted, free of charge, to any person obtaining a copy of this software, to deal in the Software without restriction — including the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies — subject to the conditions of the MIT License.

See [LICENSE](LICENSE) for full terms.

---

<p align="center">Built with ⚡ by the SportzLive team</p>
