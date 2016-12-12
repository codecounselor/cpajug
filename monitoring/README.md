# Usage

1. Install docker on your system
2. Create a `/mnt` directory, this is where the docker volumes will be created.
3. Run `docker-compose up` to pull the images from Docker Hub and start them all.

# Endpoints
Once the containers are running you can access the following:

1. Grafana (Dashboards): http://localhost:3000
1. InfluxDB Admin: http://localhost:8083
1. HTML Exporter: http://loalhost:8080

Note: The port mappings are defined in docker-compose.yml and can be modified if necessary.

# InfluxDB Line Protocol 

```
curl -i -XPOST "http://influxdb:8086/write?db=jug" --data-binary 'weather,
host=$HOST,location=us-midwest temperature=82 1465839830100400200'
```

# Telegraf StatsD 

`echo "weather.report,host=$HOST,location=us-midwest,attr=temperature:82|g" | nc -w 1 -u influxdb 8125`

# Some Influx Queries

select sum(count), max(max) from /window/ where time > now() - 2d group by time(1d)
