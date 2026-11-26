# Better Question

> An Agent Skill that acts as a prompt coach: give it a draft prompt, and it points out what's missing, fills the gaps with reasonable assumptions, and hands back an improved prompt that's ready to use. It does *not* answer the original question.

## What it does

Paste in a prompt you're about to send to an AI, and this skill reviews it and suggests improvements. It returns up to four short points about what would make the prompt stronger (missing context, unclear goals, missing constraints, etc.). Instead of making you answer those questions first, it then makes a reasonable assumption for each gap and lists them, so you can see exactly what it guessed. Finally, it writes an improved, self-contained version of your prompt in a copy-ready code block. If your prompt is already clear, it says so instead of inventing issues.

## Example

**Prompt:**
> Invoke the `better-question` skill, followed by the prompt you want to improve, e.g. `where should I go on vacation?`
>
> (How you invoke a skill depends on your tool — e.g. `/better-question where should I go on vacation?` in Claude, or your tool's skill picker / mention syntax.)

**What happens:**
The agent returns questions/issues, assumptions, and the improved prompt.

```
- What time of year are you planning to travel?
- Is there a region or country you have in mind, or are you open to anywhere?
- What kind of trip do you want: beaches, cities, outdoors, food, relaxation?
- Who's going, and is there a budget or trip length to work within?

ASSUMPTIONS FOR PROMPT IMPROVEMENT:
- Traveling in winter and looking for warm weather
- Open to anywhere in the US
- A relaxed one-week trip for two on a moderate budget

IMPROVED PROMPT SUGGESTION:
I'm planning a relaxing one-week vacation for two this winter and want somewhere
warm, ideally with beaches. We'd like to stay in the US and have a moderate
budget. Which destinations would you recommend, and why?
```

From there you can correct an assumption or answer a question (it returns an updated prompt), or send the improved prompt / ask it to go ahead, and it answers normally.

## Installation

> **Only `SKILL.md` is needed.** The skill is a single instruction file, so there's no need to download the whole folder. The other files are optional extras (icons and tool-specific config). Codex users may also want `agents/openai.yaml`; see [Usage notes](#usage-notes).

1. Download [`SKILL.md`](https://github.com/stevesohcot/agent-skills/blob/main/better-question/SKILL.md)
2. Upload / Install - may vary based on your AI Agent, but something like Settings >> Capabilities or Plugins >> Skills >> Upload skill, or, for CLI-based agents, put it in a `better-question/` folder inside your agent's skills directory (e.g. `skills/better-question/SKILL.md`)

(If your tool only accepts a .zip upload, zip a `better-question/` folder containing `SKILL.md`.)

## Repository structure

This skill lives inside the [`agent-skills`](https://github.com/stevesohcot/agent-skills) monorepo, alongside other Agent Skills:

```
agent-skills/
├── README.md                  # Index of all skills in this repo
├── LICENSE                    # MIT license, applies to the whole repo
└── better-question/
    ├── SKILL.md               # Skill instructions
    ├── .claude-plugin/
    │   └── plugin.json        # Claude plugin manifest
    ├── agents/
    │   └── openai.yaml        # Codex config
    ├── assets/
    │   ├── icon-small.svg     # Small icon (referenced by agents/openai.yaml)
    │   └── icon-large.png     # Large icon (referenced by agents/openai.yaml and .claude-plugin/plugin.json)
    └── README.md              # This file
```

## Requirements

No extra setup. It's a single instruction file with no scripts, templates, or web access, so it works in any assistant that supports Agent Skills.

## Usage notes

- **Trigger is explicit only** — this skill runs *only* when you explicitly select or invoke it. Asking "can you improve this prompt?" in normal conversation won't trigger it. (Automatic invocation is disabled via `disable-model-invocation` in `SKILL.md` for Claude and `agents/openai.yaml` for Codex. If you install only `SKILL.md` in Codex, copy `agents/openai.yaml` too to keep this setting; otherwise it relies on the skill's description to stay explicit-only, which usually works but isn't guaranteed.)
- **Input** is the text you type after the skill name. If you don't include any, it uses a prompt you clearly point to earlier in the conversation (e.g. "the prompt above"), or asks you to paste one.
- **Add notes for better results** — anything you add *about* the prompt (who it's for, what you're trying to do) is used as context for its assumptions, not treated as part of the prompt.
- **Uses what it already knows** — assumptions are based on your notes first, then the conversation and project you're working in, then general guesses. Details pulled from the conversation are written into the improved prompt so it still works if you paste it somewhere else.
- **Matches your language and tone** — the feedback and improved prompt come back in the same language and style as your original.

## Limitations

- Assumptions are guesses. Always skim the `ASSUMPTIONS` list before using the improved prompt, and correct anything that's wrong.
- It improves the prompt only; it can't tell you whether the answer you eventually get is correct.
- Because the improved prompt is meant to be self-contained, it may include details from your conversation. Check it before pasting it into a different tool or sharing it.

## Changelog / Version

- **v1.0.0** — 11/25/26 — Initial release

## License

MIT — see [LICENSE](../LICENSE)

TL;DR: I'm not a lawyer, but basically go wild, just don't erase my name from it 🙂

---

Feedback, issues, and pull requests welcome.
