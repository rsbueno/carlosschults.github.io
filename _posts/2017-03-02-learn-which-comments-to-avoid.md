---
title: "Learn which types of comments should be avoided"
ref: bad-comments
lang: en
layout: post
author: Carlos Schults
permalink: /en/types-of-comments-to-avoid/
img: https://res.cloudinary.com/dz5ppacuo/image/upload/v1488499558/comments-1038x437.jpg
tags:
- code-smell
- best-practices
- beginners
- comments
---

![](https://res.cloudinary.com/dz5ppacuo/image/upload/v1488499558/comments-1038x437.jpg)

Spoiler Alert: You should avoid most of them.
<!--more-->

"To comment or not to comment". This is a question that tends to spark heated debate. Some people say that comments are an indispensable tool. Others argue that the comments show the developer's inability to express himself clearly in the code. Who's right?

When I was in college, I considered the comments indispensable when writing code. Otherwise, how could you understand what the code should do?

After getting my degree and finding a job, things started to change. I was being exposed to *real code*; I was reading books, articles and blog posts written by influential people in our industry.

These experiences shaped my current vision.

## The dangers of bad documentation

Comments are just another form of documentation. And make no mistake: documentation is a good thing - *when done correctly and in the right amount*.

Unfortunately, it is so often done wrong!

Many types of documentation can be problematic. It is very common for the documentation to lose synchronization with what it is documenting, which is worse than not having any documentation in the first place.

This is one of the problems that comments suffer from, but it is far from being the only one.

### Commented-out Code

Let's start with the most obvious one, which is commented-out code. Some developers, when fixing a bug, for example, choose to comment the offending code out, rather than delete it.

**Don't do this!**

Commented-out code does no good to anyone. It's just waste. Rely on your version control system. It will remember the changes you made if you needed to revert them in the future.

### 'Changelog' Comments

This category of bad comments is similar to the previous category, which is caused by a lack of trust in your version control system.

What do I mean by "Changelog" comments? Comments that just list the changes made to a file:

<script src="https://gist.github.com/carlosschults/61ffc0459edf71302af6a8140a0e225c.js"></script>

Comments like this are just doing the same work as your VCS already does, but in a clumsy and error-prone way.

Do not write these types of comments. Use [git](https://git-scm.com/) and be happy.

### Redundant Comments

This type of bad comment is very easy to detect and very easy to fix. Consider the following code:

<script src="https://gist.github.com/carlosschults/d22bf34fcd542e605a31476c46cfb315.js"></script>

I think we can all agree that these comments are useless. The code is perfectly clear without them, therefore, they should be removed.

### Comments at the end of blocks

You've probably seen code like this before:

<script src="https://gist.github.com/carlosschults/2d54e29662cd1b35d3c0807138b9e989.js"></script>

Some people write them so they do not lose control of the brackets.

If you need a comment for this reason, that indicates that your method is too long and you have too many levels of indentation.

Remember the Principle of Single Responsibility: each method should do only one thing. Divide your method into small ones and the need for such comments disappears.

### Comments that delimit sections inside methods

This one is similar to the previous one. If you have several sections inside a method, each one of them with an explaining comment on top, then you're probably violating the Single Responsibility Principle.

Remove each section to its own method, use the comment text as the name for the new method, and then delete the comments.

### Out of date comments

Here's a common scenario:

- Bob writes some lines of code. He thinks the code isn't clear enough and adds some comments to express its intent.
- Fast forward some weeks. It turns out that the code Bob wrote had a bug. He is on vacation, though, so Alice is made responsible for fixing the bug.
- Alice fixes the code in a few minutes and checks in her changes. But she forgets to update the comments to reflect the changes she's made in the code.

Now what you get? Comments that lie!

**Documentation that spread lies is worse than no documentation at all.** It's a source of confusion for developers, and a fertile ground for bugs. When you spot an out-of-date comment, don't think twice: delete it right away, or rewrite it to be accurate. But most of the time you shouldn't keep the comment. See next topic for why.

### Comments created due to lack of expressiveness in the code

Consider the following code:

<script src="https://gist.github.com/carlosschults/0530c4bf5884eb0fc46e63e71908b44d.js"></script>

Maybe you don't consider the comment in the sample above to be bad. It is not that terrible, sure. But think of the missed opportunity to extract a useful method or property:

<script src="https://gist.github.com/carlosschults/c914168d48e8d5d567ed79c0d612eafb.js"></script>

In the new code, we've extracted the concept of being eligible for blood donation in a new property. The rules for blood donation eligibility are now consolidated in a single place; should they ever change, the amount of work required to update them will be minimal.

And we get the nice collateral benefit of readability: the new if statement reads almost like natural language.

## Conclusion

As we've seen, there are several types of bad comments you should be weary of. They are often signs that there may be something wrong with your code. Maybe your methods are too long. Maybe [you didn't pick good names for your variables](https://carlosschults.net/en/how-to-choose-good-names/).
 
Every time you feel the need to write a comment, stop and try to think about ways in which you could improve your code to render the comment unnecessary.

Not all comments are bad, though. In a future post, I'll write about situations in which comments can be valuable.

See you later!

## Read More

- [Apologies In Code, by Robert C. Martin](https://butunclebob.com/ArticleS.TimOttinger.ApologizeIncode)
- [Write comments that matter, by Sander Rossel](https://www.codeproject.com/tips/467657/write-comments-that-matter)
- [Please, don’t commit commented out code, by Kent C. Dodds](https://kentcdodds.com/blog/please-dont-commit-commented-out-code)
