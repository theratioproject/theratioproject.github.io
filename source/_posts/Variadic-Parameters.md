---
title: Variadic Parameters
date: 2018-11-13 21:26:53
---

A variadic parameter accepts zero or more arguments of different type. 

<!-- more -->

A variadic paramter indicates that the block or method can be called with different number of arguments of different type else the type is specified then only instance of the type can be passed as arguments. 

### Creating a variadic parameter

A variadic paramter can be written by inserting exactly three period characters `(...)` immediately after the parameter identifier.

The example below indicates how the variadic parameter can be created in *blocks* and *class* methods.

```js
block sumNumbers(numbers...)
class VariadicClass
  block VariadicClass(args...)
```

## Variadic Paremeters

The values of a variadic parameter are available in the block or method body as a list that consist of all the passed values. In a block/method, there cannot be more than one variadic parameter and it must be the last parameter in the block/method initialization. A block can contain other compulsory parameter but with the variadic parameter comming last. 
The example below shows a block with a compulsory parameters and a variadic parameters

```js
block mixedBlock(name, age, attributes...)
  @"Name : " + name
  @"Age : " + age 
  for attribute in attributes {
    @attribute
  }
```

The block above can be called with an unlimited number of arguments but must not be less than two. 

> A variadic parameter **must** contain two or more arguments when passed into the block.

The first two parameters `name` and `age` are required when calling the block. The below code shows valid and invalid calls to the **mixedBlock(...)** block above

```js
  mixedBlock("King", 26)                      #valid
  mixedBlock("King", 26, "tall", "brown eye") #valid
  mixedBlock("King")                          #error 'less parameter passed'
```

### Use Cases

Simple-lang is weakly typed so blocks and methods are referenced by their identifier (Name). Therefore, the non-existence of method overloading. Only one instance of a block/method can be created even when the length of parameters varies. A work around is to use the variadic parameter in the block then do an appropriate type check on the variadic parameter values to prevent faulty and code breaking values. Using this approach, the function of an overloaded method can be achieved. 

## Examples

#### A block that sum all the arguments

```js
block main()
	@sumAll(1,2,3,4)
	@sumAll(10,20,30,40,10,30,50,10)
	@sumAll(96,43,54,67,88,12,44,67,87,19)

block sumAll(numbers...)
  sum = 0 
  for number in numbers {
    sum += number
  }
  return sum

```

Output

```
10
200
577
```

#### A class constructor that accept 5 parameters at most

```js
call simple.debugging.Throw

block main()
	a = new TestClass()
	b = new TestClass("one", "two", "three")
	c = new TestClass(1,2,3,4,5)
	@a.Value
	@b.Value
	@c.Value
	d = new TestClass(1,2,3,4,5,6)

class TestClass

  Value = "Param Length : "

  block TestClass(params...)
    if lengthOf(params) > 5 {
      throw("Expecting 5 parameters at most")
    }
	Value += ""+lengthOf(params) + " Params : "
    for param in params {
      Value += ""+param+" "
    }
```

Output

```
Param Length : 0 Params :
Param Length : 3 Params : one two three
Param Length : 5 Params : 1 2 3 4 5

Line 61 -> Expecting 5 parameters at most
        at throw() in file Throw.sim
        at line 29 at TestClass() in file beep.sim
        at line 21 at main() in file beep.sim
        at line 14 in file beep.sim
```

*If you think something is missing or you wish to contibute you can send a PR to [simple-lang/simple](https://github.com/simple-lang/simple)*