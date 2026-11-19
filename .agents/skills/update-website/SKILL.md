---
name: update-website
description: >-
  Commits and pushes the Raised in the World GitHub Pages site with security
  checks and required assets included. Use when the user asks to update the
  website, save changes, publish, put the site online, commit, or push.
---

# Update website

This repository is a simple static site on GitHub Pages (`raisedintheworld.com` via [CNAME](../../CNAME)).

## When to run

Only run this workflow when the user clearly wants to publish: they mention updating the website, saving changes, publishing, putting it online, committing, or pushing.

## Workflow

Copy and track progress:

```
Publish checklist:
- [ ] Inspect local changes
- [ ] Security scan (no secrets)
- [ ] Required site assets included
- [ ] Commit
- [ ] Push
- [ ] Confirm in plain language
```

### 1. Inspect changes

Run in parallel:

- `git status`
- `git diff` and `git diff --staged`
- `git log origin/$(git branch --show-current)..HEAD --oneline` (if upstream exists)

If there is nothing to commit and nothing to push, tell the user the site already matches what is online.

### 2. Security scan (highest priority)

Before staging or pushing, scan changes for likely secrets:

- Passwords, API keys, tokens, private keys
- Files named like `.env`, `*.pem`, `*.key`, `credentials.json`, or similar
- New lines that look like `API_KEY=`, `SECRET=`, `TOKEN=`, etc.

If anything looks like a secret:

- Stop. Do **not** commit or push.
- Tell the user in plain language that a private file or password-like content was found. Name the file only — never paste the secret.

### 3. Required site assets (supersedes ignore rules, not security)

The live site must include every local file the pages reference.

1. Read `index.html` and `styles.css` (and any other HTML/CSS in the repo).
2. Collect paths from:
   - `src="..."`
   - `href="..."` that point to local files (not `http://`, `https://`, or `mailto:`)
   - `url(...)` in CSS
3. Resolve paths relative to each file. Each referenced path that exists on disk must be tracked and included in the commit.
4. If a page references a file that does not exist, stop and tell the user which image or file is missing.

Do **not** force-add files that failed the security scan, even if the site references them.

### 4. Stage and commit

- Respect [.gitignore](../../.gitignore). Do not commit OS junk, editor swap files, secrets, or `node_modules/` / `.venv/`.
- Include all other site files the publish needs: `index.html`, `styles.css`, `assets/`, `branding/`, images, `CNAME`, `.nojekyll`, etc.
- Write a commit message in 1–2 sentences focused on **what a visitor would notice**, not internal file names.

Never:

- `git config` changes
- `--force` push to `main` / `master`
- `--no-verify` or skipped hooks unless the user explicitly requests it

### 5. Push

- Push the current branch to `origin`.
- If the remote is ahead, try `git pull --ff-only` once, then push again.
- If pull or push fails, stop and explain what happened in plain language (no blame, no jargon).

### 6. Confirm to the user

After a successful push, say in everyday language that the changes are on the live site at **raisedintheworld.com** (GitHub Pages may take a minute or two to refresh).