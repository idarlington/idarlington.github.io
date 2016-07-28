---
layout: post
title:  "Why you should learn Scala"
description: "Reasons why you should start using scala"
comments: true
keywords: "why scala, learn scala, scala"
tags:
- Scala
---

<style>
ul {
  list-style-type: square;
  margin-bottom: 10px;
  padding-left: 30px;
}

h3 strong {
  font-weight:normal;
}
</style>
I want to believe you must have heard or read about Scala and learnt it was a JVM language. You probably thought - just another JVM language that would die out soon. Right ?  Or maybe you haven't heard of Scala. How so?

## History

Scala is short for scalable language, it combines both object oriented and functional programming concepts. It runs on the JVM (Java Virtual Machine). Scala was created by Martin Odersky (he worked on the Java compiler) and it's first release was in 2003.

In 2011, corporate stewardship was brought to bear – a set of people were making sure that the language was enterprise-ready at all times. Scala is used by some of the largest companies and startups LinkedIn, Twitter, Foursquare, The Guardian & Intel to name a few.

![Scala Companies](/assets/images/scala-companies.png "companies using scala")

I have been using Scala for over a year and I believe it won't die out. I would like to give you reasons to <del>ditch that other language and</del> start using Scala. I would be presenting my case using powerful features in Scala known as case classes (no pun intended) and `pattern matching`. Pattern matching is described as `switch on steroids` on [Scala's official website](http://www.scala-lang.org/). I think comparing it with switch cases is quite an injustice to it. It has also been called `Swiss army knife of Scala`.


### case **Concise Codes**
Unlike Java that is riddled with boiler plate codes, Scala is quite concise. Though to be fair, using Java 8 lambdas could make Java code a bit concise.

Comparing codes creating a user class in Scala and Java clearly shows Scala's concise nature.

{% highlight java %}
//Java Code
public class User {
  private String surname;
  private String email;
  public User(String name, String surname, String email) {
    this.name = name;
    this.surname = surname;
    this.email = email;
  }
  public void setName(String name) {
    this.name = name;
  }
  public void setSurname(String surname) {
    this.surname = surname;
  }
  public void setEmail(String email) {
    this.email = email
  }
  public String getName() {
    return this.name;
  }
  public String getSurname() {
    return this.surname;
  }
  public String getEmail() {
    return this.surname;
  }
}
{% endhighlight %}

{% highlight scala  %}
//Scala Code

class User(
 var name: String,
 var surname: String,
 var email: String)
{% endhighlight %}

> When we started Spark, we wanted it to have a concise API for users, which Scala did well.
>
> — *Matei Zaharia,CTO @ Databricks*

### case **Functional & OOP**
Scala mixes the functional paradigm with pure object orientation.  In  Scala, functional programming is the recommended way to program but the creators knew making that deep dive would be tough for anyone so you can still use your OOP patterns.

Functions are first class objects in Scala. Using functional programming, you will be able to write less code that is reusable and easily maintained.

Solving the first Euler problem *(Find the sum of all the multiples of 3 or 5 below 1000)* in Scala with the functional paradigm shows clean and maintainable code.
{% highlight scala  %}
val result = (1 until 1000).view.filter(n => n % 3 == 0 || n % 5 == 0).sum
{% endhighlight %}

### case **Static Typing and Type Inference**



>Statically typed programming languages do type checking (the process of verifying and enforcing the constraints of types) at compile-time as opposed to run-time.

Scala's static typing is one of my favorite feature.It has been proven that static typing improves code quality. This is important for data scientists, if you have a large job that will run for hours, you don't want to find out half way through the job that it was not a correct implementation.

Scala's static typing helps you write less tests, you don't need to write tests to check type consistency as the compiler does that for you (Sigh of relief).  This helps you reduce the amount of stupid bugs at an early stage.

 Also, with Scala's type inference you can create variables without a specified type and the type would be inferred.


### case  **Java Interoperability**
Scala has awesome Java interoperability which means you can import and use your Java codes and libraries in your Scala application (isn't that awesome?). The good thing is that integration is seamless as Scala runs on the JVM, you do it without any performance penalty.

### case **Concurrency and Distribution**
Scala is suited for multi-core programming, it has built in tools for its implementation. Using Immutable values and collections is the recommended method of programming in Scala, as it guards your data from being mangled by different processes.

Scala also uses **Akka** which is a ``toolkit and runtime for building highly concurrent, distributed, and fault tolerant event-driven applications``. Scala's functional nature makes it easier to write safe and performant multi-threaded code. There is less reliance on mutable state and Scala’s futures and actors provide powerful tools for organizing concurrent systems.

### case **High Paying Jobs and Most loved Language**
From the results of the recent [stack-overflow survey](http://stackoverflow.com/research/developer-survey-2016#technology-most-loved-dreaded-and-wanted), Scala is amongst the top five most loved  languages.  Scala has recently seen adoption as the language for introduction to computer science in some educational institutions.

It is no mistake that Spark (a data engine written in Scala) jobs and Scala jobs are the top paying tech jobs in the US and amongst the top ten paying tech jobs worldwide according to the [stack-overflow survey](http://stackoverflow.com/research/developer-survey-2016#technology-top-paying-tech). I guess if none of the above cases impressed you, this should do right?

![Loved Scala](/assets/images/loved-scala.png "scala top paying tech 2016")



### case **_**

 Other features that make Scala awesome are


- **Options** – No more NullPointerExceptions code crashes or errors.
* **One class != one file** as you can have more than a class in a file.
* **Scala traits** - multiple inheritance without some of it’s dangers but with some limitations.
* **Scala streams** - an awesome scala collection that can be used for efficient Big Data pocessing.
- **Case classes** and **pattern matching**.
* **Semicolons** are not **compulsory**.

So, what do you think? Drop your thoughts in the comments section.
