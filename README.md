# Spread tests to skip in snapd CI

This repo contains which tests should be currently skipped in spread in the snapd CI.

## How to add a new test to skip

Add a new yaml file called `skipped_test${i}.yaml` (where `i` is a positive integer) in the folder `skip` that respects the following schema:

```yaml
type: object
properties:
   spread-task:
       type: string
       description: 'Name of spread task as defined by spread (ex: tests/main/ack)'
   spread-system:
       type: string
       description: 'Name of spread system (if not specified, then task will be skipped on all systems)'
   spread-backend:
       type: string
       description: 'Name of spread backend (if not specified, then task will be skipped on all backends)'
   skip-until:
       type: string
       format: date
       description: 'yyyy-MM-dd'
   skip-reason:
       type: string
       description: 'Reason why test can be skipped (include Jira card if relevant)'
required:
   - spread-task
   - skip-until
   - skip-reason
```

## Examples

To skip `tests/main/ack` on all systems until Jan 21, 2027, add the file `skip/skipped_test0.yaml` with the following contents:

```yaml
spread-task: tests/main/ack
skip-until: 2027-01-21
skip-reason: Requires a new release from Team X
```

To skip `tests/main/ack` only on Noble until Jan 21, 2027, add the file `skip/skipped_test0.yaml` with the following contents:

```yaml
spread-task: tests/main/ack
spread-system: ubuntu-24.04-64
skip-until: 2027-01-21
skip-reason: Requires a new release from Team X
```

To skip `tests/main/ack` on all systems that run on openstack until Jan 21, 2027, add the file `skip/skipped_test0.yaml` with the following contents:

```yaml
spread-task: tests/main/ack
spread-backend: openstack
skip-until: 2027-01-21
skip-reason: Requires a new release from Team X
```

To skip `tests/main/ack` only on Noble running on openstack until Jan 21, 2027, add the file `skip/skipped_test0.yaml` with the following contents:

```yaml
spread-task: tests/main/ack
spread-system: ubuntu-24.04-64
spread-backend: openstack
skip-until: 2027-01-21
skip-reason: Requires a new release from Team X
```
