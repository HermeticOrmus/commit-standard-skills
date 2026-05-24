# Commit Standard Skills

> A single `CLAUDE.md` for disciplined git commit messages. The Ormus Commit Standard (OCS) v1.0 — Conventional Commits + Chris Beams seven rules + a couple of additions, minus the emoji + AI-footer noise.

## The shape

```
<type>(<scope>): <imperative summary, ≤72 chars, no period>

<why this change exists>

<what the diff doesn't show>

Refs: #123
Fixes: #789
```

That's it. Read like a senior engineer wrote it for the next senior engineer.

## What this covers

| Element | Rule |
|---|---|
| Type | `feat fix refactor perf docs test style chore build ci revert` |
| Scope | Optional, lowercase, kebab-case |
| Summary | Imperative, lowercase, no trailing period, ≤72 chars |
| Body | Optional. Leads with why, then what. Wrap 72. |
| Footers | `Refs`, `Fixes`, `Closes`, `BREAKING CHANGE`, `Risk`, `Verified`, `Co-Authored-By` |
| Banned | Emoji, AI footers, marketing language, " and " in subject |
| Atomicity | One concern per commit; tests with the behavior change |

Full standard: [`CLAUDE.md`](CLAUDE.md). Worked good/bad examples: [`EXAMPLES.md`](EXAMPLES.md).

## Install

### As a project CLAUDE.md

Drop [`CLAUDE.md`](CLAUDE.md) at the root of your repository.

```bash
curl -o CLAUDE.md https://raw.githubusercontent.com/HermeticOrmus/commit-standard-skills/main/CLAUDE.md
```

### As a Claude Code skill

The same content as an installable skill: [`skills/commit-standard/`](skills/commit-standard/).

### As a git commit-msg hook

A commit-msg hook that mechanically enforces the structural rules (length, type vocabulary, banned emoji) is in [`hooks/commit-msg`](hooks/commit-msg). Install:

```bash
curl -o .git/hooks/commit-msg https://raw.githubusercontent.com/HermeticOrmus/commit-standard-skills/main/hooks/commit-msg
chmod +x .git/hooks/commit-msg
```

### As a commitlint config

For CI-enforced compliance, [`commitlint.config.json`](commitlint.config.json) configures `@commitlint/cli` to validate against the structural rules.

### As a git commit template

[`commit-template.txt`](commit-template.txt) prefills the message structure on every `git commit`:

```bash
curl -o ~/.config/git/commit-template.txt https://raw.githubusercontent.com/HermeticOrmus/commit-standard-skills/main/commit-template.txt
git config --global commit.template ~/.config/git/commit-template.txt
```

## Lineage

This standard takes the durable parts of established conventions and drops the parts that don't fit:

| Kept from | What |
|---|---|
| [Chris Beams — "How to Write a Git Commit Message"](https://cbea.ms/git-commit/) | Subject ≤ 50, blank line before body, imperative mood, body wraps 72, explain why not how |
| [Tim Pope — "A Note About Git Commit Messages"](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html) | 50/72 discipline; readable in `git log --oneline` |
| [Conventional Commits 1.0](https://www.conventionalcommits.org) | `type(scope): description` shape, type vocabulary, machine-parseability |
| Angular Commit Guidelines | Clean type taxonomy |
| Linux kernel style | `area: brief description` when no clear type fits; narrative bodies for non-trivial changes |

| Dropped from | What and why |
|---|---|
| Gitmoji | No emoji prefixes. Type-as-keyword carries the signal. |
| AI tool footers | No "Generated with Claude Code", no auto-`Co-Authored-By: Claude`. Work is yours. |
| Hype/marketing language | "powerful", "stunning", "best-in-class" — out. |
| Loose Conventional Commits | No bare `chore: misc`. Scope optional only when truly repo-wide. |
| WIP commits on shared branches | Squash before push. Repo history is signal, not chronicle. |

## Why this exists

Git history is signal. The signal degrades when commits are emoji-decorated, marketing-styled, generated-with-AI-tagged, or so vague they communicate nothing. Five years from now a maintainer is going to `git blame` a line and need the why. That maintainer is sometimes future you.

The standard exists to keep `git log` useful at the timescales projects actually live on.

## What this isn't

This isn't a religion. Most reasonable commit conventions are reasonable. If your team uses Conventional Commits directly, that's fine. If your team uses the Linux kernel style, that's fine. OCS is what I default to for new repos and contributions where no style is specified.

If you're contributing upstream to a repo with its own style, follow theirs.

## See also

- [`vibe-engineer-skills`](https://github.com/HermeticOrmus/vibe-engineer-skills) — companion: how you direct AI codegen
- [`andrej-karpathy-skills`](https://github.com/HermeticOrmus/andrej-karpathy-skills) — companion: how Claude should behave when writing code
- [`markdown-discipline-skills`](https://github.com/HermeticOrmus/markdown-discipline-skills) — companion: discipline for AI-generated markdown
- [`shell-safety-skills`](https://github.com/HermeticOrmus/shell-safety-skills) — companion: bash hygiene
- [Conventional Commits 1.0](https://www.conventionalcommits.org) — the parent specification
- [Chris Beams — How to Write a Git Commit Message](https://cbea.ms/git-commit/) — the canonical longer essay

## Contributing

PRs welcome for:

- Additional good/bad examples in [`EXAMPLES.md`](EXAMPLES.md)
- Translations of the README
- Hook variants for other languages / VCS (Mercurial, Pijul, etc.)
- IDE integrations beyond the commit-msg hook (Conventional Commits VS Code, IntelliJ plugin configs)

## License

MIT.


---

## Part of the Libre Open-Source Stack for Claude Code

This repository is part of a growing family of open-source toolkits for Claude Code.

### Libre suite — comprehensive plugin bundles

- [LibreUIUX-Claude-Code](https://github.com/HermeticOrmus/LibreUIUX-Claude-Code) — UI/UX development (152 agents, 70 plugins, 76 commands, 74 skills)
- [LibreArch-Claude-Code](https://github.com/HermeticOrmus/LibreArch-Claude-Code) — Software architecture and system design
- [LibreCopy-Claude-Code](https://github.com/HermeticOrmus/LibreCopy-Claude-Code) — Technical writing and documentation engineering
- [LibreDevOps-Claude-Code](https://github.com/HermeticOrmus/LibreDevOps-Claude-Code) — DevOps engineering and infrastructure automation
- [LibreEmbed-Claude-Code](https://github.com/HermeticOrmus/LibreEmbed-Claude-Code) — Embedded systems, firmware, and IoT development
- [LibreFinTech-Claude-Code](https://github.com/HermeticOrmus/LibreFinTech-Claude-Code) — Financial technology development
- [LibreGEO-Claude-Code](https://github.com/HermeticOrmus/LibreGEO-Claude-Code) — AI-search optimization (ChatGPT, Perplexity, Gemini, Google AI Overviews)
- [LibreGameDev-Claude-Code](https://github.com/HermeticOrmus/LibreGameDev-Claude-Code) — Game development across Godot, Unity, Unreal
- [LibreMLOps-Claude-Code](https://github.com/HermeticOrmus/LibreMLOps-Claude-Code) — ML engineering and AI operations
- [LibreMobileDev-Claude-Code](https://github.com/HermeticOrmus/LibreMobileDev-Claude-Code) — Mobile app development (Flutter, React Native, native iOS, native Android)
- [LibreSecOps-Claude-Code](https://github.com/HermeticOrmus/LibreSecOps-Claude-Code) — Security operations

### Skills mini-repos — single CLAUDE.md drop-ins

- [vibe-engineer-skills](https://github.com/HermeticOrmus/vibe-engineer-skills) — Direct AI codegen well (hypothesis → scope → validate → reject working-but-wrong)
- [markdown-discipline-skills](https://github.com/HermeticOrmus/markdown-discipline-skills) — Strip AI-slop from markdown (no em dashes, no marketing fluff)
- [shell-safety-skills](https://github.com/HermeticOrmus/shell-safety-skills) — `set -euo pipefail` discipline + 15 failure-mode examples
- [unwoke-skills](https://github.com/HermeticOrmus/unwoke-skills) — Strip AI theater (ten sins to eliminate, symmetric engagement)
- [python-conventions-skills](https://github.com/HermeticOrmus/python-conventions-skills) — Modern Python 3.11+ (types, pathlib, async, ruff, mypy, uv)
- [typescript-conventions-skills](https://github.com/HermeticOrmus/typescript-conventions-skills) — TypeScript strict mode, discriminated unions, Result types
- [hermetic-laws-skills](https://github.com/HermeticOrmus/hermetic-laws-skills) — Seven Hermetic Principles applied to engineering
- [riper-workflow-skills](https://github.com/HermeticOrmus/riper-workflow-skills) — Research / Innovate / Plan / Execute / Review systematic dev
- [six-day-cycle-skills](https://github.com/HermeticOrmus/six-day-cycle-skills) — Sustainable shipping cadence with mandatory rest
- [token-optimization-skills](https://github.com/HermeticOrmus/token-optimization-skills) — Claude Code token + context optimization
- [osint-skills](https://github.com/HermeticOrmus/osint-skills) — OSINT research methodology (multi-wave investigative spiral)
- [calcinate-skills](https://github.com/HermeticOrmus/calcinate-skills) — Stage 1 of the Magnum Opus (burn project bloat)
- [claude-md-overhaul-skills](https://github.com/HermeticOrmus/claude-md-overhaul-skills) — Audit CLAUDE.md and MEMORY.md against caps
- [session-handoff-skills](https://github.com/HermeticOrmus/session-handoff-skills) — Session handoff + pickup discipline
- [naming-skills](https://github.com/HermeticOrmus/naming-skills) — Product naming methodology (mine the brand's vocabulary)
- [magnum-opus-skills](https://github.com/HermeticOrmus/magnum-opus-skills) — Seven-stage alchemy applied to project transformation

### Template source

- [andrej-karpathy-skills](https://github.com/HermeticOrmus/andrej-karpathy-skills) — the canonical single-file CLAUDE.md pattern (fork of jiayuan_jy's original)

Star the family, not just one — that's how the suite stays coherent.
