# W3 Frame Agent Skills

Reusable instructions for AI coding agents. Each skill is a folder containing a `SKILL.md` and any resources it needs. The skills are designed to work across repositories without embedding a particular project's product decisions.

## Available skills

| Skill | Purpose |
| --- | --- |
| [feature-documentation](skills/feature-documentation/SKILL.md) | Create and maintain a product feature catalogue, user stories, and acceptance criteria. |

## Install in a project

Run from the root of the repository where you want to use the skill, with Node.js and npm installed:

```sh
npx skills add W3-Frame/agent-skills --skill feature-documentation
```

Choose your agent when prompted. Installation is project-scoped by default; use `-g` to install for your user instead. The repository is private, so your Git client must have access to W3-Frame/agent-skills. Review the CLI's proposed changes before confirming. See the [skills CLI documentation](https://github.com/vercel-labs/skills#readme) for agent selection, updates, and other options.

Alternatively, copy the entire `skills/feature-documentation` folder into the skill directory used by your agent. For Codex, use `.agents/skills/feature-documentation/` in the target project or `~/.agents/skills/feature-documentation/` for personal use. Copy the `references` folder as well. Restart the agent or start a new session if needed for discovery.

## Use

Ask the agent to document a product capability, or explicitly invoke `feature-documentation` using the syntax supported by your agent (for example, `$feature-documentation` in Codex). Provide the relevant product context and decisions; the skill does not infer them from its guide. Review the resulting specifications and unresolved decisions with the product owner.

## Maintaining this collection

Add each skill under `skills/<skill-name>/` with a `SKILL.md` containing a YAML `name` and `description`. Keep supporting material in the same folder so installations remain self-contained. Changes to shared guidance affect future installations; consumers should update their installed copy deliberately.

The feature guide is based on [Tandem's feature documentation guide](https://github.com/hermannleboss/Tandem/blob/develop/docs/features/GUIDE.md); access to that source requires permission. This repository maintains its own copy so the skill works independently of Tandem.
