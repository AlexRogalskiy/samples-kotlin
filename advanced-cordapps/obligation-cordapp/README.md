# obligation-cordap

This Cordapp is the complete implementation of our signature IOU (I-owe-you) demonstration.

## Concepts

An IOU is someone who has cash that is paying it back to someone they owe it to.

You have to have the original concept of the debt itself, (the IOU), and the cash.

Then the ability to exchange assets like cash or assets, and then the ability to settle up.

Given this is intended to implement an IOU, our cordapp consists of three flows `issue`, `transfer` and `settle` flows.


### Flows

The first flows are the ones that issue the original cash and assets. You can find that the cash flow [here](https://github.com/corda/samples-java/blob/master/advanced-cordapps/obligation-cordapp/workflows/src/main/java/net/corda/samples/flows/SelfIssueCashFlow.java#L24-L32) and the IOU issurance in [IOUIssueFlow.java](https://github.com/corda/samples-java/blob/master/advanced-cordapps/obligation-cordapp/workflows/src/main/java/net/corda/samples/flows/IOUIssueFlow.java#L40-L80).

The next flow is the one that transfers ownership of that asset over to another party. That can be found in [IOUTransferFlow.java](https://github.com/corda/samples-java/blob/master/advanced-cordapps/obligation-cordapp/workflows/src/main/java/net/corda/samples/flows/IOUTransferFlow.java#L132-L159).


Finally, once we have the ability to transfer assets, we just need to settle up. That functiionality can be found [here in IOUSettleFlow.java](https://github.com/corda/samples-java/blob/master/advanced-cordapps/obligation-cordapp/workflows/src/main/java/net/corda/samples/flows/IOUSettleFlow.java#L54-L116)



## Usage

### Running the CorDapp

Once your application passes all tests in `IOUStateTests`, `IOUIssueTests`, and `IOUIssueFlowTests`, you can run the application and
interact with it via a web browser. To run the finished application, you have two choices for each language: from the terminal, and from IntelliJ.


* Terminal: Navigate to the root project folder and run `./gradlew java-source:deployNodes`, followed by
`./java-source/build/node/runnodes`

* IntelliJ: With the project open, select `Java - NodeDriver` from the dropdown run configuration menu, and click
the green play button.

### Interacting with the CorDapp

Once all the three nodes have started up (look for `Webserver started up in XXX sec` in the terminal or IntelliJ ), you can interact with the app via a web browser.
* From a Node Driver configuration, look for `Starting webserver on address localhost:100XX` for the addresses.

* From the terminal: Node A: `localhost:10009`, Node B: `localhost:10012`, Node C: `localhost:10015`.

To access the front-end gui for each node, navigate to `localhost:XXXX/web/iou/`

