---
layout: post
title: "Uncommon Kafka CLI commands"
description: "Some rarely used Kafka CLI commands to help in debugging"
comments: true
keywords: "Kafka, Kafka CLI"
tags:
- Kafka
---

<style>
ul {
  list-style-type: square;
  margin-bottom: 10px;
  padding-left: 30px;
}
ol {
  list-style-type: decimal;
  margin-bottom: 10px;
  padding-left: 30px;
}

h3 strong {
  font-weight:normal;
}
</style>


Recently, a colleague asked how to view keys of consumed records and I wasn't sure it was possible.  I thought I knew all the important cli commands then. Later on, after a google search, I found it was possible.
 
I decided to spend some time going through the Kafka console classes I use the most &mdash; `kafka.tools.ConsoleConsumer` and `kafka.tools.ConsoleProducer`.

Here are some not so common commands you can use in the CLI:

## Kafka Console Consumer

- *print.key:* 

    This property configures the console consumer to print the keys of the messages it consumes. The default value is `false`.
    
- *print.value:*

    When you are not concerned with printing the values of the records being consumed, you can set this property which configures the console consumer to/not to print values of records being consumed. The default value is `true`.

- *print.timestamp:*

    You can configure the console consumer to/not to print the timestamp of records being consumed. The default value is `false`. `NO_TIMESTAMP` is printed out if there is no timestamp configured for the records and the property is set to true.

- *key.separator:*

    This property configures the character that separates the key and value when they are both printed. The default value is the tab character `\t`.

- *line.separator:*

    Property configuring the character separating each record being consumed. The default value is `\n`.

- *formatter:*

    The name of the class to use for formatting kafka records being printed. The default value is `kafka.tools.DefaultMessageFormatter`.
    Other formatters are: `kafka.tools.LoggingMessageFormatter`, `kafka.tools.NoOpMessageFormatter`, `kafka.tools.ChecksumMessageFormatter`.



Example of console consumer command using the flags and properties defined above:

```sh

kafka-console-consumer.sh --bootstrap-server localhost:9092 \
    --topic test-topic \
    --from-beginning \
    --formatter kafka.tools.DefaultMessageFormatter \
    --property print.key=true \
    --property print.value=true \
    --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer \
    --property value.deserializer=org.apache.kafka.common.serialization.StringSerializer
```



## Kafka Console Producer

- *key.separator:*

    By default inputs to the Kafka producer console are recognised as values and null is used for the keys. This property allows users input key and value messages in the producer console.
    It represents the character separating the key and value. The default value is the `\t` character. It has to be used with the `parse.key` property.

- *parse.key:*

    This property indicates if the key is to be serialized, it is used with the `key.separator` property. The default value is `false`.

- *ignore.error:*

    This property configures the console producer to ignore errors when the `key.separator` property is set and there is not used in an input line in the console.


Example of console producer command using the flags and properties defined above:


```sh
kafka-console-producer.sh \
  --broker-list localhost:9092 \
  --topic test-topic \
  --property "parse.key=true" \
  --property "key.separator=-"


key1-value1
key2-value2
key3-value3
```
