# Subdomains vs. Subpaths

## Example using CRM 

> **Use case:** Deciding between `crm.williamjwhite.me` and `williamjwhite.me/crm`

---

## What's the Difference?

### `crm.williamjwhite.me` — Subdomain

Treats "crm" as a **separate host**. It has its own DNS record, its own SSL certificate, and is completely independent of whatever lives at `williamjwhite.me`.

**Setup requires:**

- A **CNAME DNS record** at your domain registrar: `crm` → `yourusername.github.io`
- A **`CNAME` file** in the root of your GitHub repo containing exactly:
  ```
  crm.williamjwhite.me
  ```
- GitHub Pages enabled on the repo (Settings → Pages → branch)

**What does the `CNAME` file actually do?**

It tells GitHub's CDN/edge network which custom domain should route to your repo. Without it, GitHub's servers don't know to serve your repo when someone visits `crm.williamjwhite.me`. It's a single-line file with no extension — just the bare domain name. GitHub reads it on deploy and registers the mapping on their infrastructure.

---

### `williamjwhite.me/crm` — Subpath

A route **within your main site**. Same host, same SSL cert, same DNS record as your root domain.

**Setup requires:**

- Your main site must already be serving `williamjwhite.me`
- The tracker must be one of:
  - A **subfolder** in the same repo (e.g. `/crm/index.html`)
  - A **framework route** (e.g. Next.js App Router, React Router)
  - A **reverse proxy rule** if the app is hosted separately behind the scenes
- No separate DNS record needed
- No `CNAME` file (unless the main site already has one for `williamjwhite.me`)

---

## Side-by-Side Comparison

| | `crm.williamjwhite.me` | `williamjwhite.me/crm` |
|---|---|---|
| DNS record needed | Yes — CNAME at registrar | No (uses existing) |
| `CNAME` file in repo | Yes | No |
| Own GitHub repo | Yes (fully independent) | No (shares main site) |
| SSL certificate | Separate (GitHub auto-provisions) | Shared with root domain |
| Independence | Fully isolated | Coupled to main site setup |
| Best for | Standalone apps/tools | Sections of a unified site |

---

## Which Should You Use?

**Choose the subdomain** (`crm.williamjwhite.me`) if:

- The project is a distinct, standalone app
- You want to deploy it independently (its own repo, its own pipeline)
- You don't want it coupled to changes on your main site

**Choose the subpath** (`williamjwhite.me/crm`) if:

- Your main site is already a framework app (e.g. Next.js, SvelteKit)
- You want shared navigation, layout, or auth
- You prefer everything managed in a single repo

---

## The `CNAME` File — Quick Reference

| Property | Detail |
|---|---|
| Filename | `CNAME` (no extension, uppercase) |
| Location | Root of the GitHub repo |
| Contents | One line: the full custom domain |
| Example contents | `crm.williamjwhite.me` |
| Purpose | Tells GitHub Pages which domain maps to this repo |
| Without it | GitHub serves the default `*.github.io` URL only |

---

*Last updated: March 2026*
