# Fork changes — idimsh/keelflow

This fork of [Perruer/keelflow](https://github.com/Perruer/keelflow) carries a small patch queue that makes
Agentflow V2 drive long-running CLI coding agents through [Paseo](https://github.com/getpaseo/paseo).
Everything else is upstream Keelflow, unchanged.

## Base

| Field | Value |
|---|---|
| Upstream | `Perruer/keelflow` |
| Base release | `v3.2.1` (`fc162d8da7467c8a6320b9cc836d85fa6d00d37c`) |
| Branches | `main` mirrors upstream `main`; `director` = base release + the patch queue below |
| Release tags | `v<upstream version>-director.<N>`, for example `v3.2.1-director.1` |
| Licence | Apache-2.0, as upstream |

## Patch queue

One commit per patch, each with its tests. Listed in application order.

| ID | Patch | Commit | Status |
|---|---|---|---|
| P1 | Paseo Agent node: start a Paseo agent from a flow step and store `{agentId, serverId}` in the flow state | — | planned |
| P3 | Loop-count persistence: rebuild loop counts from stored `executionData` on resume | — | planned |
| P4 | Startup crash sweep: mark executions left `INPROGRESS` as `ERROR` with a reason | — | planned |
| P6 | Wait node (optional): a dedicated STOP node "wait for agent" | — | optional |

## Rebase onto a new upstream release

1. `git fetch upstream --tags`
2. `git switch main && git merge --ff-only upstream/main && git push origin main`
3. `git switch director && git rebase --onto <new tag> <old tag>`
4. Resolve conflicts one patch at a time; keep each patch a single commit.
5. `pnpm install --frozen-lockfile && pnpm build && pnpm test`, plus the patch tests.
6. Tag `v<new version>-director.1` and push `director` and the tag to `origin`.

Never push to `upstream`.
