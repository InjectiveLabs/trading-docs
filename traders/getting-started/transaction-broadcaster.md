# Transaction Broadcaster

In the examples included in this documentation, you will see all the steps required to interact with the chain, from deriving a public key from a private key, creating messages to query the chain or creating orders, to creating and broadcasting transactions to the chain. Before going to the examples of all the possible actions it is important to state that you can avoid implementing yourself all the steps to create and configure correctly a transaction.&#x20;

If you are not interested in defining all the low level aspects you can use the component called _`MsgBroadcasterWithPk`_. To use the broadcaster you just need to create an instance of _`MsgBroadcasterWithPk`_, and once all the messages to be included in the transaction have been created, use the **broadcast** method, passing the messages as a parameter.&#x20;

The broadcaster will take care of:&#x20;

* Calculating the gas fee to pay for the transaction,
* Create the transaction and configure it,
* Sign the transaction,
* Broadcast it to the chain
