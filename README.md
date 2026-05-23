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
