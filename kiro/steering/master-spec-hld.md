---
inclusion: auto
---

# Master Spec / HLD Steering

This project uses a **Master Spec (HLD)** pattern. All individual specs in `.kiro/specs/` contribute to a single high-level design document located at `.kiro/master-spec/HLD.md`.

## Rules

1. The HLD is a **living document** — it must always reflect the current state of all delivered specs.
2. When a spec is completed or significantly updated, the HLD should be regenerated or updated to incorporate those changes.
3. The HLD captures the **what and why** at a solution level — not implementation details. Think architecture, component relationships, data flows, integration points, and key decisions.
4. Individual specs remain the source of truth for detailed task-level work. The HLD is the aggregated view.
5. The HLD should include:
   - Solution overview / purpose
   - Architecture and component map
   - Key design decisions and rationale
   - Data model summary
   - Integration points and external dependencies
   - Cross-cutting concerns (auth, logging, error handling, etc.)
   - Spec inventory with status
6. When reviewing an existing repo for an HLD-like document, check common locations: `docs/`, `design/`, `architecture/`, `HLD.md`, `DESIGN.md`, `ARCHITECTURE.md`, and the root `README.md`.

## File References

The HLD may reference individual specs using Kiro's file reference syntax:
- `#[[file:.kiro/specs/<spec-folder>/requirements.md]]`
- `#[[file:.kiro/specs/<spec-folder>/design.md]]`
