---
title: Origins of Key-Value Document Databases - NDB, the Hidden Gem from Plan 9
published: 2025-06-04
draft: false
lang: en
description: Origins of Key-Value Document Databases - NDB, the Hidden Gem from Plan 9
tags: []
---

Plan 9 was a utopian operating system that failed. It’s vision was to make distributed computing an everyday thing by treating everything as a file. And when we say everything, we mean everything, so even the hardware of each computer – allowing you to share that hardware with other machines easily. Even though this sounds technically impossible, it is very possible, and Plan 9 actually made it real! The main reason behind its failure was that this came at the cost of flexibility. In order to do that trick that it promised, Plan 9 asked the whole world to change, while it was already too late, since computer science had already started to get standardized at the time of release.

There is a dedicated post about Plan 9, “Plan 9: The Utopian OS and Lessons in Inflexible Architecture“, which you most probably have already read.

Today, we are going to unveil a very hidden gem within that operating system, which was an internal database called “NDB”, which stands for “Network Database”. “NDB” was one of the first databases that stored data as documents, treating them as key-value pairs, and not only that, indexing them! All of those features are going to be explained below.

Storing data as documents means that, in contrast to tabular databases, your data don’t have to have a structure.
In contrast, the more commonly used tabular databases are like Excel files; you have to somehow have a structure on what you write: you have columns with their titles and rows with the related data.
In documents, you are more free as you write whatever you want for each specific document, more like text files.

This is how a tabular database (or an Excel) would look like:

| Id | Name | Gender | Cat | Turtle |
| --- | --- | --- | --- | --- |
| 0 | Irina | Female | Luluka | |
| 1 | Rantouan | Male | | Galopoula |

And this is how storing indocuments(or text files) would look like:

One document for Irina:

```
Name="Irina"
Gender="Female"
Cat="Luluka"
```

And another one document for Rantouan:
```
Name="Rantouan"
Gender="Male"
Turtle="Galopoula"
```

Note how easy it is to add extra information, related and unique to each person, like the cats and turtles above with a document database and how rigid it is with a tabular one. Tabular databases have the advantage that if your data are all going to have the same structure, then you get a huge performance advantage. Document databases are more performant when your data are unstructured.

Key-value pairs mean that you store your data in a structure where it’s a pair of key (names) and values, like in the document examples above: `Pet=Luluka`. We mention this because when you store data as documents, there are many other ways to store them as well, for example, XML `<Pet>Luluka</Pet>` or JSON `{“Pet” : “Luluka”}`.

Finally, indexing means that not only data are stored, but notes on how to access them easily for the system are being kept. Indexing is very important in order for a database to be fast.
Imagine it like in the phone-book, where there is a small bookmark where names with “A” start, names with “B” start, etc. Another example is to imagine a very huge book that you just want to find something in, and usually on the first pages, there is an “index” page, where the first page of each chapter is being referenced, so you don’t have to search the whole book page by page.

Today, a software engineer would probably use Redis or MongoDB as a key-value document database. It’s very interesting to know that for all of the above things, NDB was one of the first -most probably even the first- databases to be capable of.

This gem of a database was hidden inside Plan 9, and it was mostly used for managing networks – but not only. Most of the modern operating systems still use a plain file without database supporting mechanism – it sounds logical to take more care of the network, if someone would think of Plan 9’s distributed nature.
