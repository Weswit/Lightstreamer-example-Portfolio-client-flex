# Lightstreamer - Portfolio Demo - Flex Client #

<!-- START DESCRIPTION lightstreamer-example-portfolio-client-flex -->

This project contains a simple Flex application fed through a Lightstreamer connection based on [Lightstreamer - Portfolio Demo - Java Adapter](https://github.com/Weswit/Lightstreamer-example-Portfolio-adapter-java); the demo is written for Flex 4 SDK.

[![screenshot](screen_flexportfolio_large.png)](http://demos.lightstreamer.com/Flex_PortfolioDemo/)<br>
An online demonstration is hosted on our servers at:[http://demos.lightstreamer.com/Flex_PortfolioDemo/](http://demos.lightstreamer.com/Flex_PortfolioDemo/)<br>

This is a Flex version of the [Portfolio Demo](https://github.com/Weswit/Lightstreamer-example-Portfolio-client-javascript#portfolio-demo), where a list of sent orders is kept and updated with the status of the request.<br>

This app uses the <b>Flex Client API for Lightstreamer</b> to handle the communications with Lightstreamer Server and uses the <b>Flex DataGrid</b> to display the real-time data.<br>

The left table shows the automatic binding of a Lightstreamer data table configured to exploit "two-level push" with a Flex widget (a DataGrid). You can sort on any columns and drag the columns around.<br>

Using the form to the right, you can buy or sell a stock.<br>
Clicking the "Random Orders" button, 20 random orders are placed in batch mode. Orders are placed through the [LSClient.SendMessage](http://www.lightstreamer.com/docs/client_flex_asdoc/com/lightstreamer/as_client/LSClient.html#sendMessage()) method.<br>

The DataGrid, below the orders form, mantains a list of executed orders and their statuses (PROCESSING, PROCESSED, ABORTED or ERROR). Such statuses are received by the demo code by listening for [SendMessageAbortEvent](http://www.lightstreamer.com/docs/client_flex_asdoc/com/lightstreamer/as_client/events/SendMessageAbortEvent.html), [SendMessageErrorEvent](http://www.lightstreamer.com/docs/client_flex_asdoc/com/lightstreamer/as_client/events/SendMessageErrorEvent.html), and [SendMessageProcessedEvent](http://www.lightstreamer.com/docs/client_flex_asdoc/com/lightstreamer/as_client/events/SendMessageProcessedEvent.html) events and then placed in an ArrayCollection that is in turn bound to the DataGrid.<br>

This portfolio is shared among all the connected users, so you can connect to this demo from different machines (or try at least different browsers on the same machine), then submit orders from one browser and see the updates displayed on another browser. The same portfolio is also shared among the various versions of the demo (Flex and HTML).

Tables involved:
* A [VisualTable](http://www.lightstreamer.com/docs/client_flex_asdoc/com/lightstreamer/as_client/VisualTable.html) containing 1 item subscribed to in <b>COMMAND</b> mode. Each added row automatically provokes an underlying subscription to a sub-item in <b>MERGE</b> mode, to get the real-time price for that specific stock from another feed (the same as the [Stock-List Demos](https://github.com/Weswit/Lightstreamer-example-Stocklist-client-javascript)). When a row is deleted, the underlying sub-item is automatically unsubscribed from.

<!-- END DESCRIPTION lightstreamer-example-portfolio-client-flex -->

# Build #

If you want to skip the build process of this demo please note that in the [deploy release](https://github.com/Weswit/Lightstreamer-example-Portfolio-client-flex/releases) of this project you can find the "deploy.zip" file that contains a ready-made deployment resource for Lightstreamer's internal Web Server.<br>

Otherwise, in order to proceed with the build process of this demo, this project includes the following sub-folders:
* /src<br>
  Contains the sources to build the Flex application. The code is based on Flex 4 SDK.

* /lib<br>
  Should contain the Lightstreamer library to be used for the build process.<br>
  Please, download the [latest Lightstreamer distribution](http://www.lightstreamer.com/download) and copy the Lightstreamer_as_client.swc file from the Lightstreamer Flex Client SDK (that is located under the /DOCS-SDKs/sdk_client_flex/lib folder) into this folder of the project.


# Deploy #

The "deploy" folder contains a deployment image of the demo, which includes a container page and other web resources. If you have not skipped the previous step you have to complete this with the built Flex application (Flex4PortfolioDemo.swf) and the swfobject.js version 2.2 file from [SWFObject 2](http://code.google.com/p/swfobject/downloads/list).
Otherwise get the ready-made "Flex4_PortfolioDemo" deploy folder from "deploy.zip" of the [latest release](https://github.com/Weswit/Lightstreamer-example-Portfolio-client-flex/releases) of this project.

This deployment image is ready to be deployed under Lightstreamer's internal Web Server, by copying all the contents into the "pages" directory.<br>

By the current configuration, the demo tries to access Lightstreamer Server by using the protocol, hostname and port from which the "index.html" page was requested; in other words, the demo assumes that the static resources are deployed inside Lightstreamer Server.<br>
In order to deploy the demo static resources on an external Web Server, some changes are needed on the deployment image before or after copying it into the Web Server folders.
The configuration of the hostname and port (and maybe the protocol) to be used to access Lightstreamer Server should be changed. The configuration lines can be easily found at the beginning of the "index.html" file and can be modified manually, without the need for a recompilation.<br>
Then, in order to allow the page to get resources from a different server, the Web Server address has to be included in the "/crossdomain.xml" file deployed under Lightstreamer Server.
See the <flex_crossdomain_enabled> element in the Server configuration file for details.

Anyway the [PORTFOLIO_ADAPTER](https://github.com/Weswit/Lightstreamer-example-Portfolio-adapter-java), [QUOTE_ADAPTER](https://github.com/Weswit/Lightstreamer-example-Stocklist-adapter-java), and [PortfolioMetadataAdapter](https://github.com/Weswit/Lightstreamer-example-Portfolio-adapter-java) have to be deployed in your local Lightstreamer server instance. The factory configuration of Lightstreamer server already provides this adapter deployed.<br>
The demos are now ready to be launched.

# See Also #

## Lightstreamer Adapters Needed by This Demo Client ##

<!-- START RELATED_ENTRIES -->
* [Lightstreamer - Portfolio Demo - Java Adapter](https://github.com/Weswit/Lightstreamer-example-Portfolio-adapter-java)
* [Lightstreamer - Stock-List Demo - Java Adapter](https://github.com/Weswit/Lightstreamer-example-Stocklist-adapter-java)

<!-- END RELATED_ENTRIES -->

## Related Projects ##

* [Lightstreamer - Portfolio Demos - HTML Clients](https://github.com/Weswit/Lightstreamer-example-Portfolio-client-javascript)
* [Lightstreamer - Stock-List Demos - Flex Clients](https://github.com/Weswit/Lightstreamer-example-StockList-client-flex)

# Lightstreamer Compatibility Notes #

- Compatible with Lightstreamer Flex Client API version 2.1 or newer.
- For Lightstreamer Allegro (+ Flex Client API support), Presto, Vivace.
