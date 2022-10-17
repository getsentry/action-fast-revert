action-fast-revert
==================

revert a PR directly on the primary branch

**NOTE**: this assumes PRs are merged via squash

## usage

```yaml
on:
  pull_request_target:
    types: [labeled]

jobs:
  fast-revert:
    runs-on: ubuntu-latest
    if: |
      github.event.label.name == 'Trigger: Revert'
    steps:
    - uses: actions/checkout@v3
      with:
        token: ${{ secrets.BOT_TOKEN }}
    - uses: getsentry/action-fast-revert@v2.0.0
      with:
        pr: ${{ github.event.number }}
        co_authored_by: ${{ github.event.sender.login }} <${{ github.event.sender.id }}+${{ github.event.sender.login }}@users.noreply.github.com>
        # use the identity of the token
        committer_name: getsentry-bot
        committer_email: bot@sentry.io
        token: ${{ secrets.BOT_TOKEN }}
```
