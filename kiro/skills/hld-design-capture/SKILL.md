---
name: HLD Design Capture
inclusion: auto
description: Analyze code changes and capture architecturally significant design decisions into the Master Spec HLD. Provides detection patterns for new components, integrations, data models, infrastructure, and cross-cutting concerns, plus drift detection between the HLD and actual codebase.
---

# HLD Design Capture Skill

Use this skill when you need to analyze code changes and capture design decisions in the Master Spec HLD. Activate it with `#hld-design-capture` in chat.

## When to Use

- After implementing a significant feature and wanting to ensure the HLD reflects it
- When reviewing a PR or set of changes for architectural impact
- When onboarding to a codebase and wanting to reverse-engineer the HLD from code
- When you suspect the HLD has drifted from the actual implementation

## Design Decision Detection Patterns

When analyzing code for HLD-relevant changes, look for these categories:

### 1. Structural Signals (New Components)
- New directories under `src/`, `lib/`, `app/` → likely a new module or service
- New files matching patterns: `*Controller*`, `*Service*`, `*Repository*`, `*Handler*`, `*Adapter*`, `*Gateway*`, `*Provider*`
- New `index.ts` / `__init__.py` / `mod.rs` files → module boundary
- New route definitions or API endpoint registrations

### 2. Integration Signals (External Dependencies)
- New HTTP client instantiations or API base URLs
- New database connection strings or ORM model definitions
- New message queue producers/consumers (SQS, SNS, Kafka, RabbitMQ)
- New SDK client initializations (AWS SDK, Stripe, Twilio, etc.)
- New webhook handlers or callback URLs
- New gRPC proto files or service definitions

### 3. Data Model Signals
- New migration files or schema definitions
- New ORM/ODM model classes
- New GraphQL type definitions
- New Protobuf or Avro schema files
- Significant changes to existing entity relationships

### 4. Infrastructure Signals
- New or modified Terraform resources
- New CDK constructs or CloudFormation resources
- New Docker services in compose files
- New Kubernetes manifests
- Changes to CI/CD pipeline configurations

### 5. Cross-Cutting Concern Signals
- New middleware registrations (auth, logging, rate limiting)
- New error handling patterns or custom error classes
- New logging/tracing/metrics instrumentation
- New environment variables or configuration schemas
- New security mechanisms (CORS, CSP, encryption)

## Capture Process

When capturing a design decision or architectural change:

1. **Identify the change category** from the signals above
2. **Read the current HLD** at `.kiro/master-spec/HLD.md`
3. **Check for existing coverage** — is this already documented?
4. **If new, determine the right HLD section:**
   - New service/module → Architecture & Components
   - New external dependency → Integration Points
   - New entity/schema → Data Model Summary
   - New pattern/approach → Key Design Decisions
   - New middleware/framework → Cross-Cutting Concerns
5. **Write a concise, architecture-level description** — not implementation details
6. **Include rationale** if discernible from code comments, commit messages, or PR descriptions
7. **Add source reference** — note the file path or spec that introduced it

## HLD Update Format

When adding to the HLD, follow these conventions:

For Key Design Decisions table:
```
| Decision description | Rationale (why this approach) | Spec or source reference |
```

For Integration Points table:
```
| Service/API name | Type (REST/gRPC/Queue/DB) | Brief description | Source reference |
```

For Architecture & Components, use bullet points:
```
- **Component Name** — What it does and its responsibility. (Source: path/to/file)
```

## Drift Detection

To check if the HLD has drifted from implementation:

1. List all major directories and entry points in the codebase
2. Compare against the Architecture & Components section
3. List all external client instantiations and SDK usages
4. Compare against Integration Points
5. List all model/entity definitions
6. Compare against Data Model Summary
7. Flag anything in code not in HLD (undocumented) or in HLD not in code (stale)
