---
title: "Value Objects: A Tool for Self-Documented Code and Fewer Errors"
ref: value-objects-tool
lang: en
layout: post
author: Carlos Schults
description: If you employ value objects in your code, you can make it easier to read and maintain. Learn about this technique in today's post.
permalink: /en/value-objects-tool/
canonical: https://blog.ndepend.com/value-objects-tool-self-documented-code-fewer-errors/
img: https://res.cloudinary.com/dz5ppacuo/image/upload/v1540385528/value-object-tool/value-object-tool-1038x437.jpg
tags:
- csharp
- best-practices
- ddd
- oop
- software-design
---

![](https://res.cloudinary.com/dz5ppacuo/image/upload/v1540385528/value-object-tool/value-object-tool-1038x437.jpg)


*Editorial note: I originally wrote this post for the NDepend blog.  You can [check out the original here, at their site](https://blog.ndepend.com/value-objects-tool-self-documented-code-fewer-errors/). While you’re there, take a look at NDepend.*

Have you ever heard of value objects? I bet you have. Even though they're talked about a lot less than I'd like, they're still talked about *enough *that many developers have at least some passing familiarity with the term.

"Passing familiarity" isn't good enough, though. So that's what we're fixing with this post. Today you're going to learn what value objects are and how you, as a C# developer, can harness their power to make your code clearer, self-documenting, and less error-prone.

## What Are Value Objects?

*Value objects* are one of the building blocks of domain-driven design, as proposed by Eric Evans on his seminal book [Domain-Driven Design: Tackling Complexity in the Heart of Software.](https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215)

Simply put, a value object is an object that represents a value. And I'm aware that sounds excruciatingly obvious and even boring when said this way. So, what's all the fuss about it?

## Some Properties

I think it's easier to understand value objects when we quit trying to explain what they are and talk about their characteristics instead.

### Value Objects Don't Have Identity

I think it's fair to say that the main characteristic of a value object is that it lacks *identity*.  But what does that really mean in practice?

Let's say you go to the nearest ATM and deposit a $50 bill into your checking account. Then you drive a couple of hours to another town, go to a bank there, and withdraw $50.

Now comes the question: does it matter to you that the bill you've got in your hands now isn't the same one you deposited earlier? Of course not!  And why is that? Well, the thing we generally care about, as it concerns money, is its *value,* not the vessel that holds that value*.*

In other words, we couldn't care less about the *identity* of that particular bill. The only thing that matters is its value.

It's no coincidence that money is a classic example of a value object.

### Value Objects Are Immutable

Can you change the number five? No, you can't. There's nothing you (or anyone else) can do to *mutate* the value of the number five. If you add one to it, it doesn't change; instead, you get six, which is *another* number.

Could you alter a date? Nope, you also can't do that. If you start with "2018-01-9" and add one day to it, you get "2018-01-10." You don't change the original date at all. In fact, the immutability aspect of a value object is a direct consequence of the previous point; since a value object doesn't have identity, we can say the value object *is* its value. Therefore, it doesn't even make sense to talk about changing it.

The implication of this for you as a developer is that value objects are inherently safer and easier to reason about. There's no risk of changing them by accident since they can't be changed at all.

### Value Objects Have Structural Equality

Imagine you could magically teleport people to anywhere you wish, and you've decided to swap two men called "John Smith" during the night. How do you think their respective partners would react to see a total stranger in their beds instead of their husbands?

People are obviously not interchangeable, despite sharing one or more characteristics. Even if our two Johns had not only the same name but also the same height, weight, skin color, and hair color, they would still be two completely different people. Even identical twins (or, on a slightly Black Mirror note, clones) continue to be different people, despite being as equal to one another as you can get.

On the other hand, people change continuously during their lives, but they are still the same people (as long as we don't get philosophical here, as in "[a man can't step into the same river twice](https://www.brainyquote.com/quotes/heraclitus_107157)" type of thing).

You may be wondering if I've gotten off track here, but I haven't. This only serves to illustrate the crucial differences between entities and value objects. With entities, we care about identity, not about the value of its attributes.  With value objects, we care only about the value itself.

The implication of this, in programming terms, is that value objects typically present structural equality. It makes sense to compare them by their values, not their references or identities. So, when implementing a value object, you'll want to override "Equals" and "GetHashCode."

## What's in It for Me?

By now you should have a pretty good idea of what value objects are. What's not clear yet is why you should use them.  To answer this, let's consider the following line of code:

{% highlight c# %}
    double  distance  =  4.5;
{% endhighlight %}

Is there something wrong with this? Well, I could *[Ben Kenobi](https://starwars.wikia.com/wiki/Wookieepedia:Quote_of_the_Day/Archive/Obi-Wan_Kenobi) *you and say that it might be wrong "from a certain point of view." But I won't. Instead, I'll say it's definitely wrong. It doesn't matter that it compiles. It also doesn't matter that it actually works some or even most of the time.

The problem here is the code smell known as "primitive obsession," i.e., modeling domain concepts using primitive types. The next few sections will dive in into why is this such a problem and how the use of value objects can help.

### Value Objects Provide Context

OK, so why is [primitive obsession a bad thing](https://blog.ndepend.com/easy-miss-code-smells/)? There are in fact several reasons, but one of the main problems with the code snippet presented in the previous section is that it lacks a critical piece of information. As you can see, the code assigns the value 4.5 to the variable. But 4.5 what? Meters? Kilometers? Miles? Parsecs? In other words, we don't have the **unit of measurement**.

This can be a recipe for disaster. It just takes a developer fetching a value from a database or a file, thinking it's supposed to represent meters but it's in fact kilometers. When they then proceed to use the value in a calculation, say, adding kilometers to miles...silence. Instead of failing fast, you'd get a program that silently misbehaves while corrupting data and providing inconsistent results.

Well, at least you're using [unit tests](https://blog.ndepend.com/unit-testing-affect-codebases/)...right?

Sure, nothing prevents you from encoding that information in the variable name itself:

{% highlight c# %}
	double  distanceInKilometers  =  4.5;
{% endhighlight %}

Yeah, this is slightly better than the previous version, but it's still a very brittle solution. At any moment, the value can be assigned to another variable or even passed as an argument to some function, and then the information is lost.

By using value objects, you can eliminate this problem easily. You'd just have to choose a unit to be the internal representation of the type---for distance, it probably makes sense to use meter, since it's an SI unit. And then you can provide several static factory methods for each necessary unit:

{% highlight c# %}
	var  distance  =  Distance.FromMeters(4000);
	var  distance2  =  Distance.FromKilometers(4);
	Assert.AreEqual(distance,  distance2);
{% endhighlight %}
 
If you go on to overload the "+" operator (or create a "Plus" method), you can safely add two distances that originate from different units of measurement since the internal representation is the same.

### Value Objects Are Type Safe

Let's say you have a method with this signature:

{% highlight c# %}
	double  PerformSomeImportantCalculation(double  distance,  double  temperature);
{% endhighlight %}

What would happen if you made a mistake and inverted the values when calling the method? The program would silently misbehave, and you wouldn't even be aware. Hopefully, you'd have a good QA process in place that would catch this bug before it hits production, but hope isn't exactly a strategy, right?

Well, as it turns out, that's the exact kind of problem value types are great at preventing. You'd just have to use custom types for each concept instead of relying on primitives:

{% highlight c# %}
	double  PerformSomeImportantCalculation(Distance distance,  Temperature temperature);
{% endhighlight %}

That way, you can't just pass the parameters in the wrong order: the compiler won't let you!

### Value Objects Prevent Duplication of Domain Logic

When you model domain concepts using primitive types, you tend to have a lot of code related to that concept spread throughout the whole application. Let's say you're building an application that has the concept of a license plate, and you're using strings to represent those. Of course, not all strings are valid license plates. So your code ends up with format validations for license plates everywhere.

This could be prevented by creating a "LicensePlate" class and performing the necessary validations on its constructor. That way you'd consolidate the validation code in one place; should it ever change in the future, you'd only have to change it in this one place.

## Value Objects and Value Types Aren't Synonymous

This section is necessary in order to clarify a common misconception, which is to mix up value objects with the concept of value types in C#. See, in C#, we have [two categories of types: reference types and value types.](https://carlosschults.net/en/value-reference-types-in-csharp/)

While you certainly can use structs (value types) to implement value objects---examples in the BCL would be DateTime or the primitive numeric types--- there's nothing preventing you from using classes.

On the other hand, structs are not automatically value objects. For instance, while it's considered good practice to keep structs immutable, they're not immutable by default.

In short, value type is an implementation detail in C#/.NET while value object is a design pattern. Keep that in mind and consult the [Microsoft design guidelines](https://docs.microsoft.com/EN-US/dotnet/standard/design-guidelines/choosing-between-class-and-struct) and you should be fine.

## Value Objects Are Worth It!

Value objects are a relatively low-cost technique that can greatly enhance the manageability and clarity of your code. By employing value objects, you can make your code easier to reason about, crafting APIs that are self-documenting, easy to understand, hard to use incorrectly, and inherently type-safe.