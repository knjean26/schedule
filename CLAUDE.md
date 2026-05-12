# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

`002coach.html` is a self-contained single-file pickleball coaching schedule app written in Thai. No build step, no dependencies, no package manager — open the file directly in a browser.

## Architecture

Everything lives in one HTML file:

- **CSS** (`:root` variables, responsive grid) — dark green theme using CSS custom properties
- **HTML** — three main sections: `#loginScreen`, `#app`, and modals (`#editModal`, `#pwModal`)
- **JavaScript** (inline `<script>`) — vanilla JS, no frameworks

### Data & State

All data is stored in `localStorage`:
- `pb_sessions` — JSON array of session objects `{id, dayIdx, time, title, level, students, coach, court}`
- `pb_password` — admin password (default: `admin1234`)

`DEF_SESSIONS` (hardcoded in JS) serves as the factory-reset dataset.

### Access Modes

- **Admin mode** — password login; shows add/edit/delete controls and the sidebar (coach list, settings)
- **Public mode** — no login required; read-only calendar view

`document.body.classList` toggling `admin-mode` controls sidebar visibility via CSS (`.admin-only`).

### Key Functions

| Function | Purpose |
|---|---|
| `render()` | Rebuilds the entire calendar from `sessions[]` and current `weekOffset` |
| `addSession()` | Reads form, pushes to `sessions[]`, saves, re-renders |
| `openEdit(id)` / `saveEdit()` | Populates and commits the edit modal |
| `getWeekStart(offset)` | Computes Monday of the week at `weekOffset` from today |

Sessions are filtered by `dayIdx` (0=Monday … 6=Sunday) and sorted by time string.

## Development

No tooling needed — edit the file and refresh in a browser. The app is fully functional offline.
