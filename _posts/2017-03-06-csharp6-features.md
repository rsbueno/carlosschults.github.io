---
title: It's about time you start using these C# 6 features
ref: csharp6
lang: en
layout: post
author: Carlos Schults
permalink: /en/csharp-6-features/
img: http://res.cloudinary.com/dz5ppacuo/image/upload/v1487896790/csharp6features_y5czrf.jpg
tags:
- csharp
- beginners
---
  
![](http://res.cloudinary.com/dz5ppacuo/image/upload/v1487896790/csharp6features_y5czrf.jpg)

The 7th version of C# is coming, and it's expected to bring some new and exciting features to our tool sets. Here's the thing, though: Are you up to speed with its predecessor's features?
 <!--more-->
 
A few days ago I was trying to figure out what my next post would be about. It seemed only natural to write about the features of C# 7 since we're [one day(!!!) from the release of Visual Studio 2017.]((https://blogs.msdn.microsoft.com/visualstudio/2017/02/09/visual-studio-2017-launch-event-and-20th-anniversary/))
 
But then I realized that, even though it's been almost two years since the release of C# 6, some developers still aren't comfortable with its features, and have not incorporated them into their code.
 
So, I've figured I'd take a step back and write about some C# 6 features instead. Not all of them, but those that can make your code cleaner and more expressive and are simple enough for you to use right away.
 
## String Interpolation
 
Suppose we have a `Person` class, having `Name` and `Age` as read-only properties. Something like this:
 
<script src="https://gist.github.com/carlosschults/84db03cd2a530530b72c4b9eeeb738d4.js"></script>
 
Then we have to add a method called `Introduce()`, to make our `Person` objects able to introduce themselves. For a person named "Mary" and aged 22, the method should return: "Hi! My name is Mary and I'm 22 years old."
 
There are a few ways we could do that in C# 5, as you can see in the next listing:
 
<script src="https://gist.github.com/carlosschults/9e30324951420356397c5cc8f50ea51b.js"></script>

Each one of them has their advantages and disadvantages, of course, but C# 6 offers a new way:
 
<script src="https://gist.github.com/carlosschults/17f501bd6d0ce6f5938edf17ef8e8704.js"></script>
 
You put a dollar sign at the beginning of the string, place your variables inside curly braces - and that's it!
 
String interpolation doesn't work for all occasions. If you need some special formatting on the values you still have to use `string.Format`, for instance.
 
But on a day-to-day basis, I use interpolation most of the time when I need to concatenate strings. I find it way nicer and cleaner than the other options.
 
## Auto-Property Initializer
 
Continuing with our previous example. Let's say that we need to provide a parameterless constructor in our class. Along with that, we need to provide default values for `Name` and `Age`. 

Otherwise, `Introduce` would return "Hi! My name is  and I'm 0 years old." And we wouldn't want that.
 
In C# 5, we'd have to initialize the properties inside the constructor:
 
<script src="https://gist.github.com/carlosschults/d95cade5d8d5f245a1d6bb49ef2feb1f.js"></script>
 
C# 6 let us provide default values for our properties when we declare them:

<script src="https://gist.github.com/carlosschults/e7d56c032e723f7c5110a9e3bfa1c744.js"></script>
 
## Null Conditional Operator
 
Consider the following code:
 
<script src="https://gist.github.com/carlosschults/7fb5caff2e73f4130f4db982825adbe6.js"></script>
 
Nothing remarkable about it. But there's a problem waiting to happen here. If `customer` is `null`, then this code will throw a `NullReferenceException`.
 
This is when the new "Null Conditional Operator" can come in handy:
 
<script src="https://gist.github.com/carlosschults/65bc4372a0e4fc3e8f38c0ee57905beb.js"></script>
 
How does that work? Simple: if `customer` is not `null`, the `Address` property is accessed, and its value is assigned to our local variable. However, if `customer` *is* `null`, then the whole expression evaluates to `null`. And that's what is assigned to the variable.

Another nice thing about the Null Conditional Operator is that you can use it along with the [null-coalescing operator](https://msdn.microsoft.com/en-us/library/ms173224.aspx) to easily provide a default value, instead of `null`:

<script src="https://gist.github.com/carlosschults/e17d34ba939fb7c472e164010db56377.js"></script>
 
## Expression-bodied methods and properties

This one is super easy. It's just a shorter way of writing methods, using the syntax of lambda expressions.

For instance, the two methods do the same thing:

<script src="https://gist.github.com/carlosschults/eeae77f3876f9b692ca667281b5401d0.js"></script>

This feature isn't restricted to methods, though. It can also be used with properties (only getters) and indexers.
 
## Conclusion
 
It seems clear that Microsoft's goal with C# 6 was not to add some radical new capabilities to the language. 

Rather, they had the intention to enable developers to write code in a cleaner and more concise way. And in my opinion, they succeeded.
 
You may think that some of the features don't make that much of a difference, in practice. I beg to differ. C# is often accused of being too verbose. There are situations in which you have to write a decent amount of code to accomplish something that a Ruby programmer or a Python programmer could solve with a one-liner.
 
And that's fair enough. Some (most?) of said verbosity is due to C# being a statically typed language, and let me tell you: **I'm glad for that**. I can't count how many times the compiler saved me by catching my dumb mistakes. If a little bit of verbosity is the price I have to pay for this, so be it.
 
That being said, the detractors have a point. It is possible to be *too* verbose. So, any feature that helps me eliminate some of that verbosity and write more concise code is welcome.
 
## See more
 
- [http://geekswithblogs.net/WinAZ/archive/2015/06/30/whatrsquos-new-in-c-6.0-auto-property-initializers.aspx](http://geekswithblogs.net/WinAZ/archive/2015/06/30/whatrsquos-new-in-c-6.0-auto-property-initializers.aspx)
- [https://msdn.microsoft.com/en-us/magazine/dn802602.aspx](https://msdn.microsoft.com/en-us/magazine/dn802602.aspx)
- [http://blog.caelum.com.br/novidades-do-c-6-0/](http://blog.caelum.com.br/novidades-do-c-6-0/)
