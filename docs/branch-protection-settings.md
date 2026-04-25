# Branch Protection Settings for `main`

Apply these settings in GitHub repository settings:

- Require a pull request before merging.
- Require status checks to pass before merging:
  - `CI / validate`
- Block direct pushes to `main`.
- Optionally require linear history.

These settings keep releases small and reviewable.
