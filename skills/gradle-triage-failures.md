---
name: Triage build failures
description: Group and investigate build failures across a Develocity instance.
api: openapi/gradle-develocity-openapi.yaml
operations: [GetFailureGroups, GetBuildFailures, GetBuild]
---

# Triage build failures

Investigate recurring build failures using Develocity's failure classification.

## Auth
`Authorization: Bearer <access key or token>` with the `Access build data via the API`
permission.

## Steps
1. **List failure groups** — `GetFailureGroups` (`GET /api/failures/groups`) to see
   classified failure groups with occurrence counts, first/last occurrence, an example
   failure, and the affected build ids.
2. **Pick a group** and take one of its `buildIds`.
3. **Read that build's failures** — `GetBuildFailures`
   (`GET /api/failures/builds/{id}`) for the failures recorded on a specific build.
4. **Open the build** — `GetBuild` (`GET /api/builds/{id}`) for full context on the
   failing build.

## Conventions & errors
- Errors are RFC 7807 `application/problem+json`.
- Page through large failure sets using the endpoint's documented pagination controls.
- `503` (`NotReadyError`) means the instance is not yet ready — retry with backoff.
