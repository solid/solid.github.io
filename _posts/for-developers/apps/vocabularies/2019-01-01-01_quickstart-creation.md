---
layout: post
title: "Quickstart - Create your vocabulary "
permalink: /for-developers/apps/vocabularies/create/quickstart
tags: [implement, vocabularies]
categories: [Vocabularies]
exclude: true
published: true
---

Let us build a very simple vocabulary describing [obelisks](https://en.wikipedia.org/wiki/Obelisk), so that [Cleopatra](https://cleopatra.solid.community/profile/card#me) and [Caesar](https://jcaesar.solid.community/profile/card#me) can share information about their personal collections.

## From plain English to a graphical representation

Let's start by stating in English what we'd like to put in our vocabulary:
- An `obelisk` is `owned by` a `person`.
- An `obelisk` is `built by` a `sculptor`.
- An `obelisk` has a `height`, which is a numerical value.

The highlighted elements of these sentences are going to be the 'terms' in our vocabulary. We can identify two types of terms: the things that we talk about (e.g. `obelisk` or `sculptor`), and their properties (e.g. `built by` or `height`). Let's make a graphical representation of that, by putting the things in bubbles and the properties into squares:

![The obelisk vocabulary]({{site.baseurl}}/assets/img/tutorials/vocabularies/obelisk_vocab_1.png)

## From plain English to RDF

### Identifying everything with IRIs

RDF is the language used to build vocabularies for use across the Web (aka Linked Data). In RDF, everything is identified by IRIs, which are simply standard Web URIs, but just a bit more modern in that they can contain characters from a more _Internationalised_ set of characters (e.g. 'α', 'δ', or 'ό').

First, we'll need an IRI to represent (or identify) our new vocabulary (as we said, everything in RDF is identified with IRIs!), e.g. http://w3id.org/obelisk/ns/. From there, let's now update our plain English example a little bit:
- An <u>http://w3id.org/obelisk/ns/Obelisk</u> is <u>http://w3id.org/obelisk/ns/ownedBy</u> a <u>http://w3id.org/obelisk/ns/Person</u>.
- An <u>http://w3id.org/obelisk/ns/Obelisk</u> is <u>http://w3id.org/obelisk/ns/builtBy</u> a <u>http://w3id.org/obelisk/ns/Sculptor</u>.
- An <u>http://w3id.org/obelisk/ns/Obelisk</u> has a <u>http://w3id.org/obelisk/ns/height</u>, which is a numerical value.

Identifiers quickly become unpleasant to read when they are IRIs, so RDF introduces the notion of prefixes (a simple concept borrowed from XML namespaces). From now on we'll use the prefix `obelisk:` to stand in for our vocabulary identifier `http://w3id.org/obelisk/ns/`, which means our vocabulary now looks like:
- Use the prefix 'obelisk' for our vocabulary identifier http://w3id.org/obelisk/ns/.
- An [obelisk:Obelisk](http://w3id.org/obelisk/ns/Obelisk) is [obelisk:ownedBy](http://w3id.org/obelisk/ns/ownedBy) a [obelisk:Person](http://w3id.org/obelisk/ns/Person).
- An [obelisk:Obelisk](http://w3id.org/obelisk/ns/Obelisk) is [obelisk:builtBy](http://w3id.org/obelisk/ns/builtBy) a [obelisk:Sculptor](http://w3id.org/obelisk/ns/Sculptor).
- An [obelisk:Obelisk](http://w3id.org/obelisk/ns/Obelisk) has a [obelisk:height](http://w3id.org/obelisk/ns/height), which is a numerical value.

### Things, and properties of things

So from the above we can see that we want to describe both 'things' (e.g. Obelisks and Sculptors), and the properties of those things (e.g. their height, or who built them). So to distinguish between things and their properties, RDF allows us explicit state which is which - i.e. 'things' are called Classes, and 'properties' are called Properties.

### Defining classes of things

In RDF, the general things that we can talk about are called __Classes__. Everything that went in a bubble in our first schema is therefore a Class, so we could add the following to our vocabulary:
- [obelisk:Obelisk](http://w3id.org/obelisk/ns/Obelisk) is a Class.
- [obelisk:Person](http://w3id.org/obelisk/ns/Person) is a Class.
- [obelisk:Sculptor](http://w3id.org/obelisk/ns/Sculptor) is a Class.

If we look at these sentences, they are structured exactly like the ones from the rest of our vocabulary. Let us underline the important bits in the same way:
- [obelisk:Obelisk](http://w3id.org/obelisk/ns/Obelisk) [is a](???) [class](???).
- [obelisk:Person](http://w3id.org/obelisk/ns/Person) [is a](???) [class](???).
- [obelisk:Sculptor](http://w3id.org/obelisk/ns/Sculptor) [is a](???) [class](???).

What we need now are IRI for the "[is a](???)" property and the "[Class](???)" Class. Fortunately, these are defined in the RDF and RDFS vocabularies: "[is a](???)" is defined by [rdf:type](http://www.w3.org/1999/02/22-rdf-syntax-ns#type), and "[class](???)" by [rdfs:Class](http://www.w3.org/2000/01/rdf-schema#Class). Therefore, we could write:

```turtle
@prefix obelisk: <http://w3id.org/obelisk/ns/> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

obelisk:Obelisk rdf:type rdfs:Class .
obelisk:Person rdf:type rdfs:Class .
obelisk:Sculptor rdf:type rdfs:Class .
```

And congratulations, you've just created your first snippet of RDF! This particular RDF syntax is called Turtle, there are many other standardized syntaxes, but we don't need to cover them in this tutorial.

### Defining properties of things

The properties of things in RDF are called properties (how convenient). Therefore, as we did for Classes, we might write:
- [obelisk:ownedBy](http://w3id.org/obelisk/ns/ownedBy) [is a](http://www.w3.org/1999/02/22-rdf-syntax-ns#type) [property](???).
- [obelisk:builtBy](http://w3id.org/obelisk/ns/builtBy) [is a](http://www.w3.org/1999/02/22-rdf-syntax-ns#type) [property](???).
- [obelisk:height](http://w3id.org/obelisk/ns/height) [is a](http://www.w3.org/1999/02/22-rdf-syntax-ns#type) [property](???).

We already know that [is a](http://www.w3.org/1999/02/22-rdf-syntax-ns#type) is identified by the IRI [rdf:type](http://www.w3.org/1999/02/22-rdf-syntax-ns#type), and [property](http://www.w3.org/1999/02/22-rdf-syntax-ns#Property) is identified by [rdf:Property](http://www.w3.org/1999/02/22-rdf-syntax-ns#Property) so we can now go ahead and change that into:
- [obelisk:ownedBy](http://w3id.org/obelisk/ns/ownedBy) [rdf:type](http://www.w3.org/1999/02/22-rdf-syntax-ns#type) [rdf:Property](http://www.w3.org/1999/02/22-rdf-syntax-ns#Property).
- [obelisk:builtBy](http://w3id.org/obelisk/ns/builtBy) [rdf:type](http://www.w3.org/1999/02/22-rdf-syntax-ns#type) [rdf:Property](http://www.w3.org/1999/02/22-rdf-syntax-ns#Property).
- [obelisk:height](http://w3id.org/obelisk/ns/height) [rdf:type](http://www.w3.org/1999/02/22-rdf-syntax-ns#type) [rdf:Property](http://www.w3.org/1999/02/22-rdf-syntax-ns#Property).


Which leads to our vocabulary looking like this:

```turtle
@prefix obelisk: <http://w3id.org/obelisk/ns/> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

obelisk:Obelisk rdf:type rdfs:Class .
obelisk:Person rdf:type rdfs:Class .
obelisk:Sculptor rdf:type rdfs:Class .

obelisk:ownedBy rdf:type rdf:Property .
obelisk:builtBy rdf:type rdf:Property .
obelisk:height rdf:type rdf:Property .
```

## Adding human readability

### Using labels and comments

So far we have created identifiers that are primarily intended for machines (although it is certainly not recommended, the IRIs themselves do not need to be meaningful to humans at all). For example, the following would technically be an equivalent vocabulary:
```turtle
@prefix o: <http://w3id.org/obelisk/ns/> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

o:C001 rdf:type rdfs:Class .
o:C002 rdf:type rdfs:Class .

o:p001 rdf:type rdf:Property .
o:p002 rdf:type rdf:Property .
o:p003 rdf:type rdf:Property .
```

Even if we don't want our vocabulary to look like this, the point is that it's really useful to also provide human-readable descriptions of the terms in our vocabularies. To do so we'll use the properties [`rdfs:label`](http://www.w3.org/2000/01/rdf-schema#label) to add a human-readable label for the term identified by the IRI, and [`rdfs:comment`](http://www.w3.org/2000/01/rdf-schema#comment) to add a few sentences describing what is meant by the term in the context we use it. This could lead to something like this:
```turtle
@prefix obelisk: <http://w3id.org/obelisk/ns/> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

obelisk:Obelisk rdf:type rdfs:Class ;
    # A label for readability...
    rdfs:label "Obelisk" ;
    # ... and a more descriptive comment for understandability.
    rdfs:comment "An obelisk is a four-sided pillar with a pyramid-shaped top." .

obelisk:Sculptor rdf:type rdfs:Class ;
    rdfs:label rdfs:label "Sculptor" ;
    rdfs:comment "An artist who sculpts obelisks." .

obelisk:ownedBy rdf:type rdf:Property ;
    rdfs:label "owned by" ;
    rdfs:comment "Relationship between an obelisk and the person who owns it, which is typically the person who ordered it, or to whom it was offered." .

obelisk:builtBy rdf:type rdf:Property ;
    rdfs:label "built by" ;
    rdfs:comment "Relationship between an obelisk and the person who built it." .

obelisk:height rdf:type rdf:Property ;
    rdfs:label "heigth" ;
    # Note: so far we didn't specify any units for the height (we'll fix this properly later), but we can however provide a hint in the comment.
    rdfs:comment "The distance from the ground to the highest point of the obelisk, in meters." .
```

Please note that we are using a shortcut provided by the Turtle syntax to avoid repeating the thing that we talk about when adding multiple properties to it (e.g. `obelisk:ownedBy` in the next snippet):
- The long version:  
```turtle
obelisk:ownedBy rdf:type rdf:Property .
obelisk:ownedBy rdfs:label "owned by" .
obelisk:ownedBy rdfs:comment "Relationship between an obelisk and the person who owns it, which is typically the person who ordered it, or to whom it was offered.".
```
- The shortcut:
```turtle
obelisk:ownedBy rdf:type rdf:Property ;
    # We removed the repetitions of obelisk:ownedBy, and replaced the end of line by ; instead of .
    rdfs:label "owned by" ;
    rdfs:comment "Relationship between an obelisk and the person who owns it, which is typically the person who ordered it, or to whom it was offered." .
```

## Adding some metadata

The finishing touch to this vocabulary is to add some metadata to the vocabulary itself, so that people we share this vocabulary with, or who find it on the Web, can know who created it, and when, and what it's intended purpose is without having to go through its details.

We already decided that the IRI of the vocabulary would be `http://w3id.org/obelisk/ns/`, so this is the identifier we are going to use in RDF to say stuff about the vocabulary. In Linked Data terminology a vocabulary is called an [`owl:Ontology`](http://www.w3.org/2002/07/owl#Ontology), so the first thing to say is:
```turtle
@prefix obelisk: <http://w3id.org/obelisk/ns/> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix owl: <http://www.w3.org/2002/07/owl#> .

# `obelisk:` is equivalent to http://w3id.org/obelisk/ns/
obelisk: rdf:type owl:Ontology .

# The remainder of the vocabulary is unchanged
obelisk:Obelisk a rdfs:Class ;
    rdfs:label "Obelisk" ;
    rdfs:comment "An obelisk is a four-sided pilar with a pyramid-shaped top." .
# ...
```

### Adding some description

Much like we described each term with human-friendly labels and comments, we can add a title ([`dcterms:title`](http://purl.org/dc/terms/title)) and a description ([`dcterms:description`](http://purl.org/dc/terms/description)) to our vocabulary. To make it easier to reuse, we can also indicate a preferred prefix ([`vann:preferredNamespacePrefix`](http://purl.org/vocab/vann/preferredNamespacePrefix)) and a preferred IRI ([`vann:preferredNamespaceURI`](http://purl.org/vocab/vann/preferredNamespaceURI)) (since multiple IRIs may point to the same vocabulary).
```turtle
@prefix obelisk: <http://w3id.org/obelisk/ns/> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix owl: <http://www.w3.org/2002/07/owl#> .
@prefix dcterms: <http://purl.org/dc/terms/> .

obelisk: rdf:type owl:Ontology ;
    dcterms:title "Obelisk ontology" ;
    # The description can be a multi-line text
    dcterms:description """
    The obelisk ontology aims at describing obelisks.
    """ ;
    vann:preferredNamespacePrefix "obelisk" ;
    vann:preferredNamespaceURI <http://w3id.org/obelisk/ns/> .

# The remainder of the vocabulary is unchanged
obelisk:Obelisk a rdfs:Class ;
    rdfs:label "Obelisk" ;
    rdfs:comment "An obelisk is a four-sided pilar with a pyramid-shaped top." ;
# ...
```

A reference version of this final vocabulary is available [here](assets/misc/tutorials/quickstart-obelisk.ttl).

Next step: [using this vocabulary to describe data in your pod](/for-developers/apps/vocabularies/use/quickstart).