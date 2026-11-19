---
name: preview-website
description: >-
  Opens this repository's local website in Google Chrome when the user asks to
  preview, view, or open the local version of the site.
---

# Preview website

Open the local site files for the user in Google Chrome. The website entry point is `index.html` in the repository root.

## Workflow

1. Resolve the repository root and confirm that `index.html` exists.
2. Open that local file in Google Chrome, reusing an existing Chrome window when practical. Use its absolute local file address (`file:///.../index.html`) so relative stylesheets and images load from this checkout.
3. Verify that Chrome displays the page from the local file address, rather than `raisedintheworld.com`.

Use computer interaction to open the file in Chrome. If navigating to the local file from the address bar is blocked, open the actual `index.html` file through Windows File Explorer and choose Google Chrome. If Chrome is unavailable, explain the specific blocker instead of silently opening the published site or another browser.

This skill is only for local preview. Do not edit files, publish changes, or push commits as part of previewing.
