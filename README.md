# W3 Frame Agent Skills

Reusable instructions for AI coding agents. Each skill is a folder containing a `SKILL.md` and any resources it needs. The skills are designed to work across repositories without embedding a particular project's product decisions.

## Available skills

| Skill | Purpose |
| --- | --- |
| [w3-feature-documentation](skills/w3-feature-documentation/SKILL.md) | Create and maintain a product feature catalogue, user stories, and acceptance criteria. |
| [w3-skill-improvement](skills/w3-skill-improvement/SKILL.md) | Propose actionable improvements to W3 Frame skills as GitHub issues. |

## Install in a project

Run from the root of the repository where you want to use the skill, with Node.js and npm installed:

```sh
npx skills add W3-Frame/agent-skills --skill w3-feature-documentation
```

Choose your agent when prompted. Installation is project-scoped by default; use `-g` to install for your user instead. The repository is private, so your Git client must have access to W3-Frame/agent-skills. Review the CLI's proposed changes before confirming. See the [skills CLI documentation](https://github.com/vercel-labs/skills#readme) for agent selection, updates, and other options.

Alternatively, copy the entire `skills/w3-feature-documentation` folder into the skill directory used by your agent. For Codex, use `.agents/skills/w3-feature-documentation/` in the target project or `~/.agents/skills/w3-feature-documentation/` for personal use. Copy the `references` folder as well. Restart the agent or start a new session if needed for discovery.

## Use

Ask the agent to document a product capability, or explicitly invoke `w3-feature-documentation` using the syntax supported by your agent (for example, `$w3-feature-documentation` in Codex). Provide the relevant product context and decisions; the skill does not infer them from its guide. Review the resulting specifications and unresolved decisions with the product owner.

Install `w3-skill-improvement` as well to help capture useful improvements discovered while using W3 Frame skills:

```sh
npx skills add W3-Frame/agent-skills --skill w3-skill-improvement
```

It searches for existing proposals and, when authorized, creates a sanitized issue in this repository. `w3-feature-documentation` invokes it when available and it discovers a concrete improvement. Skills do not run automatically on every agent action; install both skills in the same scope and agent for this workflow.

## Upgrading from the previous name

The skill was renamed from `feature-documentation` to `w3-feature-documentation`. Install the new name using the command above, then remove the old installation if you no longer need it:

```sh
# For a project installation, run from the project root.
npx skills remove feature-documentation

# For a global installation, use this instead.
npx skills remove feature-documentation -g
```

Review the removal prompt, especially if another source also provides a skill with the old name. If you copied the old folder manually, remove that copy manually instead. Restart the agent or start a new session after the change.

## Maintaining this collection

Prefix every skill name with `w3-` and add it under `skills/<skill-name>/` with a `SKILL.md` containing the matching YAML `name` and a `description`. For task-oriented skills, add a brief instruction to use `w3-skill-improvement` when available if using the skill reveals a concrete improvement, and to report the idea locally otherwise. Keep supporting material in the same folder so installations remain self-contained. Changes to shared guidance affect future installations; consumers should update their installed copy deliberately.

The feature guide is based on [Tandem's feature documentation guide](https://github.com/hermannleboss/Tandem/blob/develop/docs/features/GUIDE.md); access to that source requires permission. This repository maintains its own copy so the skill works independently of Tandem.
