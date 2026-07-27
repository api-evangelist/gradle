---
name: Manage Test Distribution agent pools
description: Create a Test Distribution agent pool, issue a registration key, and check status.
api: openapi/gradle-develocity-openapi.yaml
operations: [ListTestDistributionAgentPools, CreateTestDistributionAgentPool, GenerateTestDistributionAgentPoolRegistrationKey, GetTestDistributionAgentPoolStatus]
---

# Manage Test Distribution agent pools

Provision and operate Test Distribution agent pools so tests run across multiple agents.

## Auth
`Authorization: Bearer <access key or token>`. Managing agent pools requires the
appropriate Test Distribution administration permission on the Develocity instance.

## Steps
1. **List existing pools** — `ListTestDistributionAgentPools`
   (`GET /api/test-distribution/agent-pools`).
2. **Create a pool** — `CreateTestDistributionAgentPool`
   (`POST /api/test-distribution/agent-pools`) with the pool definition; capture the
   returned `poolId`.
3. **Issue a registration key** — `GenerateTestDistributionAgentPoolRegistrationKey`
   (`POST /api/test-distribution/agent-pools/{poolId}/registration-keys`) so agents can
   join the pool. Store the key securely; only its `keyPrefix` is retrievable later.
4. **Check pool status** — `GetTestDistributionAgentPoolStatus`
   (`GET /api/test-distribution/agent-pools/{poolId}/status`) to confirm agents are
   connected.

## Conventions & errors
- Errors are RFC 7807 `application/problem+json`.
- Pool config uses idempotent create-or-update PUT
  (`CreateOrUpdateTestDistributionAgentPool`) when you know the `poolId`.
- Revoke a key with `RevokeTestDistributionAgentPoolRegistrationKey` (DELETE) when rotating.
