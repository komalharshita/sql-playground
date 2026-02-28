# Changelog

All notable changes to **Komal's SQL Playground** will be documented in this file.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [2.0.0] — 2025

### 🌟 Major Release — Pink Aesthetic Redesign

#### Added
- 🌸 Complete pink aesthetic theme system (`#ff2e93` primary palette)
- 🌙 Dark / Light theme toggle with smooth CSS transitions and flash animation
- ↔️ Resizable sidebar — drag the handle to adjust width (180px–480px), VS Code style
- 50 student records (expanded from 12) across 8 academic departments
- 3 new database columns: `grade` (A+–F), `credits` (earned credits), `fee_status` (Paid / Pending / Waived)
- Smart cell color-coding for all new column values
  - Grades: emerald (A/A+), pink (B/B+), amber (C), red (D/F)
  - Fee status: emerald (Paid), amber (Pending), pink accent (Waived)
- CSS custom property dual-theme system (`[data-theme="dark"]` / `[data-theme="light"]`)
- Body `cursor: col-resize` during sidebar drag for smooth UX
- `useCallback` for resize event listeners (clean teardown)

#### Changed
- Color palette fully migrated from violet/purple to pink/rose
- Table column header color updated to `--pink`
- Scrollbar colors updated to match new palette
- Version bumped from `v1.0` to `v2.0` in footer
- Bottom strip now lists all 10 columns

---

## [1.0.0] — 2025

### 🎉 Initial Release

#### Added
- Single-file HTML application — open in browser, zero setup
- Violet / dark cyberpunk aesthetic theme
- SQL query editor with:
  - Live line numbers
  - Tab key → 2-space indent
  - `Ctrl + Enter` to execute
- AlaSQL in-browser SQL engine
- `SELECT`-only security enforcement
- Dynamic results table rendering
- 9-card collapsible SQL reference panel (sidebar):
  - SELECT, WHERE, AND/OR, ORDER BY, LIMIT, LIKE, Aggregates, GROUP BY, AS
  - Each card contains plain-English explanation + clickable code snippets
  - Clicking a snippet loads it into the editor and executes automatically
- 12 student records with 7 columns
- GitHub profile link in navbar (top-right)
- Status indicators (live dot, read-only badge)
- "Built by Komal" footer credit
- Syne + Fira Code font pairing
- Ambient glow effects (radial gradients)
- Noise texture overlay
- Custom pink scrollbar
- Row count badge with `fade-up` animation on each execution
- Error state with styled error message
- Empty state placeholder

---

## [Unreleased]

### Planned
- [ ] Syntax highlighting in query editor
- [ ] Second table (`courses`) for JOIN query practice
- [ ] Query history (last 10 queries)
- [ ] Export results as CSV
- [ ] Export results as JSON
- [ ] Mobile / responsive layout improvements
- [ ] Keyboard shortcut help modal

---

*For questions or suggestions, open an [issue](https://github.com/komal/sql-playground/issues).*
