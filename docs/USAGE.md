# Usage Guide — Komal's SQL Playground

This guide covers everything you need to use the SQL Playground effectively.

---

## Opening the App

Simply open `Komal_SQL_Server.html` in any modern browser:

| OS | Command |
|---|---|
| macOS | `open Komal_SQL_Server.html` |
| Windows | Double-click the file, or `start Komal_SQL_Server.html` |
| Linux | `xdg-open Komal_SQL_Server.html` |

**Supported browsers:** Chrome 90+, Firefox 88+, Safari 14+, Edge 90+

> ⚠️ Opening directly from the filesystem (`file://`) works fine. No local server required.

---

## Interface Overview

```
┌─────────────────────────────────────────────────────────────────┐
│  TOPBAR  │  Logo  │  Status Pills  │  Theme Toggle  │  GitHub   │
├──────────┬──────────────────────────────────────────────────────┤
│          │                                                      │
│  SQL     │   QUERY EDITOR                                       │
│  REFER-  │   ┌─────────────────────────────────────────────┐   │
│  ENCE    │   │  query.sql                        [Run]      │   │
│  PANEL   │   │  1  SELECT * FROM students;                  │   │
│          │   └─────────────────────────────────────────────┘   │
│  (drag   │                                                      │
│   edge   │   RESULTS TABLE                                      │
│   to     │   ┌─────────────────────────────────────────────┐   │
│   resize)│   │  student id │ name │ dept │ ...              │   │
│          │   │  1001       │ Aara │ CS   │ ...              │   │
│          │   └─────────────────────────────────────────────┘   │
├──────────┴──────────────────────────────────────────────────────┤
│  BOTTOM  │  table: students · columns...  │  Built by Komal     │
└─────────────────────────────────────────────────────────────────┘
```

---

## The Query Editor

### Writing Queries
Click anywhere in the editor panel and start typing your SQL query.

### Running a Query
Three ways to execute:
1. Click the **Run** button (top-right of the editor panel)
2. Press **`Ctrl + Enter`** (Windows / Linux)
3. Press **`Cmd + Enter`** (macOS)

### Keyboard Shortcuts
| Key | Action |
|---|---|
| `Ctrl + Enter` / `Cmd + Enter` | Execute current query |
| `Tab` | Insert 2-space indent at cursor position |

### Security Restriction
Only `SELECT` queries are allowed. Any query that doesn't begin with `SELECT` will be blocked:

```
✅ SELECT * FROM students;
✅ SELECT name, gpa FROM students WHERE gpa > 3.5;
❌ DROP TABLE students;   → blocked
❌ INSERT INTO students;  → blocked
❌ UPDATE students SET …; → blocked
```

---

## The Results Table

After running a query, results appear in the panel below the editor.

### Status Badge
The badge in the results header updates after every run:

| Badge | Meaning |
|---|---|
| `12 rows returned` (green) | Query ran successfully |
| `query error` (red) | Something went wrong — check the error message |
| `awaiting query` (grey) | No query has been run yet |

### Cell Color Coding
Certain values are highlighted automatically:

| Value | Color | Meaning |
|---|---|---|
| `Active` | 🟢 Emerald | Student in good standing |
| `On Probation` | 🔴 Red | Student at academic risk |
| `A+` / `A` | 🟢 Emerald | Excellent grade |
| `B+` / `B` | 🌸 Pink | Good grade |
| `C` | 🟡 Amber | Average grade |
| `D` / `F` | 🔴 Red | Failing grade |
| `Paid` | 🟢 Emerald | Fee cleared |
| `Pending` | 🟡 Amber | Fee outstanding |
| `Waived` | 🌸 Pink | Fee waived (scholarship) |
| Any number | 🟡 Amber | Numeric values right-aligned |

---

## The SQL Reference Panel (Sidebar)

The left panel contains **9 collapsible cheatsheet cards** covering the most common SQL concepts.

### Using the Cards
1. Click any card header to **expand** it and read the explanation
2. Click again to **collapse**
3. Click any **code snippet** inside a card to:
   - Load it into the query editor
   - Execute it automatically

### Cards Available
| Card | Concept Covered |
|---|---|
| `SELECT` | Fetching all or specific columns |
| `WHERE` | Filtering rows by condition |
| `AND / OR` | Combining multiple conditions |
| `ORDER BY` | Sorting results ascending or descending |
| `LIMIT` | Capping the number of rows returned |
| `LIKE` | Pattern matching with `%` wildcards |
| `Aggregates` | COUNT, AVG, MAX, MIN functions |
| `GROUP BY` | Grouping rows for aggregate summaries |
| `AS` | Aliasing columns and computed fields |

### Resizing the Sidebar
Hover over the **right edge** of the sidebar — your cursor changes to ↔. Click and drag to resize between **180px** (compact) and **480px** (wide).

---

## Theme Toggle

Click the ☀ / 🌙 button in the top-right navbar to switch between:

- **Dark mode** — `#0a0a0f` deep black background with vibrant pink accents
- **Light mode** — `#fff5fa` warm white with deeper rose tones

The transition is animated with a subtle pink flash effect.

---

## Database Reference

See the full schema and example queries in [README.md](../README.md#-database-reference).

For a complete SQL syntax reference, see [SQL_REFERENCE.md](./SQL_REFERENCE.md).

---

## Troubleshooting

### The page looks broken / unstyled
Make sure you're opening the file in a **modern browser** (Chrome, Firefox, Edge, Safari). Internet Explorer is not supported.

### My query isn't running
Check that:
1. Your query starts with `SELECT`
2. The table name is `students` (lowercase, no quotes)
3. Column names match exactly — see the schema in [README.md](../README.md)

### The sidebar won't resize
The resize handle is the thin strip on the **right edge** of the sidebar. Hover until you see the ↔ cursor, then drag.

### Fonts look wrong
The app loads fonts from Google Fonts. If you're offline, the browser will fall back to system sans-serif and monospace fonts. Everything will still work — it just won't look as polished.

---

*For more help, open an [issue on GitHub](https://github.com/komal/sql-playground/issues).*
