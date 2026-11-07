---
name: claude-voice
description: Get Claude to write blog posts, social posts, newsletters and video scripts that sound exactly like you, not like AI slop. Learns real rules from your old writing, bans words you never use, drafts with a writer agent, checks with a tough editor agent that sends back only its top 3 fixes, and never guesses your opinion. Use when the user wants something written "in my voice", says Claude's writing sounds like AI, or wants to set up their voice.
---

# Claude Voice

Make Claude write like you. Method from Nat Eliason (x.com/nateliason/status/2115803497773904292).

Two agents: a **writer** that drafts and a **tough editor** that critiques. The writer never judges its own work.

## Step 1: Learn the voice from old writing (once)

If `voice/VOICE.md` doesn't exist yet, set it up first.

1. Ask the user for a few things they posted before, ideally written **without AI**: posts, threads, blog posts, scripts, emails. Save them in `voice/samples/`.
2. Pull **real rules** from them, not a vibe. "Be casual" is not a rule. Measure and quote:
   - How long their sentences and paragraphs are (average, and the range).
   - How they open, and how they end a post.
   - Words and phrases they use a lot, with real examples.
   - Contractions, questions, lists, emoji: how often.
3. Write it all into `voice/VOICE.md` using `templates/VOICE.md`. Every rule gets a real line from the samples as proof.

## Step 2: Ban words they never use

- Start the ban list with AI words: delve, seamless, crucial, robust, moreover, furthermore, additionally, testament, tapestry, leverage, elevate, game-changer, "in today's fast-paced world".
- Then search the samples for more: any word that shows up a lot in AI writing but **0 times** in their writing goes on the list.
- Never ban a word the user actually uses.
- Save the list in `voice/VOICE.md` under Ban list.

## Step 3: Talk it out, then draft

Don't start from a blank prompt. Get the raw material from the user first:
- A voice note transcript or rough bullet points about what happened ("we launched X, here's what went wrong, here's what I learned").
- Ask a few short questions if facts are missing.

Then the **writer agent** (a subagent given `voice/VOICE.md` and the raw material) writes the first draft:
- Follow VOICE.md. Never use a banned word.
- Every fact comes from the user's material. Nothing made up.
- **Never guess the user's opinion.** If the draft needs how they feel about something and they never said it, write `[ADD YOUR TAKE HERE: how do you feel about ___?]` and move on.

## Step 4: Tough editor, top 3 fixes only

The **editor agent** (a separate subagent given `voice/VOICE.md` and the draft) critiques it hard, but sends back **only its top 3 fixes**: the line, what's wrong, and which rule it breaks. No rewrite, no long list.

Why only 3: with a long list, an agent goes for whatever is easiest to fix and skips the hard, important parts.

Loop writer → editor for **up to 3 rounds**. Stop early if the editor has nothing important left.

Before showing the user anything, the editor writes down the **3 edits it predicts the user will make**. Save them in `voice/predictions.md`. Don't show them to the writer or the user yet.

## Step 5: The user adds their take, then a final pass

1. Show the draft with every `[ADD YOUR TAKE HERE]` blank marked.
2. The user fills in the blanks in their own words.
3. Writer does a final pass so the draft fits around their take. Their words stay as they wrote them.

## Step 6: Learn from their final edits

When the user makes their own final edits:
1. Compare their final version with your draft.
2. Compare their changes with `voice/predictions.md`. What did the editor predict? What did it miss?
3. Turn what they changed into new rules in `voice/VOICE.md`, marked `(new)`. A rule that only showed up once stays `(new)`; drop the tag once it shows up again.

Every time through, there should be less for the user to fix.

## Files

```
voice/
  samples/          old writing, ideally pre-AI
  VOICE.md          rules, ban list, learned rules
  predictions.md    the editor's predicted edits for the current piece
```
