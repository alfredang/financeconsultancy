---
description: Secure-publish this project to GitHub — scan for secrets, set up Pages, README, repo About, then push
---

Publish the current project to GitHub safely. Do the steps in this order, and **stop and warn the user** if any secret-scan step finds something sensitive — do not push until it is resolved.

## 1. Security scan (BEFORE anything is pushed)
- Scan the working tree for secrets, passwords, API keys, tokens, private keys, and `.env` files. Check tracked files and anything staged.
- Look for: high-entropy strings, `password`/`secret`/`api_key`/`token`/`Authorization` assignments, AWS/Google/Stripe/GitHub key patterns, `BEGIN PRIVATE KEY`, hardcoded credentials, connection strings with embedded passwords.
- Verify a `.gitignore` exists and excludes `.env`, secrets, credentials, and local config. Add/extend it if needed.
- If anything sensitive is found: STOP, report it to the user, and propose remediation (remove from tree, rotate the secret, add to `.gitignore`, scrub history if already committed). Do not continue until cleared.

## 2. README
- Create or update `README.md` so it accurately describes the project: what it is, how to run/serve it, structure, and deployment. Keep it concise and current with the actual code.

## 3. GitHub Pages via GitHub Actions
- Ensure a workflow exists at `.github/workflows/` that deploys the site to GitHub Pages on push to the default branch. If one already exists, verify it is correct; otherwise create one (upload-pages-artifact + deploy-pages, with `pages: write` and `id-token: write` permissions).
- After pushing, ensure Pages is enabled with source = GitHub Actions (`gh api` or remind the user to enable it in repo settings if CLI cannot).

## 4. Push to GitHub
- Commit changes with a clear message and push to the remote default branch. If no remote exists, create the repo with `gh repo create` (ask the user for public/private if unclear).

## 5. Update the repo About
- Set the repository description and the homepage URL (the GitHub Pages URL) via `gh repo edit`. Add relevant topics if helpful.

## 6. Final confirmation
- Report the repo URL, the Pages URL, and confirm the secret scan passed clean before publishing.
