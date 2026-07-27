---
name: Inspect a build and its performance
description: Find a build in Develocity and inspect its attributes and Build Cache performance.
api: openapi/gradle-develocity-openapi.yaml
operations: [GetBuilds, GetBuild, GetGradleAttributes, GetGradleBuildCachePerformance]
---

# Inspect a build and its performance

Use the Develocity API to locate a build and read its diagnostics. Develocity is
self-hosted: the base URL is your own instance host, e.g. `https://develocity.example.com`.

## Auth
Send `Authorization: Bearer <access key or token>` on every request. The user needs the
`Access build data via the API` permission. Mint a short-lived token with
`CreateAccessToken` (`POST /api/auth/token`) if you only have an access key.

## Steps
1. **List recent builds** — `GetBuilds` (`GET /api/builds`) to page over builds with
   common attributes and obtain build ids (Build Scan ids).
2. **Fetch one build** — `GetBuild` (`GET /api/builds/{id}`) for the build's summary,
   build-tool type, and available model documents.
3. **Read Gradle attributes** — `GetGradleAttributes`
   (`GET /api/builds/{id}/gradle-attributes`) for tags, custom values, requested tasks,
   and environment. (Use the matching `GetMavenAttributes` / `GetNpmAttributes` /
   `GetPythonAttributes` / `GetSbtAttributes` for other build tools.)
4. **Read cache performance** — `GetGradleBuildCachePerformance`
   (`GET /api/builds/{id}/gradle-build-cache-performance`) to see cache hits/misses and
   avoided work.

## Conventions & errors
- Errors are RFC 7807 `application/problem+json` (`type`, `title`, `status`, `detail`).
- `404` means the build does not exist or you lack permission to see it.
- `401`/`403` indicate a missing/insufficient access key or token.
