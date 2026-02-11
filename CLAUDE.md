# SeeSaw 5D Workflow

This project uses the SeeSaw 5D process - an AI-driven product development workflow that guides work through five phases: Discover, Define, Design, Develop, and Delight.

## Quick Start

### Commands

- `ss5d start` - Start or resume the 5D workflow for an issue
- `ss5d status` - Show current state of the active issue
- `ss5d explore` - Start or continue an exploration experiment
- `ss5d promote` - Promote an experiment to production 5D workflow

### Example
```
ss5d start
```
```
ss5d explore
```

## How It Works

### Starting Work

When you invoke `ss5d start`:

1. Read `.ss5d/client-context.yaml` to understand the project and constraints
2. Read all persona files in `.ss5d/personas/`
3. Check if there's an active issue in progress
4. If resuming: Read the state file and existing artifacts, then pick up where you left off
5. If new: Read the current phase file, ask for issue ID and context, then begin Discovery

For new issues, I need at minimum:
- Issue ID
- Issue title
- Basic context on the problem and why we're solving it

I'll ask for anything I don't have before proceeding.

### Working Through a Phase

For each phase, I will:

1. Read available context (issue, codebase, client-context.yaml, existing artifacts)
2. Surface what I understand vs. what's unclear
3. Ask critical questions upfront
4. Draft the artifact(s) for this phase
5. Gather input from team personas (PM, Designer, Engineer, Client SME)
6. Refine based on feedback
7. Complete the phase with a summary and ready-to-paste GitHub comment

If context is clear and you want me to move faster, say **"just do it"** and I'll make reasonable assumptions and power through with minimal back-and-forth.

### Persona Collaboration

Throughout the workflow, I bring in perspectives from the product team:

- **Product Manager** - Focused on user value, business outcomes, scope, and measurement
- **UI/UX Designer** - Focused on user experience, accessibility, states, and content clarity
- **Lead Engineer** - Focused on feasibility, architecture, testing, and maintainability
- **Client SME** - Focused on domain expertise and real-world validation

These voices will surface naturally as we work - asking questions, raising concerns, suggesting alternatives. At the end of each phase, I'll do a structured checkpoint to ensure all perspectives have been heard.

### Phase Completion

When a phase is complete, I will:

1. Update the state file
2. Summarize what was produced
3. Provide a ready-to-paste comment for the GitHub issue
4. Indicate what's next

### The Five Phases

| Phase | Purpose | Key Output |
|-------|---------|------------|
| **Discover** | Understand the problem before committing to a solution | problem-brief.md |
| **Define** | Convert the problem into clear, testable requirements | acceptance-criteria.md |
| **Design** | Shape the UX and technical approach before coding | ui-ux-design-notes.md, technical-design-notes.md, telemetry-plan.md |
| **Develop** | Implement with quality, tests, and reviewability | implementation-plan.md, release-notes.md (draft) |
| **Delight** | Finalize for deploy and establish the feedback loop | release-notes.md (final), feedback-summary.md |

## Exploration Mode

For early-stage client discovery and rapid prototyping, use exploration mode instead of the full 5D process.

### When to Use Exploration

- Early client engagements with loose ideas
- Rapid prototyping to spark conversation
- Testing concepts before committing to production work
- When you need to move fast and the code is throwaway

### Starting Exploration

When you invoke `ss5d explore`:

1. Read `.ss5d/client-context.yaml` to understand the project
2. Read all persona files in `.ss5d/personas/` (for light-touch input)
3. Read `.ss5d/phases/00-explore.yaml` for exploration guidance
4. Ask what we're exploring and what we hope to learn
5. Build quickly, capture learnings, move on

### Exploration Artifacts

- **`.ss5d/exploration-log.md`** - Running log of all experiments
- **`/prototypes/`** - Throwaway prototype code (at repo root)

### Persona Involvement

Personas still chime in during exploration, but with a light touch:
- Quick questions to clarify intent
- Occasional reality checks
- Bias toward speed over rigor

### Building Prototypes

All prototype code lives in `/prototypes/` at the repo root. Each prototype gets its own subdirectory:
```
/prototypes/
  client-app/
  admin-app/
```

These are throwaway. Optimize for speed and learning, not quality.

### Documenting Experiments

After each experiment, document in `.ss5d/exploration-log.md`:
- What we tried
- What we learned
- Questions that emerged
- Links to assets

### Promoting to Production

When an experiment proves out and is worth building properly:
```
ss5d promote
```

I will:
1. Ask which experiment you're promoting
2. Ask for the GitHub issue ID
3. Create the artifact folder at `.ss5d/artifacts/<issue-id>/`
4. Create `state.yaml` with current phase set to `discovery`
5. Create a draft `problem-brief.md` seeded with learnings from the experiment

Then run `ss5d start` to continue with the full 5D Discovery phase, refining the draft with full persona input.

## File Structure
```
/
├── CLAUDE.md                 # This file (workflow instructions for Claude)
├── prototypes/               # Throwaway prototype code (exploration mode)
│   └── README.md
└── .ss5d/
    ├── README.md             # Workflow documentation for humans
    ├── client-context.yaml   # Project-specific domain knowledge
    ├── exploration-log.md    # Log of exploration experiments
    ├── personas/
    │   ├── product-mgr.yaml
    │   ├── ui-ux-designer.yaml
    │   ├── lead-engineer.yaml
    │   └── client-sme.yaml
    ├── phases/
    │   ├── 00-explore.yaml   # Exploration phase (lightweight)
    │   ├── 01-discovery.yaml
    │   ├── 02-define.yaml
    │   ├── 03-design.yaml
    │   ├── 04-develop.yaml
    │   └── 05-delight.yaml
    └── artifacts/
        ├── _templates/
        └── <issue-id>/
```

## Reading the Workflow Files

When working on an issue, I should read:

1. **Always**: `.ss5d/client-context.yaml`
2. **Always**: All persona files in `.ss5d/personas/`
3. **Always**: The current phase file (e.g., `.ss5d/phases/01-discovery.yaml`)
4. **If resuming**: `.ss5d/artifacts/<issue-id>/state.yaml` and existing artifacts
5. **As needed**: Relevant codebase files based on the issue

When exploring, I should read:

1. **Always**: `.ss5d/client-context.yaml`
2. **Always**: All persona files in `.ss5d/personas/` (for light-touch input)
3. **Always**: `.ss5d/phases/00-explore.yaml`
4. **Always**: `.ss5d/exploration-log.md` (to see prior experiments)
5. **As needed**: Existing prototype code in `/prototypes/`

## State Management

State is tracked per-issue at `.ss5d/artifacts/<issue-folder>/state.yaml`:
```yaml
issue:
  id: 42
  title: "Add version number to footer"
  url: "https://github.com/org/repo/issues/42"

current-phase: define

phases:
  discovery:
    status: complete
    completed-at: 2025-01-30T14:32:00Z
  define:
    status: in-progress
    started-at: 2025-01-31T09:15:00Z
  design:
    status: pending
  develop:
    status: pending
  delight:
    status: pending

artifacts:
  - problem-brief.md
  - acceptance-criteria.md

open-questions:
  - "Confirm with client: should version show build number or just semver?"
```

### State Values

- `pending` - Phase not yet started
- `in-progress` - Currently working on this phase
- `complete` - Phase finished, artifacts produced

## Creating Issue Folders

When starting a new issue, create the artifact folder:

1. Take the issue ID (e.g., `42`)
2. Combine as: `<id>` (e.g., `42`)
3. Create folder at: `.ss5d/artifacts/42/`
4. Initialize `state.yaml` with the issue info and `current-phase: discovery`

## GitHub Integration

After completing each phase, I'll provide a ready-to-paste comment for the GitHub issue that includes:

- Phase completed
- Summary of decisions/outputs
- Link to relevant artifacts
- Current status

This keeps the GitHub issue in sync with the workflow progress.
