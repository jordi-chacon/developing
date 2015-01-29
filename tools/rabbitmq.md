##### Service responsibilities on startup
*28-01-2015* On startup, a service should be in charge of:
* creating the exchange it is going to publish to.
* creating the queue it is going to consume from.
* binding that queue to the correct exchange.
