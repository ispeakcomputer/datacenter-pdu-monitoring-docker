### Commands that you may need for testing purposes

**Run the Docker Compose File**

docker-compose up -d 

Must be in the folder with the docker-compose.yml file -d means this will detach and run in the background

**Run telegraf with docker**

``` docker run -d --name=telegraf --net=graphana-net -v telegraf.conf telegraf ```

**Influx DB with docker**

``` docker run -d -p 8086:8086 -p 8083:8083 --net=graphana-net -v influxdb:/var/lib/influxdb -e INFLUXDB_ADMIN_ENABLED=true -e INFLUXDB_REPORTING_DISABLED=true -e INFLUXDB_ADMIN_USER=admin -e INFLUXDB_ADMIN_PASSWORD=admin influxdb ```

**Graphana with docker**

``` docker run -d -p 3000:3000 --net=graphana-net grafana/grafana ```

**influx queries for testing**

``` create db : curl -POST http://localhost:8086/query --data-urlencode "q=CREATE DATABASE mydb" ```

``` Show database: curl -G http://localhost:8086/query --data-urlencode "q=SHOW DATABASES" ```

``` Measurements: curl -G http://localhost:8086/query --data-urlencode "q=SHOW MEASUREMENTS ON mydb" ```

**run a single telegraf collection, outputing metrics to stdout. This checks Telegraf input plugin**
 
``` telegraf --config telegraf.conf –test

``` curl -G \'http://localhost:8086/query?db=telegraf\' --data-urlencode \'q=show series on "telegraf"\' ```

**deploy**

Create a user on the box you are moving to.

move grafana-storage folder and the telegraf.conf config to the folder where you put 
the docker-composer.yml then run 

``` docker-compose up ```
 

