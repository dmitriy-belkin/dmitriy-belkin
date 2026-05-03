## Automated Gist update scripts for my profile pins.

  
I just wanted a nicer looking profile, so after having edited my README to perfection, I also added some fancy automated gists as pins. They show really cool stats IMO and uh.. yeah. 


None of these have been created by me! I just changed the workflows to clone their repo, instead of me having to fork it and checking out my fork. This means that my repository tab looks less ugly, while still keeping the same functionality.

## Readme stat / pin cards

[`readme-cards.yml`](./readme-cards.yml) downloads SVGs into [`.github/readme-cards/`](../readme-cards) so the profile README can use `raw.githubusercontent.com/.../readme-cards/*.svg`. The public **`github-readme-stats.vercel.app`** is often **503 (deployment paused)**; the workflow uses mirror **`github-readme-stats-eight-theta.vercel.app`**. Run **Sync readme cards** if you change repos or the profile shows gray placeholders.

## Metrics infographic

[`metrics.yml`](./metrics.yml) runs [lowlighter/metrics](https://github.com/lowlighter/metrics) and commits **`github-metrics.svg`** to the root of this repo.

**Token:** [`metrics.yml`](./metrics.yml) uses **`GH_TOKEN`** — the same repository secret as Productive Box / Lang Box / Steam (classic PAT with **`gist`** + **`repo`** as needed). You do **not** need a separate `METRICS_TOKEN` unless you want metrics on a different PAT. Docs: [metrics — GitHub Action](https://github.com/lowlighter/metrics/blob/master/.github/readme/partials/documentation/setup/action.md).

**Tuning:** edit [`metrics.yml`](./metrics.yml) — options are in `with:`; see [core](https://github.com/lowlighter/metrics/blob/master/source/plugins/core/README.md) and [`source/plugins/`](https://github.com/lowlighter/metrics/tree/master/source/plugins).

Do **not** add a `push: main` trigger to this workflow unless you exclude `github-metrics.svg` — otherwise each commit of the SVG would re-trigger the job.

## Contribution snake

[`snake.yml`](./snake.yml) uses [Platane/snk](https://github.com/Platane/snk) (`svg-only@v3`) and publishes SVGs to branch **`output`**. The profile README loads them from `raw.githubusercontent.com`. After the first push, open **Actions → Generate contribution snake → Run workflow** if the animation 404s until the cron runs.

## Troubleshooting pinned gists

- **`GH_TOKEN` / `GH_PAT`:** Gist workflows need a PAT with **`gist`** scope (`GH_TOKEN` is shared across Time / Langs / Steam / Activity). `GITHUB_TOKEN` cannot update gists.
- **Activity gist empty / “Bad credentials”:** Rotate **`GH_TOKEN`** in repo secrets (classic PAT: enable **gist**). Run **Actions → Activity Box → Run workflow**. [`activities.yml`](./activities.yml) updates the gist via **github-script** (supports manual runs).
- **Steam / langs / time boxes:** If pins stop updating, check failed workflow runs and rotate expired tokens.

## Credits:
1. "When do I usually work?"    = [Productive Box](https://github.com/maxam2017/productive-box)
2. "What did I do recently?"    = [Activity Box](https://github.com/JasonEtco/activity-box)
3. "What langs do I use a lot?" = [Lang Box](https://github.com/inokawa/lang-box)
4. "What games do I play?"      = [Steam Box](https://github.com/YouEclipse/steam-box)