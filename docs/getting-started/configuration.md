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

## Configure the broker
Depending on the amount of documents you are dealing with, you may want to control max memory usage allowed (Xmx) for broker. 

The `<FAST2_HOME>/config/env.properties` file is configured by default to 1GB for this resource :

```ini
...
# Broker Maximum memory allowed (Xmx)
BROKER_MAX_MEMORY=1G
```

If the campaign are involving a couple of millions of documents, increasing this value to 8GB or 16GB will help increasing the performance rate of the migration.

## Configure the worker(s)
Depending on the amount of documents and the number of tasks you are dealing with, you may want to control max memory usage allowed (Xmx) for worker.

The default setting is 1GB for this resource:
```` markdown title="./config/env.properties"
...
# Worker Maximum memory allowed (Xmx)
WORKER_MAX_MEMORY=1G
````

Keep in mind that this property is designed for workers started from the binary `start-worker.sh|.bat`. If you intend to target the embedded worker, go to `./config/application.properties` instead:
```ini
...
# Broker embedded worker max memory
broker.embeddedworker.max.memory=1G
```

For more information about the worker, head out to the [dedicated section](/documentation/advanced/workers/).

## Configure the UI port

Fast2 application run on the 1789 port by default. To change this, add or update the parameters below:

```` markdown title="/config/application.properties" hl_lines="4"
...
# Remote broker port to use by the worker
# broker.port=1789
server.port=1789
````

Put the same value for these two properties.

## Configure the background database

???+ note
    Although Fast2 was first shipped with an embedded Elasticsearch database, the ETL has switched to OpenSearch as of its [v2.5.0](/release-note/release-note-2-5-0/). <br/>However the configuration of both these databases are quite similar. This is why we will refer to them as the "background database".

The database communicates with the broker via the port 1790 (as illustrated in the [architecture section](/documentation/presentation/#architecture)).

For more details on this component such as configuration, refer to [dedicated section](/documentation/elasticsearch).


## Configure the dashboard add-on

> Although Fast2 was first shipped with a Kibana add-on, the ETL has switched to OpenSearch dashboard as of its [v2.5.0](/release-note/release-note-2-5-0/). <br/>However the configuration of both these vizualisation tools are quite similar. This is why we will refer to them as the "dashboard".

Fast2 does not embed any dashboard by default. However, you can get the add-on through the same portal you downloaded the Fast2 binaries. Unzip the package at the root of Fast2 installation folder.

This hierarchy will make Fast2 automatically start your dashboard. 

You will still be able to disable Kibana by updating the `config/application.properties` file : 
```ini
...
broker.kibana.embedded.enabled=false
```

The dashboard only communicates with the database (as illustrated in the [architecture section](/documentation/presentation/#architecture)), and is accessible via the port 1791.

> Not having integrated the dashboard component will not prevent you from starting Fast2 and running it properly.

The ports related to dashboard usage can be updated as well, based on the knowledge accessible [here](/documentation/advanced/kibana#kibana-ports).

For basic understanding and usage of this component, refer to [dedicated section](/documentation/advanced/kibana/).
For advanced configuration and handling, head out to [the advanced section](/documentation/advanced/kibana_next_level/).

