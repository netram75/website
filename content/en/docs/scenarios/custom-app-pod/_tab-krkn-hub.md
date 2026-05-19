## krkn-hub

The custom app pod scenario is available through krkn-hub container:

```bash
docker run quay.io/krkn-chaos/krkn-hub \
  -e NAMESPACE_PATTERN="kube-system" \
  -e NAME_PATTERN="coredns.*" \
  -e KILL=1
```

### Environment Variables

| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `NAMESPACE_PATTERN` | Yes | - | Regex pattern for namespace |
| `NAME_PATTERN` | Yes | - | Regex pattern for pod names |
| `KILL` | No | 1 | Number of pods to terminate |
| `KRKN_POD_RECOVERY_TIME` | No | 120 | Recovery time in seconds |

### Example

```bash
docker run quay.io/krkn-chaos/krkn-hub \
  -e NAMESPACE_PATTERN="^production$" \
  -e NAME_PATTERN="api-server.*" \
  -e KILL=2
```
