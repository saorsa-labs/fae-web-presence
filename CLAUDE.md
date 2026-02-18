# CLAUDE.md

This file provides guidance to Claude Code when working with this repository.

## Project Overview

This repo contains 10 static websites for the Fae AI companion project, all hosted on Firebase Hosting under the `fae-web-presence` Firebase project. Each site lives in its own directory named after its domain.

## Architecture

- **Hosting:** Firebase Hosting (multi-site configuration)
- **Firebase Project ID:** `fae-web-presence`
- **Sites:** 10 static sites, each in a directory named after its domain
- **DNS:** GoDaddy, A records pointing to Firebase IPs
- **SSL:** Automatically provisioned by Firebase

### Key Files

- `firebase.json` — Defines hosting targets and which directory serves each site
- `.firebaserc` — Maps deploy targets to Firebase site IDs

### Important: thefae.com Site ID

The Firebase site ID for `thefae.com` is `thefae-site` (not `thefae-com`). This is because `thefae-com` was reserved by another project. The deploy target `thefae-com` in `firebase.json` maps to `thefae-site` via `.firebaserc`.

## Site Directory Mapping

| Directory | Firebase Site ID | Custom Domain |
|-----------|------------------|---------------|
| `thefae.com/` | `thefae-site` | thefae.com |
| `myfae.ai/` | `myfae-ai` | myfae.ai |
| `withfae.ai/` | `withfae-ai` | withfae.ai |
| `getfae.ai/` | `getfae-ai` | getfae.ai |
| `jointhefae.com/` | `jointhefae-com` | jointhefae.com |
| `downloadfae.com/` | `downloadfae-com` | downloadfae.com |
| `ai-companion.com/` | `ai-companion-com` | ai-companion.com |
| `meetfae.ai/` | `meetfae-ai` | meetfae.ai |
| `meetfay.ai/` | `meetfay-ai` | meetfay.ai |
| `meetfaye.ai/` | `meetfaye-ai` | meetfaye.ai |

## Development Commands

```bash
# Deploy all sites at once
firebase deploy --only hosting

# Deploy a single site (use the target name from firebase.json)
firebase deploy --only hosting:myfae-ai

# List all hosting sites
firebase hosting:sites:list --project fae-web-presence

# Check domain status via API
# See README.md for details
```

## Working with Sites

Each site directory is a self-contained static site. The `index.html` in each directory is the entry point.

### Editing a Site

1. Edit files in the relevant directory (e.g., `myfae.ai/index.html`)
2. Deploy: `firebase deploy --only hosting:myfae-ai`

### Adding Assets

Place CSS, JS, images, etc. directly in the site's directory. Firebase serves everything in the directory as static files.

### Adding a New Site

1. Create a Firebase hosting site: `firebase hosting:sites:create <site-id> --project fae-web-presence`
2. Add the target mapping to `.firebaserc` under `targets.fae-web-presence.hosting`
3. Add a hosting entry to `firebase.json` with `target` and `public` fields
4. Create the directory with at minimum an `index.html`
5. Add the custom domain in the Firebase console
6. Configure DNS (A records: `151.101.1.195`, `151.101.65.195`)

## Guidelines

- Each site is independent — changes to one site do not affect others
- All sites are static HTML/CSS/JS — no server-side rendering or build step
- Keep sites lightweight and fast-loading
- The aesthetic across sites should be consistent: warm, natural, Celtic/Scottish-inspired
- Footer on all sites: "Created by Saorsa Labs, sponsored by the Autonomi Foundation"
- Do not modify `firebase.json` or `.firebaserc` unless adding/removing sites
- Always deploy after making changes — there is no CI/CD auto-deploy yet
