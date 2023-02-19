# Docker-compose

- [x] Running Docker instance of Jaeger with elasticsearch storage type
- [x] grafana, prometheus with push gateway and alertmanager

## Added Fluent bit

1. helm repo add fluent https://fluent.github.io/helm-charts
2. helm upgrade --install fluent-bit fluent/fluent-bit
3. helm upgrade -f .\values.yaml fluent-bit fluent/fluent-bit