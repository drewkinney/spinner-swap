# Spinner Swap

Replace Claude Code's spinner verbs with anything you want.

By default Claude Code cycles through "Thinking...", "Analyzing...", "Processing..." while it works. Spinner Swap lets you replace all of them — your list, or a theme-generated one built from a vibe you describe. Full replace. No defaults bleeding through.

## Install

```
mkdir -p ~/.claude/skills/spinner-swap && curl -o ~/.claude/skills/spinner-swap/SKILL.md https://raw.githubusercontent.com/drewkinney/spinner-swap/main/SKILL.md
```

Restart Claude Code. Then use `/spinner-swap` or just tell Claude what you want.

## Use

- **"swap my spinners"** → paste your list, done
- **"give me punk verbs"** → Theme Mode, Claude asks a few questions and builds the list
- **"make it 1970s Italian horror"** → Theme Mode, same deal

## Two Modes

### Bring Your Own List

You have the verbs. Claude parses any format — one per line, comma-separated, quoted, messy — and writes them. Confirms before touching anything.

### Theme Mode

Name a vibe. Genre. Era. Activity. Aesthetic. Claude asks 2–3 clarifying questions to lock in the right register, then generates 12–15 present-participle verbs that fit. Not a dictionary lookup — something with texture.

You can ask for adjustments before it writes.

**Examples of theme done right:**

*Late-night diner cook:*
Griddling, Plating, Degreasing, Restocking, Wiping, Firing, Ringing, Sliding, Wrapping, Counting, Closing, Mopping

*1970s analog synthesizer:*
Patching, Oscillating, Drifting, Filtering, Gating, Sequencing, Modulating, Clipping, Sustaining, Releasing, Tuning, Cascading

*Competitive eating:*
Dunking, Inhaling, Cramming, Pacing, Sweating, Chewing, Timing, Surging, Bonking, Recovering, Finishing, Surviving

## How It Works

Writes `spinnerVerbs` to `~/.claude/settings.json` with `mode: "replace"`. Takes effect next session.

```json
"spinnerVerbs": {
  "mode": "replace",
  "verbs": ["Thrashing", "Moshing", "Shredding", "..."]
}
```

## License

MIT
