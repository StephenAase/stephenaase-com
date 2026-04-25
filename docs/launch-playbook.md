# Launch Playbook

## DNS + HTTPS (GitHub Pages)

Set these records where `stephenaase.com` is managed:

- `A` -> `185.199.108.153`
- `A` -> `185.199.109.153`
- `A` -> `185.199.110.153`
- `A` -> `185.199.111.153`
- `AAAA` -> `2606:50c0:8000::153`
- `AAAA` -> `2606:50c0:8001::153`
- `AAAA` -> `2606:50c0:8002::153`
- `AAAA` -> `2606:50c0:8003::153`
- `CNAME` for `www` -> `stephenaase.com`

`CNAME` file in repo root is already set to `stephenaase.com`.

## Rollback

If a release breaks production, revert the merge commit on `main` and redeploy.

## 30-Day cadence

- Week 1: foundation + live homepage
- Week 2: about + project card
- Week 3: SEO metadata + analytics
- Week 4: accessibility pass + backlog grooming
