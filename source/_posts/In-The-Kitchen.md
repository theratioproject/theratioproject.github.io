---
title: In The Kitchen
date: 2018-10-31 21:26:53
tags: whats-cooking
---

A lot of work has been going on since the last release on the 5th of August. 

<!-- more -->

Since the last release ( 0.3.36 ), the simple-lang community have been working endlessly and tiredlessly towards the next release. Let's see what has been going on behind the scenes :

## PR Count

Since the last release, **11** PRs have been merged into the _master_ branch containing heavy weight commits of important feature additions, bug fixes, enhancement and a lot more. One major PR is still on hold, I'll give you a subtle gist on what the PR is all about.

## Adding Cross-Platform Unix Build

The idea of using a universal makefile and/or build file was brought by one of the core Mac contributors, [appcypher](https://github.com/appcypher). In this PR, he defines universality in the Unix OSes to reduce the amount of build files simple has.

### What's This Universality ?

Both Mac and Linux are Unix OSes i.e they share almost the same file heirachy system. In this build files, he merges, [appcypher](https://github.com/appcypher), the build instructional codes from the Linux and Mac system and [mykeels](https://github.com/mykeels), another core Mac contributor, intelligently matches the OS type to create their respective shared libraries.

## PR

The PR status is still on hold but definitely has a ton of comments, you can check it [here](https://github.com/simple-lang/simple/pull/29)

## What Is In The Kitchen ?

Apart from the universal makefile in progress, a number of features have been added likewise enhancements and bug fixes. These additions will be discussed accordinly:

### 1. Module Call Style

One of the most interesting enhancement done to the module path in simple-lang is the change of style in module call. Formerly, modules are called in this manner:

```simple
call "modulegrandparent/moduleparent/module"
```

That style had the VM look for the module in the `simple` module path and it's depth was 5-foot directory level but after a suggestion was raised in the [IRC Channel](https://gitter.com/simple-language) by a core contributor [Youngestdev](https://github.com/Youngestdev), it was implemented here in this [PR](https://github.com/simple-lang/simple/pull/34) by the Author of simple-lang, [TheCarisma](https://github.com/Thecarisma).

> It's one of my best feature currently.

### 2. The final keyword

Simple is a weakly typed language and might become a strictly typed language, see [this](https://github.com/simple-lang/simple/issues/42). So, variables are easily over written in simple-lang and also, some hidden bugs result in some cases, such bugs are really hard to detect as they throw no error and the code works fine but the logic behind is faulty. The `final` keyword is birthed as a result. 
  The final keyword, serves as a constant; any variable declared with final cannot be over written easily.

```
final a = 10

a = 20 // Error !
```

### 3. A New OOP Style

This is perhaps my best feature yet. Well, there is a new style of declaring classes, bringing more beauty to the OOP world in `simple`. The new styles for creating classes are:

#### A. Vintage Style

Given a master test class, `TestClass` :

```js
class TestClass

	Back = "Gray"
	Fore = "Red"
	
	block setBack(value)
		Back = value + "_" + Back
	
	block getBack()
		return Back+"_"+Fore
```

Formerly, to set the value of Back and Fore, we do this:

```js

test = new TestClass
test.setBack = "Whatever"

test.getBack() // Return value of Back

```

But now, using the vintage style, we can access the values directly :

```js

test2 = new TestClass
test2.Back = "Well ?"

test2.Back // Return value of Back

```

> This approach, relieves the need for setters and getters like `getBack()` and `setBack()`.

#### B. Braces Style

Another new addition, is the braces style. The braces style also refutes the need for setters and getters but instead of using the vintage style to set class values, the braces style is used. Here's the test class illustrating this style:

```js

class TestClass

	name = "Unknown"
	age = 101
	gender = "Amphrodite"

```

For a variable inheriting this class, it sets its' values as thus:

```js

testExample = new TestClass { name = "Abdulazeez Adeshina" gender = "Male" age = 16 }

// Returning values

@ testExample.name
@ testExample.gender
@ testExample.age

```

How nice isn't it ?

### 4. List Rendering

The new kind of for loop allows to iterate over the items in a list rather than the index e.g

```js

list = ["one", "two", "three"]
for x in list {
    @x
}
```

Output :

```

one
two
three
```

> it allows iterating over a list faster than using the index list[index] in a for loop

#### List printing

Formerly, List are printed into the console in an unordered manner which make it difficult to visually review the list. The following list is printed in below manner before and after the new feature request was merged.

```js
list = [["a", "b", "c"], "ade", 2, 3, 4, 5, 6, 7, 8, 9]
```

Before :

```
a
b
c

ade
2
3
4
5
6
7
8
9
```

Now

```
[["a", "b", "c"], "ade", 2, 3, 4, 5, 6, 7, 8, 9]
```

## Android Support

This is actually to put you in suspense, a full blog post will be written on the support for Android. It has been implemented and working perfectly well in the emulator and still undergoing rigorous tests.