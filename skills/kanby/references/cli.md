# Kanby CLI reference

Set `KANBY_TOKEN` for agents and CI. `KANBY_URL` is optional and defaults to the hosted Kanby service.

| Intent            | Command                                                                             |
| ----------------- | ----------------------------------------------------------------------------------- |
| Verify access     | `kanby auth status --json`                                                          |
| List project      | `kanby project list --json`                                                         |
| List tasks        | `kanby task list [--status ideas\|building\|shipped] --json`                        |
| Inspect task      | `kanby task get <ref> --json`                                                       |
| Create task       | `kanby task create "<title>" [--status ideas] [--note "..."] --json`                |
| Edit task         | `kanby task update <ref> [--title "..."] [--note "..."] [--status building] --json` |
| Split into tasks  | `kanby task split <ref> "<child one>" "<child two>" --json`                         |
| Claim work        | `kanby task claim <ref> [--lease 15] --json`                                        |
| Renew claim       | `kanby task heartbeat <ref> [--lease 15] --json`                                    |
| Report checkpoint | `kanby task progress <ref> "<message>" --json`                                      |
| Link GitHub       | `kanby task link <ref> <issue-or-pr-url> --json`                                    |
| Complete          | `kanby task complete <ref> [--message "..."] --json`                                |
| Release           | `kanby task release <ref> --json`                                                   |

Task refs are the short prefixes returned by list/create. Mutations accept `--idempotency-key <stable-key>`.

For automatic Pull Request association, put `Kanby-Task: <ref>` on its own line in the PR body or name the branch `kanby/<ref>-description`. Project owners can disable this rule in Kanby Settings; `task link` remains the explicit fallback.

Exit codes: `0` success, `1` validation/network/general error, `2` authentication error, `3` claim or idempotency conflict.
