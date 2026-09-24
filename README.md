# INSPIRE GitHub PWA Wrapper V2 — Redirect Mode

This version DOES NOT use an iframe.

Flow:
GitHub Pages PWA
→ branded splash
→ top-level browser redirect
→ INSPIRE Apps Script

Apps Script URL:
https://script.google.com/macros/s/AKfycbzsW1cYUPoJwd2R1xUDbSxFE6QM_qFsGyL4eYYGDwLtN5NtXa3EGe3vYz5wrPryAbIjCA/exec

## Replace V1 on GitHub

Upload/replace:
- index.html
- manifest.webmanifest
- service-worker.js
- .nojekyll
- icons/ (all files)

You can delete the old `offline.html`; V2 does not need it.

Commit changes to `main`.
GitHub Pages should redeploy automatically.

## VERY IMPORTANT AFTER UPDATE

Because V1 installed a service worker, your phone may keep an old cached version.

After GitHub Pages finishes deploying:
1. Open the GitHub Pages URL in Chrome normal mode.
2. Refresh several times or clear site data for the GitHub Pages site.
3. Confirm the screen says:
   `INSPIRE PWA WRAPPER V2 · REDIRECT MODE`
4. Only then test the automatic redirect.

If the old iframe version remains, uninstall/delete the old Home Screen shortcut and clear site data for:
`boyhcblackowl-coder.github.io`

Then reopen the GitHub URL.

## Test target

Open:
https://boyhcblackowl-coder.github.io/INSPIRE-2.0/

Expected:
1. Black Owl splash appears.
2. After about 0.9 seconds, the browser navigates away from GitHub Pages.
3. INSPIRE Apps Script opens as a TOP-LEVEL page.
4. There is no iframe.

## Diagnostic account buttons

If redirect reaches Apps Script but Chrome normal still errors, return to the GitHub page and wait ~5 seconds or use the troubleshooting controls.

There are test links for:
- authuser=0
- authuser=1
- authuser=2

These are diagnostics only, not intended as the permanent employee workflow.

## Interpretation of the test

If V2 works in Chrome normal:
Great — the issue was primarily iframe/session handling. We can keep this launcher model.

If V2 still fails in Chrome normal but works in Incognito:
The failure is not caused by the GitHub iframe. It means the Apps Script top-level URL itself conflicts with the normal Chrome Google session/multi-login context. In that case a GitHub redirect cannot remove the issue, because the browser eventually still navigates to script.google.com.

## Add to Home Screen

Do this only after Chrome normal successfully reaches INSPIRE.

Android:
Chrome → ⋮ → Add to Home screen / Install app

iPhone:
Safari → Share → Add to Home Screen

Note:
Because V2 redirects outside the GitHub PWA scope to `script.google.com`, the final Apps Script page may show browser UI depending on Android/iOS behavior. V2's purpose is first to isolate whether iframe embedding was the cause.
