---

# 3. curiosity-os

═══════════════════════════════════════════════════

# Curiosity OS

A static, offline-friendly portal for building questioning and critical thinking habits. Built for students, teachers, parents and self-learners.

**Live:** [curiosity-os.vercel.app](https://curiosity-os.vercel.app)

---

## What it does

Most learning environments reward recall and compliance. They rarely teach the thing underneath: how to interrogate a claim, trace a cause, or notice when an argument has a hole in it.

Curiosity OS gives that a place to be practised. It has two halves. An interactive 3D concept map of reasoning ideas that can be explored by wandering and tracing connections rather than reading in order. And a library of written playbooks with structured timelines, prompts and named failure points, meant to be run in a room with other people rather than read alone.

It runs entirely client-side. No login, no database, no tracking, no analytics. That is deliberate: the likely users include minors in schools, and the safest way to handle their data is not to collect any. It also means the whole thing works offline and on low-bandwidth connections.

## Key numbers

| Item | Count |
|---|---|
| Concept nodes | 147 |
| Links between concepts | 381 |
| Thematic wings | 4 |
| Written playbooks | 36 |
| Learning paths | 6 |

The four wings are Decode, Cognition, Relate and Sandbox. The map can be viewed through Student, Mentor and Builder perspectives.

## How it works

Markdown playbooks are compiled at build time into static JSON indices by a custom Node script, with a companion validator that catches schema problems before the build rather than after. The 3D graph reads pre-computed layout coordinates from a static JSON file. Bookmarks and local state live in browser storage.

```
[markdown playbooks] ──(build:activities)──► [static JSON index] ──┐
                                                                   ├──► React UI ◄──► localStorage
[universe JSON files] ─────────────────────────────────────────────┘
                              │
                              ▼
                   [3D force-directed graph]
```

## What is real and what is a demo

**Shipped:** the 3D WebGL concept map with force-directed physics across 147 nodes and 381 links, the 36 written playbooks with preparation notes, age levels, steps and failure points, the 6 learning paths, and the build-time compilation and validation pipeline.

**Coded but currently bypassed:** the step-by-step facilitation HUD with countdown timers, the evidence-tagging terminal, the guided post-session reflection workspace, and the activity planner with bookmark queues. All four are fully implemented in the repository but their routes redirect to the static detail pages, because the project moved toward being an open directory rather than a session runner.

**Contains no AI or machine learning of any kind.** Internal naming like "Neural Core" and "Cognition OS" is thematic. There are no LLM calls and no models. The concept relationships are hand-structured JSON traversed by custom logic.

## Hardest problems solved

**Keeping a WebGL graph stable inside Next.js.** Force graph components leak memory and break on hot reload and route changes under server-side rendering. Resolved by dynamically importing the component with SSR disabled and wrapping render in a mounted guard, so the WebGL context only ever initialises client-side.

**Static compilation with schema validation.** To support a zero-database architecture, a build script parses markdown frontmatter, maps category enums and emits lightweight JSON indices. A separate validator runs first and fails the build on schema drift, which stops malformed content from silently breaking layout.

**Coordinate pinning in a force-directed layout.** Live physics layouts reposition nodes on every load, which destroys any sense of place. The graph loads pre-computed coordinates and pins nodes with explicit position overrides, keeping a consistent spatial map while retaining interactive physics.

## Limitations

1. Facilitation timers, evidence tagging, reflection and the planner are all unreachable behind redirects.
2. All state lives in browser storage, so clearing the cache erases bookmarks and saved sessions. There is no export or import.
3. The 3D graph is heavy on low-end mobile devices. A directory fallback exists, but there is no low-poly mode.
4. Content is fixed at build time. There is no editing interface.

## Stack

Next.js 16.1, React 19.2, Tailwind CSS 4, Three.js 0.183, React Three Fiber 9.5, React Three Drei 10.7, `react-force-graph-3d` 1.29, three-spritetext, Framer Motion, gray-matter, react-markdown, remark-gfm.

## Running it

```bash
git clone https://github.com/tharungajula2/curiosity-os.git
cd curiosity-os
npm install
npm run dev
```

## Contact

Tharun Gajula · Bengaluru, India
[tharun.gajula.2@gmail.com](mailto:tharun.gajula.2@gmail.com) · [LinkedIn](https://linkedin.com/in/tharungajula) · [Portfolio](https://tharungajula.vercel.app)

═══════════════════════════════════════════════════

---
