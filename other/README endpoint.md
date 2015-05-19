# Akana Professional Services Version Endpoint Selector

## Installation
- You must install the pso Version Endpoint Selector
    + unzip the com.akana.pso.endpointselector_7.2.zip into the /sm70 directory.
    + stop all ND nodes
    + Run the configurator in update mode for all ND instances:
        * Run this command, depending on your environment:
            - Windows: `<Gateway base dir>\sm70\bin\startup.bat configurator -Dsilent=true -DdeploymentName=Standalone -Dproperties=C:\\myprops.properties`
            - UNIX/Linux: `<Gateway base dir>/sm70/bin/startup.sh configurator -Dsilent=true -Dproperties=/export/home/username/myprops.properties`
            - The myprops.propertis path must be the fully qualified path, and the file contents will look like:
            ```
            container.instance.name=<instance name, e.g. ND>
            wizard.mode=update
            ```
    + Using the SOA Admin Console, install the following feature in each ND container:
        * Akana Software HTTP Endpoint Selector Accept Header Version 
    + Restart all ND containers.

## Validation
Validation is done by first creating and hosting a service that has an output serialization of something like 'applicaion/json; v=3'.

Once a new service is hosted, it can be invoked by an outside consumer.  The consumer would need to send in a request like the following:

  ```
    GET /credit-cards/accounts/1234 HTTP/1.1
    Accept-Encoding: gzip,deflate
    Accept: application/json; v=3
    Host: enord-macbook-pro.local:9920
    Connection: Keep-Alive
    User-Agent: Apache-HttpClient/4.1.1 (java 1.5)
  ```

This feature will be invoked to verify all loaded services and only select the proper endpoint based off of the output serialization match the Accept header passed in on the original request.

You can validate the proper endpoint has been properly selected by viewing the logs.  Your logs will look in this manner:

```
      [7] VirtualHostEndpointSelector.select()
      [7] HttpAcceptHeaderEndpointSelector.select()
      [8] In Http Method: GET
      [8] Performing a match on endpoints based on the Accept Header 'v' parameter..
      [8] Accept Header == application/json; v=3
      [8] api == /credit-cards/accounts/1234
      [8] Checking operation: POST/stopTransactionsInAccount
      [8] Checking operation: GET/getOne
      [8] Location: /credit-cards/accounts/{accountReferenceId}
      [8] Oops, we have a parameter
      [8] Need to check for a parameterized api
      [8] newApi (/credit-cards/accounts/{accountReferenceId}) == location (/credit-cards/accounts/{accountReferenceId})
      [8] HttpAcceptHeaderEndpointSelector.select()
      [8] Found a match of application/json; v=3, which matched the endpoints Accept Header
      [9] Adding Endpoint CreditCardAccountsPortName
      [9] 1endpoint(s) matched.
```