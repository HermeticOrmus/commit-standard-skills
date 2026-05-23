# Using this repo with Cursor

The commit-standard discipline applies to AI-assisted commits, including those Cursor proposes via its Git integration.

## In this repository

The rule [`.cursor/rules/commit-standard.mdc`](.cursor/rules/commit-standard.mdc) is committed with `alwaysApply: true`.

## Use the same discipline elsewhere

**Cursor**: Copy `.cursor/rules/commit-standard.mdc` into that project's `.cursor/rules/`.

**Other AI tools**: Copy [`CLAUDE.md`](CLAUDE.md) to the project root.

## Install the commit-msg hook

For mechanical enforcement of structural rules (subject length, type vocabulary, banned emoji, no AI footers):

```bash
curl -o .git/hooks/commit-msg https://raw.githubusercontent.com/HermeticOrmus/commit-standard-skills/main/hooks/commit-msg
chmod +x .git/hooks/commit-msg
```

The hook rejects commits that violate the standard. Bypass with `--no-verify` if needed (and explain in the next commit why).

## Install the git commit template

```bash
curl -o ~/.config/git/commit-template.txt https://raw.githubusercontent.com/HermeticOrmus/commit-standard-skills/main/commit-template.txt
git config --global commit.template ~/.config/git/commit-template.txt
```

The template prefills the structure in your editor on every `git commit`.

## Install commitlint for CI

If your CI runs commitlint, point it at [`commitlint.config.json`](commitlint.config.json):

```bash
curl -o commitlint.config.json https://raw.githubusercontent.com/HermeticOrmus/commit-standard-skills/main/commitlint.config.json
```

Then in your CI:

```yaml
- run: npx commitlint --from=main --to=HEAD
```
