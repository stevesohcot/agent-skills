---
name: medium-pre-publish-checklist
description: Runs a seven-part Medium.com pre-publish checklist — title, keywords, SEO-friendly title, meta description/subtitle, hero image prompt, grammar/spelling pass, and content review (angle, accuracy, structure). Final output will be an interactive checklist. Trigger only on the literal command "/medium-pre-publish-checklist".
---

# Medium Pre-Publish Checklist

A repeatable pre-publish checklist for Medium.com blog posts, run on demand via an explicit command. Given a finished draft, produce seven deliverables in a single pass, in a consistent format every time:

1. Title
2. Keywords
3. SEO-Friendly Title
4. Meta Description (Subtitle)
5. Hero Image Prompt
6. Grammar / Spelling Pass
7. Content (angle, accuracy, structure)

This skill produces recommendations, not automatic edits; the author applies the ones they agree with.

## When to run this

Trigger exclusively when the person's message contains the literal command `/medium-pre-publish-checklist`. Do not infer intent to run this skill from context or tone. If someone describes a Medium-related task without the command, just help normally without invoking this skill.

## Input

The command is followed by one of:
- **Pasted or uploaded article text** (plain text, Markdown, or a file).
- **A URL to the draft** — fetch it with Claude's web fetch tool. Note: Medium draft/unpublished-story links are normally gated behind the author's login session, so an unauthenticated fetch will often fail, redirect to a login page, or return a paywall stub rather than the real content. If the fetch doesn't clearly return the article body, say so plainly and ask the person to paste the draft text instead of guessing at content from a partial or blocked fetch. Published, publicly accessible Medium URLs should fetch normally.

If neither text nor a URL is present after the command, ask for the draft; don't invent one.

## The 7 Deliverables

Produce the deliverables in order.

Deliverable 3 depends on Deliverables 1 and 2; Deliverable 4 depends on Deliverable 2.

### 1. Title
This deliverable only produces the title and the reasoning for it (ex. upfront hook or subject identification).

First, check the draft's Title by looking at the first line. Is it:
- **A genuine title** — a specific, deliberate title the author wrote, whether or not it's formatted differently from the body (quoted, marked "Title:", a heading, or just a clearly title-shaped first line). If found, include it as an extra row in the candidates table below, labeled "Author's original" — evaluated with the same Strength/Risk criteria as the generated candidates, so it's weighed fairly in the recommendation rather than skipped past.
- **A placeholder** — generic non-title text like "Untitled," "[Title Here]," or "Draft Title," or a genuine attempt that's too thin to count as a real title (e.g. just a few vague words). Treat this the same as no title at all; don't add it to the final table of candidate titles.
- **Missing** — the draft just starts with body text, no separate title line. Proceed with only the generated candidates.

Act as a skeptical, experienced editor and headline writer — don't just generate titles that sound good; find the article's actual strongest hook first. Briefly identify, and show this reasoning before the candidates:
- Core subject, or main takeaway
- Most surprising/interesting aspect, or strongest potential headline hook

Generate one title candidate for each angle that genuinely fits the article — skip any angle the article doesn't support rather than stretching it, but generate **at least 3 candidates**; if fewer than 3 angles genuinely fit, use judgment to adapt the closest-fitting remaining angles rather than shipping fewer than 3:
- Curiosity-driven
- Benefit-driven
- Problem/solution
- How-to
- Straightforward/SEO-focused — specific and search-friendly, front-loading the article's core topic rather than being clever
- Narrative/case-study — e.g. "I built X, here's what I learned"; fits pieces recounting something the author built or a problem that was solved

Constraints for every candidate:
- Avoid generic, clickbait, sensational, or AI-sounding titles. A title can be curious and compelling enough to make someone want to click, but that appeal has to come from an honest, accurate hook — one that hints at what the article delivers without overselling it.
- 100 characters max, 40–50 preferred (Medium truncates longer titles in feed/social previews).

Present the candidates as a table: **Candidate | Strength | Risk** — one honest line each, no numeric scores. Then recommend the best one, in one or two sentences that clearly follow from its strength/risk notes above, not a separate judgment call. If every candidate is genuinely weak, say so plainly — "this is the best of a bad set" is a legitimate recommendation. Note that Deliverable 7 (Content) is where a different-angle flag for the article itself belongs.

### 2. Keywords
"Keywords" here means keywords, topics, and reader interests interchangeably; whatever terms capture what the article is actually about and who would search for it.

**Generate 10 candidates**, based on the draft content. Do not guess based on what's popular and related to this topic and don't pad with generic terms the article doesn't support.

Rank them from most to least useful, based on two things:
- How central the term is to the article
- A rough guess at how often people actually search for it

Claude doesn't have real keyword-volume data, so the "how often people search for it" part is just a best guess — general knowledge is usually enough, but do a quick web search if a term's popularity genuinely isn't clear.

Put the term that's both most central to the article and likely to get searched at #1. From there:
- Mix broad and narrower terms as you go down the list; don't cluster the broad ones at the top and dump the narrow ones at the bottom.
- List all 10 in order, **marking the top 5 as recommended**.

### 3. SEO-Friendly Title
- This is used in place of the Title on search engine results pages (e.g. Google). It's a distinct field from the Title above, not necessarily a duplicate of it.
- Using the winning candidate from Deliverable 1 as the basis, create 3 variations built around the #1-ranked keyword from Deliverable 2 (optionally pairing it with another of the top-5 keywords, but only pair a second keyword in if it reads naturally).
- Each variation should:
  - Be genuinely different from the other two, not just reworded. At least one should lead with the #1-ranked keyword; the others can lead with a different keyword or the article's core value.
  - Accurately reflect what the article actually delivers, not just the keyword(s) it's built around.
- **Maximum 60 characters**, but **40–50 characters is preferred**.
- Present the 3 variations as a list, each with the character count shown.

### 4. Meta Description (Subtitle)

- **Detect the current Subtitle:**
  - **A genuine subtitle** — a specific, deliberate one-line summary the author wrote. If found, include it as an extra option below, labeled "Author's original," evaluated the same way as the generated options.
  - **A placeholder or generic subtitle** (e.g. "Subtitle here," or just repeating the title) — treat this the same as no subtitle; don't include it.
  - **Missing** — proceed with only the generated options.

- This is used in place of the article's Subtitle on search engine results pages. **Maximum 140 characters**, including spaces. Count them explicitly and show the count.
- Should summarize the article's core value, not just restate the title.
- Utilize keywords in the description; include the #1-ranked keyword from Deliverable 2 as part of the summary, phrased naturally rather than stuffed in.
- Accurately reflect what the article actually delivers, not just the keyword(s) it's built around.
- Present 2 generated options as a list (plus the author's original above, if found). Make the generated options genuinely different from each other, not just reworded — e.g. one leading with the article's core value, one leading with what problem it solves or who it's for.

### 5. Hero Image Prompt
At the time of writing, Claude is unable to generate an image. Instead, produce a **ready-to-use image generation prompt**: a single paste-able paragraph (for ChatGPT, Midjourney, DALL·E, Ideogram, etc.).

The prompt should specify:
- The subject/composition — a specific visual scene or metaphor drawn from the article's actual central concept, not a literal restatement of the text
- Compose it as a wide, landscape-oriented image; suited for a horizontal header banner (not square or portrait).
- Style/mood inferred from the article's own tone (e.g. minimalist/technical, warm/narrative, bold/editorial). Don't default to any fixed palette or brand.
- An explicit instruction to avoid rendering readable text in the image, since image generators are not reliable in printing text

The prompt paragraph must begin with this exact lead-in sentence, followed by a colon: "You are writing a blog article. Given the paragraph below, create an image:" After the colon, in the same paragraph, add in the prompt.

Keep the visual-description portion (everything after the colon) to roughly 2–4 sentences so the whole prompt stays paste-friendly.

Also supply 3 search terms to use for a user to search stock photos, labeled as "Fallback Search Terms". Pull them from what's actually depicted or discussed in the article, not generic category words.

### 6. Grammar / Spelling Pass
- Go through the draft and list corrections as **before → after** pairs with a one-phrase reason (typo, subject-verb agreement, comma splice, etc.), grouped in the order they appear.
- Don't rewrite style or voice — only fix actual errors. If a sentence is awkward but not wrong, leave it and don't flag it as an "error."

### 7. Content

**Different angle flag:** if the article would benefit from a different angle to make the title, or the piece as a whole, substantially stronger, mention it here.

**Accuracy check:**
- Identify every checkable factual claim in the draft (statistics, dates, named tools/products/versions, attributed quotes, historical claims, etc). If the draft makes no checkable factual claims (pure opinion/narrative piece), say so explicitly rather than forcing findings.
- For each claim:
  - If checking it needs up-to-date info (a stat, a version number, something recent), look it up instead of guessing from memory.
  - Indicate if it's right, questionable, or wrong.
  - Explain why in plain terms.
  - Don't fix it yourself — flag it and let the author decide, since they know what they actually meant to say.
- Present findings as a table: **Claim | Status | Reasoning**.

**Structure & flow:**
- Read the piece as a whole and flag structural issues separate from grammar (line-level correctness, covered in Deliverable 6) and from accuracy (fact-level correctness, covered above). This checks whether the piece reads well overall.
- Check for: a weak or missing hook in the opening, an unclear or missing takeaway/conclusion, sections that drag or feel repetitive, and points that seem out of order or disconnected from the piece's main idea.
- Present findings as a short list of specific issues (quote or point to the section in question), each with a one-line suggestion. If the structure/flow are solid, say so plainly rather than inventing issues to fill the section.

## Final Output

Present all seven sections with clear headers, in the order above, so the format is identical every time. Always show the character count for the SEO-Friendly Title and the Meta Description.

After presenting the seven sections as text, always produce the accompanying interactive checklist as the last step.

1. Copy `assets/checklist-template.html` to a writable location (e.g. `/home/claude/`).
2. Edit the copy with `str_replace`:
   - Fill in `SEED_NOTES` with the actual generated content for each section — the winning title option, the top 5 recommended keywords, the winning SEO-Friendly Title option (with its character count noted), the Meta Description (with its character count noted), the hero image prompt and the 3 Fallback Search Terms, a summary of the grammar/spelling corrections suggested, and a summary of the Content section (the different-angle possibility, a summary of the accuracy-check findings, and a summary of the structure/flow findings). Escape quotes/newlines for a JS string (`\n` for line breaks, `\"` for double quotes, or switch that field to backticks if the content itself contains double quotes).
3. Save the edited file to `/mnt/user-data/outputs/<slug>-checklist.html`.
4. Call `present_files` on it so it renders as a file the author can open and check off.

The checklist doesn't save progress — checks and edits only last for the current viewing session. Mention this briefly so the author doesn't expect it to persist after they close it.
