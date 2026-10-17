# PR Dashboard

A map of your open GitHub pull requests: one row per repository, one column for your PRs, one for the reviews requested from you.

Page: https://wowawiwa.github.io/pr-dashboard/

## What the page shows

- **My PRs** are sorted from closest to merge to furthest: approved, feedback received, waiting for review, nothing requested yet. Four round badges, aligned on every card, say what is missing. The first two are about people (reviews, draft), the last two about the code (CI checks, conflicts). Hovering a badge explains it and names who did what.
- **Review requests** lists requests to you by name first, then requests to your team, oldest first. Links lead to the PRs you already reviewed or commented on.
- **Pause** sets a PR aside at the bottom of its cell. **Hide** removes it until the PR changes.
- The page refreshes only when you ask: the Refresh button, or ⌘R / Ctrl+R, which the page catches instead of reloading.

## Token

The page calls the GitHub API straight from the browser, with no server. It never stores the token. The token lives in your password manager, then in the tab's memory, and only goes to `api.github.com`. Closing the tab forgets it.

The page opens on a login form with a single field. For Bitwarden to fill it, create a login with the token as password and `https://wowawiwa.github.io/pr-dashboard/` as URI. Bitwarden then fills it with its shortcut (⌘⇧L), from its menu in the field, or on its own if you turn on autofill on page load for that login. The dashboard opens as soon as the field is filled.

The login screen links to a classic token with the `repo` and `read:org` scopes already checked. Pick a short expiration. If your org enforces SSO, authorize the token for it with “Configure SSO”.

Your repository list and your paused or hidden PRs stay in the browser's localStorage. None of it is sensitive.

## Development

A single file, `index.html`, with no dependency and no build step. To test the rendering without a token, pass an answer to the `prdash.query` request to `prdash.render(json)` in the console.
