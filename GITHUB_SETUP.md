# GitHub Setup Guide

*How to push this repository to GitHub and keep it organized.*

---

## 1. Create the GitHub Repository

1. Go to [github.com/new](https://github.com/new)
2. Repository name: `1149-ideas` (or `founder-os`, `idea-repo` — your choice)
3. **Set to Private** — this is your personal knowledge base
4. Do NOT initialize with README (you already have one)
5. Click Create Repository

---

## 2. Push from Local Machine

```bash
# Navigate to this folder (wherever you unzipped it)
cd path/to/idea-repo

# Initialize git
git init

# Set your identity
git config user.name "Founder Alex"
git config user.email "your@email.com"

# Add all files
git add .

# First commit
git commit -m "init: 1149 idea repository — 18 projects, 30 documents"

# Connect to GitHub (replace YOUR_USERNAME)
git remote add origin https://github.com/YOUR_USERNAME/1149-ideas.git

# Push
git push -u origin main
```

---

## 3. Recommended GitHub Settings

### Branch protection
Settings → Branches → Add rule for `main`:
- ✅ Require pull request reviews before merging
- ✅ Require status checks (if you add CI later)

### Labels
Create these labels for Issues:
- `idea` — new idea capture
- `documentation` — adding white paper / tech spec
- `connection` — linking ideas together
- `needs-triage` — unreviewed captures
- `priority-critical` / `priority-high` / `priority-medium` / `priority-low`

### Projects (GitHub Projects)
Create a GitHub Project board with columns:
```
Seed  →  In Development  →  Active  →  Paused  →  Archived
```
Link each idea folder to a card.

---

## 4. Daily Workflow

### Capturing a new idea (< 2 min)
```bash
# Option A: Add to IDEAS_REGISTRY.md directly
# Open the file, add one row to "Concept / Seed Ideas"

# Option B: GitHub Issue (from phone/anywhere)
# Click "New Issue" → "New Idea — Quick Capture"
```

### Developing an idea
```bash
# Create the folder
mkdir ideas/apps/my-new-idea

# Copy template
cp _templates/WHITE_PAPER_TEMPLATE.md ideas/apps/my-new-idea/WHITE_PAPER.md

# Edit
code ideas/apps/my-new-idea/WHITE_PAPER.md

# Commit
git add .
git commit -m "ideas/apps/my-new-idea: add white paper draft"
git push
```

### Weekly review
```bash
# See what changed this week
git log --since="7 days ago" --oneline

# See which ideas still need work
grep -r "In Development\|stub\|TODO" ideas/ --include="*.md" -l
```

---

## 5. Useful Git Commands for This Repo

```bash
# Search for a concept across all docs
grep -r "solidarity" ideas/ --include="*.md" -l

# Find all ideas tagged with a specific tag
grep -r "ECC" ideas/ --include="*.md" -l

# Find all ideas without a tech spec
for d in ideas/*/*/; do
  [ ! -f "${d}TECH_SPEC.md" ] && echo "No TECH_SPEC: $d"
done

# See all status:active ideas
grep -r "^status: active" ideas/ --include="*.md" -l

# Word count of entire repository
find ideas/ -name "*.md" -exec wc -w {} + | tail -1
```

---

## 6. Optional: GitHub Pages

Turn this repo into a browsable knowledge base:
1. Settings → Pages → Source: main branch, /docs folder
2. Add a `docs/` folder with an `index.md`
3. Use a simple Jekyll theme

This gives you a private web interface for navigating your ideas — useful for sharing with collaborators without giving full git access.

---

## 7. Automation (Optional, n8n)

Once the repo is on GitHub, automate:

```
n8n workflow: "Idea Capture"
  Trigger: Telegram message to your bot starting with "/idea"
  → Parse title + one-line description
  → Create GitHub Issue using "New Idea" template
  → Reply with: "Captured as Issue #XX ✓"
```

This lets you capture ideas from your phone in 10 seconds.

---

*Repository: 1149 // Idea Repository*
