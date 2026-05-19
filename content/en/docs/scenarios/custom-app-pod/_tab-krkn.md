## krkn

The custom app pod scenario is available in krkn through the plugin-based scenario system.

### Scenario File

Example scenario file: [customapp_pod.yml](https://github.com/krkn-chaos/krkn/blob/main/scenarios/openshift/customapp_pod.yml)

### Basic Usage

```yaml
- id: kill-custom-pods
  config:
    namespace_pattern: "my-namespace"
    name_pattern: "my-app.*"
    krkn_pod_recovery_time: 120
    timeout: 180
    kill: 1
```

### Configuration in config.yaml

Add to your main krkn config:

```yaml
scenarios:
  - name: custom-app-scenario
    file: scenarios/openshift/customapp_pod.yml
    enabled: true
```
