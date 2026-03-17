---
id: "8008"
title: "UU Interactive — Technical Specification"
layer: "03_Meta_Ecosystems"
status: concept
version: 0.1
updated: 2026-03-17
author: Founder Alex
---

# UU Interactive — Technical Specification

**UU Interactive — Technical Architecture Document**  
**Version 1.0**  
**Date:** March 14, 2026  
**Project:** uu-interactive (GitHub: uu-interactive)  
**Status:** Backend + Story Builder Specification  

---

### 1. Executive Overview

**uu-interactive** is a full-stack platform that starts as interactive vertical cinema (60-second episodes) and evolves into DAO 2.0 collective decision-making.  

The frontend website already exists.  
This document defines the **missing pieces**:
- **Backend** (real-time voting, user management, story storage)  
- **Story Builder** — a powerful **node-based visual editor** (called **Nexus Editor**) where Mind Masters and creators build and publish branching stories.

**Core principle**: Every story is a directed graph of 1-minute video nodes. Creators see the full timeline + branches at a glance. Viewers vote in real time. The same system later powers real-world votes.

**Key Features of Nexus Editor**:
- Drag-and-drop node graph (React Flow / xyflow)
- Each node = 60-second video episode + vote options
- Visual branches + “fruits” (terminal outcome nodes that can trigger real-world actions)
- Real-time preview and publish button
- Version history + collaborative editing (future)

---

### 2. High-Level Architecture

```
Frontend (Next.js – already exists)
    ↓
Nexus Editor (React Flow + Next.js app)
    ↓
Supabase Backend
    ├── Database (Postgres)
    ├── Realtime (voting + live graph updates)
    ├── Storage (video files + thumbnails)
    ├── Edge Functions (voting logic, outcome triggers)
    └── Auth (email + optional wallet)

External:
    - Bunny.net / Vimeo (video CDN)
    - Stripe (payments)
    - YouTube API (free tier polling)
```

---

### 3. Backend – Supabase Setup

We use **Supabase** as the single source of truth (free tier is enough for MVP).

**Database Tables** (main schema):

```sql
-- Stories
stories (
    id uuid primary key,
    title text,
    creator_id uuid,
    is_published boolean default false,
    created_at timestamp
)

-- Episodes (Nodes)
episodes (
    id uuid primary key,
    story_id uuid references stories,
    title text,
    video_url text,           -- Bunny.net link
    duration int default 60,  -- always ~60 seconds
    node_type text check (node_type in ('start', 'episode', 'vote', 'outcome')),
    position jsonb            -- {x: 150, y: 300} for graph
)

-- Branches (Edges)
branches (
    id uuid primary key,
    from_episode_id uuid references episodes,
    to_episode_id uuid references episodes,
    label text,               -- e.g. "Lethal", "Spare", "Path A"
    vote_weight int default 1
)

-- Votes (Realtime)
votes (
    id uuid primary key,
    episode_id uuid references episodes,
    user_id uuid,
    choice text,              -- "Lethal" / custom label
    created_at timestamp
)

-- Outcomes ("Fruits")
outcomes (
    id uuid primary key,
    episode_id uuid references episodes,
    title text,
    description text,
    real_world_action jsonb   -- { "type": "fund", "amount": 1500, "project": "ocean-cleanup" }
)

-- Users & Membership
profiles, subscriptions (Stripe integration via Supabase Edge Functions)
```

**Realtime Channels**:
- `votes:episode_id` — live vote counter
- `graph:story_id` — live updates when creator moves nodes

**Storage Buckets**:
- `videos` (1-minute clips)
- `thumbnails`

**Edge Functions** (Node.js):
- `calculate-majority` — decides next episode after voting window
- `trigger-outcome` — when terminal node reached, executes real-world action

---

### 4. Nexus Editor – Node-Based Story Builder

**Technology**: React Flow (xyflow) – the best open-source node editor in 2026.  
Fully embedded in a protected admin route `/builder/[story-id]`.

**Node Types** (custom React components):
1. **Start Node** – purple, single output
2. **Episode Node** – video preview + title + upload button (60s max)
3. **Vote Node** – 2–4 choice buttons (auto-generates branches)
4. **Outcome Node** (“Fruit”) – terminal, green/red, can link to real-world DAO action

**Features**:
- Canvas with zoom/pan/minimap
- Drag nodes → auto-save position to DB
- Right-click → add vote options
- Sidebar: Media library, vote analytics preview, publish button
- “Timeline View” toggle — linear list of all 1-minute fruits
- Export: JSON graph + full video package

**Collaboration**: Supabase Realtime + row-level security (only Mind Masters + story creator can edit).

---

### 5. Voting & Publishing Flow

1. Creator uploads 1-minute videos in Nexus Editor → builds graph.
2. Publishes story → episodes become public.
3. Viewer watches current node → votes appear (React Flow preview in player).
4. Realtime majority wins → next node unlocks automatically.
5. When Outcome Node reached → system triggers real-world action (if configured).

---

### 6. Step-by-Step Instruction: Build the Full Project (MVP in 3–4 weeks)

**Week 1 – Backend Foundation**

1. Create Supabase project → name it `uu-interactive-prod`
2. Run the SQL schema above (copy-paste into SQL editor)
3. Enable Realtime on `votes`, `episodes`, `branches`
4. Create Storage bucket `videos` (public + RLS)
5. Add Edge Functions:
   - `calculate-majority`
   - `trigger-outcome`

**Week 2 – Nexus Editor (Node-Based Tool)**

6. In your existing Next.js repo create new route `/builder`
7. `pnpm add reactflow @xyflow/react zustand`
8. Create `components/NexusEditor.tsx` using official React Flow template
9. Implement custom nodes (EpisodeNode, VoteNode, OutcomeNode)
10. Connect to Supabase:
    - Load graph on mount (`supabase.from('episodes').select()`)
    - onNodeDragStop / onEdgesChange → auto-save
    - Real-time subscription to graph updates

**Week 3 – Voting Player + Integration**

11. Extend existing frontend player to read current `episode_id`
12. Show React Flow mini-map of the whole story (read-only for viewers)
13. Add voting buttons that insert into `votes` table
14. Use Edge Function to calculate winner and unlock next episode

**Week 4 – Polish & Deploy**

15. Add Stripe webhook for membership tiers (Voter / Co-Creator / Architect)
16. Implement “Fruits” (outcome) dashboard for Mind Masters
17. Deploy:
    - Frontend + Nexus Editor → Vercel
    - Supabase → already cloud
    - Videos → Bunny.net (cheapest + fast)
18. Test first story “10 000 000” end-to-end

**Required Environment Variables** (`.env.local`):

```env
NEXT_PUBLIC_SUPABASE_URL=...
NEXT_PUBLIC_SUPABASE_ANON_KEY=...
SUPABASE_SERVICE_ROLE_KEY=...   # for Edge Functions
BUNNYNET_API_KEY=...
STRIPE_SECRET_KEY=...
```

---

### 7. Security & Permissions (RLS)

- Public can read published stories + vote (if paid or free tier)
- Only authenticated creators can edit their own stories
- Mind Masters group has full access

---

### 8. Future Roadmap (after MVP)

- Multi-user real-time collaboration in Nexus Editor
- AI assistant: “suggest next branch”
- Mobile version of builder
- Open-source the voting engine

---

** GitHub repo https://github.com/AlexSheff/uu-interactive **


We are building the operating system for collective storytelling — let’s ship it. 🚀

---

*Tech Spec · Reality Refactor Lab · 1149*
