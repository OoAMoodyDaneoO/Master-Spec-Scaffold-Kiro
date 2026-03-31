---
inclusion: auto
description: Steering rules for maintaining the Master Spec HLD as a living document. Covers update triggers from specs and code changes, architectural signal detection, and references to the HLD design capture skill and HLD maintainer agent.
---

# Master Spec / HLD Steering

This project uses a **Master Spec (HLD)** pattern. All individual specs in `.kiro/specs/` contribute to a single high-level design document located at `.kiro/master-spec/HLD.md`.

## Rules

1. The HLD is a **living document** — it must always reflect the current state of all delivered specs AND the actual codebase.
2. When a spec is completed or significantly updated, the HLD should be regenerated or updated to incorporate those changes.
3. When source code changes introduce new components, integrations, data models, or architectural patterns, the HLD should be updated even if no spec was involved.
4. The HLD captures the **what and why** at a solution level — not implementation details. Think architecture, component relationships, data flows, integration points, and key decisions.
5. Individual specs remain the source of truth for detailed task-level work. The HLD is the aggregated view.
6. The HLD should include:
   - Solution overview / purpose
   - Architecture and component map
   - Key design decisions and rationale
   - Data model summary
   - Integration points and external dependencies
   - Cross-cutting concerns (auth, logging, error handling, etc.)
   - Spec inventory with status
7. When reviewing an existing repo for an HLD-like document, check common locations: `docs/`, `design/`, `architecture/`, `HLD.md`, `DESIGN.md`, `ARCHITECTURE.md`, and the root `README.md`.
8. Be conservative with code-triggered updates — only update the HLD for genuinely significant architectural changes, not every code edit. Bug fixes, refactors, and formatting changes do not warrant HLD updates.

## Code Change Detection

The following code changes are architecturally significant and should trigger HLD updates:
- New services, controllers, handlers, adapters, or gateways → Architecture & Components
- New external API clients, database connections, message queues, or SDK usages → Integration Points
- New ORM models, migration files, or schema definitions → Data Model Summary
- New middleware, auth mechanisms, logging frameworks, or error handling patterns → Cross-Cutting Concerns
- New architectural patterns (event-driven, CQRS, microservices) → Key Design Decisions
- New infrastructure resources (Terraform, CDK, Docker, K8s) → Architecture & Components / Integration Points

## Tools

- Use the `#hld-design-capture` skill in chat for guided design decision capture from code
- Use the `hld-maintainer` sub-agent for full HLD audits, drift detection, and bulk updates
- Hooks automatically trigger on code file edits, creations, and deletions

## File References

The HLD may reference individual specs using Kiro's file reference syntax:
- `#[[file:.kiro/specs/<spec-folder>/requirements.md]]`
- `#[[file:.kiro/specs/<spec-folder>/design.md]]`
