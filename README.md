# Design Reference Adapter

A Pi skill for turning external design guidance into concise, repo-specific skills.

This repository does **not** define a design system. Instead, it provides an adaptation workflow for creating or updating local project skills from external design prompt libraries, design-system checklists, or UI-review procedures while preserving the target repository's own conventions.

## What it does

Use this skill when you want to:

- create a repo-specific design, frontend, or UI-review skill;
- adapt an external design prompt or design-system reference into a local Pi skill;
- refresh an existing local design skill from an upstream reference;
- compare local design skills against an external design reference.

Do **not** use it for ordinary UI implementation, polish passes, accessibility fixes, or component reviews. Those should use the target repo's local frontend/design/accessibility guidance instead.

## Repository contents

```txt
design-reference-adapter/
├── README.md      # Project overview and usage
├── SKILL.md       # Skill entrypoint and activation rules
└── REFERENCE.md   # Detailed adaptation workflow, guardrails, and templates
```

## Core principles

- **Local authority first**: repo-local guidance, design systems, docs, skills, and validation commands override external references.
- **External references are advisory**: extract reusable patterns; do not blindly import external instructions or prose.
- **Mode separation**: keep mockup workflows distinct from production implementation workflows.
- **Constraint separation**: distinguish brand-faithful work from divergent design exploration.
- **Calibrated review**: match critique strictness to user intent, artifact maturity, and promotion goal.
- **Rendered review when possible**: UI review skills should inspect screenshots, mockups, lab routes, or preview states, not source alone.
- **Promotion discipline**: classify artifacts as reference, mockup, lab prototype, or production candidate before implementation.
- **Maturity-scaled accessibility**: treat accessibility findings differently for references, mockups, lab prototypes, and production candidates.
- **Language discipline**: preserve product/domain naming and flag overconfident capability claims.
- **Concise generated skills**: adapt the smallest useful workflow, not a full generic design manual.

## Installation

Keep source skills in a generic agents directory, then symlink them into Pi's skills directory:

```sh
SKILL_NAME=design-reference-adapter
SOURCE_SKILL_DIR="$HOME/.agents/skills/$SKILL_NAME"
PI_SKILL_DIR="$HOME/.pi/agent/skills/$SKILL_NAME"

mkdir -p "$HOME/.agents/skills" "$HOME/.pi/agent/skills"
cp -R design-reference-adapter "$SOURCE_SKILL_DIR"
ln -sfnT "$SOURCE_SKILL_DIR" "$PI_SKILL_DIR"
```

If the skill already lives under `~/.agents/skills`, only run the symlink step:

```sh
SKILL_NAME=design-reference-adapter
ln -sfnT "$HOME/.agents/skills/$SKILL_NAME" "$HOME/.pi/agent/skills/$SKILL_NAME"
```

Copy or symlink it into a project's local skills directory instead if you want it scoped to a single repo.

## Usage

Ask an agent to create, adapt, refresh, or compare a repo-specific design skill. For example:

```txt
Use the design-reference-adapter skill to adapt this external design checklist into a local UI polish skill for this repo.
```

The skill will:

1. confirm the adaptation target;
2. inspect the target repository's local sources of truth;
3. fetch external references only when explicitly allowed;
4. translate useful patterns into repo-specific guidance;
5. produce a concise local skill or an implementation plan.

## Default external reference

If the user explicitly requests an external adaptation but does not provide a source, the skill uses:

```txt
https://github.com/Trystan-SA/claude-design-system-prompt
```

## Output expectations

Generated local skills should include:

- the target repo's stack and file conventions;
- local design-system and brand constraints;
- relevant domain terminology;
- mockup vs production rules where applicable;
- accessibility expectations;
- validation commands;
- provenance for materially adapted external references.

See [`REFERENCE.md`](REFERENCE.md) for the full workflow, gotchas, and suggested output templates.
