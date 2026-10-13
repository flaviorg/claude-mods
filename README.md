<div align="center">

# ◆ claude-mods

**Original mods for Claude Code — small add-ons that change how it looks and behaves, written from scratch against the official mods API.**

[![Claude Code mods](https://img.shields.io/badge/Claude_Code-mods-0d0d0f?style=flat-square)](https://code.claude.com/docs/en/plugins/mods/overview)
[![License: MIT](https://img.shields.io/badge/license-MIT-8a877f?style=flat-square)](LICENSE)

</div>

Each mod lives in its own repository and installs on its own. This repository is the family
marketplace: add it once and install any of them.

```text
/plugin marketplace add flaviorg/claude-mods
/plugin install tripwire@claude-mods
```

## The mods

| | Mod | What it does | Status |
|---|---|---|---|
| ◆ | [**tripwire**](https://github.com/flaviorg/tripwire) | Holds a destructive command — `rm -rf`, force push, hard reset — and shows what it would destroy before it runs. You cancel or proceed. | 0.1.0 |
| ◆ | [**canopy**](https://github.com/flaviorg/canopy) | Your project's file tree beside the chat. Each file Claude touches keeps its state in its own color: being edited, edited, committed, being read, read. | 0.1.0 |
| ◆ | [**crew**](https://github.com/flaviorg/crew) | A live panel of the subagents Claude delegates to: model, context, tokens, cost and time, each with an animated mascot. | 0.1.0 |
| ◆ | **taximeter** | A band above the prompt with the session's real cost, tokens per minute and where it's heading. | planned |
| ◆ | **pomodoro** | A focus timer in the band that pauses while Claude works and rings when it's done. | planned |
| ◆ | **scribe** | Drafts the commit message and changelog entry as Claude edits; `/changelog` copies it. | planned |
| ◆ | **radar** | Runs the affected tests after each edit and shows green/red per file, like a local CI. | planned |

Every mod follows the same rules — see [`docs/conventions.md`](docs/conventions.md):
TypeScript, tests with `claude plugin test`, `claude plugin validate --strict` clean, hooks
that block commands fail closed, no network, and one visual signature (`◆`).

## Trust

A mod runs with your permissions inside Claude Code. Before installing any of these, you can
list exactly what it does without running it:

```bash
claude plugin validate ./tripwire
```

## License

[MIT](LICENSE) © flaviorg
