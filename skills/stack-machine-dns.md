---
name: Manage DNS records
description: Read and upsert DNS records in a StackMachine-managed domain zone.
api: graphql/stack-machine-schema.graphql
operations: [getAllDomains, upsertDNSRecord, getAllDNSRecords, deleteDNSRecord]
---

# Manage DNS records

Use the StackMachine GraphQL API at `https://api.stackmachine.com/graphql` with your `STACKMACHINE_API_KEY`.

## Steps

1. **Find the zone.** Call `getAllDomains` to locate the managed domain.
2. **List records.** Call `getAllDNSRecords` (paginate via Relay `first`/`after`, reading `pageInfo.endCursor`).
3. **Create/update a record.** Call the `upsertDNSRecord` mutation with the record type, name, value, and TTL.
4. **Delete.** Call `deleteDNSRecord` with the record's global id.

## Rules

- Lists are Relay connections — always follow `pageInfo.hasNextPage`.
- Pass a `clientMutationId` on mutations; inspect `errors[]` on failure.
