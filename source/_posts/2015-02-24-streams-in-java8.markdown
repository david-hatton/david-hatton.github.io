---
layout: post
title: "Streams in Java8"
date: 2015-02-24 22:35:42 +0000
comments: true
categories:
---
I've been working on some prototype activities recently which has allowed me to finally try out some of the (not so) new features in Java8. After a week or so of using these I have to say I am not looking forward to going back to the day job (JEE6/JSE7).

These new features like steams, optionals, lambdas, etc really move Java forward significantly in terms of the capabilities of the language, resulting in far more simple, concise, yet eminently understandable code.

The natural reaction for Java8 newbies is to be a little daunted by these new syntaxes, especially around lambda expressions, and honestly I was a little concerned about how this new syntax would affect the cleanliness of the code. But the key point really is that the lambdas are really only a very small part of the new capabilities of Java8 and can possibly be considered as syntactic clean-up of our good ole anonymous classes.

What I want to focus on in this post is one of the most significant ways Java8 can greatly simplify data handling - the concept of streams. The new interface <code>[java.util.stream.Stream]</code> essentially adds support to how we can manipulate data in Collections. What makes this so powerful is that <code>Stream</code> lets the designer focus only on how we wants to manipulate the data rather than having to write boiler plate code involving iterators, for loops etc.

There are many facets to the Stream interface, but fundamentally it provides a number of methods which can be used to easily process the data in the stream. These methods fall into two main categories:

 - intermediate operations which return another stream (and this can be chained together in a pipeline)
  - terminal operations which close the stream/pipeline and return a result from the overall pipelines




``` java The old way to decorate a collection
public Collection<ManagedObject> findMoOfType2(final String type) {
  final OSQLSynchQuery<OrientVertex> query = new OSQLSynchQuery<>("select from " + type);
  final Iterable<OrientVertex> allNodes = graphDb.command(query).execute();
  return stream(allNodes.spliterator(),false).
                 map(OrientManagedObject::new).
                 collect(toList());
}
```

Text goes here.
{% codeblock Some more stuff lang:java %}
public Collection<ManagedObject> findMoOfType2(final String type) {
  final OSQLSynchQuery<OrientVertex> query = new OSQLSynchQuery<>("select from " + type);
  final Iterable<OrientVertex> allNodes = graphDb.command(query).execute();
  return stream(allNodes.spliterator(),false).
                 map(OrientManagedObject::new).
                 collect(toList());
}
{% endcodeblock %}

[java.util.stream.Stream]: http://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html
