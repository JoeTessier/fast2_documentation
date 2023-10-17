# Is this page still useful ??

<!--

Fast2 is migration tool specifically oriented for documents and annotations transfers. It embeds a workflow engine specially designed for mass migrations of contents and data.

Between the different steps retrieving the data from any storage system (Data Warehouse, ECM Engine, Excel...), the tool integrates transformation and conversion facilities to give them even more values. Whether functional or business rules need to be dealt with, Fast2 can be adapted to edge-cases needs.

And eventually, your assets will be injected into a newer ECM system, which better meets your requirements. This last phase relies on a constantly growing list of connectors, offering either support of the newest document storage systems or higher-complexity levels of features already integrated.

Data traceability is an important aspect in any type of migration. To tackle this migration challenge, Fast2 embeds a **database**, where all data passing or created through Fast2 will be stored. A **dashboard add-on** (not required for standard utilisation of the migration tool) can be set up on your environment, for a more complete solution to monitor your migrations and make sure everything is compliant, as you expected.

## :material-vector-square-edit: Conception

Fast2 is based on Java. To turn it into a web application we use the famous framework **GWT**. Even if it's not longer supported by Google it offers many benefits :

- The code generated by GWT supports all major browsers
- Rich and complete libraries to build complexe user interfaces
- A solid HTML 5 foundation, independent of fashionable and unsustainable JavaScript frameworks
- Full Java without any Javascript code allowing better application maintenance
- Easy debugging mode designed for developers
- Communication with servers through asynchronous calls
- A history management system on the browser

Precisely, we used the [MVP](http://www.gwtproject.org/articles/mvp-architecture.html) (Mode-View-Presenter) pattern to build the Fast2 v2. Besides, the Google implementation of this pattern is named Activity & Places (A&P). As you can guess, the *Activity* takes the role of the *Presenter*. The *Place* will be the *View*. A place is considered as a web page and is therefore in the history of your navigator.

For the design of widgets we used the [uiBinder](http://www.gwtproject.org/doc/latest/DevGuideUiBinder.html) tool to map XML objects to java objects. The scheme below is here to show the different place which a user can visit.

![My image title](https://dummyimage.com/600x400/){ loading=lazy }


- Design Place : Workflow management (add tasks, configure them...)
- Run Place : Run your map and see performance statistics
- Explorer Place : Look into a specific task to see what happend inside
- Configuration Place : Manage your maps, campaigns, shared objects and workers
- Monitor Place : Redirect you to Kibana URL linked to the Fast2's ElasticSearch instance

## :material-angle-obtuse: Architecture
Fast2 is accessible from the port 1789. It can be easily modify from the [configuration files](../configuration#fast2-port).

Actions performed by users are transmitted to the broker through a REST API. A dedicated worker is always present for the broker. However, you can add many workers as you wish depending on your needs. New workers will communicate to the broker through another API to be synchronised between them.

When workers have done their job, the rendering is shared with the broker who hastens to store everything in ElasticSearch to maintain maximum traceability.

A Kibana instance (accessible from the port 5601 by default) is connected to ElasticSearch to build reports of migration.

![documentation/product-architecture.png](https://dummyimage.com/600x400/){ loading=lazy }


### :material-database-outline: Internal database

Known as the first product of the suite ELK, Elasticsearch is a powerful noSQL database. It uses directly document metadata rather than schema or tables. One of the major benefits is its open-source system allowing real-time search and analysis of complex system. Having noSQL structure allows you to have a scalable and even more snappy product.

With a documented REST API coupled to our broker, we built a whole system able to store, trace and analyze your data.

More details are available in the [dedicated section](../elasticsearch).

### :material-chart-bar: Dashboards

Kibana is like the fifth wheel in the cart, to be precise the third since is the last product of the ELK suite. It will fill the missing ElasticSearch features like visualization and data management. You will have the ability to build histograms and many others types of graphs. This is the perfect tool for creating relevant reports of a migration. Your data will no longer hold any secrets from you. -->