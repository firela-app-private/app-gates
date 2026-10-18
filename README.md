# app-gates

GitHub Actions workflows used by Firela projects. See `.github/workflows/`.

## main-test.yml — post-merge born-red leg (ops#344)

Runs the full flutter test suite on the app repo's (`fire-la/firela-app-private`) main HEAD — the squashed main tree is otherwise never run by any gate (PR gates only see PR trees; adjudicated from app-private#812 after the 2026-10-18 #808/#784 silent-red window).

- **Triggers**: `workflow_dispatch` (optionally with a pinned `sha`, used for red-tree replay evidence), `push` to *this* repo's main (= self-test on workflow edits), daily `schedule` backstop.
- **App-main movement detection**: the agent-ops Mac kicker (`relay-gates-kick.sh` main-HEAD probe, 15-min cadence) dispatches this workflow with the moved SHA. Cross-repo push webhooks are structurally unavailable — a workflow only hears its own repo's events and fire-la org Actions are disabled (ops#328).
- **Visibility**: a red main tree fails the job → `gh run list -R firela-app-private/app-gates`. No check runs posted; zero app-gates.yml / mergegate changes.
- **Quota**: public repo → standard runner minutes free (ops#328).
