<div align="center">

# Komal's SQL Playground

**A browser-based SQL learning terminal with a student academic database.**

[![Live Demo](https://img.shields.io/badge/Live-Demo-ff2e93?style=for-the-badge&logo=github)](https://komal.github.io/sql-playground)
[![HTML](https://img.shields.io/badge/HTML5-Single%20File-ff7ab8?style=for-the-badge&logo=html5)](./Komal_SQL_Server.html)
[![License](https://img.shields.io/badge/License-MIT-ffc1e3?style=for-the-badge)](./LICENSE)
[![Made With Love](https://img.shields.io/badge/Made%20with-💖-ff2e93?style=for-the-badge)](https://github.com/komal)

<br/>

<img width="959" height="403" alt="image" src="https://github.com/user-attachments/assets/4e077890-597e-42b2-9fb8-d166e2832b81" />


> *A production-quality SQL workbench that runs entirely in the browser — no backend, no setup, no dependencies to install.*

</div>

---

## Features

| Feature | Description |
|---|---|
| **Pink Aesthetic Theme** | Elegant, feminine, professional dark UI with a vibrant `#ff2e93` pink palette |
| **Dark / Light Toggle** | Smooth theme switching with full CSS variable system |
| **Resizable Sidebar** | Drag the sidebar edge to resize like VS Code |
| **SQL Reference Panel** | 9 collapsible cheat cards with clickable snippets that load directly into the editor |
| **Live SQL Execution** | Write and run `SELECT` queries instantly — no server needed |
| **Read-Only Security** | Only `SELECT` statements are permitted — safe for learning environments |
| **50-Row Academic Dataset** | Rich student database across 8 departments with 10 columns |
| **Smart Cell Coloring** | Status, grade, and fee columns are color-coded automatically |
| **Keyboard Shortcut** | `Ctrl + Enter` (or `Cmd + Enter`) to run queries |
| **Line Numbers** | Editor shows live line numbers as you type |
| **Tab Key Support** | Press Tab in the editor to insert 2-space indentation |

---

## 🚀 Quick Start

### Option 1 — Open Directly (Zero Setup)

Download [`Komal_SQL_Server.html`](./Komal_SQL_Server.html), then double-click to open in any modern browser.

```
That's it. No npm install. No server. No build step.
```

### Option 2 — Clone the Repository

```bash
git clone https://github.com/komalharshita/sql-playground.git
cd sql-playground
open Komal_SQL_Server.html   # macOS
# or
start Komal_SQL_Server.html  # Windows
# or
xdg-open Komal_SQL_Server.html  # Linux
```

### Option 3 — GitHub Pages (Recommended for Sharing)

1. Fork this repository
2. Go to **Settings → Pages**
3. Set source to `main` branch, `/ (root)`
4. Your playground will be live at `https://<your-username>.github.io/sql-playground`

---

## Database Reference

The playground ships with a single table: **`students`**

```sql
-- Table schema
CREATE TABLE students (
  student_id  INT,      -- Unique ID (1001–1050)
  name        STRING,   -- Full student name
  department  STRING,   -- Academic department
  year        INT,      -- Year of study (1–4)
  gpa         FLOAT,    -- GPA (2.1 – 4.0)
  attendance  INT,      -- Attendance percentage (48–99)
  status      STRING,   -- 'Active' | 'On Probation'
  grade       STRING,   -- 'A+' | 'A' | 'B+' | 'B' | 'C' | 'D' | 'F'
  credits     INT,      -- Credits earned (12–128)
  fee_status  STRING    -- 'Paid' | 'Pending' | 'Waived'
);
```

**Departments included:**

`Computer Science` · `Data Science` · `Mathematics` · `Physics` · `Chemistry` · `Electronics` · `Mechanical Engg`

**50 records** with realistic, varied data — a mix of honor roll students, students on probation, scholarship recipients (`fee_status = 'Waived'`), and everything in between.

---

## Example Queries to Try

```sql
-- Top 5 students by GPA
SELECT name, department, gpa
FROM students
ORDER BY gpa DESC
LIMIT 5;

-- At-risk students (low GPA AND low attendance)
SELECT name, gpa, attendance, status
FROM students
WHERE gpa < 3.0 AND attendance < 65;

-- Department summary report
SELECT department,
  COUNT(*) AS student_count,
  ROUND(AVG(gpa), 2) AS avg_gpa,
  MIN(attendance) AS lowest_att
FROM students
GROUP BY department
ORDER BY avg_gpa DESC;

-- Pending fee breakdown
SELECT name, department, year, fee_status
FROM students
WHERE fee_status = 'Pending'
ORDER BY year ASC;

-- 4th year honor students
SELECT name, grade, gpa, credits
FROM students
WHERE year = 4 AND gpa >= 3.7
ORDER BY gpa DESC;
```

---

## 🛠️ Tech Stack

| Technology | Role |
|---|---|
| **React 18** (CDN) | UI component rendering |
| **AlaSQL 1.7.3** | In-browser SQL engine |
| **Babel Standalone** | JSX transpilation in the browser |
| **Font Awesome 6.5** | Icons |
| **Syne** (Google Fonts) | Display / UI font |
| **Fira Code** (Google Fonts) | Monospace / code font |
| **Vanilla CSS** | All styling via CSS custom properties |


---

## 📁 Project Structure

```
sql-playground/
│
├── 📄 Komal_SQL_Server.html      ← The entire application (open this!)
├── 📄 README.md                  ← You are here
├── 📄 LICENSE                    ← MIT License
├── 📄 CHANGELOG.md               ← Version history
├── 📄 CONTRIBUTING.md            ← How to contribute
├── 📄 CODE_OF_CONDUCT.md         ← Community guidelines
│
├── 📁 docs/
│   ├── 📄 USAGE.md               ← Detailed usage guide
│   ├── 📄 SQL_REFERENCE.md       ← Full SQL syntax reference
│   └── 📁 assets/
│       └── 🖼️  preview.png        ← Screenshot for README
│
└── 📁 .github/
    ├── 📄 PULL_REQUEST_TEMPLATE.md
    └── 📁 ISSUE_TEMPLATE/
        ├── 📄 bug_report.md
        └── 📄 feature_request.md
```

---

## Theme System

The app uses a CSS custom property system with two fully-defined themes:

```css
/* Dark Theme (default) */
--bg:        #0a0a0f;   /* Deep black background   */
--surface:   #14141c;   /* Panel surfaces          */
--pink:      #ff2e93;   /* Primary pink accent     */
--pink-acc:  #ff7ab8;   /* Soft rose accent        */
--pink-lt:   #ffc1e3;   /* Light pink highlight    */

/* Light Theme */
--bg:        #fff5fa;   /* Warm white background   */
--pink:      #d4006b;   /* Deeper pink for contrast*/
```

Toggle is in the top-right navbar (☀ / 🌙 button).

---

## 🤝 Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](./CONTRIBUTING.md) before opening a pull request.

**Quick ideas to contribute:**
- Add more SQL concept cheatsheet cards
- Expand the dataset with more rows or columns
- Add a second table (e.g., `courses`) for JOIN examples
- Syntax highlighting in the editor
- Export results as CSV

---

## Roadmap

- [ ] Syntax highlighting in the query editor
- [ ] Multiple table support (JOIN queries)
- [ ] Export results as CSV / JSON
- [ ] Query history (last 10 queries)
- [ ] Saved queries with localStorage
- [ ] Mobile-responsive layout

---

## 📄 License

This project is licensed under the **MIT License** — see [LICENSE](./LICENSE) for details.

---

<div align="center">

Made with 💖 by **[Komal Harshita](https://github.com/komalharshita)**

*If this helped you learn SQL, please consider giving it a ⭐*

</div>
