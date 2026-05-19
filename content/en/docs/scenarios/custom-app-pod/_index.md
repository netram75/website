---
title: Custom App Pod Scenario
description: Test application resilience by terminating specific application pods using pattern matching
weight: 45
---

## Overview

The custom app pod scenario tests how your application responds when specific pods are terminated. Unlike generic pod kill scenarios, this scenario lets you target pods by name pattern, making it useful for testing behavior when specific components fail.

## Use Cases

- Test deployment rollout when specific pod instances are killed
- Verify application logic that depends on pod naming conventions
- Test multi-replica applications with specialized pod roles
- Validate monitoring and alerting for specific pod failures

## Scenario Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `namespace_pattern` | regex | Yes | - | Regex pattern to match target namespace |
| `name_pattern` | regex | Yes | - | Regex pattern to match pod names |
| `krkn_pod_recovery_time` | integer | No | 120 | Expected pod recovery time in seconds |
| `timeout` | integer | No | 180 | Timeout for pod termination operation in seconds |
| `kill` | integer | No | 1 | Number of pods to terminate matching the criteria |
| `node_label_selector` | string | No | - | Optional: Target pods only on nodes with matching labels |

## Examples

### Target coredns pods in kube-system

```yaml
- id: kill-coredns
  config:
    namespace_pattern: "^kube-system$"
    name_pattern: "coredns.*"
    krkn_pod_recovery_time: 120
    timeout: 180
    kill: 1
```

### Target custom application pods

```yaml
- id: kill-app-pods
  config:
    namespace_pattern: "^my-app$"
    name_pattern: "my-app-worker-.*"
    krkn_pod_recovery_time: 60
    kill: 2
```

## Pattern Matching

Both `namespace_pattern` and `name_pattern` use regex syntax:

- `.*` matches any characters (zero or more)
- `^` matches start of string
- `$` matches end of string

Examples:
- `^kube-system$` - exactly matches "kube-system"
- `coredns.*` - matches "coredns" followed by anything
