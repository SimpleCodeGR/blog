---
title: Origins of Javascript and Why We Prefer “Let” Instead of “Var”
published: 2025-06-09
draft: false
lang: en
description: Origins of Javascript and Why We Prefer “Let” Instead of “Var”
tags: []
---

If you wish to make an apple pie from scratch, you must first invent the universe.

---

In the 1930s, Alonzo Church introduced Lambda calculus. It is a formal system for expressing mathematical logic and computations using functions. Long before computations were performed by machines, they were done by humans, and Lambda calculus helped formalize these processes in written form.

Lambda calculus looks like this:
```
λx.x*2 // function that takes input xx and returns x*2

λx.λy.x^2+y^2 // function that takes input x,y and returns the sum of them in power of 2
```

In the 1940s, Steve Russell, Timothy P. Hart and Mike Levin specified Lisp, a programming language based on the concepts of Lamda calculus. In 1970s, MIT created Scheme, a lisp dialect.

Scheme looks like this :

```
(display "Hello, World!")
(newline)
```

In 1987, Self was created by David Ungar, Randall Smith, Stanford University, Sun Microsystems, as a dialect of Smalltalk. Smalltalk created on 1969 at Xerox PARC by Learning Research Group (LRG) scientists, including Alan Kay, Dan Ingalls, Adele Goldberg, Ted Kaehler, Diana Merry, and Scott Wallace.

Self looks like this :

```
"Hello, World!" println.
```

In the early 1990s, Sun Microsystems began developing Java. This language was created by them because none of the existing languages were capable of solving their problems. After a lot of experimentation with the dominant language at the time, C++, they created and tested an extension of C++ called C++++, which much they didn’t finish and later became C# by Microsoft. Based on their experiments, they created Java.

Java looks like this :

```
public class HelloWorld {
  public static void main(String[] args) {
    System.out.println("Hello, World!");
  }
}
```

Note that Java has a C language-style syntax. C is a very good, probably the best, and very old language still used today for hard tasks like writing operating systems. It’s very fast but hard to write.

In 1995, Netscape hired Brendan Eich to implement the Scheme language in the browser. Instead of doing that, he created a new language, combiningJava‘s syntax (essentially C), most of theScheme (for nearly everything), andSelf‘s prototype (for easy data structure and no classes in contrast to Java). Essentially, he incorporated anything from famous languages at the time that made developers’ lives easier and blended them all together.

The result was the language that we all love, Javascript.

It’s worth noting that Self’s prototype had no classes and still had objects, whereas objects in most languages are a byproduct of classes and not an abstract structure solely for holding data. Even though JavaScript later implemented classes, they are not widely used even today, and objects remain an abstract structure for holding data. In other languages, abstract structures that hold data are called differently; for example, in C#, they are called “Struct”.

Since Brendan Eich created that language we all use in only… 10 days, some things were not finished. One of those things was scope. As Brendan Eich himself said, if he had worked a few more days on the language, he would have fixed scoping better. He didn’t, and that resulted in issues with the scope of variables, such as how a global variable is accessed from functions below or how a variable can be shared across different functions, becoming problematic. It took many years to fix that, as companies were all trying to create their own and only own JavaScript dialect for their browser. For example, Netscape had its own, created by Eich, and then Microsoft had JScript. They were all sabotaging the standardization of the language.

During the 2000s, JavaScript became increasingly useful in everyday life, and many other companies joined the club. Eventually, they all agreed to standardize JavaScript. The ECMA standard was created, and they fixed the scoping problem by introducing “let” and “const” instead of “var” as new better working ways to define new variables, without removing “var” for backward compatibility reasons. This resulted in much better scoping and a much better Javascript.

In 2009, Ryan Dahl took Javascript out of the browser and created an executable that allowed you to run JavaScript code on a terminal. This was named Node.js, and nowadays it’s used everywhere to create applications that are built in JavaScript but don’t run in the browser. However, many of those apps, whether they’re desktop apps made with the “Electron” framework or mobile apps made with Cordova, Ionic, React Native, or any other framework, may run on Node but still launch a browser (without visible controls or an address bar) to display a UI with modern graphics. This is because browsers tend to be the most preferable way to run something nowadays.
