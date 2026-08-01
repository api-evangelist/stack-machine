---
name: Deploy and publish an app
description: Deploy a StackMachine app from a connected repo via autobuild, watch the build, and publish the resulting version.
api: graphql/stack-machine-schema.graphql
operations: [deployViaAutobuild, autobuildDeploymentStatus, publishDeployApp, getDeployApp]
---

# Deploy and publish an app

Use the StackMachine GraphQL API at `https://api.stackmachine.com/graphql`. Authenticate with your API key in `STACKMACHINE_API_KEY` (see `authentication/stack-machine-authentication.yml`).

## Steps

1. **Kick off the build.** Call the `deployViaAutobuild` mutation with the target app/repo inputs. Pass a stable `clientMutationId` (and an SDK idempotency key) so a retried deploy is not duplicated — see `conventions/stack-machine-conventions.yml`.
2. **Watch the build.** Poll `autobuildDeploymentStatus` (query) with the returned build id, or subscribe to the `autobuildDeployment` / `streamLogs` subscription for live progress.
3. **Publish the version.** Once the build succeeds, call `publishDeployApp` to make the new version active.
4. **Confirm.** Call `getDeployApp` (by id or name) and check the active version.

## Rules

- Mutations are Relay-style: read the returned payload's `clientMutationId` to correlate.
- On error, inspect the top-level `errors[]` array and `extensions.code` (`UNAUTHENTICATED`, `FORBIDDEN`, `BAD_USER_INPUT`) — see `errors/stack-machine-error-codes.yml`.
