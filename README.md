# Curiosity OS

**An open learning experience for practicing better questions, evidence-based reasoning, and connected thinking.**

Curiosity OS pairs a navigable 3D concept graph with a library of practical activity playbooks. Explore concepts through the **Curiosity Verse**, browse six curated learning paths, or search and filter activities by purpose, mode, preparation, energy, and duration.

> **Project status:** A functioning learning portal and early-stage concept product. The graph, learning paths, activity library, and activity detail pages are implemented. The in-app activity runner, reflection routes, and planner route currently redirect or route elsewhere; they are not an end-to-end session workflow.

## What is implemented

- A WebGL knowledge map with **147 concepts**, **381 relationships**, four thematic wings, saved layout coordinates, node search and selection, and Student, Mentor, and Builder views.
- **36 Markdown activity playbooks**, rendered through an activity library and detail pages, plus **10 collections** and **six curated learning paths**.
- Local browser storage for graph visits and planner/evidence state models. The latter models exist in code, but their planned runner and planner routes are not currently reachable as working flows.
- A small Node content pipeline that validates and compiles Markdown activity and collection files into JSON artifacts.

## Product and engineering decisions

- The concept graph is authored as structured JSON; a separate teaching-state file and saved layouts are joined by node ID at the server page before the graph is rendered.
- Activity playbooks use Markdown with YAML frontmatter, keeping authored content readable while allowing the UI to consume a structured index.
- Browser-local state avoids an account or database requirement, but it is device-local and can be cleared with site data.
- The repository contains early and unfinished surfaces alongside the working browse experience. See the [limitations and route status](PROJECT_BLUEPRINT.md#maturity-and-implemented-surfaces) before treating planned flows as shipped.

## Stack

| Area | Technologies |
|---|---|
| Application | Next.js 16 App Router, React 19, TypeScript |
| Styling and interaction | Tailwind CSS 4, Framer Motion, Lucide React |
| 3D visualization | Three.js, React Three Fiber/Drei, `react-force-graph-3d`, `three-spritetext` |
| Content | Markdown, `gray-matter`, `react-markdown`, `remark-gfm` |
| Browser state | React Context and `localStorage` |

Versions and scripts are defined in [`package.json`](package.json) and [`package-lock.json`](package-lock.json).

## Run locally

Requires Node.js and npm.

```bash
git clone https://github.com/tharungajula2/curiosity-os.git
cd curiosity-os
npm install
npm run dev
```

Open `http://localhost:3000`. See the [Project Blueprint](PROJECT_BLUEPRINT.md) for architecture, content workflows, and troubleshooting.

## Demo status

The previous README listed [curiosity-os.vercel.app](https://curiosity-os.vercel.app). That address could not be verified during this documentation review, so it is not presented as a working demo. The source repository is the reliable way to explore the project.

## Documentation

- **[Project Blueprint](PROJECT_BLUEPRINT.md)** — a source-grounded guide to the app, data flow, graph, state, setup, and known gaps.
