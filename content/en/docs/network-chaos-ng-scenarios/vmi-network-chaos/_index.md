---
title: VMI Network Chaos
description: Injects network faults such as packet loss, latency, and bandwidth limits on a target Virtual Machine Interface (VMI)
weight: 4
---

## Scenario Description

The VMI Network Chaos scenario injects network faults directly on a target Virtual Machine Instance running on OpenShift Virtualization (KubeVirt) using Linux traffic control (`tc netem`). It supports packet loss, artificial latency, and bandwidth throttling. Use this scenario to validate how your virtualized workloads behave under degraded network conditions.

## Prerequisites

- A running OpenShift cluster with OpenShift Virtualization installed
- krkn-chaos installed and configured
- Target VMI must be running and accessible

## Scenario Configuration

```yaml
vmi_network_chaos_scenario:
  namespace: "default"     # namespace of the target VMI
  vmi_name: ""             # name of the target VMI
  interface: "eth0"        # network interface inside the VMI
  loss: 0                  # packet loss percentage (0-100)
  latency: 0               # added latency in milliseconds
  bandwidth: ""            # bandwidth limit e.g. "100mbit"
  duration: 60             # chaos duration in seconds
  wait_timeout: 300
```

### Example

```yaml
vmi_network_chaos_scenario:
  namespace: "production"
  vmi_name: "web-server-vm"
  interface: "eth0"
  loss: 5
  latency: 100
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
  --namespace production \
  --vmi-name web-server-vm \
  --loss 5 \
  --latency 100 \
  --duration 120
```

### krknctl

```bash
krknctl run vmi-network-chaos \
  --namespace production \
  --vmi-name web-server-vm \
  --loss 5 \
  --latency 100 \
  --duration 120
```