---
name: Manage app secrets and env vars
description: Set, read, and delete an app's secrets / environment variables on StackMachine.
api: graphql/stack-machine-schema.graphql
operations: [upsertAppSecret, getAppSecrets, deleteAppSecret]
---

# Manage app secrets and env vars

Use the StackMachine GraphQL API at `https://api.stackmachine.com/graphql` with your `STACKMACHINE_API_KEY`.

## Steps

1. **List current secrets.** Call `getAppSecrets` for the app.
2. **Set a secret.** Call the `upsertAppSecret` mutation with the app id, key, and value.
3. **Delete a secret.** Call `deleteAppSecret` with the app id and key.

## Rules

- Never log secret values. Treat the API key and secret values as sensitive.
- Pass a `clientMutationId` on mutations for safe retries; handle `errors[]` with `extensions.code` per `errors/stack-machine-error-codes.yml`.
