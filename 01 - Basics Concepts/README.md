# Section 01: Basics Concepts

- [Object Oriented Programming](#object-oriented-programming)
  - [Data and Code](#data-and-code)
  - [Three Based Pillars](#three-based-pillars)
- [Simple Example in Python](#simple-example-in-python)
  - [Functional Programming](#functional-programming)
  - [Object-Oriented Programming](#object-oriented-programming-1)
- [Class and Object](#class-and-object)
- [Constructor, Instance Attributes and `self`](#constructor-instance-attributes-and-self)
- [Encapsulation: Public, Private and Protected](#encapsulation-public-private-and-protected)
  - [Protected and Private](#protected-and-private)
  - [Example of Encapsulation](#example-of-encapsulation)
- [Class Attributes](#class-attributes)
  - [Instance Attributes and Class Attributes](#instance-attributes-and-class-attributes)
  - [Pitfall of Immutable Objects](#pitfall-of-immutable-objects)
- [Class Methods and Static Methods](#class-methods-and-static-methods)

## Object Oriented Programming

### Data and Code

**Object Oriented Programming (OOP)** is a programming paradigm based on the concepts of "Objects", which can contain data and code:

- Data is in the form of fields (attributes or properties).
- Code is in the form of procedures (methods).

<br/>
<div align="right">
  <b><a href="#section-01-basics-concepts">[ ↥ Back To Top ]</a></b>
</div>
<br/>

### Three Based Pillars

There are the three based pillars we have to respect and abide by:

- **Encapsulation** refers to hiding data and operations inside the class. (Note that this pillar is not very achievable in Python because we can't have classes hiding its implementation as we have in C++/Java)
- **Inheritance** refers to organising our code and writing classes in a tree-like form, where we write a base class that has some common traits which can be inherited by ancestors.
- **Polymorphism** refers to changing behavior depending on object types.

Some books or articles include the fourth pillar **abstraction**, but it is already inclued in  **Encapsulation** in someone's opion.

<br/>
<div align="right">
  <b><a href="#section-01-basics-concepts">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Simple Example in Python

Let's take the following example. Our requirement is to compute the area of a square.

### Functional Programming

We're defining a stateless piece of code of function that does something.

```python
def compute_square_area(side_length):
    return pow(side_length, 2)


if __name__ == "__main__":
    print(compute_square_area(15))
```

<br/>
<div align="right">
  <b><a href="#section-01-basics-concepts">[ ↥ Back To Top ]</a></b>
</div>
<br/>

### Object-Oriented Programming

We have to think about the square as an object, which is going to have some attributes and behavior.

```python
class Square:
    def __init__(self, side_length):
        self.side_length = side_length

    def compute_area(self):
        return pow(self.side_length, 2)


if __name__ == "__main__":
    example_square = Square(15)
    print(example_square.compute_area())
```

<br/>
<div align="right">
  <b><a href="#section-01-basics-concepts">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Class and Object

Take the `Square` class we previously created as an example.

- A **class** is a blueprint or a model from which we can create instances or objects.
- An **object** can be created from certain class.

In our case, we can create smaller or bigger squares by providing different values of the `side_length`.

```python
class Square:
    def __init__(self, side_length):
        self.side_length = side_length

    def compute_area(self):
        return pow(self.side_length, 2)


if __name__ == "__main__":
    example_square = Square(15)
    print(example_square.compute_area())

    small_square = Square(5)
    print(small_square.compute_area())

    large_square = Square(500)
    print(large_square.compute_area())
```

<br/>
<div align="right">
  <b><a href="#section-01-basics-concepts">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Constructor, Instance Attributes and `self`

Let's create a class called `Email` and talk about the **constructor**.

```python
class Email:
    def __init__(self, subject, body):
        self.subject = subject
        self.body = body

    def send(self, to):
        print(f"Sending email with subject: {self.subject} and body: {self.body} to : {to}")


if __name__ == "__main__":
    greeting_email = Email("Welcome!", "Welcome to here!")
    greeting_email.subject = "Greeting!"
    greeting_email.send("bob@nasa.gov")
    greeting_email.send("liz@buckingham.uk")
```

- A **constructor** is the function will be called when creating an instance of class the first time.
- Every class constructor is defined by writing a special method `__init__` in Python.
- The object we are creating from a class is actually the `self` object writing as the first parameter inside every method of a class.

<br/>
<div align="right">
  <b><a href="#section-01-basics-concepts">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Encapsulation: Public, Private and Protected

### Protected and Private

All of the data encapsulation concept is about hiding pieces of data or implementation details inside the class without making them available to the outer scope. There were two methods of hiding data by using protected or private members:

- **Protected** means that it can be only accessed from within the class and from other classes that are subclassing our class through inheritance.
- **Private** is removing the permission for subclasses and makes the member available only from within the class.

Since there are no keywords `protected` and `private` in Python, we can only use the **naming conventions** to achieve similar behavior (the conventions are not really hidden).

<br/>
<div align="right">
  <b><a href="#section-01-basics-concepts">[ ↥ Back To Top ]</a></b>
</div>
<br/>

### Example of Encapsulation

When sending emails, we have to specify from whom the email is sent. But we only want the email to be sent from the domain name where the website is hosted.

```python
class Email:
    def __init__(self, subject, body, from_recipient):
        self.subject = subject
        self.body = body

        split = from_recipient.split("@")
        if split[1] != "epicpython.io"
            raise Exception("Invalid Domain")

        self._from_recipient = from_recipient

    @property
    def from_recipient(self):
        return self.__from_recipient

    @from_recipient.setter
    def from_recipient(self, from_recipient):
        split = from_recipient.split("@")
        if split[1] != "epicpython.io"
            raise Exception("Invalid Domain")
        self.__from_recipient = from_recipient

    def send(self, to):
        print(f"Sending email from: {self.__from_recipient} with subject: {self.subject} and body: {self.body} to : {to}")


if __name__ == "__main__":
    greeting_email = Email("Welcome!", "Welcome to here!", "greeting@epicpython.io")
    print(greeting_email.from_recipient)
    greeting_email.subject = "Greeting!"
    greeting_email.send("bob@nasa.gov")
    greeting_email.send("liz@buckingham.uk")
```

- `_`: One single underscore used as a prefix in the member name will make it **protected**.
- `__`: Two single underscore used as a prefix in the member name will makt it **private**.

If we want to be able to read/write the private attribute normally, we can achieve this by making it a property or a property setter with the help of the property decorator `@property` or the property setter decorator `@PROPERTYNAME.setter`.

<br/>
<div align="right">
  <b><a href="#section-01-basics-concepts">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Class Attributes

### Instance Attributes and Class Attributes

- **Instance Attribute**: the instance attributes are tied to the instance that is created from that. Note that the instance attributes can differ from object to object.
- **Class Attribute**: the class attributes are tied to the class. We can define them after the class definition and write before the constructor.

Let's see the `Email` class and add the class attributes `valid_domain` which is used for every email to validate the from recipient.

```python
class Email:
    valid_domain = "epicpython.io"

    def __init__(self, subject, body, from_recipient):
        self.subject = subject
        self.body = body

        split = from_recipient.split("@")
        if split[1] != self.valid_domain
            raise Exception("Invalid Domain")

        self._from_recipient = from_recipient

    @property
    def from_recipient(self):
        return self.__from_recipient

    @from_recipient.setter
    def from_recipient(self, from_recipient):
        split = from_recipient.split("@")
        if split[1] != self.valid_domain
            raise Exception("Invalid Domain")
        self.__from_recipient = from_recipient

    def send(self, to):
        print(f"Sending email from: {self.__from_recipient} with subject: {self.subject} and body: {self.body} to : {to}")


if __name__ == "__main__":
    greeting_email = Email("Welcome!", "Welcome to example.com!", "greeting@epicpython.io")
    bf_email = Email("Black Friday 2028!", "50% discount on our platform", "bf@epicpython.io")

    # change the class attribute
    Email.valid_domain = "example.com"

    greeting_email.from_recipient = "greeting@example.com"
    bf_email.from_recipient = "bf@example.com"

    greeting_email.send("bob@nasa.gov")
    bf_email.send("alex@gmail.com")
```

Since the `valid_domain` attribute is tied to the class `Email`, we can change it for both instances created from the it by referencing the class itself instead of the instances.

<br/>
<div align="right">
  <b><a href="#section-01-basics-concepts">[ ↥ Back To Top ]</a></b>
</div>
<br/>

### Pitfall of Immutable Objects

If we change the class attribute by accessing the instance, the change would impact only one instance.

```python
# change the class attribute by referencing the class it self
Email.valid_domain = "example.com"

# change the class attribute by accessing the instance
greeting_email.valid_doman = "example.com"
```

Be very careful because this behavior will not apply in all cases! If the class attribute type is immutable objects such as a list. The updated list will propagate to all instances even if we're doing it from an instance.

```python
class Test:
    test_list = []

# create the instances from class Test
t1 = Test()
t2 = Test()
print(t1.test_list)       # []
print(t2.test_list)       # []

# append the list by referencing the class it self
Test.test_list.append(1)
print(t1.test_list)       # [1]
print(t2.test_list)       # [1]

# append the list by accessing the instance
t2.test_list.append(2)
print(t1.test_list)       # [1, 2]
print(t2.test_list)       # [1, 2]

# check the address with id()
print(id(t1.test_list))   # 1928918893888
print(id(t2.test_list))   # 1928918893888

t1.test_list.append(5)

print(id(t1.test_list))   # 1928918893888
print(id(t2.test_list))   # 1928918893888

# assign the list by accessing the instance
t1.test_list = [10, 20]

print(id(t1.test_list))   # 1928911604864
print(id(t2.test_list))   # 1928918893888

print(t1.test_list)       # [10, 20]
print(t2.test_list)       # [1, 2, 5]
```

- When we are creating the empty list inside the class, all instances are pointing to the same address where that list resides.
- The `append()` method is reusing the address and adding one element to the same list.

In order to modify the list only for one of the instance, we should use an assignment. Note that the Python model is **passed by object reference**.

<br/>
<div align="right">
  <b><a href="#section-01-basics-concepts">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Class Methods and Static Methods

- **The Class Methods** don't have access to the instance attributes. They have access to the class from the class object.
- **The Static Methods** don't have access to either the class or the instance. Just like a normal function that doesn't belong to a class.

```python
class Email:
    valid_domain = "epicpython.io"

    def __init__(self, subject, body, from_recipient):
        self.subject = subject
        self.body = body
        self.is_from_recipient_valid(self.valid_domain, from_recipient)
        self._from_recipient = from_recipient

    @property
    def from_recipient(self):
        return self.__from_recipient

    @from_recipient.setter
    def from_recipient(self, from_recipient):
        self.is_from_recipient_valid(self.valid_domain, from_recipient)
        self.__from_recipient = from_recipient

    def send(self, to):
        print(f"Sending email from: {self.__from_recipient} with subject: {self.subject} and body: {self.body} to : {to}")

    @classmethod
    def greeting(cls):
        return cls("Welcome", "Welcome to epicpython.io", "greeting@epicpython.io")

    @staticmethod
    def is_from_recipient_valid(valid_domain, from_recipient):
        split = from_recipient.split("@")
        if split[1] != self.valid_domain
            raise Exception("Invalid Domain")


if __name__ == "__main__":
    greeting_email = Email.greeting()
    bf_email = Email("Black Friday 2028!", "50% discount on our platform", "bf@epicpython.io")

    bf_email.from_recipient = "bf@epicpython.uk"

    greeting_email.send("bob@nasa.gov")
    bf_email.send("alex@gmail.com")
```

<br/>
<div align="right">
  <b><a href="#section-01-basics-concepts">[ ↥ Back To Top ]</a></b>
</div>
<br/>