---
name: Coder v1 FAQ
description: FAQ using Coder v1
tags: [FAQ, v1]
---

# v1 FAQ
- [Build log says not enough resources](#build-log-says-not-enough-resources)

# Build log says not enough resources
Administrators can limit the computing resources consumed with resource quotas which are defined at the Organization-level.

Here is a screenshot of the Organization/Edit UI where quotas are defined. These are the maximum compute per user and there is no limit to the number of workspaces a user can build as long as these aggregate quotas are not exceeded.

![configuring resource quotas](./assets/org-resource-quotas.png)

Here is a screenshot of the build log error when a user exceeds their quota.

![build log exceeding quota](./assets/resource-quota-exceeded.png)

Here is a screenshot from the Create Workspace UI if a quota is exceeded.

![create workspace quota exceeded](./assets/create-workspace-quota-exceeded.png)

## Resources
