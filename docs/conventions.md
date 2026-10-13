# Conventions for every mod in this family

These rules come from Anthropic's mods documentation and from how the built-in mods are
written. A pull request to any mod repo is checked against them.

## Files

- `.claude-plugin/plugin.json` (name, version, description, author, repository, license,
  keywords, `userConfig`, `types` when `$.state` is used) and
  `.claude-plugin/marketplace.json` (one plugin, `source: "./"`), so the repo installs on its own.
- `hooks/hooks.json` → `{ "modules": ["./register.ts"] }` (or `.tsx` when the tree is JSX).
- `hooks/register.ts` is the **only** file that touches `$`. Pure logic goes in small sibling
  files with one job each, and is unit-tested without the mods API.
- `tests/*.test.ts` with `claude-code/testing`; `docs/media/<mod>.gif`; `README.md`; `LICENSE` (MIT).

## Code

- TypeScript ES modules, no bundler, no `node_modules`. Only relative imports plus `claude-code`.
- Every mods API call written in full (`$.ui.open(...)`); `$` is passed only to top-level
  functions of `register.ts`. This is what lets `claude plugin validate` list every call.
- Names are lowercase and never start with `claude-`. Commands never collide with built-ins.
- State: module variables for throwaway values; `$.state` atoms for what a drawing depends
  on; `$.store` for settings and history. Reload after `/clear`, `/resume`, `/branch` via
  `classic.SessionStart`.
- A `tool.call` hook that can deny has a `.catch` that returns `{ deny }` when
  `next.called` is false. Guards fail closed.
- Never wait on a promise of your own for long: the hook budget is 10 s and a skipped guard
  lets the command through. Wait inside mods API calls (`$.ui.ask`, `$.process.run`) instead.
- Panes the mod opens by itself respect the 144-column rule; when `isPlaced` is false, show
  a toast. Read `e.props.bodyColumns` and truncate. Check `e.surface` before `Raster`/`Image`.
- No `$.http`. No telemetry of our own.

## Look

- Header line in every pane: `◆ <name>` bold, then dim facts separated by ` · `.
- One accent color per mod, used only for what is live. Everything else is default or dim.
- Glyphs: `●` running/high, `✓` done, `✗` failed, `○` idle/medium, `◌` pending.
- Buttons: `plain: true` with a visible hotkey; the safe choice first.
- The band above the prompt is one line, no border, and keeps other mods' content as a sibling.
- Empty states say what will happen; never a blank pane.

## Quality gates

```bash
claude plugin validate --strict .
claude plugin test .
claude --plugin-dir .        # try it in a real session, terminal and Desktop app
```

README sections: pitch, GIF, install, what it does, commands, options, privacy (what it
reads and runs), "Tested with Claude Code x.y.z", development, license.
