# snap-openstack dashboard (demo)

A demo of [ci-dashboard](https://github.com/johnramsden/ci-dashboard) watching [canonical/snap-openstack](https://github.com/canonical/snap-openstack). The repository holds no dashboard code: only [`.github/ci-dashboard.yml`](.github/ci-dashboard.yml) and a [workflow](.github/workflows/ci-dashboard.yml) that runs the action daily and publishes the site to the `gh-pages` branch.

What it shows:

- **CI health**: the post-merge flaky rate of `main`, `stable/2025.1` and `stable/2024.1`, counting only push, schedule and manual runs. The tag-sync bot and the TICS upload are excluded. The stable branches only get data once something runs on them outside pull requests.
- **Releases**: every published revision of the `openstack` snap and the commit it was built from, parsed from its `<track>-<sha>` version string. Older revisions whose version carries no commit (`2023.1`, `yoga`) show as unknown.

To run it: push this repository to GitHub, run the workflow once (Actions, CI dashboard, Run workflow), then enable Pages from the `gh-pages` branch, `/ (root)`.

To preview locally without GitHub:

```bash
export GH_TOKEN=$(gh auth token)
uvx --from git+https://github.com/johnramsden/ci-dashboard@v1 ci-dashboard build --config .github/ci-dashboard.yml --output-dir /tmp/site
xdg-open /tmp/site/index.html
```
