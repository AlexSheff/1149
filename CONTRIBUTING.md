# Contributing to the 1149 Idea Repository

*This is a personal repository. "Contributing" here means: adding and developing your own ideas if you are Founder Alex, or proposing connections if you are a collaborator.*

---

## For Founder Alex — Adding a New Idea

### Fast capture (< 2 minutes)
1. Open `IDEAS_REGISTRY.md`
2. Add a row to **Concept / Seed Ideas** with: ID, title, one sentence, category, connections
3. Done. The idea is captured. Develop it later.

### Full idea development (when you are ready)
1. Create the folder: `ideas/{category}/{slug}/`
2. Copy the right template from `_templates/`
3. Fill in the front matter (at minimum: id, title, category, status, tags)
4. Write at least sections 1–4 (Problem, Vision, Philosophy, Mechanism)
5. Add the idea to `README.md` Registry table
6. Add the idea to `IDEAS_REGISTRY.md`
7. Add connections to `CONNECTIONS.md`

### Naming conventions
- Folder slugs: `kebab-case` (e.g. `choose-and-own`, `ai-cinema-lab`)
- Document names: always `WHITE_PAPER.md` or `TECH_SPEC.md` (uppercase, exact)
- IDs: 3-digit zero-padded (`001`, `012`, `S01` for seeds)

---

## Document Rules

### Front matter is required
Every document must have the YAML front matter block at the top.
The minimum required fields are: `id`, `title`, `category`, `status`, `tags`.

### One sentence summary
Every white paper must start with a blockquote `>` that is a single, precise sentence.
If you cannot write that sentence, the idea is not yet ready for a white paper.

### The Solidarity Check
Every idea that touches City Quest, Good Project Corp, 4Boon, or any economic system must answer:
> **"Where does the solidarity happen in this code / process / structure?"**
If the answer is "we hope people will be generous" — the design is incomplete.

### Status lifecycle
```
🟡 Concept  →  🔵 Research  →  🟢 Active  →  (⚪ Paused or 🔴 Archived)
```

Ideas can move backward. Paused ideas are not failures.

---

## File Structure Rules

```
ideas/
├── {category}/
│   └── {slug}/
│       ├── WHITE_PAPER.md     ← philosophy, vision, mechanism
│       ├── TECH_SPEC.md       ← architecture, stack, algorithms
│       ├── NOTES.md           ← informal scratch pad (optional)
│       └── assets/            ← diagrams, screenshots (optional)
```

Never put multiple ideas in one folder.
Never create files outside the established structure without updating README.md.

---

## For Collaborators

If you are not Founder Alex:
1. Open a GitHub Issue using the "New Idea" template to propose additions or connections
2. Do not create files directly — propose via issue
3. All additions to the repository require explicit confirmation from Founder Alex

---

*Repository: 1149 // Idea Repository — Founder Alex*
