# Medium Pre-Publish Checklist

> A Claude Skill that runs a repeatable, 7-part editorial pass on a Medium.com draft — title, keywords, SEO title, meta description, hero image prompt, grammar pass, and content review — and hands back an interactive checklist.

[Read the write-up on Medium](https://stevesohcot.medium.com/how-a-claude-skill-ends-my-medium-publish-day-delays-be8f8d44eeaa)

## What it does

Paste in a finished Medium draft, and this skill acts as a skeptical editor rather than a cheerleader: it produces 3+ title candidates (with an honest strength/risk read on each), 10 ranked keyword candidates, 3 SEO-title variations, 2 meta-description options, a ready-to-paste hero-image-generation prompt, a grammar/spelling pass (before → after, no style rewrites), and a content review that checks factual claims and structural flow. It gives recommendations, (not automatic edits). The final step packages everything into an interactive HTML checklist you can open and check off.

## Example

**Prompt:**
> `/medium-pre-publish-checklist` [pasted draft text or a link to the published article]

**What happens:**
Claude returns all seven sections as text (title options, keywords, SEO title, meta description, hero image prompt, grammar corrections, content review), then generates a standalone HTML checklist file summarizing each section, ready to open and check off while you make final edits. Note: checklist progress isn't saved between sessions - it's a one-time working copy, not a persistent tracker.

## Installation

> **Important:** This skill needs both `SKILL.md` *and* `assets/checklist-template.html` to work. The final step (the interactive checklist) reads that template file directly — if only `SKILL.md` gets uploaded/copied on its own, the text checklist will still generate, but the final interactive HTML file will fail. Make sure your install method carries the whole folder, not just the one file.

### Claude.ai / Claude Desktop / Claude Cowork
1. Download the **entire folder** — `SKILL.md` and the `assets/` folder together — from the [`medium-pre-publish-checklist` folder](https://github.com/stevesohcot/claude-skills/tree/main/medium-pre-publish-checklist) of this repo, or download a packaged `.skill` file from [Releases](https://github.com/stevesohcot/claude-skills/releases) if provided.
2. [Steps to upload/install — e.g., Settings → Capabilities → Skills → Upload skill]
3. After installing, confirm `assets/checklist-template.html` shows up alongside `SKILL.md` in the skill's files before relying on it.

### Claude Code
1. Clone the monorepo, then copy or symlink this skill's folder into your skills directory:
   ```bash
   git clone https://github.com/stevesohcot/claude-skills.git
   cp -r claude-skills/medium-pre-publish-checklist ~/.claude/skills/
   ```
2. No additional setup or dependencies required — just make sure `assets/` came along with the copy.

## Repository structure

This skill lives inside the [`claude-skills`](https://github.com/stevesohcot/claude-skills) monorepo, alongside other Claude Skills:

```
claude-skills/
├── README.md                          # Index of all skills in this repo
├── LICENSE                            # MIT license, applies to the whole repo
└── medium-pre-publish-checklist/
    ├── SKILL.md                       # Skill instructions (7-part checklist logic, triggering rule)
    ├── assets/
    │   └── checklist-template.html    # HTML template Claude fills in and hands back as the final interactive checklist
    └── README.md                      # This file
```

## Requirements

None — works out of the box. For draft URLs, note that unpublished/gated Medium draft links usually can't be fetched (they sit behind your login session); paste the draft text directly in that case. Publicly published Medium URLs fetch normally.

## Usage notes

- **Trigger is explicit only** — this skill runs *only* when your message contains the literal command `/medium-pre-publish-checklist`. It won't infer intent from a Medium-related question asked normally.
- Input is either pasted/uploaded draft text or a URL to the draft, following the command.

## Limitations

- Doesn't have real keyword search-volume data — keyword ranking is Claude's best-effort judgment (backed by a web search when a term's popularity is unclear), not analytics.
- Can't generate the hero image itself — it produces a prompt for you to paste into an image generator.
- Only fixes clear grammar/spelling errors; it won't rewrite your voice or style.
- Checklist progress doesn't persist after you close the file.

## Changelog / Version

- **v1.0.0** — 8/28/26 — Initial release

## License

MIT — see [LICENSE](../LICENSE)

TL;DR: I'm not a lawyer, but basically go wild, just don't erase my name from it 🙂

## More

Read the full write-up on Medium: [https://stevesohcot.medium.com/how-a-claude-skill-ends-my-medium-publish-day-delays-be8f8d44eeaa](https://stevesohcot.medium.com/how-a-claude-skill-ends-my-medium-publish-day-delays-be8f8d44eeaa)

---

Feedback, issues, and pull requests welcome.
