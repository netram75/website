---
title: VMI Network Chaos
description: Injects network faults such as packet loss, latency, and bandwidth limits on a target Virtual Machine Interface (VMI)
weight: 3
---

## Scenario Description

The VMI Network Chaos scenario injects network faults directly onto a Virtual Machine Interface (VMI) within an OpenShift Virtualization (KubeVirt) environment using Linux traffic control (`tc netem`). It supports packet loss, artificial latency, and bandwidth throttling. Use this scenario to validate how your application behaves under degraded network conditions when running on virtual machines.

## Prerequisites

- A running OpenShift cluster with KubeVirt installed
- krkn-chaos installed and configured
- Target VMI must be running and accessible

## Scenario Configuration

```yaml
vmi_network_chaos_scenario:
  namespace: ""         # namespace of the target VMI
  vmi_name: ""          # name of the target VMI
  interface: "eth0"     # network interface inside the VMI
  loss: 0               # packet loss percentage (0-100)
  latency: 0            # added latency in milliseconds
  bandwidth: ""         # bandwidth limit e.g. "100mbit"
  duration: 60          # chaos duration in seconds
  wait_timeout: 300
```

### Example

```yaml
vmi_network_chaos_scenario:
  namespace: "vmi-ns"
  vmi_name: "my-vmi-app"
  interface: "eth0"
  loss: 10
  latency: 200
  duration: 120
  wait_timeout: 600
```

## Scenario Execution

### krkn

```bash
python run_kraken.py --config config/vmi_network_chaos.yaml
```

### krkn-hub

```bash
krkn-hub run vmi-network-chaos \
  --namespace vmi-ns \
  --vmi-name my-vmi-app \
  --loss 10 \
  --latency 200 \
  --duration 120
```

### krknctl

```bash
krknctl run vmi-network-chaos \
  --namespace vmi-ns \
  --vmi-name my-vmi-app \
  --loss 10 \
  --latency 200 \
  --duration 120
```