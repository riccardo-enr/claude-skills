---
name: keybindings-help
description: Configure Claude Code keyboard shortcuts. Use when the user wants to rebind keys, add chord shortcuts, change the submit key, customize keybindings, or modify ~/.claude/keybindings.json.
allowed-tools: Read, Edit
---

Help the user configure their Claude Code keybindings.

The config file lives at `~/.claude/keybindings.json`. Changes are picked up automatically without restart.

## File structure

```json
{
  "$schema": "https://www.schemastore.org/claude-code-keybindings.json",
  "$docs": "https://code.claude.com/docs/en/keybindings",
  "bindings": [
    {
      "context": "Chat",
      "bindings": {
        "ctrl+e": "chat:externalEditor",
        "ctrl+u": null
      }
    }
  ]
}
```

Set a key to `null` to unbind it. Reserved (cannot rebind): `Ctrl+C`, `Ctrl+D`.

## Contexts

`Global`, `Chat`, `Autocomplete`, `Confirmation`, `Transcript`, `HistorySearch`, `Task`, `ThemePicker`, `Tabs`, `Attachments`, `Footer`, `MessageSelector`, `DiffDialog`, `ModelPicker`, `Select`, `Plugin`, `Settings`, `Help`

## Key actions by context

**Global:** `app:interrupt` (Ctrl+C), `app:exit` (Ctrl+D), `app:toggleTodos` (Ctrl+T), `app:toggleTranscript` (Ctrl+O)

**Chat:** `chat:submit` (Enter), `chat:cancel` (Escape), `chat:cycleMode` (Shift+Tab), `chat:modelPicker` (Meta+P), `chat:thinkingToggle` (Meta+T), `chat:externalEditor` (Ctrl+G), `chat:stash` (Ctrl+S), `chat:undo` (Ctrl+_), `chat:imagePaste` (Ctrl+V), `chat:newline`

**Autocomplete:** `autocomplete:accept` (Tab), `autocomplete:dismiss` (Escape), `autocomplete:previous` (Up), `autocomplete:next` (Down)

**Confirmation:** `confirm:yes` (Y/Enter), `confirm:no` (N/Escape), `confirm:previous` (Up), `confirm:next` (Down), `confirm:nextField` (Tab), `confirm:cycleMode` (Shift+Tab), `confirm:toggleExplanation` (Ctrl+E), `permission:toggleDebug` (Ctrl+D)

**Transcript:** `transcript:toggleShowAll` (Ctrl+E), `transcript:exit` (Ctrl+C/Escape)

**HistorySearch:** `historySearch:next` (Ctrl+R), `historySearch:accept` (Escape/Tab), `historySearch:cancel` (Ctrl+C), `historySearch:execute` (Enter)

**Task:** `task:background` (Ctrl+B)

**Tabs:** `tabs:next` (Tab/Right), `tabs:previous` (Shift+Tab/Left)

**Select:** `select:next` (Down/J/Ctrl+N), `select:previous` (Up/K/Ctrl+P), `select:accept` (Enter), `select:cancel` (Escape)

**History:** `history:search` (Ctrl+R), `history:previous` (Up), `history:next` (Down)

## Keystroke syntax

- Modifiers: `ctrl`, `alt`/`opt`, `shift`, `meta`/`cmd`
- Chords (sequences): `ctrl+k ctrl+s` (press Ctrl+K then Ctrl+S)
- Uppercase implies Shift: `K` = `shift+k`
- Special keys: `escape`, `enter`, `tab`, `space`, `up`, `down`, `left`, `right`, `backspace`, `delete`

## Steps

1. Read `~/.claude/keybindings.json` if it exists (it may not yet)
2. Apply the user's requested changes, creating the file if needed
3. Confirm what was changed
