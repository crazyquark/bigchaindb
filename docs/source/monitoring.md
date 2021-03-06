# Monitoring

BigchainDB uses [StatsD](https://github.com/etsy/statsd) for monitoring. We require some additional infrastructure to take full advantage of its functionality:

* an agent to listen for metrics: [Telegraf](https://github.com/influxdata/telegraf),
* a time-series database: [InfluxDB](https://influxdata.com/time-series-platform/influxdb/), and
* a frontend to display analytics: [Grafana](http://grafana.org/).

We put each of those inside its own Docker container. The whole system is illustrated below.

![BigchainDB monitoring system diagram: Application metrics flow from servers running BigchainDB to Telegraf to InfluxDB to Grafana](./_static/monitoring_system_diagram.png)

For ease of use, we've created a Docker [_Compose file_](https://docs.docker.com/compose/compose-file/) (named `docker-compose-monitor.yml`) to define the monitoring system setup. To use it, just go to to the top `bigchaindb` directory and run:
```text
$ docker-compose -f docker-compose-monitor.yml build
$ docker-compose -f docker-compose-monitor.yml up
```

then point a browser tab to:

[http://localhost:3000/dashboard/script/bigchaindb_dashboard.js](http://localhost:3000/dashboard/script/bigchaindb_dashboard.js)

The login and password are `admin` by default. If BigchainDB is running and processing transactions, you should see analytics—if not, [start BigchainDB](installing.html#run-bigchaindb) and load some test transactions:
```text
$ bigchaindb-benchmark load
```

then refresh the page after a few seconds.

If you're not interested in monitoring, don't worry: BigchainDB will function just fine without any monitoring setup.

Feel free to modify the [custom Grafana dashboard](https://github.com/rhsimplex/grafana-bigchaindb-docker/blob/master/bigchaindb_dashboard.js) to your liking!