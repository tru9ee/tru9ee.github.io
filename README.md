# Tokyo Hosting — GitHub Pages edition

This package creates the static dashboard for **https://tru9ee.github.io** and a separate workflow folder for a **private** scripts repository.

## Important architecture

- `tru9ee.github.io` is a public static website. GitHub Pages does not provide private password-protected pages on a free account.
- Python scripts live in a separate private repository named `tokyo-scripts`.
- The website contains links to the private repository and its Actions page. GitHub asks you to sign in and enforces repository permissions.
- GitHub Actions runs scripts on demand, not forever. GitHub-hosted jobs have a maximum six-hour run duration; free usage quotas also apply.
- Do not put a GitHub token or password in this website's HTML/JavaScript.

## Part A — Publish the website

1. Download and extract this ZIP.
2. Create a **public** GitHub repository named exactly `tru9ee.github.io` under the `tru9ee` account.
3. Upload `index.html` and the `assets/` folder from this package to the repository root. Do not upload the `private-runner/` folder here.
4. In repository Settings → Pages, select **Deploy from a branch**, branch `main`, folder `/ (root)`, then Save.
5. Wait for GitHub Pages to publish. Your site will be at `https://tru9ee.github.io`.

## Part B — Create the private Python repository

1. Create another GitHub repository named `tokyo-scripts`.
2. Set visibility to **Private**.
3. Upload the contents of this package's `private-runner/` folder to the root of `tokyo-scripts`. This includes `.github/workflows/run-script.yml` and the `scripts/` folder.
4. In the private repo, open Actions. If GitHub asks, enable Actions.
5. Add your own Python files to `scripts/`, for example `scripts/main.py`.
6. Open Actions → Run Python script → Run workflow. Enter `scripts/main.py` as the script path, then run.
7. Open the run to view logs or cancel an active run.

The dashboard links already point to:
- `https://github.com/tru9ee/tokyo-scripts`
- `https://github.com/tru9ee/tokyo-scripts/actions/workflows/run-script.yml`
- `https://github.com/tru9ee/tokyo-scripts/actions`

If you choose a different private repository name, edit those three URLs in `index.html`.

## Security and privacy

- Keep `tokyo-scripts` private. Only accounts you authorize can see its files and workflow logs.
- GitHub Pages site content is public. Do not put private information on the Pages repository.
- There is intentionally no fake password form. A password embedded in client-side JavaScript is visible to visitors and is not real access control.
- The workflow grants only read access to repository contents and does not expose a personal access token to the uploaded script.
- Only run scripts you wrote or have reviewed. Scripts execute arbitrary code on a hosted runner and may use the runner's network.
- This is not a permanent server. Workflows are finite jobs, not a 24/7 process manager.

## Project layout

```text
tokyo-hosting-github-pages/
├── index.html
├── assets/
│   └── style.css
└── private-runner/
    ├── .github/
    │   └── workflows/
    │       └── run-script.yml
    └── scripts/
```
