## krknctl

Run the custom app pod scenario with krknctl:

```bash
krknctl scenario run custom-app-pod \
  --namespace-pattern "^kube-system$" \
  --name-pattern "coredns.*" \
  --kill 1
```

### Parameters

| Flag | Required | Description |
|------|----------|-------------|
| `--namespace-pattern` | Yes | Regex pattern for target namespace |
| `--name-pattern` | Yes | Regex pattern for pod names |
| `--kill` | No | Number of pods to kill (default: 1) |
| `--krkn-pod-recovery-time` | No | Expected recovery time in seconds |

### Example

```bash
krknctl scenario run custom-app-pod \
  --namespace-pattern "production" \
  --name-pattern "worker-.*" \
  --kill 2
```
