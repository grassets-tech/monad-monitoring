# Monad Monitoring


## Grafana dashboard for Monad Validator Testnet-2 (centralized setup).

It assumes that you already have Grafana/Prometheus/Node Exporter setup.

1. Add flag `--collector.textfile.directory=/path/to/dir` into the node exporter service
2. Copy sh script to the Monad Node server
3. Confgure crone to run script periodically


Kudos: https://github.com/staking4all

## Dont forget to congigure OTEL Collector

OTEL Collector usage
```
Install & Start OTEL Collector
curl -fsSL -o /tmp/otelcol_0.125.0_linux_amd64.deb https://github.com/open-telemetry/opentelemetry-collector-releases/releases/download/v0.125.0/otelcol_0.125.0_linux_amd64.deb
dpkg -i /tmp/otelcol_0.125.0_linux_amd64.deb
cp /opt/monad/scripts/otel-config.yaml /etc/otelcol/config.yaml
```

```
systemctl start otelcol
```

In the latest systemd file, support was added for the OTEL collector. Through this, you will be able to see all the relevant Monad-specific metrics (available at 0.0.0.0:8889/metrics), while also pushing metrics to a Category Labs OTLP endpoint so that the CL team can help with debugging if any issues arise.

## Add otel-collector in the Prometheus yml

vi prometheus.yml
```
  - job_name: 'otel-collector' # Monad
    scrape_interval: 5s
    static_configs:
      - targets: ['134.119.187.253:8889']
```

Restart prometheus
```
sudo service prometheus restart
```
