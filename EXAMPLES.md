# Examples

Good and bad commit messages with explanations.

## Good examples

### Concise fix

```
fix(screenshot): honor --output paths with a directory component

Bare basenames still land in the configured screenshotDir. Paths with a
separator (./foo, /abs/foo, sub/foo) are honored as written; the CLI
resolves relatives against its own cwd before sending so they don't
silently bind to the daemon's cwd.
```

**Why this works**:
- Type + scope: `fix(screenshot)`
- Imperative subject ≤ 72 chars
- Body explains *what* changed (the new behavior) and *why* it matters (silent cwd binding was wrong)
- Doesn't restate the diff
- No emoji, no marketing language

### Refactor with reference

```
refactor(auth): extract token-refresh into its own service

Pulled the refresh loop out of `Session.acquire()` so the same logic
covers the worker pool and the CLI. No behavior change; the worker
inherits the same retry/backoff that the CLI had.

Refs: #412
```

**Why this works**:
- `refactor` type explicitly signals "no behavior change"
- Body explains the motivation (worker pool needed the same logic)
- Confirms the no-behavior-change invariant explicitly (preempts review questions)
- References the linked issue without closing it (it's still open for downstream work)

### Feature with risk callout

```
feat(orders): add bulk-cancel endpoint

Front-of-house wanted to cancel up to 500 orders in one call after a
warehouse mis-pick. The endpoint takes a list of order IDs and a
required reason code; cancellation is best-effort with a per-ID result
list, not transactional.

Risk: bad reason code or partial failure can leave orders in mixed
states. Mitigation: response includes per-ID outcome; the dashboard
surfaces partial failures and the worker requeues retryable IDs.

Refs: #1820
```

**Why this works**:
- Type signals user-visible new capability (`feat` → minor bump)
- Body leads with why (warehouse mis-pick scenario)
- Then what (best-effort, per-ID result, not transactional)
- Explicit Risk footer because this is destructive at scale
- Mitigation named in the same paragraph as the risk

### Chore with link to upstream issue

```
chore(deps): bump anthropic-sdk-python 0.42 → 0.45

Picks up the cache-control header fix (anthropics/anthropic-sdk-python#891)
that was making prompt-cache misses harder to debug.
```

**Why this works**:
- Specific (`chore(deps)`), not just `chore`
- Version numbers in subject for `git log --grep` discoverability
- Body explains why this specific bump matters (the upstream fix)

### Revert

```
revert: feat(orders): add bulk-cancel endpoint

This reverts commit 4f2a91b. The endpoint is racing against the
in-flight write path under load — a different design is needed.

Refs: #1820, incident #1834
```

**Why this works**:
- `revert:` prefix signals what kind of commit this is
- Subject mirrors the reverted commit's subject for easy grep
- Body references the SHA, explains *why* the revert (the race), and links to the incident

## Bad examples

### Everything wrong

```
🐛 fix: small fix to screenshot 🚀

Generated with Claude Code (https://claude.com/claude-code)
Co-Authored-By: Claude <noreply@anthropic.com>

This is a great improvement that makes the tool way better!
```

**Why this is bad**:
- 🐛 + 🚀 emoji in subject (banned)
- "small fix" — non-specific
- "to screenshot" — no scope structure
- AI tool footer (banned)
- Auto-`Co-Authored-By: Claude` (banned unless explicitly requested)
- "great improvement" + "way better" — hype, no substance
- Body adds zero information

### Pure vagueness

```
update files
```

**Why this is bad**:
- No type
- No scope
- No imperative ("update" is fine but the rest is null)
- Body absent
- Tells the reader nothing

### Multi-concern subject

```
feat(api): add login endpoint and refactor auth and update docs
```

**Why this is bad**:
- Two " and " in subject = three commits crammed into one
- Each concern should be its own commit:
  - `feat(api): add login endpoint`
  - `refactor(auth): consolidate session handling`
  - `docs(auth): document the login flow`
- Atomicity rule: if you can write " and ", split.

### Restating the diff

```
fix: corrected the issue where the user was unable to login because of the bug in the authentication module that was introduced in the previous release
```

**Why this is bad**:
- Subject is way over 72 chars
- Past tense ("corrected") — should be imperative ("fix")
- "issue where the user was unable to login" restates the diff
- "because of the bug in the authentication module" is the wrong level — say what the actual bug was
- "that was introduced in the previous release" — irrelevant to the fix; if it matters, it's a body item

### Tautological

```
fix(login): fix login

Fixes the login bug.
```

**Why this is bad**:
- Body adds nothing the subject didn't say
- Doesn't explain what was wrong
- Doesn't explain what the fix did
- "fix login" / "fix the login bug" / "fixes the login bug" — same content three ways

### Hype body

```
feat(dashboard): add real-time analytics

This is an absolutely stunning addition to our world-class dashboard.
Users will love the seamless, powerful new insights they get from this
revolutionary feature. We're confident this will be a game-changer.
```

**Why this is bad**:
- "stunning", "world-class", "seamless", "powerful", "revolutionary", "game-changer" — marketing fluff
- Zero technical content
- Doesn't say what's actually different in the code
- Says nothing the reviewer can't see from the marketing brief

### Bare chore

```
chore: misc
```

**Why this is bad**:
- "misc" tells the future maintainer nothing
- If it's truly miscellaneous (multiple small things), split them
- If it's one thing, name it: `chore(deps): bump express to 4.18.2` or `chore(repo): add .editorconfig`

## When to skip the standard

For private branches where you'll squash before push, WIP commits like `wip: testing approach A` are fine. The standard applies to commits that land on shared branches.

For trivial typo fixes to documentation, `docs: fix typo in README` is sufficient — no body needed.

For commits that go upstream to a project with its own commit style (Linux kernel, Rust, Chromium), follow that project's style, not OCS. Per-tool playbooks in your own repo can record where the conventions diverge.

## Self-test

Before `git commit`, run mentally:

1. Subject ≤ 72? Aim 50.
2. Imperative mood? "add", not "added" or "adds".
3. Lowercase first letter, no trailing period?
4. Type chosen deliberately? Not `chore` because lazy.
5. Scope present and meaningful? Or truly repo-wide.
6. Body leads with why?
7. No emoji anywhere?
8. No AI footers?
9. No " and " in subject?
10. Diff matches the message? No drive-by changes that aren't named.

If you can't pass all ten, the commit isn't ready.
