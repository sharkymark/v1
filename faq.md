---
name: Coder v1 FAQ
description: FAQ using Coder v1
tags: [FAQ, v1]
---

# v1 FAQ
- [Build log says not enough resources](#build-log-says-not-enough-resources)
- [Configure seccompProfile settings for a workspace container](#seccompprofile-settings)

# Build log says not enough resources
Administrators can limit the computing resources consumed with resource quotas which are defined at the Organization-level.

Here is a screenshot of the Organization/Edit UI where quotas are defined. These are the maximum compute per user and there is no limit to the number of workspaces a user can build as long as these aggregate quotas are not exceeded.

![configuring resource quotas](./assets/org-resource-quotas.png)

Here is a screenshot of the build log error when a user exceeds their quota.

![build log exceeding quota](./assets/resource-quota-exceeded.png)

Here is a screenshot from the Create Workspace UI if a quota is exceeded.

![create workspace quota exceeded](./assets/create-workspace-quota-exceeded.png)

# seccompProfile settings
You can set a site-wide template in Manage/Admin/Templates to allow custom annotations. If you are using workspace templates, you can add the annotation in the template, or within the site-wide template.
- Adjust the site-wide template to set workspace.specs.kubernetes.annotations.policy: write in the site-wide template policy (by default, templates aren’t allowed to set custom annotations) https://<your Access URL>/admin?tab=templates
```yaml
version: "0.2"
workspace:
    configure:
        start:
            policy: write
    dev-urls:
        policy: write
    specs:
        kubernetes:
            annotations:
                policy: write
```
- Add the annotation in the workspace template
```yaml
version: 0.2
workspace:
  type: kubernetes
  specs:
    kubernetes:
      image:
        value: gcr.io/coder-dogfood/master/coder-dev-ubuntu
      container-based-vm:
        value: false
      cpu:
        value: 2
      memory:
        value: 4
      disk:
        value: 16
      annotations:
        value:
          - key: container.seccomp.security.alpha.kubernetes.io/workspace
            value: runtime/default
```
- Or add in the site-wide template if users will only build workspaces from images and not workspace templates.
```yaml
version: "0.2"
workspace:
    configure:
        start:
            policy: write
    dev-urls:
        policy: write
    specs:
        kubernetes:
            annotations:
                value:
                  - key: seccomp.security.alpha.kubernetes.io/pod
                    value: runtime/default                       
```

## Resources
