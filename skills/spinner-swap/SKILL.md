---
name: spinner-swap
description: Replace Claude Code spinner verbs with a custom list. User provides verbs; skill writes them to ~/.claude/settings.json with mode "replace". Invoke when user says "swap my spinners", "replace spinner verbs", "update my spinner", or gives you a list of verbs to use as spinners.
---

# Spinner Swap

Replace the default Claude Code spinner verbs with whatever you want.

**Announce at start:** "Using spinner-swap to replace your spinner verbs."

## What This Does

Claude Code shows a rotating verb while it thinks — "Thinking...", "Analyzing...", etc. You can replace all of them. This skill swaps the full list. Your verbs. No defaults bleeding through.

## Step 1: Get the Verbs

If the user already provided a list in their message, use it. Skip asking.

If no list was provided, ask:

> "Drop your verb list. One per line or comma-separated — both work."

Accept any format:
- One per line
- Comma-separated
- Quoted or unquoted
- With or without trailing punctuation

Strip quotes, commas, periods, ellipses. Capitalize first letter of each verb. Result: clean array of strings.

## Step 2: Confirm

Show the parsed list before writing:

```
Swapping to:
- Thrashing
- Moshing
- Shredding
[...]

Write these? (yes/no)
```

Wait for yes. Don't write without confirmation.

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

## Step 4: Confirm

```
Done. X verbs loaded. Spinner runs your list only.
Takes effect next session.
```

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

**Only one verb:** Valid. Write it. Claude Code handles a list of one.

## What Not to Touch

- Don't change `mode` to `"append"` — replace is the point
- Don't add verbs the user didn't provide
- Don't reformat the rest of settings.json
- Don't strip existing keys
