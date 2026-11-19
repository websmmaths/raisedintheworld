---
name: explain-changes
description: >-
  Explains unpublished website changes in plain language for a non-technical
  user. Use when the user asks what changed, wants changes explained, or asks
  what is different since the last update or publish.
---

# Explain changes

Help the site owner understand what is different between their computer and what is already on the live site.

## When to run

Use when the user asks what changed, wants an explanation of their edits, or asks what is different since the last publish — **without** automatically committing or pushing unless they also ask to update the website.

## What to compare

Treat “since the last publish” as:

1. Uncommitted changes in the working tree (`git status`, `git diff`)
2. Local commits not yet on `origin` (`git log origin/<branch>..HEAD`)

Compare against the remote tracking branch for the current branch when it exists.

## How to explain

Write for someone with **no** programming or git background.

### Structure

1. **Headline** — one sentence: what a visitor would notice overall.
2. **Details** — short bullets, each describing a visible change:
   - Wording, headlines, button labels
   - Photos or images added, removed, or swapped
   - Colors, spacing, or layout
   - New links or where buttons go
   - New pages or sections

### Rules

- Do **not** lead with commit hashes, branch names, or file paths.
- Do **not** paste raw diffs unless the user explicitly asks for technical detail.
- If nothing is unpublished: say **“The website matches what is already online.”**
- If a change touches a likely secret file (`.env`, keys, tokens), say a **private file** changed. Do not show its contents or values.
- Keep tone calm and specific. Prefer “The footer now includes Facebook” over “Modified index.html.”

### Examples

**Good:**

> You updated the bottom of the page so people can email you, and you added links to Instagram, TikTok, and Facebook.

**Avoid:**

> `index.html` +4 lines in `.social` flex container.