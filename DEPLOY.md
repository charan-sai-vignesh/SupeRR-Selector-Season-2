# Publish the Pressure Lab dashboard

The dashboard is a static, self-contained page; it needs no backend, build step, or API key. `index.html` forwards to `dashboard.html` so the folder has a default landing page.

## Quick public preview (Netlify Drop)

1. Open Netlify Drop at https://app.netlify.com/drop and sign in or create an account.
2. Drag the `Data Pack` folder onto the page. If the platform rejects unrelated source files, create a small deploy folder containing only `index.html` and `dashboard.html` and upload that folder.
3. Netlify will provide a public `*.netlify.app` URL. Open it and test the batter/bowler tabs, filters and player details.
4. To update the live page, upload the same two files again through the site's deploy page.

## GitHub Pages option

1. Create a GitHub repository and add `index.html` and `dashboard.html` at its root.
2. In repository Settings → Pages, choose deployment from the `main` branch and `/ (root)`.
3. Wait for the Pages build and use the provided `https://<account>.github.io/<repository>/` address.

## Local preview

From this folder, run a simple static server and open `http://localhost:8000/`. The page works directly from the HTML file too, but a server more closely matches a hosted deployment.

The dashboard is interactive but its underlying analysis is a fixed snapshot of the supplied 2022–2026 data. It does not update automatically with auction news, live scores, player availability or roster changes. No hosting account was available in this workspace, so the public deployment must be completed from the owner's account using one of the options above.
