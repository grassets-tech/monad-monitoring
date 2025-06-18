# Monad Monitoring


Grafana dashboard for Monad Validator Testnet-2 (centralized setup).

It assumes that you already have Grafana/Prometheus/Node Exporter setup.

1. Add flag `--collector.textfile.directory=/path/to/dir` into the node exporter service
2. Copy sh script to the Monad Node server
3. Confgure crone to run script periodically


Kudos: https://github.com/staking4all
