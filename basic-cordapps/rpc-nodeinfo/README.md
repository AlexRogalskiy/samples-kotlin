# NodeInfo

Allows one to get some rudimentary information about a running Corda node via RPC

Useful for debugging network issues, ensuring flows have loaded etc.

After cloning, use the _getInfo_ gradle task to retrieve node information.



## Concepts


Here we'll be using java just to create an RPC call against a corda node.


You'll find our example to do this in [Main.java](https://github.com/corda/samples-java/blob/master/basic-cordapps/rpc-nodeinfo/java-app/src/main/java/net/corda/Main.java#L31-L46)

```java
        System.out.println("Node connected: " + proxy.nodeInfo().getLegalIdentities().get(0));

        System.out.println("Time: " + proxy.currentNodeTime());

        System.out.println("Flows: " + proxy.registeredFlows());

        System.out.println("Platform version: " + proxy.nodeInfo().getPlatformVersion());

        System.out.println("Current Network Map Status --> ");
        proxy.networkMapSnapshot().iterator().forEachRemaining(it -> {
            System.out.println("-- " + it.getLegalIdentities().get(0) + " @ " + it.getAddresses().get(0).getHost());
        });

        System.out.println("Registered Notaries --> ");
        proxy.notaryIdentities().iterator().forEachRemaining(it -> {
            System.out.println("-- " + it.getName());
        });
```


## Usage



### Deploy and run the node

```
./greadlew deployNodes
./build/node/runnodes
```

Then run the following task against Party A defined in the CorDapp Example:

Java version:

    ./gradlew java-app:getInfo -Phost="localhost:10007" -Pusername="user1" -Ppassword="test"

In a closer look of the parameters:

- Phost: The RPC connection address of the target node
- Pusername: The username used to login (specified in the node.conf)
- Ppassword: The password used to login (specified in the node.conf)

### Sample Output

```
./gradlew getInfo -Phost="localhost:10006" -Pusername="user1" -Ppassword="test"

> Task :getInfo
Logging into localhost:10006 as user1
Node connected: O=PartyA, L=London, C=GB
Time: 2018-02-27T11:30:37.729Z.
Flows: [com.example.flow.ExampleFlow$Initiator, net.corda.core.flows.ContractUpgradeFlow$Authorise, net.corda.core.flows.ContractUpgradeFlow$Deauthorise, net.corda.core.flows.ContractUpgradeFlow$Initiate, net.corda.finance.flows.CashConfigDataFlow, net.corda.finance.flows.CashExitFlow, net.corda.finance.flows.CashIssueAndPaymentFlow, net.corda.finance.flows.CashIssueFlow, net.corda.finance.flows.CashPaymentFlow]
Platform version: 2
Current Network Map Status -->
-- O=PartyA, L=London, C=GB @ localhost
-- O=Controller, L=London, C=GB @ localhost
-- O=PartyB, L=New York, C=US @ localhost
-- O=PartyC, L=Paris, C=FR @ localhost
-- O=Notary, L=London, C=GB @ localhost
Registered Notaries -->
-- O=Notary, L=London, C=GB
-- O=Controller, L=London, C=GB
```

### Errors

`Exception in thread "main" ActiveMQSecurityException[errorType=SECURITY_EXCEPTION message=AMQ119031: Unable to validate user]`

Caused by: Wrong RPC credentials. Check the node.conf file and try again.

`Exception in thread "main" ActiveMQNotConnectedException[errorType=NOT_CONNECTED message=AMQ119007: Cannot connect to server(s). Tried with all available servers.]`

Caused by: Network connectivity issues or node not running.
