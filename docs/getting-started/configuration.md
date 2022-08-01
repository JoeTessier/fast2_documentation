---
# weight : 15

title : Configuration
tags: ["configuration","broker","worker","ports"]

---

Once Fast2 is installed, several components can be easily configured to adapt the software as much as your constraints might require.

Among all these components, you can find : 

- the [broker](#configure-the-broker)
- the [worker(s)](#configure-the-workers)
- the [UI port](#configure-the-ui-port)
- the [background database](#configure-the-background-database)
- the [dashboard add-on](#configure-the-dashboard-add-on)

## :material-chef-hat: Configure the broker
Depending on the amount of documents you are dealing with, you may want to control max memory usage allowed (Xmx) for broker. 

The `<FAST2_HOME>/config/env.properties` file is configured by default to 1GB for this resource :

```ini
...
# Broker Maximum memory allowed (Xmx)
BROKER_MAX_MEMORY=1G
```

If the campaign are involving a couple of millions of documents, increasing this value to 8GB or 16GB will help increasing the performance rate of the migration.



##  :material-database-outline: Configure the background database

???+ note
    Although Fast2 was first shipped with an embedded Elasticsearch database, the ETL has switched to OpenSearch as of its [v2.5.0](/release-note/release-note-2-5-0/). <br/>However the configuration of both these databases are quite similar. This is why we will refer to them as the "background database".

The database communicates with the broker via the port 1790 (as illustrated in the [architecture section](/documentation/presentation/#architecture)).

For more details on this component such as configuration, refer to [dedicated section](/documentation/elasticsearch).
