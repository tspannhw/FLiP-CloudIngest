# FLiP-CloudIngest

Ingest real-time to any cloud


## Reference

* https://github.com/tspannhw/FLiP-SQL


## Ingest NVIDIA XAVIER Data into Cloud Postgresql

```

bin/pulsar-client consume "persistent://public/default/iotjetsonjson" -s "iotjetsonjson-reader" -n 0
bin/pulsar-admin schemas get persistent://public/default/iotjetsonjson

bin/pulsar-admin sinks create --archive ./connectors/pulsar-io-jdbc-postgres-2.8.0.nar --inputs iotjetsonjson --name iotjetsonjson-postgres-jdbc-sink --sink-config-file conf/iotjetsonjsonpgsql.yml --parallelism 1
bin/pulsar-admin sinks list --tenant public --namespace default
bin/pulsar-admin sinks get --tenant public --namespace default --name iotjetsonjson-postgres-jdbc-sink 
bin/pulsar-admin sinks status --tenant public --namespace default --name iotjetsonjson-postgres-jdbc-sink 


```


## Ingest Stocks REST into JDBC

```

bin/pulsar-daemon start websocket
bin/pulsar-admin schemas delete stocks
bin/pulsar-admin schemas delete stocks-partition-0
bin/pulsar-admin schemas delete persistent://public/default/stocks-partition-0
bin/pulsar-admin schemas delete persistent://public/default/stocks
bin/pulsar-admin topics list public/default
bin/pulsar-admin topics create persistent://public/default/stocks
bin/pulsar-admin sinks get --tenant public --namespace default --name stocks-postgres-jdbc-sink 


```

