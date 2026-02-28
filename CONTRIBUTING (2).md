# Contributing to Komal's SQL Playground

First off — thank you for taking the time to contribute! 🌸

Whether it's fixing a typo, improving the dataset, adding a new cheatsheet card, or proposing a whole new feature — every contribution is appreciated.

---

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
- [Getting Started](#getting-started)
- [Style Guidelines](#style-guidelines)
- [Pull Request Process](#pull-request-process)
- [Reporting Bugs](#reporting-bugs)
- [Suggesting Features](#suggesting-features)

---

## Code of Conduct

This project follows the [Contributor Covenant Code of Conduct](./CODE_OF_CONDUCT.md).
By participating, you agree to uphold this standard. Please report unacceptable behaviour to the repository owner.

---

## How Can I Contribute?

### 🐛 Bug Fixes
Found something broken? Open a bug report issue first, then submit a fix via pull request.

### 💡 New Features
Check the [Roadmap in README](./README.md#-roadmap) for planned features. For anything outside that list, open a feature request issue before writing code so we can discuss feasibility.

### 📚 Data & Content
- Add more student records (keep total ≤ 100 for performance)
- Add more SQL reference cheatsheet cards
- Improve existing explanations for clarity

### 🎨 Design Tweaks
Minor visual improvements (spacing, hover effects, animation polish) are welcome as PRs directly.

### 📖 Documentation
Fixing typos, improving examples, or adding new docs in the `/docs` folder is always welcome.

---

## Getting Started

Since this is a **zero-dependency, single-file project**, setup is trivial:

```bash
# 1. Fork the repository on GitHub

# 2. Clone your fork
git clone https://github.com/<your-username>/sql-playground.git
cd sql-playground

# 3. Open the file in a browser to test
open Komal_SQL_Server.html

# 4. Make your changes in any text editor

# 5. Refresh the browser to test — no build step needed
```

That's it. There's no `npm install`, no webpack, no compilation.

---

## Style Guidelines

### HTML / CSS
- All styling lives inside the `<style>` block in `Komal_SQL_Server.html`
- Use the **CSS custom property system** (`--pink`, `--bg`, `--surface`, etc.) — never hardcode hex values for themed elements
- Both `[data-theme="dark"]` and `[data-theme="light"]` variable sets must be updated when adding new themed styles
- Maintain the **Syne** (UI) + **Fira Code** (monospace) font pairing

### JavaScript / React
- All logic is inside `<script type="text/babel">`
- Keep SQL execution logic (`execute()`) and security check (`startsWith("select")`) untouched
- Use React functional components with hooks only
- New state should live in the component that needs it — avoid prop drilling for new features

### Data / SQL
- New student records must include **all 10 columns** (no nulls)
- Keep `gpa` values between `2.0` and `4.0`
- Keep `attendance` between `40` and `100`
- `status` must be exactly `"Active"` or `"On Probation"` (affects cell coloring)
- `fee_status` must be exactly `"Paid"`, `"Pending"`, or `"Waived"` (affects cell coloring)
- `grade` must be one of: `"A+"`, `"A"`, `"B+"`, `"B"`, `"C"`, `"D"`, `"F"`

### Commit Messages
Use the following prefixes:

```
feat:     A new feature
fix:      A bug fix
data:     Changes to the student dataset
style:    CSS / visual changes (no logic changes)
docs:     Documentation only
refactor: Code restructuring with no behaviour change
chore:    Maintenance (no user-facing changes)
```

**Examples:**
```
feat: add query history panel with last 10 queries
fix: prevent sidebar from exceeding max-width on small screens
data: expand dataset to 60 student records, add engineering dept
docs: add JOIN examples to SQL_REFERENCE.md
style: increase table row padding for readability
```

---

## Pull Request Process

1. **Create a branch** from `main` with a descriptive name:
   ```bash
   git checkout -b feat/query-history
   git checkout -b fix/sidebar-overflow
   git checkout -b data/add-more-records
   ```

2. **Make your changes** and test thoroughly in both dark and light themes.

3. **Test these scenarios** before submitting:
   - [ ] `SELECT * FROM students;` runs and shows all rows
   - [ ] An invalid query (e.g., `DROP TABLE students`) is blocked with an error message
   - [ ] Theme toggle works in both directions
   - [ ] Sidebar resizes smoothly between 180px and 480px
   - [ ] All 9 cheatsheet cards open, close, and load snippets correctly
   - [ ] `Ctrl + Enter` executes the query

4. **Update documentation** if needed:
   - Add new columns to the schema in `README.md`
   - Update `CHANGELOG.md` under `[Unreleased]`
   - Update `docs/USAGE.md` if user-facing behaviour changed

5. **Open a Pull Request** with:
   - A clear title following the commit prefix convention
   - Description of what changed and why
   - Screenshots if there are visual changes

---

## Reporting Bugs

Please use the [Bug Report template](.github/ISSUE_TEMPLATE/bug_report.md) and include:

- **Browser & version** (e.g., Chrome 124, Firefox 125)
- **Operating system**
- **Steps to reproduce** (be specific)
- **Expected behaviour**
- **Actual behaviour**
- **Screenshot** if applicable

---

## Suggesting Features

Please use the [Feature Request template](.github/ISSUE_TEMPLATE/feature_request.md) and include:

- **The problem** you're trying to solve
- **Your proposed solution**
- **Alternatives you've considered**
- Any **mockups or examples** from other tools

---

Thank you again for contributing! Every improvement, no matter how small, makes this a better learning tool for everyone. 💖
