# Section 02: Intermediate Concepts

- [Inheritance](#inheritance)
  - [Overview](#overview)
  - [The "is a" Relationship](#the-is-a-relationship)
- [Multi-Level Inheritance](#multi-level-inheritance)
  - [Overview](#overview-1)
  - [Extends Class](#extends-class)
- [Multiple Inhertance (Diamond Inheritance)](#multiple-inhertance-diamond-inheritance)
  - [Overview](#overview-2)
  - [Extends Class](#extends-class-1)
- [Method Resolution Order (MRO)](#method-resolution-order-mro)

## Inheritance

### Overview

The diagram can give us a quick overview of what inheritance is.

<p align="center">
  <img src="https://i.imgur.com/BuGb1vj.png" alt="Inheritance" height="250px">
</p>

- We have two classes `A` and `B`. Class `A` is the **base class (also called parent class or super class)** and class `B` is the **derived class (also called child class or subclass)**.
- Inheritance is the concept that we can have a behavior which is common to multiple classes. Classes which inherit that behavior and also adds new functionality that is specific only to each particular class.

<br/>
<div align="right">
  <b><a href="#section-02-intermediate-concepts">[ ↥ Back To Top ]</a></b>
</div>
<br/>

### The "is a" Relationship

A good example for demonstrating inheritance is a scenario including animals. Let's create the class to represent dogs and cats.

- The cats and dogs have much in common.
  - a list of traits: breed, color and weight...
  - a list of behavior: walking, eating and sleeping...
- The cats and dogs have some characteristics that make them different.
  - barks and meows

The relationship between a dog or a cat and an animal in general is known as an **"is a" relationship**.

```python
class Animal:
    def __init__(self, breed, color, weight):
        self.breed = breed
        self.color = color
        self.weight = weight

    def walk(self):
        print("I am walking.")

    def eat(self):
        print("I am eating.")

    def sleep(self):
        print("I am sleeping.")


class Dog(Animal):
    def bark(self):
        print("I am barking.")


class Cat(Animal):
    def meow(self):
        print("I am meowing.")
```

Please note that in order to inherit from the `Animal` class, we have to define it before the child classes, otherwise it will not work.

<br/>
<div align="right">
  <b><a href="#section-02-intermediate-concepts">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Multi-Level Inheritance

### Overview

Multi-level Inheritance is used whenever you want to further extend the traits or behavior of a class. The diagram can give us a quick overview of what multi-level inheritance is.

<p align="center">
  <img src="https://i.imgur.com/0si7CM9.png" alt="Multi-level Inheritance" height="400px">
</p>

<br/>
<div align="right">
  <b><a href="#section-02-intermediate-concepts">[ ↥ Back To Top ]</a></b>
</div>
<br/>

### Extends Class

A good example of multi-level inheritance is a police dog that is a special dog with all the capabilities of a normal dog. But it also has the advantage of detecting drugs.

- A police dog is a special dog.
- Every dog is an animal.

```python
class Animal:
    def __init__(self, breed, color, weight):
        self.breed = breed
        self.color = color
        self.weight = weight

    def walk(self):
        print("I am walking.")

    def eat(self):
        print("I am eating.")

    def sleep(self):
        print("I am sleeping.")


class Dog(Animal):
    def bark(self):
        print("I am barking.")


class PoliceDog(Dog):
    def __init__(self, breed, color, weight, hours_on_mission):
        super().__init__(breed, color, weight)
        self.hours_on_mission = hours_on_mission

    def detect_drugs(self):
        print("Sniff...sniff... I smell some weed here!")
```

Note that we need to call the constructor of the parent class by using the `super()` keyword.

<br/>
<div align="right">
  <b><a href="#section-02-intermediate-concepts">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Multiple Inhertance (Diamond Inheritance)

### Overview

**Multiple Inheritance (or Diamond Inheritance)** let a class inherit from more than one class simultaneously. The diagram can give us a quick overview of what multiple inheritance is.

<p align="center">
  <img src="https://i.imgur.com/tWc0pqd.png" alt="Multiple Inheritance" height="250px">
</p>

It is maily used in the context of the so-called **mixin classes**. These mixin classes are not made to stand on their own and are only classes which store stateless behavior.

- Mixin Classes are not made to stand on their own.
- Mixin Classes are only classes which store stateless behavior.
- Mixin Classes don't have any "is-a" relationships.

<br/>
<div align="right">
  <b><a href="#section-02-intermediate-concepts">[ ↥ Back To Top ]</a></b>
</div>
<br/>

### Extends Class

We have created the `PoliceDog` class in order to provide it with the ability of detecting drugs. If we want to do this by using a multiple inheritance and the mixing class, we have to **create another class to store the ability to detect drugs**.

```python
class Animal:
    def __init__(self, breed, color, weight):
        self.breed = breed
        self.color = color
        self.weight = weight

    def walk(self):
        print("I am walking.")

    def eat(self):
        print("I am eating.")

    def sleep(self):
        print("I am sleeping.")


class Dog(Animal):
    def bark(self):
        print("I am barking.")


class DetectDrugsMixin:
    def detect_drugs(self):
        print("I'm detecting some drugs here!")


class PoliceDog(Dog, DetectDrugsMixin):
    def __init__(self, breed, color, weight, hours_on_mission):
        super().__init__(breed, color, weight)
        self.hours_on_mission = hours_on_mission
```

In order to inherit the `detect_drugs` behavior, we need to also inherit the `DetectDrugsMixin` class.

<br/>
<div align="right">
  <b><a href="#section-02-intermediate-concepts">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Method Resolution Order (MRO)

The **Method Resolution Order (MRO)** is a very important concept when using multiple inheritance: "When inherited classes have the same methods or variables, which one is going to be used in the end?"

```python
class Base1:
    x = "base1"

class Base2:
    x = "base2"

class Derived(Base1, Base2):
    pass

print(Derived.x)      # "base1"
print(Derived.mro())  # [__main__.Derived, __main__.Base1, __main__.Base2, object]
```

If we call the `mro()` method on the class, it will return a list and the lookup will start from the first element of the list and will end at the last one. Note that the last one element would be `object` because everything is an object in Python.

<br/>
<div align="right">
  <b><a href="#section-02-intermediate-concepts">[ ↥ Back To Top ]</a></b>
</div>
<br/>