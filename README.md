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
