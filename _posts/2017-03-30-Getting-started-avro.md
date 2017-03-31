---
layout: post
title:  "Getting started with Apache Avro"
description: "Guide to understanding apache avro and setting up avro schemas."
comments: true
keywords: "Avro, Apache Avro, Avro Schema"
tags:
- Avro
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

## What is Avro ?
Avro is a data serialisation and RPC system like protobuff and thrift. It relies on a schema-based system. This schema is in JSON which is an advantage as most languages already have JSON libraries.
Theoretically, Avro can be used in any language but it has APIs for PHP, Java, Perl, Python, C, C++, C#, Go, Haskell and Ruby.

## Where Avro shines
Comparing Avro with similar systems (protobuff, thrift, message pack), these are the areas where it differs :

<ul markdown="1">
<li markdown="1">
 *Dynamic typing:*

Serialisation and deserialization can be done without code generation. Code generation is also available for statically typed languages as an optional optimisation.
</li>

<li markdown="1">
*Schema evolution:*

 Avro requires schemas when data is written or read. Most interesting is that you can use different schemas for serialisation and deserialization, and Avro will handle the missing/extra/modified fields.
</li>

<li markdown="1">
*Untagged data:*

Other serialisation systems like protobuff tag data but providing a schema with binary data allows each datum be written without the overhead. The result is more compact data encoding and faster data processing.
</li>
</ul>

## Why you need Avro (or serialisation libraries generally):
* You save storage space. [Uber](https://eng.uber.com/trip-data-squeeze/) drastically reduced their storage needs by implementing data serialization and compression.
*  It significantly reduces the amount of time spent processing data.
* Translates to less money saved on provisioning hardware.

## Data types in Avro
Avro supports a range of data types. These types could be either primitive, complex or logical types.

### Primitive types: 
1. *null :* no value
2. *boolean :* a binary value
3. *int :* 32-bit signed integer
4. *long :* 64-bit signed integer
5. *float :* single precision (32-bit) IEEE 754 floating-point number
6. *double :* double precision (64-bit) IEEE 754 floating-point number
7. *bytes :* sequence of 8-bit unsigned bytes
8. *string :* Unicode character sequence

### Complex Types:
Avro also provides complex data types which are majorly a combination of primitive types. The complex types are:

<ol markdown="1">

<li markdown="1">

#### *Records:*
A record is a collection of multiple types. A record is equivalent to a JSON object or a dictionary in python. 
{% highlight js  %}
{
    "type":"record",
    "name":"Point",
    "fields":[
        {
            "name":"x",
            "type":"int"
        },
        {
            "name":"y",
            "type":"int"
        }
    ]
}
{% endhighlight %}

</li>

<li markdown="1">

#### *Enum:*
An enumeration is a list of items in a collection.
{% highlight js  %}
{
    "type":"enum",
    "name":"Suit",
    "symbols":[
        "SPADES",
        "HEARTS",
        "DIAMONDS",
        "CLUBS"
    ]
}
{% endhighlight %}
</li>

<li markdown="1">

#### *Arrays:*
{% highlight js  %}
{ " type " : " array ", " items " : " int " }
{% endhighlight %}
</li>

<li markdown="1">

#### *Maps:*
Map keys are assumed to be strings. Eg :
{% highlight js  %}
{"type": "map", "values": "long"}
{% endhighlight %}
</li>

<li markdown="1">

#### *Unions:*
Unions are represented using JSON arrays.

`["null", "string"]` declares a schema which may be either a null or string.
</li>

<li markdown="1">

#### *Fixed:*
This data type is used to declare a fixed-sized field that can be used for storing binary data. It has field name and data as attributes. Name holds the name of the field, and size holds the size of the field.
</li>
</ol>

## Defining a schema
As indicated, Avro schemas are defined with JSON. The Schema is a representation of the data to be serialized in avro data types.

Creating a schema for this Object
{% highlight js  %}
{
    "products":[
        {
            "id":1,
            "name":"A green door",
            "price":12.50,
            "tags":[
                "home",
                "green"
            ]
        },
        {
            "id":1,
            "name":"A green door",
            "price":12.50,
            "tags":[
                "home",
                "green"
            ]
        },
        {
            "id":1,
            "name":"A green door",
            "price":12.50,
            "tags":[
                "home",
                "green"
            ]
        }
    ]
}
{% endhighlight %}


would result in : 
{% highlight js  %}
{
    "namespace":"com.idarlington.avro",
    "type":"record",
    "name":"stream",
    "fields":[
        {
            "name":"products",
            "type":{
                "type":"array",
                "items":{
                    "name":"product",
                    "type":"record",
                    "fields":[
                        {
                            "name":"id",
                            "type":"integer"
                        },
                        {
                            "name":"name",
                            "type":"string"
                        },
                        {
                            "name":"price",
                            "type":"float"
                        },
                        {
                            "name":"tags",
                            "type":{
                                "type":"array",
                                "items":"string"
                            }
                        }
                    ]
                }
            }
        }
    ]
}
{% endhighlight %}

To validate and test your avro schema, you can check [this](http://sh6.tarantool.org/) out.

My next post would be on serialzing and deserializing with Avro. If you liked this post, please share ♥.