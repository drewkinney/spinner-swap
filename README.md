# Spinner Swap

Replace Claude Code's spinner verbs with anything you want.

By default Claude Code cycles through "Thinking...", "Analyzing...", "Processing..." while it works. Spinner Swap lets you replace all of them — punk verbs, cooking verbs, your band's name repeated 13 times. Doesn't matter. Your list, full replace, no bleed-through from defaults.

## Install

```
claude plugin install drewkinney/spinner-swap
```

## Use

```
/spinner-swap
```

Or just tell Claude: "swap my spinners" and give it a list.

## How It Works

The skill reads your list, confirms it, then writes `spinnerVerbs` to `~/.claude/settings.json` with `mode: "replace"`. Takes effect next session.

## Example

```
Thrashing
Moshing  
Shredding
Distorting
Rebelling
Skanking
Stagediving
Fuzzing
Feedbacking
Cranking
Subverting
Disrupting
Resisting
```

## License

MIT
