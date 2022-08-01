# The broker

## :material-chef-hat: Configure the broker

Depending on the amount of documents you are dealing with, you may want to control max memory usage allowed (Xmx) for broker. 

By default, only 1GB is allocated for this resource :

```ini title="/config/env.properties"
...
# Broker Maximum memory allowed (Xmx)
BROKER_MAX_MEMORY=1G
```

If the campaign are involving a couple of millions of documents, increasing this value to 8GB or 16GB will definitely help increasing the performance rate of the migration.


## :material-laptop: Configure the UI port

The UI port is also subject to configuration. 

Fast2 application run on the 1789 port by default. To change this, add or update the parameters below:

```` markdown title="/config/application.properties" hl_lines="4"
...
# Remote broker port to use by the worker
# broker.port=1789
server.port=1789
````

Put the same value for these two properties.