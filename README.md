# Kiro Master Spec / HLD Scaffold

A Kiro scaffold that maintains a **living High-Level Design (HLD)** document by aggregating all your individual specs into a single solution-level view.

---

## What This Does

Kiro treats specs as detailed, task-level documents (closer to an LLD). This scaffold adds the missing HLD layer — a single document at `.kiro/master-spec/HLD.md` that reflects your entire solution's architecture, design decisions, data models, and integration points by pulling from all your specs.

It works through three Kiro hooks, a steering file, and a skeleton HLD template.

---

## What's Included

```
.kiro/
├── steering/
│   └── master-spec-hld.md              # Always-on steering that teaches Kiro about the HLD pattern
├── hooks/
│   ├── generate-hld.kiro.hook          # Manual hook: generate/update HLD from all specs
│   ├── hld-on-spec-change.kiro.hook    # Auto hook: nudges HLD update when any spec is edited
│   └── discover-existing-hld.kiro.hook # Manual hook: find & migrate existing design docs
└── master-spec/
    └── HLD.md                          # The living HLD document (skeleton to start)
```

---

## Three Scenarios

### Scenario 1: Existing Project with Multiple Specs

You already have a Kiro project with specs in `.kiro/specs/` and want to create the HLD.

**Steps:**
1. Copy this scaffold's `.kiro/` contents into your project's `.kiro/` folder (merge, don't overwrite)
2. Open the Kiro Agent Hooks panel in the explorer sidebar (or use Command Palette → "Open Kiro Hook UI")
3. Find and trigger the **"Generate / Update HLD"** hook
4. Kiro will scan all your specs and produce a complete HLD at `.kiro/master-spec/HLD.md`
5. Review the generated HLD and make any manual additions or corrections
6. From now on, the **"HLD Update Reminder on Spec Change"** hook will automatically prompt Kiro to update the HLD whenever you edit a spec file

**That's it.** The HLD is now a living document that evolves with your specs.

### Scenario 2: New Project (Greenfield)

You're starting fresh and want the HLD pattern from day one.

**Steps:**
1. Copy this scaffold's `.kiro/` contents into your new project
2. The skeleton HLD at `.kiro/master-spec/HLD.md` is already in place with placeholder sections
3. Start creating specs normally using Kiro's spec workflow
4. Each time you complete or significantly update a spec, the auto-hook will prompt Kiro to update the HLD
5. You can also manually trigger **"Generate / Update HLD"** at any time to do a full refresh

**Tip:** When creating your first spec, mention in your prompt that the project uses the Master Spec pattern. The steering file will guide Kiro to keep the HLD in mind.

### Scenario 3: Existing Repo with Design Docs (e.g., from GitHub)

You have a repo that already contains architecture or design documentation somewhere (maybe `docs/ARCHITECTURE.md`, a detailed README, or scattered design files) and you want to consolidate it into the HLD format.

**Steps:**
1. Copy this scaffold's `.kiro/` contents into your repo
2. Open the Kiro Agent Hooks panel
3. Trigger the **"Discover Existing HLD"** hook
4. Kiro will search your repo for existing design documents in common locations:
   - `docs/`, `design/`, `architecture/` folders
   - Files named `HLD.md`, `DESIGN.md`, `ARCHITECTURE.md`, `SOLUTION.md`
   - README sections with architecture content
   - `.github/` folder and wiki references
5. If found, Kiro will migrate that content into `.kiro/master-spec/HLD.md` in the standard format
6. The original documents are preserved — nothing is deleted
7. If you also have specs in `.kiro/specs/`, those will be merged in too

---

## How the Hooks Work

| Hook | Trigger | What It Does |
|------|---------|--------------|
| **Generate / Update HLD** | Manual (you click it) | Full scan of all specs → generates or updates the HLD |
| **HLD Update Reminder on Spec Change** | Auto (on spec file edit) | Checks if the edit is significant enough to warrant an HLD update |
| **Discover Existing HLD** | Manual (you click it) | Searches repo for existing design docs and migrates them |

### Triggering Manual Hooks

Manual hooks appear in the **Agent Hooks** section of the Kiro explorer panel. Click the play/trigger button next to the hook name to run it.

Alternatively, use the Command Palette and search for "Open Kiro Hook UI".

---

## The HLD Structure

The generated HLD follows this standard structure:

1. **Solution Overview** — What the project does and why it exists
2. **Architecture & Components** — Major modules/services and their relationships
3. **Key Design Decisions** — Architectural choices and rationale (sourced from spec designs)
4. **Data Model Summary** — Aggregated entities and relationships
5. **Integration Points** — External APIs, databases, third-party services
6. **Cross-Cutting Concerns** — Auth, logging, error handling, security, performance
7. **Spec Inventory** — Table of all specs with status and summary

---

## Customization

### Steering

Edit `.kiro/steering/master-spec-hld.md` to adjust the rules Kiro follows when working with the HLD. For example, you could:
- Add project-specific sections to the HLD template
- Change the threshold for what counts as a "significant" spec change
- Add references to external design documents using `#[[file:path]]` syntax

### Hooks

Edit the `.kiro.hook` files in `.kiro/hooks/` to adjust prompts or behavior. The hook prompts are plain English — modify them to match your team's conventions. You can also manage hooks visually from the Agent Hooks panel in the Kiro explorer sidebar.

### HLD Template

Edit `.kiro/master-spec/HLD.md` directly to add sections, notes, or context that Kiro should preserve when regenerating. The generate hook is designed to update rather than replace, so manual additions are kept.

---

## Tips

- Run **"Generate / Update HLD"** after completing a batch of specs rather than after every small edit — the auto-hook handles incremental updates
- The HLD uses Kiro file references (`#[[file:...]]`) to link back to source specs — these work in Kiro's context system
- Commit the HLD to version control so your team can review it in PRs
- The HLD is intentionally high-level — if you need implementation details, that's what individual specs are for
