# claude-skills

> A collection of [Claude Skills](https://github.com/anthropics/skills) I've built — reusable, repeatable workflows for Claude to run on demand.

## Skills

| Skill | What it does |
|---|---|
| [`medium-pre-publish-checklist`](./medium-pre-publish-checklist) | Runs a 7-part editorial pass on a Medium draft — title, keywords, SEO title, meta description, hero image prompt, grammar pass, and content review — and hands back an interactive checklist. |

*More skills will be added here as they're built.*

## Using these skills

Each skill lives in its own folder with a `SKILL.md` (the instructions Claude reads) and its own `README.md` (usage details, examples, and limitations for humans browsing this repo). See the individual skill's README for install steps specific to it.

General install pattern:

```bash
git clone https://github.com/stevesohcot/claude-skills.git
cp -r claude-skills/<skill-name> ~/.claude/skills/    # Claude Code
```

For Claude.ai / Claude Desktop / Claude Cowork, download the specific skill's folder (or a packaged `.skill` file, if provided) and upload it via Settings → Capabilities → Skills.

## About

I write about building these (and other dev projects) on [Medium](https://stevesohcot.medium.com) and at [SteveSohcot.com](https://stevesohcot.com).

## License

MIT — see [LICENSE](./LICENSE). Applies to all skills in this repo unless a skill's own folder says otherwise.
