---
name: Attach and verify a custom domain
description: Attach a custom domain to a StackMachine app and verify ownership.
api: graphql/stack-machine-schema.graphql
operations: [upsertAppDomain, verifyAppDomain, getAllDomains, deleteAppDomain]
---

# Attach and verify a custom domain

Use the StackMachine GraphQL API at `https://api.stackmachine.com/graphql` with your `STACKMACHINE_API_KEY`.

## Steps

1. **Attach the domain.** Call the `upsertAppDomain` mutation with the app id and the hostname.
2. **Verify ownership.** Call `verifyAppDomain` to trigger/confirm DNS verification. If verification is pending, add the required DNS records first (see the Manage DNS records skill).
3. **List/confirm.** Call `getAllDomains` to confirm the domain is attached and verified.
4. **Remove (optional).** Call `deleteAppDomain` to detach a domain.

## Rules

- Pass a `clientMutationId` on each mutation for correlation and safe retries.
- Handle `errors[]` with `extensions.code` per `errors/stack-machine-error-codes.yml`.
