---
name: spinner-swap
description: Replace Claude Code spinner verbs with a custom list or a theme-generated list. Invoke when user says "swap my spinners", "replace spinner verbs", "update my spinner", gives a list of verbs, or names a theme ("give me punk verbs", "make it cooking", "generate a list").
---

# Spinner Swap

Replace the default Claude Code spinner verbs with whatever you want — your own list, or a theme-generated one.

**Announce at start:** "Using spinner-swap to replace your spinner verbs."

## What This Does

Claude Code cycles through a verb while it thinks — "Thinking...", "Analyzing...", etc. This skill replaces the full list. No defaults bleeding through.

---

## Mode Detection

Read the user's message. Pick one mode:

**Bring Your Own List** — user gave explicit verbs. Go to [Step 1A].

**Theme Mode** — user named a vibe, genre, aesthetic, activity, or said "random" / "generate" / "surprise me". Go to [Step 1B].

If unclear, ask: "Got a list, or want me to build one from a theme?"

---

## Step 1A: Bring Your Own List

User provided verbs. Parse them:

- Accept one per line, comma-separated, quoted or unquoted, with or without trailing punctuation
- Strip quotes, commas, periods, ellipses
- Capitalize first letter of each verb
- Result: clean array of strings

Skip to [Step 2].

---

## Step 1B: Theme Mode

Build a verb list that fits the user's world. This is a creative act. The verbs should feel like they belong — not a generic dictionary lookup, but something with a specific texture.

### Clarify First

Before generating, ask 2–3 focused questions to lock in the right register. Don't ask more than 3. Don't ask obvious things already stated.

Pick from these based on what's missing:

**Tone** — "Serious or playful? Aggressive, meditative, absurd?"

**Era / reference point** — "Any specific decade, scene, or cultural moment?"

**Specificity** — "Broad theme or a particular corner of it? (e.g. 'jazz' vs. 'late-night Blue Note sessions')"

**Intensity** — "Slow and deliberate, or fast and chaotic?"

**Length preference** — "How many verbs? (Default: 12–15)"

**Existing example** — "Drop one verb that's already perfect. I'll match it."

Only ask what matters for the theme. If the user said "1970s Italian horror film" you don't need to ask about era. Read what's there.

### Generate the List

After clarification, compile 12–15 verbs (or user's requested count) that:

- Are present-participle ("-ing") form — same grammar as "Thinking", "Analyzing"
- Fit the theme's specific register, not just the general category
- Have texture variation — not all the same syllable length or energy
- Would make someone smile (or wince) when they see them flash by

**Examples of theme done right:**

*Late-night diner cook:*
Griddling, Plating, Degreasing, Restocking, Wiping, Firing, Ringing, Sliding, Wrapping, Counting, Closing, Mopping

*1970s analog synthesizer:*
Patching, Oscillating, Drifting, Filtering, Gating, Sequencing, Modulating, Clipping, Sustaining, Releasing, Tuning, Cascading

*Competitive eating:*
Dunking, Inhaling, Cramming, Pacing, Sweating, Chewing, Timing, Surging, Bonking, Recovering, Finishing, Surviving

Don't explain the verbs. Don't justify the choices. Just present the list.

### Offer a Regenerate

After showing the list, add one line:

> "Want a different angle, or swap any of these out?"

If they want changes, adjust and re-present. Don't start the clarification questions over.

Skip to [Step 2].

---

## Step 2: Confirm

Show the parsed or generated list before writing:

```
Swapping to:
- Verb1
- Verb2
- Verb3
[...]

Write these? (yes/no)
```

Wait for yes. Don't write without confirmation.

---

## Step 3: Write to settings.json

Target file: `~/.claude/settings.json`

Read the current file. Find or create the `spinnerVerbs` key. Write:

```json
"spinnerVerbs": {
  "mode": "replace",
  "verbs": [
    "Verb1",
    "Verb2",
    "..."
  ]
}
```

Mode is always `"replace"` — this skill owns the spinner, it doesn't append to defaults.

Preserve all other keys in the file exactly. No reformatting. No touching anything else.

---

## Step 4: Confirm

```
Done. X verbs loaded. Spinner runs your list only.
Takes effect next session.
```

---

## Edge Cases

**Empty list after parsing:** Tell the user. Don't write an empty array.

**settings.json doesn't exist:** Create it with just the spinnerVerbs key:
```json
{
  "spinnerVerbs": {
    "mode": "replace",
    "verbs": ["..."]
  }
}
```

**Malformed settings.json:** Read, parse, report the error, stop. Don't overwrite a broken file.

**Only one verb:** Valid. Write it.

**User wants to keep some defaults:** Not supported. This skill replaces. If they want append behavior, tell them to set `mode: "append"` manually.

---

## What Not to Touch

- Don't change `mode` to `"append"` — replace is the point
- Don't add verbs the user didn't ask for (BYOL mode)
- Don't reformat the rest of settings.json
- Don't strip existing keys
- Don't explain verb choices unprompted
