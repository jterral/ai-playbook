---
name: bruno-e2e
description: Run Bruno e2e tests interactively
user-invocable: true
tools: [bash]
---

## Prerequisites

- **Bruno CLI**: Must be installed (`bru` command available)
- **Bruno project**: Project must have `.bruno/` directory with environments and requests
- **Environment setup**: `.bruno/environments/` must contain at least one environment file
- **Access**: Appropriate credentials for the target environment

## Steps

1. List available environments from `.bruno/environments/`
2. Ask the user which environment to use
3. List available requests from `.bruno/` recursively
4. Ask: "Run all requests or a specific one?"
   - If specific, show the list and ask which one
5. Run `bru run {target} --env {environment} --env-global {global-env}`
6. Report passed/failed requests with details on failures
