# Object-Oriented Programming (OOP) in Python

Object-Oriented Programming (OOP) is a programming approach where we organize code using objects.

An object contains data, called attributes, and behavior, called methods.

In Python, a class is used as a blueprint for creating objects.

## Class and Object

A class defines the structure and behavior of an object, while an object is an actual instance of that class.

```python
class Car:
    def __init__(self, brand):
        self.brand = brand

    def drive(self):
        print(f"{self.brand} is driving")


# Creating objects
car1 = Car("Toyota")
car2 = Car("BMW")

car1.drive()
car2.drive()
```

Here:

- `Car` is the class.
- `car1` and `car2` are objects.
- `brand` is an attribute.
- `drive()` is a method.
- `__init__()` initializes the object when it is created.

## Four Main Principles of OOP

The four main principles of Object-Oriented Programming are:

1. Encapsulation
2. Inheritance
3. Polymorphism
4. Abstraction

## 1. Encapsulation

Encapsulation means keeping data and the methods that operate on that data together, while controlling how the data is accessed.

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def deposit(self, amount):
        self.__balance += amount

    def get_balance(self):
        return self.__balance


account = BankAccount(1000)

account.deposit(500)

print(account.get_balance())
```

Here, `__balance` is not intended to be accessed directly from outside the class. The balance is changed through methods such as `deposit()`.

## 2. Inheritance

Inheritance allows a child class to reuse properties and methods from a parent class.

```python
class Animal:
    def eat(self):
        print("Eating")


class Dog(Animal):
    def bark(self):
        print("Barking")


dog = Dog()

dog.eat()
dog.bark()
```

Here, `Dog` inherits the `eat()` method from `Animal`.

This helps reduce duplicate code and makes code easier to reuse.

## 3. Polymorphism

Polymorphism means that the same method can behave differently for different objects.

```python
class Dog:
    def sound(self):
        print("Bark")


class Cat:
    def sound(self):
        print("Meow")


animals = [Dog(), Cat()]

for animal in animals:
    animal.sound()
```

The same `sound()` method is called for both objects, but each object provides its own behavior.

Output:

```text
Bark
Meow
```

## 4. Abstraction

Abstraction means hiding unnecessary implementation details and exposing only what is required.

Python provides abstract classes through the `abc` module.

```python
from abc import ABC, abstractmethod


class Payment(ABC):
    @abstractmethod
    def pay(self):
        pass


class UPI(Payment):
    def pay(self):
        print("Processing UPI payment")


class CreditCard(Payment):
    def pay(self):
        print("Processing credit card payment")


payment = UPI()

payment.pay()
```

The user only needs to call `pay()`. The internal implementation of the payment process is hidden.



## Reference

This introduction is based on the provided OOP reference document.

The reference document also points to the following official Python documentation:

- Python Classes: https://docs.python.org/3/tutorial/classes.html
- Python Data Model: https://docs.python.org/3/reference/datamodel.html
- Abstract Base Classes: https://docs.python.org/3/library/abc.html