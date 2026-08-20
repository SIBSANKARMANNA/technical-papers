# SOLID Principles in Python

SOLID is a group of five object-oriented design principles that help us write code that is easier to understand, maintain, test, and extend.

The main idea is simple: keep classes focused, reduce unnecessary dependencies, and make it easier to add new features without breaking existing code.

## S — Single Responsibility Principle (SRP)

A class should have one responsibility, or one main reason to change.

- Keep related work together.
- Avoid putting database, email, reporting, and business logic in one class.
- Smaller responsibilities make code easier to test and maintain.

### Problem

The `Order` class below is doing too many things.

```python
class Order:
    def calculate_total(self):
        print("Calculating total")

    def save_to_database(self):
        print("Saving order")

    def generate_invoice(self):
        print("Generating invoice")

    def send_email(self):
        print("Sending email")
```

The class has multiple reasons to change.

### Better Design

```python
class Order:
    def calculate_total(self):
        print("Calculating total")


class OrderRepository:
    def save(self):
        print("Saving order")


class InvoiceService:
    def generate_invoice(self):
        print("Generating invoice")


class EmailService:
    def send_email(self):
        print("Sending email")
```

Now each class has one clear responsibility.

## O — Open/Closed Principle (OCP)

Software should be open for extension but closed for modification.

- We should be able to add new behavior.
- We should avoid repeatedly changing existing, tested code.
- Polymorphism and abstraction are commonly used to achieve this.

### Problem

```python
class PaymentProcessor:
    def pay(self, payment_type):
        if payment_type == "credit":
            print("Credit Card Payment")
        elif payment_type == "upi":
            print("UPI Payment")
        elif payment_type == "paypal":
            print("PayPal Payment")
```

Every time a new payment method is added, this class has to be modified.

### Better Design

```python
from abc import ABC, abstractmethod


class PaymentProcessor(ABC):
    @abstractmethod
    def pay(self):
        pass


class CreditCardPayment(PaymentProcessor):
    def pay(self):
        print("Credit Card Payment")


class UPIPayment(PaymentProcessor):
    def pay(self):
        print("UPI Payment")


class PayPalPayment(PaymentProcessor):
    def pay(self):
        print("PayPal Payment")


payments = [
    CreditCardPayment(),
    UPIPayment(),
    PayPalPayment(),
]

for payment in payments:
    payment.pay()
```

If we need Bitcoin later, we can add another class without changing the existing payment classes.

## L — Liskov Substitution Principle (LSP)

A child class should be usable wherever its parent class is expected without breaking the program.

- A child class should follow the behavior promised by the parent.
- Do not use inheritance when the child cannot properly support the parent's behavior.
- LSP makes polymorphism reliable.

### Problem

```python
class Bird:
    def fly(self):
        print("Flying")


class Sparrow(Bird):
    pass


class Penguin(Bird):
    def fly(self):
        raise Exception("Penguins cannot fly")
```

`Penguin` is a `Bird`, but it cannot properly support the behavior promised by `Bird`.

### Better Design

```python
class Bird:
    def eat(self):
        print("Eating")


class FlyingBird(Bird):
    def fly(self):
        print("Flying")


class Sparrow(FlyingBird):
    pass


class Penguin(Bird):
    pass
```

Now `Penguin` does not inherit a behavior that it cannot support.

## I — Interface Segregation Principle (ISP)

A class should not be forced to depend on methods that it does not need.

- Prefer small and focused interfaces.
- Avoid one large interface containing unrelated operations.
- Classes should implement only the capabilities they actually support.

### Problem

```python
from abc import ABC, abstractmethod


class PaymentService(ABC):
    @abstractmethod
    def pay(self):
        pass

    @abstractmethod
    def refund(self):
        pass

    @abstractmethod
    def pay_emi(self):
        pass


class GiftCardPayment(PaymentService):
    def pay(self):
        print("Gift Card Payment")

    def refund(self):
        raise NotImplementedError

    def pay_emi(self):
        raise NotImplementedError
```

The gift card is forced to implement methods that it does not support.

### Better Design

```python
from abc import ABC, abstractmethod


class Payable(ABC):
    @abstractmethod
    def pay(self):
        pass


class Refundable(ABC):
    @abstractmethod
    def refund(self):
        pass


class EMICompatible(ABC):
    @abstractmethod
    def pay_emi(self):
        pass


class GiftCardPayment(Payable):
    def pay(self):
        print("Gift Card Payment")


class UPIPayment(Payable, Refundable):
    def pay(self):
        print("UPI Payment")

    def refund(self):
        print("UPI Refund")


class CreditCardPayment(Payable, Refundable, EMICompatible):
    def pay(self):
        print("Credit Card Payment")

    def refund(self):
        print("Credit Card Refund")

    def pay_emi(self):
        print("Credit Card EMI Payment")
```

Each class now implements only the capabilities it needs.

## D — Dependency Inversion Principle (DIP)

High-level code should not directly depend on low-level concrete implementations. Both should depend on an abstraction.

- Depend on abstractions rather than concrete classes.
- Avoid creating dependencies directly inside business logic.
- Dependency Injection is a common technique used to achieve this.

### Problem

```python
class CreditCardPayment:
    def pay(self, amount):
        print(f"{amount} paid using Credit Card")


class OrderService:
    def __init__(self):
        self.payment = CreditCardPayment()

    def place_order(self, amount):
        print("Creating order")
        self.payment.pay(amount)
        print("Order placed")
```

`OrderService` is tightly coupled to `CreditCardPayment`.

If we change to UPI, we have to modify `OrderService`.

### Better Design

```python
from abc import ABC, abstractmethod


class PaymentProcessor(ABC):
    @abstractmethod
    def pay(self, amount):
        pass


class CreditCardPayment(PaymentProcessor):
    def pay(self, amount):
        print(f"{amount} paid using Credit Card")


class UPIPayment(PaymentProcessor):
    def pay(self, amount):
        print(f"{amount} paid using UPI")


class OrderService:
    def __init__(self, payment_processor):
        self.payment_processor = payment_processor

    def place_order(self, amount):
        print("Creating order")
        self.payment_processor.pay(amount)
        print("Order placed")


credit_card = CreditCardPayment()
service = OrderService(credit_card)

service.place_order(2000)
```

Now we can use UPI without changing `OrderService`.

```python
upi = UPIPayment()
service = OrderService(upi)

service.place_order(2000)
```

The dependency is provided from outside. This is dependency injection.


## Final Idea

SOLID is not about creating as many classes as possible. It is about making the design easier to change.

A good way to remember the five principles is:

- S: One class, one responsibility.
- O: Extend without modifying stable code.
- L: Child should behave like its parent.
- I: Keep interfaces small and focused.
- D: Depend on abstractions, not concrete implementations.

## Reference

https://www.baeldung.com/solid-principles
https://www.splunk.com/en_us/blog/learn/solid-design-principle.html

