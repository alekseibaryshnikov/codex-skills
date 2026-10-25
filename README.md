# Codex skills

Independent, reusable skills for designing, building, and testing software with Codex. Install the skills you need; each directory is a complete skill package.

## Skill catalog

| Skill | Purpose | Package |
| --- | --- | --- |
| `design-web-apps` | Design and build web apps with clear tasks, a distinctive visual identity, complete interactions, and responsive layouts. Includes usability, accessibility, performance, and visual review guidance. | [Instructions](skills/design-web-apps/SKILL.md) |
| `sdd-tdd` | Use source comments as maintained specification artifacts, document tests against acceptance criteria, and run observed red-to-green cycles before implementing behavior changes. | [Instructions](skills/sdd-tdd/SKILL.md) |

## Repository layout

```text
skills/
  design-web-apps/
    SKILL.md
    agents/
    assets/
    references/
  sdd-tdd/
    SKILL.md
    agents/
    references/
```

The repository root is a catalog, not a skill. Each skill lives under `skills/<skill-name>/` and owns its instructions, metadata, and supporting resources. Keep the entire directory together when installing it. The previous `design-web-apps/` package now lives at `skills/design-web-apps/`; use the new path for future installations. Existing installed copies are unaffected.

## Install one or several skills

Ask Codex with the Skill Installer available:

```text
Use $skill-installer to install these skills from
https://github.com/alekseibaryshnikov/codex-skills:
- skills/design-web-apps
- skills/sdd-tdd
```

Include only the paths you want. Install the individual skill directories, not the repository root. If a skill is already installed, inspect and update that existing copy deliberately rather than creating a second copy with the same name.

For repository-local use, copy the selected skill directories into that project's `.agents/skills/`. Merely cloning this collection does not activate its contents as project-local skills.

See the [official skill documentation](https://learn.chatgpt.com/docs/build-skills) for supported discovery locations, installation, and invocation in your host.

## Use the skills

After installation, invoke `$design-web-apps` or `$sdd-tdd` in Codex, or let the host select a skill when the request matches its description. Both packages allow implicit invocation. UI design work can use both: `design-web-apps` guides the product and interface, while `sdd-tdd` governs behavioral contracts, test documentation, and implementation order.

To require SDD/TDD across your projects without mentioning the skill in every request, add a standing instruction to the global `AGENTS.md` in your Codex home directory:

```text
For every feature, bug fix, or code refactor, automatically load and follow
the installed sdd-tdd skill before editing production code. If it isn't in
the initial skill list, read skills/sdd-tdd/SKILL.md relative to this global
AGENTS.md. Don't silently skip the workflow if the file is unavailable.
```

This is an agent instruction, not a CI gate. Project-specific instructions can override global guidance. Read the [AGENTS.md documentation](https://learn.chatgpt.com/docs/agent-configuration/agents-md) for discovery and precedence. Ordinary prose-only work does not require a TDD cycle.

## Add another skill

1. Create `skills/<skill-name>/SKILL.md` with `name` and `description` in YAML frontmatter. Use the same name for the directory and skill.
2. Add `agents/openai.yaml`, `references/`, `assets/`, or `scripts/` only when the skill needs them. Keep resource links relative to the owning skill so it remains independently installable.
3. Add the skill to the catalog above and review its trigger description for overlap with existing skills.
4. Validate the package with the Skill Creator's validator when available. Check local links and metadata, and run any executable examples or scripts. For workflow skills, test a realistic task and inspect actual actions; a final diff alone cannot establish test-first ordering.
