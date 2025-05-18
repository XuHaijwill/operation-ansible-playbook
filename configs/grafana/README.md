# CPU Monitoring
```yml
groups:
  - name: CPU High Usage Alerts
    rules:
      - alert: HighCPUUsage
        expr: 100 - (avg by (instance) (rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100) > 80
        for: 2m
        labels:
          severity: warning
        annotations:
          summary: "Instance {{ $labels.instance }} CPU usage is high"
          description: "CPU usage is above 80% (current value: {{ $value }}%) for more than 2 minutes."
```