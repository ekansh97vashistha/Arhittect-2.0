# Architect 2.0

> A vibe-coding platform for agentic applications — built for non-technical builders and technical developers, on one shared project.

**Status:** 📋 Product spec stage — this repo currently holds the PRD and design thinking, not implementation.

---
**Link to Prototype** : https://ignite-purpose-forge.lovable.app/
## The idea

Architect today is a prompt-to-app builder for non-technical users: describe a product, get a working application. It's great at zero-to-one — but the moment a project needs a real engineer, it hits a wall. The generated code isn't something a developer can confidently take over and extend.

**Architect 2.0** keeps everything Architect 1.0 does well and adds a second, equally first-class way of working: a developer-grade environment — file tree, real editor, terminal, git, framework choice — operating on the *exact same project*.

Not two products. One project, two front doors.

## Why this exists

| Today | With Architect 2.0 |
|---|---|
| Lovable / Rocket / Emergent: great for founders, but the code is stack-locked — a developer inherits it by rewriting it | A developer opens the *same* project — real files, real git, real terminal, no rewrite |
| Cursor / Antigravity: great for engineers, but no one-prompt path from idea → running agentic app | A founder gets that path, and the project they build is exactly what an engineer picks up later |

The differentiator isn't either audience alone — it's owning the handoff between them, which is where most agentic-app ideas currently die.

## Who it's for

- **Non-technical founders** who want to go from idea to a live, shareable app by describing what they want — and don't want that work thrown away the moment they bring on a developer.
- **Developers** — joining a founder's project, or building solo — who want a real IDE (file tree, editor, terminal, git) and framework-agnostic agent scaffolding, not a shallow wrapper over a chat box.

## Documentation

- 📄 **[Full Product Requirements Document](docs/PRD.md)** — complete spec: problem statement, personas, feature inventory, functional-vs-dummy scope, and a screen-by-screen flow for every surface (authentication, homepage, chat, app preview, agent building, build progress, GitHub, deployment, and more).

## Feature coverage at a glance

| # | Surface | Spec |
|---|---|---|
| 01 | Authentication (email + Google) | [§9.2](docs/PRD.md#92-authentication--sign-in-functional--email-and-google) |
| 02 | Homepage | [§9.1](docs/PRD.md#91-homepage-dummy-content-real-routing) |
| 03 | Chat window | [§9.9](docs/PRD.md#99-chat-window-dummy--shared-component-across-both-views) |
| 04 | App preview | [§9.10](docs/PRD.md#910-app-preview-dummy) |
| 05 | Agent section | [§9.12](docs/PRD.md#912-agent-building-in-any-framework-agent-section) |
| 06 | UI getting built | [§9.7](docs/PRD.md#97-ui-getting-built--the-build-progress-experience-dummy) |
| 07 | GitHub integration | [§9.13](docs/PRD.md#913-github-connection-dummy) |
| 08 | Deploying the app | [§9.14](docs/PRD.md#914-deployment-dummy) |
| + | Mode selection, invite/handoff, settings, tips & discovery, and more | [§9.3, §9.15–9.18](docs/PRD.md) |

## Scope of this phase

Per the brief, most flows are **dummy flows** — UI-complete and fully walkable, backed by simulated data rather than live logic. Two pieces are built to actually work:

- **Authentication** — real email/password and Google OAuth sign-in, with a real session.
- **Database** — real persistence for accounts, projects, collaborators, and a per-project history log.

See [§7 of the PRD](docs/PRD.md#7-functional-vs-dummy-scope) for the full functional-vs-dummy breakdown, surface by surface.

## Repo structure

```
architect-2.0/
├── README.md          ← you are here
├── docs/
│   └── PRD.md          ← full product requirements document
└── (implementation to follow)
```

## Roadmap

- [x] Product spec — problem, personas, feature inventory, functional/dummy scope
- [x] Screen-by-screen UX flows, authentication through deployment
- [ ] Wireframes / high-fidelity mocks for key screens
- [ ] Functional slice: auth + database
- [ ] Dummy-flow prototype for remaining surfaces
- [ ] Technical-workspace deep dive (file tree, editor, terminal)

## License

TBD.
