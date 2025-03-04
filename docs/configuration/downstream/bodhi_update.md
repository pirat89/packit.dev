---
title: Bodhi updates
sidebar_position: 3
---

# `job: bodhi_update`

Create a new update in
[Fedora Bodhi](https://bodhi.fedoraproject.org) for successful
Koji build.
A Packit config file needs to be in the dist-git repository
to allow this job to be triggered.
Packit loads the config from the default dist-git branch (usually `rawhide`). Packit configs on other branches are ignored.

For now, the Bodhi update is created only for builds submitted by the Packit FAS user.
(See [`koji_build`](/docs/configuration/downstream/koji_build) job for more details on how to set this up.)
This is just for the early stage of this job, and
we can easily turn off that filter.
Let us know if you need this condition to be removed.

There is no UI provided by Packit for the job,
but it is visible across Fedora systems
like a manually created Bodhi update, and you can utilise
[Fedora Notifications](https://apps.fedoraproject.org/notifications/about)
to tweak the notifications settings.

For retriggering the job, see [our release guide](/docs/fedora-releases-guide).

:::tip Downstream configuration template

You can use our [downstream configuration template](/docs/configuration/downstream_configuration_template) 
for creating your Packit configuration in dist-git repository.

:::

:::tip Automate the setup

You can also use [packit dist-git init](/docs/cli/dist-git/init.md) CLI command to create your
Packit dist-git configuration.

:::

## Supported triggers

* **commit** - Packit uses the original action as a config trigger, so you need to use `commit` as a trigger.
  The real trigger is a successful Koji build (that was triggered from a commit).

## Required parameters

* **dist_git_branches** - the name of the dist-git branch(es) the build we want to use is coming from.
  You can also use the [aliases provided by Packit](/docs/configuration#aliases)
  to not need to change the config file when the new system version is released.


## Example
```yaml
issue_repository: https://github.com/my-username/packit-notifications

jobs:
- job: bodhi_update
  trigger: commit
  dist_git_branches:
    - fedora-branched # rawhide updates are created automatically
    - epel-8
```
