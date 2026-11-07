# Claude Voice

A Claude skill that gets Claude to write like you, not like AI slop. Works for blog posts, social posts, newsletters and video scripts.

1. **Learns real rules** from your old writing: sentence length, how you open and end, words you use.
2. **Bans words you never use** (delve, seamless…), plus any word your writing never has.
3. **Two agents:** a writer drafts from your voice note or bullet points, and a tough editor critiques it.
4. **Top 3 fixes only**, up to 3 rounds. A long list makes the agent fix the easy stuff and skip what matters.
5. **Never guesses how you feel.** It leaves `[ADD YOUR TAKE HERE]` and you fill it in.
6. **Learns from your final edits**, so you fix less every time.

Method from Nat Eliason: https://x.com/nateliason/status/2115803497773904292

## Install

**Claude Code** (paste in your terminal):

```bash
git clone https://github.com/sullyo/claude-voice ~/.claude/skills/claude-voice
```

**Claude app (claude.ai / desktop):** click the green **Code** button → **Download ZIP**, then in Claude go to Settings → Capabilities → Skills → Upload skill.

## Use it

1. Tell Claude: **"set up my voice"** and paste a few things you wrote before AI.
2. Then: **"write a post about ___ in my voice"** and give it a voice note or bullet points.
3. Fill in the `[ADD YOUR TAKE HERE]` blanks.
4. Make your final edits and paste them back so Claude learns.
