---
title: "Mutation Testing: What It Is and How It Makes Code Coverage Matter"
ref: mutation
lang: en
layout: post
author: Carlos Schults
permalink: /en/mutation-testing/
img: https://res.cloudinary.com/dz5ppacuo/image/upload/v1595528879/mutation/mutation-testing-1038x437.jpg
description: Learn how mutation testing can help you turn code coverage into a meaningful metric, by ensuring the quality of your unit tests.
canonical: https://blog.ncrunch.net/post/mutation-testing-code-coverage.aspx
tags:
- software-testing
- automated-testing
- unit-testing
- code-coverage
- mutation-testing
- tdd
---

![]({{ page.img }})

<span>Photo by <a href="https://unsplash.com/@wocintechchat?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Christina @ wocintechchat.com</a> on <a href="https://unsplash.com/s/photos/software-testing?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span>

*Editorial note: This post was originally written for the NCrunch blog. You can [check out the original here, at their site]({{ page.canonical }}).*

I've been fascinated by mutation testing since I found out about it. I thought I'd finally found the answer to so many problems I had when writing tests. With mutation testing, I now had a way to really trust my tests. At last, code coverage had meaning again.

Then, I was dumbstruck as I realized that very few developers shared my interest in mutation testing. In fact, I dare say that most developers haven't even heard about it. And that's a shame because they—and we, as an industry—are missing out on so many benefits.

So, this post is my humble attempt to remedy the situation. I'll start by explaining the current dilemmas developers face regarding the reliability of the tests they write. Then, I'll proceed to show you how mutation testing is the answer to these dilemmas. I'll explain what it is, how it can make your tests more trustworthy, and how it can turn code coverage into the valuable metric it should be.

## The Problem: Trustworthiness of Tests

When learning about [unit tests][1]—or automated tests in general—most people will ask the same or a similar question: _How do I know my tests are right?_ That's a legitimate concern. If your tests aren't trustworthy, then you might be better off with no tests at all.

So what's the answer? How do people deal with the problem of test trustworthiness without relying on mutation testing?

## Making Tests Reliable Without Mutation Testing

There are techniques developers employ to improve the reliability of their tests, and we'll briefly cover some of them in this section. If you're experienced with unit testing, you're probably familiar with them. Let's dive in.

### Keep Your Tests Simple

The first technique we'll cover here to improve the reliability of your tests is just to keep them simple. And by "simple" I mean with less cyclomatic complexity. The lower the [cyclomatic complexity][2] of a given piece of code, the likelier it is that it actually does what you think it does. Simple code is easier to reason about, which is a property you definitely want your unit tests to have.

Keep test code simple to the point of being obvious. That means, for instance, avoiding loops or decision structures. Also, avoid doing anything fancy to compute the expected result (more on that in the next section). Hard-code it instead.

### Don't Duplicate Implementation Code

Let's say you're doing the [Roman numerals kata][3]. Resist the temptation to automatically generate the expected values ("I" for 1, "II" for 2, and so on). Instead, hard-code the values. If the repetition really bothers you and your test framework allows it, use parametrized tests.

Why would that be a problem? Simple: The fancier your test code gets, the more likely it's duplicating production code. If that's the case, you might be unlucky enough to find yourself in the situation where your production code is wrong (it doesn't solve the problem as it's supposed to do) but the tests pass. That's one of the worst possible scenarios. It's even worse than having no tests at all.

### Ensure You See the Test Failing

Ensure each test fails at least once before it passes. If you see the test failing when you think it should be failing and vice versa, that's a sign you're moving in the right direction. It doesn't guarantee anything, but it decreases the likelihood the test is passing due to a coincidence.

Here's how you'd do it. As soon as you get to the green phase, damage the implementation code in such a way that one or more tests should fail. You could invert conditionals, replace strings or numeric literals with random values, or even delete an if-statement. If you manage to sabotage production code and get away with it, that's not a good sign. Your test suite is either wrong or incomplete. In a sense, you're testing the tests.

Developers who employ [TDD (test-driven development)][4] kind of already do that by definition. Since you write a failing test and then proceed to make it pass, you're seeing the test fail. Of course, the test should fail in the expected manner. Meaning that if you're performing an assertion, the test should fail due to an assertion failure and not, say, because the method under test throws an exception. Yes, this is better than nothing, but it still might not be enough. Since a unit test represents a single-use case, it's totally possible to introduce a defect to production code in such a way that this particular test still passes.

## We Must Do Better: Enter Mutation Testing

So you've just applied the technique described in the last section. Good! Not perfect, though. Here comes a problem. You can't just insert a lot of defects and run the tests, because you wouldn't be able to identify which defect was responsible for the tests failing. The correct way to do it is to insert a single deliberate defect, run all the tests, verify their result, and _then_ roll back the change. After that, you can introduce another mistake, run all the tests again, verify the result, roll back the change...rinse and repeat. Needless to say, such an approach is extremely slow, tedious, and error-prone.

That's where mutation testing comes in.

### What's Mutation Testing, Anyway?

Mutation testing is nothing more, nothing less, than automating the whole "sabotaging production code and running tests to see if they fail" process you just saw. To use mutation testing, you need a mutation testing framework. The framework will alter production code, introducing defects that are called "mutations." For each mutation introduced, the framework will again run the suite of unit tests. If all tests pass, we say the mutation survived. That's a bad thing. It means that either your suite is lacking tests or the existing ones are wrong.

If, on the other hand, one or more tests fail, that means the mutation was killed, which is a good thing. The framework will repeat that process until it's tested the relevant portion of the codebase. When it's all done you can check the results, which will contain the number of mutations introduced, as well as the ratio of surviving vs. killed mutants.

### Mutation Testing Makes Code Coverage Better

One of the most controversial topics in the unit testing world is the argument about code coverage. Some developers say that getting to full coverage is essential; others will argue that's a useless metric. Who's right?

First of all, you have to understand that this issue isn't black and white. As is the case with pretty much everything in software, there's some nuance. Of course code coverage isn't useless. Knowing that your codebase has, say, 10% of test coverage is definitely a useful piece of data. Such a coverage is way too low: Seeing the green bar won't offer them any confidence. That's not to say that having 100% coverage is necessarily a good thing in itself. You could have tests that don't have assertions, for instance. Yes, this is a contrived example, but something like that could (and sometimes does) happen.

A more common occurrence would be to just have tests that don't exercise enough paths in the software. In short: Low code coverage is definitely a bad thing, but high (or full) code coverage is not _necessarily_ a good thing since it says nothing about the quality of the tests in the suite.

Since mutation testing does verify the quality of the test suite, it's the missing piece of the puzzle. If your codebase has a high code coverage and the results of mutation tests show that most or all mutations introduced are being killed, then smile! You probably have a great test suite in place!

## Embrace Mutation Testing Today

In today's post, we talked about the problem of test trustworthiness, then proceeded to review some techniques and guidelines you can use to overcome that challenge. Finally, we saw how mutation testing is the superior approach to solving that problem.

Here's the thing: The techniques we covered are good guidelines to follow when writing unit tests. Your tests will benefit from abiding by them, whether you employ mutation testing or not. But guidelines can only take you so far. They depend too much on human willpower and discipline, and we all have limited amounts of those. In order to take the quality of your tests to the next level, you need to embrace automation.

It takes just a few minutes of googling to find a mutation testing tool for your preferred tech stack. Do that today, and stop missing out on the benefits that mutation testing can provide you and your team!

[1]: https://carlosschults.net/en/unit-testing-for-beginners-part1/
[2]: https://en.wikipedia.org/wiki/Cyclomatic_complexity
[3]: https://codingdojo.org/kata/RomanNumerals/
[4]: https://carlosschults.net/en/csharp-unit-testing-intro-tdd/
