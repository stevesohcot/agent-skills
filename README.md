# agent-skills

> A collection of [Agent Skills](https://agentskills.io) I've built — reusable, repeatable workflows for AI agents to run on demand. Agent Skills are an open format supported by both [Anthropic (Claude)](https://github.com/anthropics/skills) and [OpenAI (Codex)](https://github.com/openai/skills).

## Skills

| Skill | What it does |
|---|---|
| [`better-question`](./better-question) | Coaches you on a draft prompt without answering it — points out what's missing, fills the gaps with stated assumptions, and hands back an improved, ready-to-use prompt. |
| [`medium-pre-publish-checklist`](./medium-pre-publish-checklist) | Runs a 7-part editorial pass on a Medium draft — title, keywords, SEO title, meta description, hero image prompt, grammar pass, and content review — and hands back an interactive checklist. |

*More skills will be added here as they're built.*

## Installation

Each skill has its own folder containing:

- `SKILL.md` — the instructions the agent reads
- `README.md` — usage, examples, and limitations

To install a skill:

- **Chat apps (Claude, ChatGPT):** download the skill's folder as a .zip and upload it under your agent's skills settings.
- **CLI agents (Claude Code, Codex):** copy the folder into your agent's skills directory, e.g. `skills/<skill-name>/SKILL.md`.

Check each skill's README for anything specific to it.

## About

I write about building these (and other dev projects) on [Medium](https://stevesohcot.medium.com) and at [SteveSohcot.com](https://stevesohcot.com).

## License

MIT — see [LICENSE](./LICENSE). Applies to all skills in this repo unless a skill's own folder says otherwise.
