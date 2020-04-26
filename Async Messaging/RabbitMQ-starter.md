# RabbitMQ Starter - Simple Reference

Prepared based on https://www.rabbitmq.com/tutorials/tutorial-two-java.html

## Intro

**RabbitMQ** is a message broker: It accepts and forwards messages

```
A producer is a user application that sends messages. Producer never sends message directly to a queue. 
It only sends it to Exchange
```
```
A queue is a buffer that stores messages
```
```
A consumer is a user application that receives messages
```
Default port - **5672**

## Standard RabbitMQ Flows

1. The producer publishes a message to the exchange
2. The exchange receives the message and is now responsible for the routing of the message
3. Binding must be set up between the queue and the exchange. In this case, we have bindings to two different queues from the exchange. The exchange routes the message into the queues
4. The messages stay in the queue until they are handled by a consumer
5. The consumer handles the message

**Reference** : https://www.cloudamqp.com/blog/2015-09-03-part4-rabbitmq-for-beginners-exchanges-routing-keys-bindings.html#standard-rabbitmq-message-flow

## Exchange

**Exchange** receives messages from producers and the other side it pushes them to queues

### Binding Keys

``` 
Binding Key connects exchange with Queue
```
### Routing Key
```
Routing Key is the key specified by the producer
```

### Exchange Types
```
Fanout	 - Ignores the routing key and sends to all queues
Direct	 - Messages will be routed if routing key == binding key
Topic 	 - Allows partial match of the routing key and binding key 
Header	 - Uses message header instead of routingKey
Nameless - Sends message where the routingKey=queueName, ignoring bindingKey
(Indirectly allows sending messages directly to the Queues)
```

## Work Queues (Task Queues)

Each task (item in queue) is delivered to exactly one worker.

### Which worker will get the Message ?
By default, RabbitMQ will send message to consumer in sequence. On average every consumer will get the same number of messages. Its based called round-robin

### How to Avoid Msg loss ?
To avoid failure in worker leading to loss of message, RabbitMQ supports Message Ack

> An ack(nowledgement) is sent back by the consumer to tell RabbitMQ that a particular message has been received, processed and that RabbitMQ is free to delete it

autoAck is turned on by default. It can be turned off by sending false to autoAck while calling basicConsume() method

>  Attempts to acknowledge using a different channel will result in a channel-level protocol exception

### Avoid Msg loss during RabbitMQ server node crash/restart

#### Declare queue as durable while creating

```java
boolean durable = true;
channel.queueDeclare("hello", durable, false, false, null);
```

#### Mark message as persistent 

```java
channel.basicPublish("", "task_queue",
            MessageProperties.PERSISTENT_TEXT_PLAIN,
            message.getBytes());
```

**Note** Marking persistent won't suffice guarantee of msg. RabbitMQ doesn't do fsync(2) for every message.

RabbitMQ blindly dispatches every n-th message to the n-th consumer irrespective of their previous unacknowledged messages.
 
To avoid it, set basicQos = 1 in Receiver (Worker)
 ```java
 int prefetchCount = 1;
 channel.basicQos(prefetchCount);
```

basicQos = 1 -> Not to give more than one message to a worker at a time

## Publish/Subscribe

```java
channel.basicPublish("", "hello", null, message.getBytes());
```

First parameter in basicPublish defines the Exchange name. "" refers to default exchange

## Dead Letter Exchange

Explanation taken from a Medium post

When you create a queue (A) bound to an exchange (X), you can also specify an exchange (DLX) to redirect expired and rejected messages to. This is the dead letter exchange. Then you have another queue (B) bound to this dead letter exchange (DLX) to consume messages as they drop off the original queue (A)

**Reference** : https://medium.com/@kiennguyen88/rabbitmq-delay-retry-schedule-with-dead-letter-exchange-31fb25a440fc
