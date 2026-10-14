# renovate-runner

Runs [Renovate](https://docs.renovatebot.com/) hourly for every `haproxy-haptic`
repository that the `haptic-renovate` GitHub App is installed on and that has a
Renovate configuration. Each repository keeps its own `renovate.json`.

The runner authenticates with a one-hour installation token of the
`haptic-renovate` app. It needs the repository variable `RENOVATE_APP_ID` and
the secret `RENOVATE_APP_PRIVATE_KEY`. The key lives only here, outside the CI
of the repositories Renovate updates.

Each run uploads its debug log as the `renovate-log` artifact for 7 days. Read
it first when a Renovate pull request is missing or broken:

```bash
gh run download <run-id> --repo haproxy-haptic/renovate-runner --name renovate-log
```

Start a run without waiting for the schedule:

```bash
gh workflow run renovate.yml --repo haproxy-haptic/renovate-runner
```

Updates to this runner's own pins never merge automatically; review them before
merging, because the runner holds the app's private key.
