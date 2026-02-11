# SeeSaw 5D Process

This directory contains the SeeSaw 5D workflow - an AI-driven product development process that guides work through five phases: **Discover**, **Define**, **Design**, **Develop**, and **Delight**.

## Why 5Ds?

Building great products requires more than just writing code. It requires understanding the problem, aligning on what success looks like, designing thoughtful solutions, implementing with quality, and validating that we actually delivered value.

The 5D process ensures we do all of this consistently - whether the full team is collaborating live or an individual is working solo with AI teammates filling in the perspectives of their absent colleagues.

### The Five Phases

| Phase | Purpose | Key Question |
|-------|---------|--------------|
| **Discover** | Understand the problem before committing to a solution | What problem are we really solving and for whom? |
| **Define** | Convert the problem into clear, testable requirements | What does "done" look like? |
| **Design** | Shape the UX and technical approach before coding | How will we build this? |
| **Develop** | Implement with quality, tests, and reviewability | Does this meet our criteria? |
| **Delight** | Finalize for deploy and establish the feedback loop | How will we know it worked? |

## How It Works

### AI-Driven Collaboration

When working through an issue, the AI brings in perspectives from the product team:

- **Product Manager** - User value, business outcomes, scope, measurement
- **UI/UX Designer** - User experience, accessibility, states, content clarity
- **Lead Engineer** - Feasibility, architecture, testing, maintainability
- **Client SME** - Domain expertise, real-world validation

These voices surface naturally during work - asking questions, raising concerns, suggesting alternatives. This means a developer working at 2am still gets PM and Designer input, and a designer exploring flows still gets engineering feasibility checks.

### Artifacts Over Meetings

Each phase produces concrete artifacts that capture decisions, context, and rationale. This creates:

- **Shared understanding** - Everyone can see what was decided and why
- **Onboarding documentation** - New team members can read the history
- **Audit trail** - We can trace back why something was built a certain way
- **AI context** - Future AI sessions have the full picture

## Directory Structure
```
.ss5d/
├── README.md                 # This file
├── client-context.yaml       # Project-specific domain knowledge
├── personas/
│   ├── product-mgr.yaml      # Product Manager persona
│   ├── ui-ux-designer.yaml   # UI/UX Designer persona
│   ├── lead-engineer.yaml    # Lead Engineer persona
│   └── client-sme.yaml       # Client SME persona
├── phases/
│   ├── 01-discovery.yaml     # Discovery phase instructions
│   ├── 02-define.yaml        # Define phase instructions
│   ├── 03-design.yaml        # Design phase instructions
│   ├── 04-develop.yaml       # Develop phase instructions
│   └── 05-delight.yaml       # Delight phase instructions
└── artifacts/
    ├── _templates/           # Artifact templates
    │   ├── problem-brief.md
    │   ├── acceptance-criteria.md
    │   ├── decision-record-adr.md
    │   ├── ui-ux-design-notes.md
    │   ├── technical-design-notes.md
    │   ├── telemetry-plan.md
    │   ├── implementation-plan.md
    │   ├── release-notes.md
    │   └── feedback-summary.md
    └── <issue-id>/           # Issue-specific artifacts
        ├── state.yaml        # Workflow state
        └── ...               # Phase artifacts
```

## Getting Started

### For a New Team Member

1. **Read this README** - You're doing that now
2. **Review client-context.yaml** - Understand the project, client, and domain
3. **Skim the persona files** - See what each role cares about
4. **Skim the phase files** - Understand what happens at each stage

### Working on an Issue

1. Open the project in your AI-powered IDE (Claude Code, Cursor, etc.)
2. Start the workflow:
```
   ss5d start
```
3. The AI will ask for the issue ID and any context it needs
4. Work through each phase - the AI guides you and brings in persona perspectives
5. Artifacts are created in `.ss5d/artifacts/<issue-id>/`
6. At each phase completion, you'll get a ready-to-paste GitHub comment

### Checking Status

To see where you are on the current issue:
```
ss5d status
```

### Resuming Work

If you step away and come back later, just run `ss5d start` again. The AI reads the state file and picks up where you left off.

## The Artifacts

| Artifact | Created In | Purpose |
|----------|------------|---------|
| `problem-brief.md` | Discover | Articulates the problem, user, value, and scope |
| `acceptance-criteria.md` | Define | Testable statements defining "done" |
| `decision-record-adr.md` | Any phase | Log of decisions with context and rationale |
| `ui-ux-design-notes.md` | Design | UX flows, states, accessibility, interactions |
| `technical-design-notes.md` | Design | Architecture, testing strategy, observability |
| `telemetry-plan.md` | Design | Success metrics and usability signals |
| `implementation-plan.md` | Develop | Breakdown of implementation steps |
| `release-notes.md` | Develop → Delight | User-facing description of the change |
| `feedback-summary.md` | Delight | Framework for gathering and acting on feedback |

## Customizing for Your Project

### Client Context

Edit `client-context.yaml` to capture:
- Client and project information
- Domain terminology and concepts
- User types and stakeholders
- Business and technical constraints

This context informs the AI throughout the workflow.

### Personas

The persona files in `personas/` can be adjusted if your team has different concerns or communication styles. The structure is:
- `mission` - What this role is trying to achieve
- `concerns` - What they care about and push for
- `questions` - What they naturally ask at each phase
- `voice` - How they communicate

## Questions?

If something isn't working or doesn't make sense, reach out to the SeeSaw team or open an issue in this repository.
