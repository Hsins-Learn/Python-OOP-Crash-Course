# Section 03: Advanced Topics

- [Polymorphism and Method Overriding](#polymorphism-and-method-overriding)
  - [Etymology of "Polynorphism"](#etymology-of-polynorphism)
  - [Method Overriding](#method-overriding)
- [Operator Overloading](#operator-overloading)
  - [Operator Overloading and Magic Methods](#operator-overloading-and-magic-methods)
  - [Most Common Magic Methods](#most-common-magic-methods)
- [Abstract Classes and Methods](#abstract-classes-and-methods)
  - [Abstract Classes](#abstract-classes)
  - [The `abc` Package](#the-abc-package)
  - [Achieve The Behavior of Interfaces](#achieve-the-behavior-of-interfaces)

## Polymorphism and Method Overriding

### Etymology of "Polynorphism"

The word "Polynorphism" is composed of two words "poly" (means "many") and "morphism" (means "form"). So Polynorphism **represents the ability to take multiple forms**.

<br/>
<div align="right">
  <b><a href="#section-03-advanced-topics">[ ↥ Back To Top ]</a></b>
</div>
<br/>

### Method Overriding

Let's make both the cat and the dog to `eat()` in different way. First we would notice that the `Animal` based class is defining the `eat()` behavior, but if we want to change it, we can simply define the same `eat()` method.

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

    def eat(self):
        print("I am eating like a dog")


class DetectDrugsMixin:
    def detect_drugs(self):
        print("I'm detecting some drugs here!")


class PoliceDog(Dog, DetectDrugsMixin):
    def __init__(self, breed, color, weight, hours_on_mission):
        super().__init__(breed, color, weight)
        self.hours_on_mission = hours_on_mission

class Cat(Animal):
    def meow(self):
        print("I am meowing")

    def eat(self):
        print("I am eating like a cat")


def make_animal_eat(animal):
    animal.eat()

if __name__ == "__main__":
    blue_cat = Cat("British Shorthair", "blue", 7000)
    golden_dog = Dog("Golden Retriever", "golden", 5000)

    make_animal_eat(blue_cat)
    make_animal_eat(golden_dog)
```

<br/>
<div align="right">
  <b><a href="#section-03-advanced-topics">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Operator Overloading

### Operator Overloading and Magic Methods

The operators include `+`, `-`, `>` and `==` are'nt used only in the context of mathematical expressions, but we also want to use them on objects of the same type.

In order to achieve that, we need to define the magic methods. A **magic methods** name starts and ends in double underscore `__` (also called **Dunder**).

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

    def eat(self):
        print("I am eating like a dog")

    def __eq__(self, other):
        return type(self) == type(other) and self.weight == other.weight

    def __nq__(self, other):
        return type(self) == type(other) and self.weight != other.weight

    def __str__(self):
        return f"I'm a dog of {self.breed} breed, my fur color is {self.color} and I weigh {self.weight}."


class DetectDrugsMixin:
    def detect_drugs(self):
        print("I'm detecting some drugs here!")


class PoliceDog(Dog, DetectDrugsMixin):
    def __init__(self, breed, color, weight, hours_on_mission):
        super().__init__(breed, color, weight)
        self.hours_on_mission = hours_on_mission

class Cat(Animal):
    def meow(self):
        print("I am meowing")

    def eat(self):
        print("I am eating like a cat")


def make_animal_eat(animal):
    animal.eat()

if __name__ == "__main__":
    blue_cat = Cat("British Shorthair", "blue", 7000)
    golden_dog = Dog("Golden Retriever", "golden", 5000)
    french_dog = Dog("French Bulldog", "brown", 2000)
    golden_dog2 = Dog("Golden Retriever", "golden", 2000)

    print(golden_dog != french_dog)
    print(french_dog == golden_dog2)
    print(french_dog != golden_dog2)
```

Moreover, we can use the magic method `__str__` to have a pretty custom representation of the objects.

<br/>
<div align="right">
  <b><a href="#section-03-advanced-topics">[ ↥ Back To Top ]</a></b>
</div>
<br/>

### Most Common Magic Methods

Most frequently used magic methods:

- Addition (`+`): `__add__(self, other)`
- Subtraction (`-`): `__sub__(self, other)`
- Multiplication (`*`): `__mul__(self, other)`
- Floor division (`//`): `__floordiv__(self, other)`
- True division (`/`): `__truediv__(self, other)`
- Modulo (`%`): `__mod__(self, other)`
- Power (`**`): `__pow__(self, other)`
- Less than (`<`): `__lt__(self, other)`
- Greater than (`>`): `__gt__(self, other)`
- Less than or equal (`<=`): `__le__(self, other)`
- Greater than or equal (`>=`): `__ge__(self, other)`
- Equals (`==`): `__eq__(self, other)`
- Not equals (`!=`): `__ne__(self, other)`

<br/>
<div align="right">
  <b><a href="#section-03-advanced-topics">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Abstract Classes and Methods

### Abstract Classes

An **Abstract Class** is a class that has a normal implementation, but also abstract members which are not implemented in the based class (but they must be implemented in the subclasses in order to satisfy the blueprint).

We would use an abstract class as a base class when we're planning to inherit the base class multiple times and we want that every derived class to have at least one member that they should implement by itself.

<br/>
<div align="right">
  <b><a href="#section-03-advanced-topics">[ ↥ Back To Top ]</a></b>
</div>
<br/>

### The `abc` Package

We can make the decision to use the `Animal` class as an abstract class because we implemented different behaviors for the `eat()` method.

In order to make a class abstract, we need to import the `abs` class from the `abc` package and make it a super class.

```python
from abs import ABC, abstractmethod


class Animal(ABC):
    def __init__(self, breed, color, weight):
        self.breed = breed
        self.color = color
        self.weight = weight

    def walk(self):
        print("I am walking.")

    @abstractmethod
    def eat(self):
        print("I am eating.")

    def sleep(self):
        print("I am sleeping.")


class Dog(Animal):
    def bark(self):
        print("I am barking.")

    def eat(self):
        print("I am eating like a dog")

    def __eq__(self, other):
        return type(self) == type(other) and self.weight == other.weight

    def __nq__(self, other):
        return type(self) == type(other) and self.weight != other.weight

    def __str__(self):
        return f"I'm a dog of {self.breed} breed, my fur color is {self.color} and I weigh {self.weight}."


class DetectDrugsMixin:
    def detect_drugs(self):
        print("I'm detecting some drugs here!")


class PoliceDog(Dog, DetectDrugsMixin):
    def __init__(self, breed, color, weight, hours_on_mission):
        super().__init__(breed, color, weight)
        self.hours_on_mission = hours_on_mission

class Cat(Animal):
    def meow(self):
        print("I am meowing")

    def eat(self):
        print("I am eating like a cat")


def make_animal_eat(animal):
    animal.eat()

if __name__ == "__main__":
    blue_cat = Cat("British Shorthair", "blue", 7000)
    golden_dog = Dog("Golden Retriever", "golden", 5000)
    french_dog = Dog("French Bulldog", "brown", 2000)
    golden_dog2 = Dog("Golden Retriever", "golden", 2000)

    print(golden_dog != french_dog)
    print(french_dog == golden_dog2)
    print(french_dog != golden_dog2)
```

<br/>
<div align="right">
  <b><a href="#section-03-advanced-topics">[ ↥ Back To Top ]</a></b>
</div>
<br/>

### Achieve The Behavior of Interfaces

The **interface** is all about not implemented members. Since Python doesn't have interfaces implemented in the standard library, we can achieve the behavior of an interface wih the help of abstract classes.

In order to create a so-called interface in Python, we can do it by creating an abstract class and making all the methods abstract and the attributes abstract properties.

```python
from abc import ABC, abstractmethod


class IEmail(ABC):
    @abstractmethod
    def send(self):
        pass

    @property
    @abstractmethod
    def valid_domain(self):
        pass


class Email(IEmail):
    valid_domain = "epicpython.io"

    def send(self):
        print(f"Sending an email from the email class with the valid domain {self.valid_domain}.")


if __name__ == "__main__":
    email = Email()
    email.send()
```

If we're going to define an abstract attribute, we need to use two decorators (`@property` and `abstractmethod`). Please note that **the order of decorators matters**, so we need to place the `@property` decorator at the top.

<br/>
<div align="right">
  <b><a href="#section-03-advanced-topics">[ ↥ Back To Top ]</a></b>
</div>
<br/>
