# Dashboards


!!! Warning

    Prior to the v2.5, Fast2 was relying on Kibana for data vizualisation. This component has been dropped in favor of OpenSearch dashboards. 

    However the configuration of these tools are very close (if not identical). 




## :material-chart-bar: Configure the dashboards

Fast2 does not embed any dashboard by default. However, you can get the add-on through the same portal you downloaded the Fast2 binaries. Unzip the package at the root of Fast2 installation folder.

This hierarchy will make Fast2 automatically start your dashboard. 

You will still be able to disable the dashboard add-on: 

=== "v2.4-"

    ```ini title="./config/application.properties"
    broker.kibana.embedded.enabled=false
    ```

=== "v2.6+"

    ```ini title="./config/application.properties" hl_lines="2" linenums="26"
    # Set to false to disable start of broker's embedded Opensearch Dashboards
    # broker.dashboards.embedded.enabled=true
    # broker.dashboards.embedded.port=1791
    # broker.dashboards.embedded.maxRetries=200
    ```

The dashboard only communicates with the database (as illustrated in the [architecture section](/documentation/presentation/#architecture)), and is accessible via the port 1791.

> Not having integrated the dashboard component will not prevent you from starting Fast2 and running it properly.

The ports related to dashboard usage can be updated as well, based on the knowledge accessible [here](/documentation/advanced/kibana#kibana-ports).

For basic understanding and usage of this component, refer to [dedicated section](/documentation/advanced/kibana/).
For advanced configuration and handling, head out to [the advanced section](/documentation/advanced/kibana_next_level/).

