# Medium Pre-Publish Checklist

> An Agent Skill that runs a repeatable, 7-part editorial pass on a Medium.com draft — title, keywords, SEO title, meta description, hero image prompt, grammar pass, and content review — and hands back an interactive checklist.

[Read the write-up on Medium](https://stevesohcot.medium.com/how-a-claude-skill-ends-my-medium-publish-day-delays-be8f8d44eeaa)

## What it does

Paste in a finished Medium draft, and this skill acts as a skeptical editor rather than a cheerleader: it produces 3+ title candidates (with an honest strength/risk read on each), 10 ranked keyword candidates, 3 SEO-title variations, 2 meta-description options, a ready-to-paste hero-image-generation prompt, a grammar/spelling pass (before → after, no style rewrites), and a content review that checks factual claims and structural flow. It gives recommendations (not automatic edits). The final step packages everything into an interactive HTML checklist you can open and check off.

## Example

**Prompt:**
> Invoke the `medium-pre-publish-checklist` skill, followed by [pasted draft text or a link to the published article]
>
> (How you invoke a skill depends on your tool — e.g. `/medium-pre-publish-checklist` in Claude, or your tool's skill picker / mention syntax.)

**What happens:**
The agent returns all seven sections as text (title options, keywords, SEO title, meta description, hero image prompt, grammar corrections, content review), then generates a standalone HTML checklist file summarizing each section, ready to open and check off while you make final edits. (If your assistant can't create files, it outputs the HTML in a code block for you to save instead.) Note: checklist progress isn't saved between sessions - it's a one-time working copy, not a persistent tracker.

## Installation

> **Important:** This skill needs both `SKILL.md` *and* `assets/checklist-template.html` to work. The final step (the interactive checklist) reads that template file directly — if only `SKILL.md` gets uploaded/copied on its own, the text checklist will still generate, but the final interactive HTML file will fail. Make sure your install method carries the whole folder, not just the one file.

1. Download the **entire folder** — `SKILL.md` and the `assets/` folder together — from the [`medium-pre-publish-checklist` folder](https://github.com/stevesohcot/agent-skills/tree/main/medium-pre-publish-checklist) as a .zip
2. Upload / Install - may vary based on your AI Agent, but something like Settings >> Capabilities or Plugins >> Skills >> Upload skill, or, for CLI-based agents, copy the folder into your agent's skills directory



## Repository structure

This skill lives inside the [`agent-skills`](https://github.com/stevesohcot/agent-skills) monorepo, alongside other Agent Skills:

```
agent-skills/
├── README.md                          # Index of all skills in this repo
├── LICENSE                            # MIT license, applies to the whole repo
└── medium-pre-publish-checklist/
    ├── SKILL.md                       # Skill instructions (7-part checklist logic, triggering rule)
    ├── .claude-plugin/
    │   └── plugin.json                # Claude plugin manifest
    ├── agents/
    │   └── openai.yaml                # Codex config
    ├── assets/
    │   ├── checklist-template.html    # HTML template the agent fills in and hands back as the final interactive checklist
    │   ├── icon-small.svg             # Small icon (referenced by agents/openai.yaml)
    │   └── icon-large.png             # Large icon (referenced by agents/openai.yaml and .claude-plugin/plugin.json)
    └── README.md                      # This file
```

## Requirements

No extra setup. Fetching a draft URL needs an assistant with web access, and the interactive checklist works best in an assistant that can create files (otherwise it prints the HTML in a code block for you to save). For draft URLs, note that unpublished/gated Medium draft links usually can't be fetched (they sit behind your login session); paste the draft text directly in that case. Publicly published Medium URLs fetch normally.

## Usage notes

- **Trigger is explicit only** — this skill runs *only* when you explicitly select or invoke it. It won't infer intent from a Medium-related question asked normally. (Automatic invocation is disabled via `disable-model-invocation` in `SKILL.md` for Claude and `agents/openai.yaml` for Codex.)
- Input is either pasted/uploaded draft text or a URL to the draft, provided along with the skill invocation.

## Limitations

- Doesn't have real keyword search-volume data — keyword ranking is the model's best-effort judgment (backed by a web search when a term's popularity is unclear, if your assistant has web search), not analytics.
- Produces a hero image *prompt*, not the image itself — paste it into your image generator of choice.
- Only fixes clear grammar/spelling errors; it won't rewrite your voice or style.
- Checklist progress doesn't persist after you close the file.

## Changelog / Version

- **v1.0.1** — 11/26/26 — Generic for more AI Assistants (ex. ChatGPT), minor updates
- **v1.0.0** — 8/28/26 — Initial release

## License

MIT — see [LICENSE](../LICENSE)

TL;DR: I'm not a lawyer, but basically go wild, just don't erase my name from it 🙂

## More

Read the full write-up on Medium: [https://stevesohcot.medium.com/how-a-claude-skill-ends-my-medium-publish-day-delays-be8f8d44eeaa](https://stevesohcot.medium.com/how-a-claude-skill-ends-my-medium-publish-day-delays-be8f8d44eeaa)

---

Feedback, issues, and pull requests welcome.
