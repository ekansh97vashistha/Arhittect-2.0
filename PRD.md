# Architect 2.0 — Product Requirements Document

*A vibe-coding platform for agentic applications — built for non-technical builders and technical developers on one shared project*

**Prepared by:** Ekansh
**Document status:** Draft for review — v1.1
**Scope:** Product & UX specification. No implementation code in this phase.

---

# 1. Overview & Purpose

Architect today is a prompt-to-app builder for non-technical users: describe a product, get a working application. It has proven the core loop — plain-language input, generated output, one-click publish — but it stops there. It cannot be handed to a developer, it does not support real codebases, and it has no path for anyone who wants to work in code.

Architect 2.0 keeps every capability of the current product and adds a second, equally first-class way of working: a developer-grade environment — file tree, real editor, terminal, git, framework choice — operating on the exact same project. The two experiences are not separate products; they are two views onto one underlying agentic application and one underlying repository.

This document specifies the full product: every screen, every flow from authentication through deployment, and exactly what is real versus simulated in this phase. No implementation code is included — this is the specification the build will follow.

# 2. Problem Statement

- Architect 1.0 serves founders well but hits a wall the moment a project needs a real engineer — the generated app is not something a developer can confidently take over and extend.

- Competing "vibe coding" tools (Lovable, Rocket.new, Emergent) share this same ceiling: excellent at zero-to-one, but the code they produce is stack-locked and not built for a developer to inherit.

- Competing developer tools (Cursor, Antigravity) solve the opposite problem — full control for engineers — but offer no one-prompt path from idea to running app, and no experience a non-technical founder could use unassisted.

- Nobody today lets a founder and an engineer work on the same product, in the interface suited to each, without a rewrite or a tool switch in between.

# 3. Goals

- Preserve every existing Architect 1.0 capability for non-technical users — nothing about today's product gets worse or disappears.

- Add a developer-grade workspace (file tree, editor, terminal, git, framework selection) usable on the same project a non-technical user created.

- Cover every core surface a platform like this needs — authentication, homepage, chat, app preview, agent building, the build process itself, GitHub, and deployment — as a fully specified, walkable flow, not just the headline features.

- Ship authentication (including Google Sign-In) and a real database as functional slices, so the prototype is not 100% simulated.

- Prove the handoff moment — a founder's project becoming something a developer can pick up — as a designed part of the product, not an afterthought.

## 3.1 Non-Goals for this Phase

- No production-grade code generation engine — generation steps are simulated (dummy progress, canned but realistic output) except where explicitly marked Functional.

- No real deployment to live infrastructure — the Deploy flow is a dummy flow that ends in a realistic (but non-hosting) confirmation screen and a fake live URL.

- No real GitHub OAuth/API integration — the GitHub connection flow is simulated end-to-end.

- No billing/payment processing — pricing screens exist for completeness but take no real payment.

- No multi-framework agent execution — the framework picker and agent trace viewer are UI-complete but do not run real agents in this phase.

# 4. Target Users & Personas

### Persona A — "Priya," the non-technical founder

- Has a product idea, no engineering background. Wants to see something working today, not a technical spec.

- Success looks like: a live, shareable app URL, built entirely by describing what she wants in plain language.

- Never wants to see a file tree, a terminal, or an error stack trace by default.

### Persona B — "Dev," the engineer joining or building solo

- Comfortable in an IDE and a terminal; evaluates any AI tool against Cursor, which is the incumbent in their daily workflow.

- Success looks like: real file access, a real diff before anything is committed, and a codebase clean enough to keep extending by hand.

- Will abandon the tool within minutes if the "technical mode" turns out to be a shallow wrapper over the same chat box Priya uses.

### Persona C — the shared project

Most real usage sits between A and B: Priya starts a project solo, then invites Dev partway through — or Dev scaffolds a project and hands a specific agent's behaviour to Priya to tune. Every flow below is written with this handoff in mind, not just the two personas in isolation.

# 5. Guiding Design Principle: One Project, Two Front Doors

The product is not "Architect for beginners" plus "Architect for developers" as two SKUs. It is one project record — one agent graph, one repository, one deployment history — rendered through two modes that a user (or a single project) can switch between at any time:

**Simple View —** canvas, live preview, plain-language agent flow diagram, one-click actions. Nothing technical is shown unless requested.

**Code View —** file tree, code editor, terminal, git diffs, framework and deployment configuration. Nothing is hidden or abstracted away.

A visible toggle in the top bar ("Simple View / Code View") switches the same project between the two — this is the single most important UI element in the product, because it is the physical proof that the bridge is real and not marketing.

# 6. Feature Inventory

Carried over unchanged from Architect 1.0, plus what Architect 2.0 adds. This is the checklist the flows in Section 9 walk through.

## 6.1 Carried over from Architect 1.0 (non-technical, must not regress)

| **Feature**               | **Description**                                                                     |
|---------------------------|-------------------------------------------------------------------------------------|
| Prompt-to-app generation  | Describe a product in plain language; get a working app with a live preview.        |
| Visual edits              | Click an element in the preview and change copy, layout, or style directly.         |
| Plain-language agent flow | See what the agent does as a simple diagram of steps, editable in natural language. |
| One-click publish         | Publish the app to a shareable URL without any configuration.                       |
| Project history           | A simple, restorable timeline of past versions.                                     |

## 6.2 New in Architect 2.0

| **Feature**                             | **Description**                                                                             | **Audience**                                           |
|-----------------------------------------|---------------------------------------------------------------------------------------------|--------------------------------------------------------|
| Simple View / Code View toggle          | Switch the same project between canvas and IDE rendering.                                   | Both                                                   |
| Full IDE workspace                      | File tree, code editor, integrated terminal, diff view.                                     | Technical                                              |
| Import existing project                 | Bring in a GitHub repo or zip; Architect indexes it before touching anything.               | Both                                                   |
| Framework picker                        | Choose the agent framework a project is built on at creation, or per-agent later.           | Technical (auto-selected for non-technical)            |
| Agent trace / debug view                | Inspect an agent's reasoning steps, tool calls, and outputs.                                | Technical (available, de-emphasised for non-technical) |
| Real GitHub connection                  | Two-way sync — commits, branches, PRs.                                                      | Both, different depth                                  |
| Deployment with environment control     | Choose environment/target; view logs; roll back.                                            | Technical (one-click default for non-technical)        |
| Invite & handoff flow                   | A designed moment for a founder to bring in a developer, or vice-versa.                     | Both                                                   |
| Authentication & account                | Real sign-up/login (email + Google), session, and profile.                                  | Both — Functional                                      |
| Google Sign-In                          | One-click OAuth sign-up/login via Google; matches or creates an account by verified email.  | Both — Functional                                      |
| Project database                        | Real persistence of projects, users, and history.                                           | Both — Functional                                      |
| Build-progress visualization            | The app assembling itself, shown live during generation.                                    | Both, different depth                                  |
| Developer/non-technical onboarding step | First screen after sign-up; sets which workspace opens first and how the Dashboard renders. | Both — Functional                                      |
| Contextual tips / discovery prompts     | Lightweight, dismissible tips, including teaching Simple View users how to reach Code View. | Both, aimed mainly at non-technical                    |

# 7. Functional vs. Dummy Scope

Per the brief, most flows in this phase are dummy flows that demonstrate the intended UX without real backend logic. Authentication (email and Google) and the project database are the pieces built to actually work. This table is the single source of truth for what to expect when reviewing the prototype.

| **Area**                                     | **Status**                  | **Notes**                                                                                                                    |
|----------------------------------------------|-----------------------------|------------------------------------------------------------------------------------------------------------------------------|
| Sign-up / Login — email                      | Functional                  | Real account creation, password hashing, session persistence in the database.                                                |
| Sign-up / Login — Google                     | Functional                  | Real OAuth 2.0 / OpenID Connect; account matched or created by verified email; session issued identically to the email path. |
| Mode Selection (developer vs. non-technical) | Functional                  | First onboarding step after sign-up; choice is saved to the account and determines which workspace opens first.              |
| Project database                             | Functional                  | Real create/read/update of project, account, and collaborator records, plus a per-project history/event log.                 |
| Homepage                                     | Dummy content, real routing | Marketing content and example prompts are static; Sign up / Log in / "start building" CTAs route into the real auth flow.    |
| Prompt-to-app generation                     | Dummy                       | Simulated plan → simulated progress steps → canned preview output relevant to the prompt category.                           |
| Import existing project                      | Dummy                       | Upload/connect UI is real; indexing and analysis results are simulated.                                                      |
| UI getting built (build progress)            | Dummy                       | Scripted step sequence and log lines; preview and file tree populate from canned, category-matched content.                  |
| Chat window                                  | Dummy                       | Full conversational UI and message states; responses are canned, not generated live.                                         |
| App preview                                  | Dummy                       | Live-feeling preview pane reacting to edits; content is simulated, not a running application.                                |
| Visual edits                                 | Dummy                       | Click-to-edit UI works on a static preview; changes are not persisted to real code.                                          |
| Agent flow diagram & trace view              | Dummy                       | Fully navigable UI with realistic sample data; no live agent execution.                                                      |
| Framework picker                             | Dummy                       | Selection is stored on the project record (functional-adjacent); no real scaffolding runs.                                   |
| Code editor / file tree / terminal           | Dummy                       | Real editor component (e.g., Monaco) with sample files; terminal shows scripted output, not a live shell.                    |
| GitHub connection                            | Dummy                       | Simulated OAuth screen and repo picker; no live GitHub API calls.                                                            |
| Deployment                                   | Dummy                       | Realistic progress and logs UI; ends in a fabricated live URL, not real hosting.                                             |
| Invite / handoff                             | Dummy                       | Invite UI and generated summary are real UI, simulated email/notification.                                                   |
| Notifications                                | Dummy                       | Generated from the same event log used for Project History; no real push/email delivery.                                     |
| Tips & discovery                             | Dummy                       | Scripted tip content and triggers (e.g., after first build); no personalization or real usage-based logic yet.               |
| Billing                                      | Dummy                       | Plan selection UI only; no payment processor integrated.                                                                     |

# 8. End-to-End Flow Map

The full loop, at a glance, before the screen-by-screen detail in Section 9. Both personas pass through the same numbered spine; where a step forks by persona, both branches are shown.

1. Homepage → Sign up or Log in (email or Google)
2. First-time only: Mode selection ("I want to build without code" / "I'm a developer")
3. Dashboard (project list, empty state for new accounts)
4. New Project → choose Prompt (build new) or Import (bring existing)
5. Plan review — storyboard (Simple View) or architecture doc (Code View) — user approves or edits
6. UI getting built — live build-progress visualization
7. Workspace opens — Canvas (Simple View) or IDE (Code View), toggle always visible; Chat window and App preview are shared surfaces inside both
8. Iterate — chat/visual edits (Simple) or direct file edits/chat (Code); Agent section available in both
9. Connect GitHub (optional at this point, required before Deploy in Code View)
10. Deploy — one-click (Simple) or environment-configured (Code)
11. Live app confirmation screen with shareable URL
12. Back to Dashboard — project now shows status, URL, and an Invite action for handoff

# 9. Detailed Flows & Screen Specifications

Each subsection below lists the screen's purpose, its key UI elements, and the step-by-step flow. Differences between Simple View and Code View are called out explicitly; where a flow is identical for both, it is written once.

## 9.0 Feature Coverage Map

Direct mapping from the required feature list to where each is specified below, plus the additional surfaces this document adds beyond that list.

| **#** | **Required feature**                  | **Covered in**                                                                                              |
|--------|---------------------------------------|-------------------------------------------------------------------------------------------------------------|
| 01     | Authentication                        | 9.2 Authentication & Sign-In (incl. Google)                                                                 |
| 02     | Homepage                              | 9.1 Homepage                                                                                                |
| 03     | Chat window                           | 9.9 Chat Window                                                                                             |
| 04     | App preview                           | 9.10 App Preview                                                                                            |
| 05     | Agent section                         | 9.12 Agent Building in Any Framework                                                                        |
| 06     | UI getting built                      | 9.7 UI Getting Built (Build Progress)                                                                       |
| 07     | GitHub integration                    | 9.13 GitHub Connection                                                                                      |
| 08     | Deploying the app                     | 9.14 Deployment                                                                                             |
| +     | Additional (not in the original list) | 9.15 Invite & Handoff · 9.16 Settings & Account · 9.17 Additional Platform Features · 9.18 Tips & Discovery |

## 9.1 Homepage [Dummy content, real routing]

### Screen: Homepage

- Hero: large prompt box ("What do you want to build?") with rotating example prompts as placeholder text, spanning both audiences (e.g. "A support agent that answers order questions" / "Import my repo and add a billing agent").

- Secondary row of example prompt chips, clickable to pre-fill the hero box.

- "How it works" strip: three icons — Prompt, Build, Deploy — each with one line of copy, shared language for both audiences.

- A small, secondary "For developers" link/section: one line ("Bring your own repo. Real files, real git, real terminal.") linking straight into the Code View entry point — this is the one place the homepage explicitly signals technical capability, so a developer landing on the page doesn't assume it's a beginner-only tool and bounce.

- Top nav: Log in, Sign up. Footer: standard links (not detailed here).

### Behaviour: prompt continuity for logged-out users

- If a logged-out visitor types a prompt and submits, the text is held in session storage and the user is routed into Sign up; on successful account creation they land directly in Plan Review (9.5) with that prompt already submitted, not back at a blank homepage. This one continuity rule is what keeps the homepage prompt box from feeling like a decoy.

### Flow

1. Visitor lands on Homepage, either types a prompt or clicks Sign up/Log in directly.
2. If a prompt was typed: submit → routed to Sign up with the prompt held.
3. Completes Authentication (9.2) → resumes directly into Plan Review with the prompt intact.

## 9.2 Authentication & Sign-In [Functional — email and Google]

### Screen: Sign up

- Primary fields: name, email, password (real validation and hashing).

- "Continue with Google" button, equally prominent — real OAuth 2.0 / OpenID Connect in this phase, not simulated.

- On email submit: account row created in the database (auth_provider = email), session issued, redirect to Mode Selection (or resumed prompt, per 9.1).

- On Google click: standard Google consent screen → on approval, Architect matches an existing account by verified email or creates a new one (auth_provider = google, name/avatar populated from the Google profile) → session issued identically to the email path → same redirect.

### Screen: Log in

- Email + password, or "Continue with Google"; "Forgot password" link is present but dummy (no real email sent in this phase).

- Returning users skip Mode Selection and land directly on the Dashboard, in whichever View mode they last used.

### Edge case: account linking

- If a user signs up with Google using an email that already has a password-based account, Architect signs them into the existing account rather than creating a duplicate — surfaced as a one-line notice ("Signed in with your existing account").

### Flow — email

1. Homepage/nav → Sign up.
2. Fills form, submits → account and session created in the real database.
3. Redirected to Mode Selection (first-time only) or resumed prompt (9.1).

### Flow — Google

1. Homepage/nav → Sign up or Log in → Continue with Google.
2. Google consent screen → approve.
3. Account matched or created, session issued → same redirect as the email path.

## 9.3 Mode Selection [Functional preference, first onboarding step]

This is deliberately the very first thing a new account sees — before the Dashboard, before any project exists. The answer shapes every screen that follows, so it can't be a buried settings toggle discovered later.

### Screen: "How do you want to work?"

- Two large cards, shown immediately after account creation: "I'm not a developer — build without code" (Simple View default) and "I'm a developer" (Code View default), each with a one-line description and a small illustrative screenshot of what that person's screen will look like.

- Footer note: "You can switch anytime — this just sets your starting point." This is important: the choice must never feel like a locked-in account type.

- Selection is stored on the account record (Functional) as a default_view preference, not a hard permission.

### Behaviour: what changes immediately after choosing

- Selects "Build without code": lands on a Dashboard styled for Simple View — the empty-state prompt box is front and center, no repo/framework language anywhere. The first project created opens straight into Canvas View (9.8).

- Selects "I'm a developer": lands on a Dashboard with an "Import from GitHub" quick action pinned alongside "+ New Project," and the Framework picker is visible by default when starting a new project. The first project created opens straight into IDE View (9.11).

- Both paths keep the Simple View / Code View toggle visible in the top bar regardless of the answer — this screen only sets which one opens first, it never removes the other.

### Flow

1. Account created (9.2) → Mode Selection shown automatically, before the Dashboard.
2. User picks one of the two cards.
3. Choice saved to the account (Functional) → Dashboard renders in the matching mode, and the first new project opens directly into the matching workspace.

## 9.4 Dashboard [Functional data, dummy content]

### Screen: Project list

- Empty state (new account): centered "+ New Project" card with the same prompt box as the Homepage.

- Populated state: grid of project cards — name, thumbnail/preview, status pill (Draft / Building / Live), last-edited time, and quick actions (Open, Invite, Deploy status).

- Top-right: account menu, View mode toggle (sets default for new projects), "+ New Project" button.

- Project list itself reads/writes to the real database — creating, renaming, and deleting projects works end-to-end even though what's inside a project is simulated.

## 9.5 New Project — Prompt to Build (Simple View)

### Screen: Prompt intake

- Single large text box with example prompts as placeholders. Submit triggers a short clarifying-questions exchange in the Chat Window (9.9), e.g. "What should happen when it can't answer a question?" — answers are canned follow-ups keyed to the prompt, not a real reasoning model.

### Screen: Plan review (storyboard)

- A vertical storyboard: 3–5 cards, each a plain-language step ("Understands the customer's question" → "Looks up the order" → "Replies or escalates"), plus a rough preview thumbnail.

- Buttons: "Looks good, build it" / "Let me adjust something" (reopens chat to amend the plan).

### Flow

1. Dashboard → + New Project → Prompt to Build.
2. Enter prompt → answer 1–2 clarifying questions.
3. Review storyboard plan → approve → proceeds to UI Getting Built (9.7).

## 9.6 New Project — Prompt / Import (Code View)

### Screen: Project setup

- Three entry options as equal tabs: "Prompt", "Import from GitHub", "Blank repository".

- Prompt tab: same text box as Simple View, plus a visible Framework picker (LangGraph / CrewAI / OpenAI Agents SDK / Claude Agent SDK / MCP-only / Auto-detect) and a deployment target dropdown (shown but not required yet).

### Screen: Plan review (architecture doc)

- Rendered as an editable document: agent list, each agent's tools, data flow between them, and the file structure that will be generated — shown as markdown/YAML the user can edit inline before generating.

### Screen: Import from GitHub

- "Connect GitHub" → simulated OAuth consent screen → simulated repo picker → "Import" → proceeds into UI Getting Built (9.7) in its indexing form.

### Flow

1. Dashboard → + New Project → Code View is already active for this persona.
2. Choose Prompt, Import, or Blank.
3. (Prompt) Set framework → review architecture doc → generate. / (Import) Connect → pick repo.
4. Proceeds to UI Getting Built (9.7).

## 9.7 UI Getting Built — the Build Progress Experience [Dummy]

Called out as its own surface because it is the moment a user is asked to trust the platform before seeing any result — the difference between a spinner and a visibly assembling product is most of the perceived quality of a vibe-coding tool.

### Screen: Build progress — Simple View

- The App Preview pane (9.10) is visible throughout and fills in progressively — a header appears, then a hero section, then supporting content — rather than staying blank until a single "done" moment.

- A persistent step list beside it: Plan → Scaffold → Style → Connect → Test → Ready, each with a checkmark as it completes, plus one line of current activity ("Designing the interface…").

- Deliberately no fake percentage counter — a step list that visibly advances is more trustworthy than a progress bar that stalls at 90%.

### Screen: Build progress — Code View

- Split view: left panel streams scripted log lines like a CI build ("Installing dependencies… Scaffolding agent graph… Running smoke test…"); right panel is the file tree, with each file highlighting briefly as it "completes."

- Same six-stage step list as Simple View, shown as a slim strip above the split view so both audiences share one mental model of progress.

### Error state (dummy)

- A rare simulated "hit a snag" state — one step shown with a warning icon, a one-line explanation, and a Retry button — included specifically so the platform has a defined failure UX rather than only ever demoing the happy path.

### Flow

1. Plan approved (9.5 or 9.6) → Build Progress screen opens automatically.
2. Steps advance over ~8–12 seconds; preview/file tree fill in alongside.
3. "Ready" step completes → auto-transition into the Workspace (9.8 or 9.11).

## 9.8 Workspace — Canvas View (Simple View)

### Layout

- Center: App Preview (9.10).

- Right: Chat Window (9.9) for prompt-driven changes.

- Left (collapsible): "How it works" — the plain-language Agent Section (9.12) flow diagram.

- Top bar: project name, Simple View / Code View toggle, Publish button, Invite button.

### Feature: Visual edits

1. Click any element in the preview.
2. A small floating toolbar appears: text, color, spacing controls.
3. Change is applied instantly to the preview (dummy) and logged as a new entry in Project History.

## 9.9 Chat Window [Dummy — shared component across both views]

One underlying component, skinned differently per view, so the interaction model for "describe a change" is consistent everywhere in the product.

### Screen elements

- Message list: user prompts right-aligned; Architect's replies left-aligned, each with a short "what I did" summary in Simple View ("Added a settings screen and linked it from the menu").

- Persistent input box with an attach/screenshot button — a screenshot or hand-drawn mockup can be dropped in and referenced in the next prompt, mirroring the screenshot-to-UI pattern from tools like v0.

- Regenerate and stop-generating controls on the most recent response.

- Inline suggestion chips after a response ("Make it more casual," "Add a settings page") to reduce blank-box hesitation.

- Collapse/expand toggle so the panel doesn't have to dominate the workspace once a project is underway.

### States

- Idle, generating (typing-indicator), error ("That didn't work — want me to try a different approach?"), and empty (first-open, shows 3 example prompts relevant to the project's category).

### Code View difference

- Same component, labeled "Composer." Each response's "what I did" summary is replaced with a file-level diff summary ("Changed 3 files, +42/-11") that expands into the actual diff in the editor (9.11), rather than a plain-language description.

## 9.10 App Preview [Dummy]

The live-feeling rendering of the product being built — the main surface in Simple View, a secondary pane in Code View.

### Screen elements

- Device-width toggle: mobile / tablet / desktop.

- Refresh button and a "view source for this screen" link — lets a Simple View user peek at the underlying structure without leaving Simple View or triggering a full mode switch.

- Code View adds a console/log tab beside the preview, for inspecting simulated runtime output (console logs, simulated network calls).

**Behaviour**

- Every accepted change — visual edit, chat-driven edit, or direct file edit — updates the preview with a brief highlight/flash on the changed region, so the user always sees exactly what moved, not just that something did.

## 9.11 Workspace — IDE View (Code View)

### Layout

- Classic three-pane layout: file tree (left), editor with tabs (center), terminal (bottom, collapsible).

- Right-side dockable panel: Chat Window/Composer (9.9), Agent Trace (9.12), and Git (diffs, branch, commit). App Preview (9.10) opens as an additional pane.

- Top bar: project name, Simple View / Code View toggle, branch selector, Deploy button, Invite button.

- Command palette (Cmd/Ctrl+K) for jump-to-file and common actions — included specifically because its absence is the fastest way to lose a technical evaluator.

### Feature: File tree & editor

- Real code editor component (e.g., Monaco) loaded with a realistic sample file structure generated from the plan (or imported repo); syntax highlighting and multi-tab editing work; saved edits persist for the session (dummy — not compiled or executed).

### Feature: Terminal

- Scripted terminal: a fixed set of commands (npm install, npm run dev, git status, etc.) return realistic canned output; free-form commands return a friendly "not available in this preview" message rather than an error.

## 9.12 Agent Building in Any Framework (Agent Section)

### Screen: Framework picker

- Available at project creation (9.6) and later from Project Settings → Framework. Options: LangGraph, CrewAI, OpenAI Agents SDK, Claude Agent SDK, MCP-only (no framework), Auto-detect (on import).

- Choosing a framework changes the sample file structure shown in the IDE (e.g., a LangGraph project shows a graph.py with node/edge definitions; a CrewAI project shows agents.yaml and tasks.yaml) — dummy but framework-accurate content, so it reads as credible to a developer.

### Screen: Agent Trace / Debug view

- A timeline of steps for a sample run: each row shows the agent, the tool called, the input, and the output, expandable for full detail — modelled on the trace views developers already expect from LangSmith-style tooling.

- Present in both views, but only surfaced by default in Code View; reachable from Simple View via "See what happened" on any preview interaction, kept collapsed by default.

## 9.13 GitHub Connection [Dummy]

### Screen: Connect

- Entry points: Project Settings → Integrations, auto-prompted the first time a Simple View user hits Publish, or required before Deploy in Code View.

- "Connect GitHub" → simulated consent screen → simulated account picker → simulated repo picker (create new / select existing).

**Behaviour after connecting**

- Simple View: sync is invisible — every meaningful change appears in Project History with a generated commit-style message, no git terminology surfaced.

- Code View: a real Git panel — branch selector, staged/unstaged diff, commit message field, simulated "Push" updating a visible commit log and a fabricated PR link.

## 9.14 Deployment [Dummy]

### Screen: Deploy — Simple View

- Single "Publish" button in the top bar → progress animation ("Packaging your app… Going live…") → confirmation card with a fabricated live URL and a Copy Link / Share button.

### Screen: Deploy — Code View

- "Deploy" opens a panel: environment choice (Preview / Staging / Production), a review of the commit being deployed, and a Deploy button.

- Progress view shows scripted build logs ("Installing dependencies… Building… Running health check… Deployed."), ending in a live-URL confirmation plus Rollback pointing at the previous (fabricated) deployment.

### Screen: Deployment history

- A list of past deployments (sample data) with timestamp, environment, status, and a Rollback action — present in both views, more prominent in Code View.

## 9.15 Invite & Handoff [Dummy UI, real project association]

### Screen: Invite

- "Invite" button (top bar, both views) opens a modal: email field, role (Can edit / Can view), and an auto-generated one-paragraph plain-language summary of what the project does and how it's structured.

- Sending an invite creates a real project-collaborator record in the database (Functional) even though email delivery is simulated.

### Screen: Invitee landing

- A developer invited into a Simple View project lands directly in Code View with a one-time "Welcome — here's what you're joining" panel: architecture summary, a suggested first file to read, and a dismissible IDE tour.

### Screen: Scoped access

- An engineer can right-click a single agent node in the flow diagram → "Share this agent for editing" → generates a scoped Simple View link that opens only that agent's plain-language instruction panel.

## 9.16 Settings & Account [Mixed]

- Profile & account: name, email, password change, and "Manage connected accounts" (shows Google if linked; a user cannot remove their only sign-in method) — Functional.

- Billing & plan: plan comparison cards, "Upgrade" button — Dummy, no payment processor.

- Integrations: GitHub connection status (9.13), API key placeholders for model providers — Dummy, keys stored as opaque placeholders, not validated.

- Default view preference: Simple View / Code View — Functional, read by the Dashboard and every new project.

## 9.17 Additional Platform Features [beyond the required list]

Surfaces a platform like this needs even though they weren't named explicitly — included per the brief's instruction to think holistically rather than stop at the given list.

- Notifications — toast + bell icon with a short list (build finished, deploy live, teammate joined); Dummy, generated from the same event log used for Project History.

- Command palette / global search — Cmd/Ctrl+K in both views: searches projects and recent prompts in Simple View, full file/action search in Code View.

- Empty & error states — explicitly defined for every list-type screen (Dashboard, Deployment history, GitHub repo picker), since an undefined empty state is where demos visibly break.

- Environment variables & secrets — a Settings panel for API keys/secrets used by agent tools, masked by default; editable in Code View, shown as read-only "Connected" status in Simple View.

- Custom domain for deployment — Code View only, an input plus a simulated DNS verification step under the Deployment panel.

- Help & first-run guidance — a dismissible tour on first entry to each major surface, plus a persistent "?" affordance opening contextual help.

- Feedback affordance — a lightweight "This didn't do what I expected" link on every generation/edit result, feeding the same event log — groundwork for improving generation quality later even though this phase doesn't act on it.

## 9.18 Tips & Discovery — Surfacing Code View to Non-Technical Users [Dummy]

Mode Selection (9.3) only sets a starting point, not a ceiling — but a non-technical user who never sees an obvious reason to open Code View will never discover it's there. This feature exists specifically to close that gap, without turning into an intrusive forced tour.

### Screen elements

- A lightbulb "Tips" icon in the top bar, present in both views, that shows a small badge when an unseen tip is available.

- A first-run tip card, anchored near the Simple View / Code View toggle, that appears automatically a short while after a non-technical user's first successful build: "Curious how this is built? Click here to peek at the real code." with two actions — "Show me" and "Maybe later."

- A Tips panel (opened from the lightbulb icon) listing a short set of contextual tips relevant to the user's current screen — e.g. "Drag an element in the preview to reposition it," "Invite a developer anytime from the top bar," "Switch to Code View to see the real files" — each dismissible individually.

- A "Don't show tips" toggle in Settings (9.16) for users who want the system off entirely.

### Flow — discovering Code View

1. Non-technical user completes their first build (9.7) and lands in Canvas View (9.8).
2. After a short delay (or on a later visit), the first-run tip card appears near the View toggle, introducing Code View by name.
3. "Show me" → the project switches live into Code View and opens the same one-time "Welcome — here's what you're in" panel used for invited developers (9.15), so the switch lands as an orientation rather than a confusing drop into a file tree.
4. "Maybe later" → the card dismisses and the same tip remains available from the Tips panel for whenever the user is ready.

# 10. Technical Notes for the Functional Slice

This section is intentionally light — per scope, no implementation happens in this phase. It records only the shape of the pieces committed to as Functional, so the build phase has a starting point.

**Authentication —** email/password with hashed credentials and a server-side session, plus Google Sign-In via OAuth 2.0 / OpenID Connect. Google accounts are matched to an existing user by verified email or create a new one; both paths issue the same session type.

**Database —** a real relational store (e.g., Postgres) holding accounts (with auth_provider), sessions, projects, project-collaborators, and a history/event log per project — this is the data the Dashboard, Invite flow, Notifications, and Project History screens genuinely read and write.

**Everything else —** front-end state only. Dummy flows use realistic, category-matched sample content (keyed off the user's prompt or chosen framework) rather than generic lorem-ipsum placeholders, so the prototype reads as credible in a walkthrough.

# 11. Success Metrics (for this phase)

- A reviewer can complete the full loop — sign up (email or Google) → build (or import) → connect GitHub → deploy → see a live URL — without hitting a dead end, in both Simple and Code View.

- Every item on the required feature list (Section 9.0) has a walkable, screen-level spec, not just a mention.

- A technical reviewer, on seeing Code View for the first time, does not ask "where's the file tree / terminal / diff view" — i.e., the IDE view reads as credible against Cursor at a glance.

- A non-technical reviewer never has to see git, YAML, or a terminal unless they explicitly opt into Code View.

- The Simple View ↔ Code View toggle and the Invite/handoff flow remain the two moments that most clearly demonstrate the "one project, two front doors" thesis in a live walkthrough.

# 12. Risks & Open Questions

- Risk: dummy flows that feel dummy undercut the pitch faster than missing features would — sample content must be category-matched to the user's actual prompt, not generic.

- Risk: if Code View is visibly a thinner experience than Simple View, technical credibility is lost immediately — the command palette and real diff view (9.11) are non-negotiable, not stretch items.

- Risk: adding Google Sign-In as a second functional auth path doubles the surface area of the one piece of the prototype that must not break — account-linking edge cases (9.2) need explicit test coverage even at prototype stage.

- Open question: should Mode Selection (9.3) be skippable entirely, defaulting new accounts to Simple View, to keep the fastest path to "wow" for the majority non-technical audience?

- Open question: which framework (9.12) should be the default for prompt-built projects where the user never opens the picker — this choice quietly shapes every generated sample file structure.

# 13. Appendix — Glossary

| **Term**    | **Meaning in this document**                                                         |
|-------------|--------------------------------------------------------------------------------------|
| Simple View | The non-technical canvas experience — live preview, chat, plain-language agent flow. |
| Code View   | The developer IDE experience — file tree, editor, terminal, git.                     |
| Agent graph | The set of agents, their tools, and the flow between them that makes up a project.   |
| Functional  | Backed by real logic and real data in this phase.                                    |
| Dummy       | UI-complete and navigable, backed by simulated/canned data in this phase.            |
| Handoff     | The designed moment a project moves from one persona's primary view to the other's.  |
