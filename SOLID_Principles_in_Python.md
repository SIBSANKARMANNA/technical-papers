# SOLID Principles in Python

## Introduction

As software applications grow, their codebase becomes increasingly complex. New features are added, bugs are fixed, and multiple developers work on the same project. Without proper design principles, software often becomes difficult to understand, maintain, extend, and test.

To address these challenges, software engineers follow a set of object-oriented design principles known as **SOLID**. These principles provide guidelines for designing classes and modules that are **loosely coupled**, **highly cohesive**, **maintainable**, and **scalable**.

Rather than introducing new programming syntax, SOLID teaches developers **how to organize classes and their responsibilities**. These principles are widely used in enterprise applications, web development, desktop software, mobile applications, and large-scale distributed systems.

A strong understanding of SOLID enables developers to write cleaner code, reduce future maintenance costs, and build software that can evolve without frequent modifications.

---

# Table of Contents

1. Introduction
2. What are SOLID Principles?
3. Why Do We Need SOLID?
4. Problems Without SOLID
5. Meaning of SOLID
6. Single Responsibility Principle (SRP)
7. Open/Closed Principle (OCP)
8. Liskov Substitution Principle (LSP)
9. Interface Segregation Principle (ISP)
10. Dependency Inversion Principle (DIP)
11. SOLID Principles Together
12. Advantages of SOLID
13. Disadvantages of SOLID
14. Best Practices
15. Common Mistakes
16. Real-world Applications
17. Summary
18. References

---

# What are SOLID Principles?

**SOLID** is a collection of **five object-oriented design principles** that help developers create software that is easier to understand, extend, test, and maintain.

These principles were introduced by **Robert C. Martin (popularly known as Uncle Bob)** based on earlier object-oriented design concepts introduced by **Bertrand Meyer**.

SOLID does **not** introduce new syntax or programming features. Instead, it provides a set of design guidelines for organizing classes, objects, and their relationships.

When followed correctly, SOLID promotes:

- High Cohesion
- Low Coupling
- Better Code Reusability
- Easier Unit Testing
- Better Maintainability
- Improved Scalability
- Flexible Software Design

---

# Why Do We Need SOLID?

Consider a software project that initially contains only a few hundred lines of code.

As the project grows:

- New features are added.
- Business requirements change.
- More developers join the project.
- Bugs are fixed.
- Existing functionality is modified.

Without proper design, developers often encounter the following problems:

- Large classes containing unrelated responsibilities.
- One change breaking multiple modules.
- Difficulty adding new features.
- High dependency between classes.
- Duplicate code.
- Difficult unit testing.
- Poor readability and maintainability.

SOLID principles were created to solve these design problems by encouraging **small, focused, and loosely coupled classes**.

---

# Problems Without SOLID

Consider the following class.

```python
class Employee:

    def calculate_salary(self):
        print("Calculating Salary")

    def save_to_database(self):
        print("Saving Employee")

    def generate_report(self):
        print("Generating Report")

    def send_email(self):
        print("Sending Email")
```

At first glance, the code appears correct.

However, this class performs **multiple unrelated responsibilities**.

```
Employee
│
├── Calculate Salary
├── Save Database
├── Generate Report
└── Send Email
```

Now imagine the following changes:

- The salary calculation logic changes.
- The database changes from MySQL to PostgreSQL.
- The report format changes from PDF to Excel.
- The email service changes to an external API.

Each change requires modifying the same class.

This leads to:

- Increased risk of bugs.
- Difficult testing.
- Frequent code modifications.
- Poor maintainability.

This is exactly the type of problem that SOLID principles help solve.

---

# Meaning of SOLID

SOLID is an acronym formed from the first letter of five object-oriented design principles.

| Letter | Principle | Purpose |
|----------|-----------|---------|
| **S** | Single Responsibility Principle | A class should have only one responsibility. |
| **O** | Open/Closed Principle | Software should be open for extension but closed for modification. |
| **L** | Liskov Substitution Principle | Child classes should be replaceable wherever parent classes are used. |
| **I** | Interface Segregation Principle | Clients should not be forced to depend on methods they do not use. |
| **D** | Dependency Inversion Principle | High-level modules should depend on abstractions rather than concrete implementations. |

---

# Understanding the SOLID Principles

Although each principle focuses on a different aspect of software design, they all work together to achieve a common goal:

- Build software that is easier to maintain.
- Reduce coupling between classes.
- Improve code readability.
- Make testing easier.
- Allow new features to be added with minimal changes.
- Encourage reusable and extensible designs.

The following sections explain each principle individually with practical Python examples, real-world analogies, and best practices.

---

# Relationship Between OOP and SOLID

Before learning SOLID, it is important to understand that **SOLID is built on top of Object-Oriented Programming (OOP).**

OOP provides the fundamental concepts:

- Classes
- Objects
- Encapsulation
- Inheritance
- Polymorphism
- Abstraction

SOLID uses these OOP concepts as building blocks to create better software designs.

```
Object-Oriented Programming
│
├── Classes
├── Objects
├── Encapsulation
├── Inheritance
├── Polymorphism
└── Abstraction
        │
        ▼
   SOLID Principles
        │
        ▼
Clean, Maintainable, Scalable Software
```

In simple terms:

- **OOP teaches you how to create classes and objects.**
- **SOLID teaches you how to design those classes correctly.**

Without OOP, SOLID cannot be applied effectively.

---

## Key Takeaways

- SOLID is a set of **five design principles**, not a programming language feature.
- SOLID focuses on **software design**, not syntax.
- The principles complement Object-Oriented Programming.
- Following SOLID leads to software that is easier to maintain, extend, and test.
- SOLID is widely used in enterprise applications, backend development, frameworks, and large-scale software systems.

---

# Single Responsibility Principle (SRP)

## Definition

The **Single Responsibility Principle (SRP)** states that:

> **A class should have only one reason to change.**

In other words, a class should have **one responsibility** or **one job**.

If a class performs multiple unrelated tasks, changes in one task may unintentionally affect the others, making the software difficult to maintain and test.

---

# Why Do We Need SRP?

Imagine an online shopping application.

When a customer places an order, several operations need to be performed:

- Calculate the total amount.
- Save the order to the database.
- Generate an invoice.
- Send a confirmation email.

A beginner might write all these operations inside a single class.

Although the program works, the design is poor because one class is responsible for multiple independent tasks.

---

# Bad Design (Violates SRP)

```python
class Order:

    def calculate_total(self):
        print("Calculating total amount...")

    def save_order(self):
        print("Saving order to database...")

    def generate_invoice(self):
        print("Generating invoice...")

    def send_confirmation_email(self):
        print("Sending confirmation email...")
```

### Usage

```python
order = Order()

order.calculate_total()
order.save_order()
order.generate_invoice()
order.send_confirmation_email()
```

### Output

```
Calculating total amount...
Saving order to database...
Generating invoice...
Sending confirmation email...
```

---

# What's Wrong with This Design?

The `Order` class is responsible for **four different jobs**.

```
                Order
                  │
     ┌────────────┼────────────┐
     │            │            │
 Calculate     Save        Generate
  Total       Database     Invoice
                  │
             Send Email
```

Now suppose:

- The database changes from **MySQL** to **PostgreSQL**.
- The invoice changes from **PDF** to **Excel**.
- The email service changes to **AWS SES**.

Even though the order calculation hasn't changed, the **Order** class must still be modified.

This means the class has **multiple reasons to change**, violating SRP.

---

# Good Design (Follows SRP)

Instead of one large class, divide the responsibilities into separate classes.

```python
class Order:
    """
    Responsible only for order calculations.
    """

    def calculate_total(self):
        print("Calculating total amount...")


class OrderRepository:
    """
    Responsible only for storing orders.
    """

    def save(self):
        print("Saving order to database...")


class InvoiceService:
    """
    Responsible only for invoice generation.
    """

    def generate_invoice(self):
        print("Generating invoice...")


class EmailService:
    """
    Responsible only for sending emails.
    """

    def send_confirmation(self):
        print("Sending confirmation email...")
```

---

# Usage

```python
order = Order()
repository = OrderRepository()
invoice = InvoiceService()
email = EmailService()

order.calculate_total()
repository.save()
invoice.generate_invoice()
email.send_confirmation()
```

### Output

```
Calculating total amount...
Saving order to database...
Generating invoice...
Sending confirmation email...
```

---

# Why Is This Better?

Now each class has **only one responsibility**.

```
Order
│
└── Calculate Total


OrderRepository
│
└── Save Order


InvoiceService
│
└── Generate Invoice


EmailService
│
└── Send Confirmation Email
```

Suppose the company changes the email provider.

Only this class changes:

```
EmailService
```

The remaining classes remain untouched.

Similarly,

If invoice generation changes:

Only

```
InvoiceService
```

needs modification.

This reduces the chances of introducing bugs into unrelated parts of the system.

---

# Real-world Analogy

Think of an online shopping company.

Different employees perform different tasks.

```
Customer Places Order
          │
          ▼

   Billing Department
          │
Calculate Amount

          ▼

 Warehouse
          │
 Pack Product

          ▼

Delivery Team
          │
Deliver Product

          ▼

Email Team
          │
Send Confirmation
```

Imagine asking **one employee** to do all these jobs.

The system would become difficult to manage, and any change in one task would affect the entire workflow.

Similarly, in software design, **one class should perform one well-defined responsibility**.

---

# Advantages of SRP

- Easier to understand.
- Easier to test.
- Easier to maintain.
- Reduces code duplication.
- Improves readability.
- Makes debugging simpler.
- Encourages reusable components.
- Reduces coupling between classes.

---

# Best Practices

✔ Keep classes small and focused.

✔ Group related functionality together.

✔ Avoid creating "God Classes" that perform many unrelated tasks.

✔ Separate business logic, database operations, reporting, and communication into different classes.

---

# Common Beginner Mistakes

❌ Putting database code inside business classes.

❌ Sending emails from model classes.

❌ Generating reports inside entity classes.

❌ Creating one class with dozens of unrelated methods.

---

# Interview Tip

A common interview question is:

> **What does "one reason to change" mean?**

It **does not** mean a class should have only one method.

It means **all methods in the class should support a single responsibility**.

For example:

```python
class BankAccount:

    def deposit(self):
        pass

    def withdraw(self):
        pass

    def check_balance(self):
        pass
```

This class has **three methods**, but they all relate to **one responsibility**: managing a bank account.

Therefore, it still follows the Single Responsibility Principle.

However,

```python
class BankAccount:

    def deposit(self):
        pass

    def withdraw(self):
        pass

    def send_email(self):
        pass

    def generate_salary_report(self):
        pass
```

Now the class manages:

- Banking
- Email
- Reporting

These are unrelated responsibilities, so the class violates SRP.

---

# Key Takeaways

- A class should have **one responsibility**.
- A class should have **one reason to change**.
- Separate unrelated functionality into different classes.
- SRP improves maintainability, readability, and testability.
- SRP forms the foundation for the remaining SOLID principles.

---

# Open/Closed Principle (OCP)

## Definition

The **Open/Closed Principle (OCP)** states that:

> **Software entities (classes, modules, functions) should be open for extension but closed for modification.**

This means:

- **Open for Extension** → We should be able to add new functionality.
- **Closed for Modification** → Existing, tested code should not need to be changed.

The primary goal of OCP is to reduce the risk of introducing bugs into existing software when adding new features.

---

# Why Do We Need OCP?

Suppose our online shopping application currently supports only **Credit Card** payments.

Later, the company decides to support:

- UPI
- PayPal
- Net Banking

A common beginner approach is to repeatedly modify the existing payment class whenever a new payment method is introduced.

This violates OCP because existing code changes every time a new feature is added.

---

# Bad Design (Violates OCP)

```python
class PaymentProcessor:

    def pay(self, payment_type):

        if payment_type == "credit":
            print("Processing Credit Card Payment")

        elif payment_type == "upi":
            print("Processing UPI Payment")

        elif payment_type == "paypal":
            print("Processing PayPal Payment")
```

### Usage

```python
payment = PaymentProcessor()

payment.pay("credit")
payment.pay("upi")
```

### Output

```
Processing Credit Card Payment
Processing UPI Payment
```

---

# What's Wrong with This Design?

Every time a new payment method is introduced, we must modify this class.

For example:

Today:

```
Credit Card
```

Tomorrow:

```
Credit Card
UPI
```

Next Month:

```
Credit Card
UPI
PayPal
```

Next Year:

```
Credit Card
UPI
PayPal
Apple Pay
Google Pay
Bitcoin
```

The class continuously changes.

Each modification increases the possibility of introducing bugs into previously working code.

---

# Good Design (Follows OCP)

Instead of modifying the existing class, we create new classes that extend the system.

---

## Step 1 — Create an Abstract Payment Class

```python
from abc import ABC, abstractmethod

class PaymentProcessor(ABC):

    @abstractmethod
    def pay(self):
        pass
```

---

## Step 2 — Implement Individual Payment Methods

```python
class CreditCardPayment(PaymentProcessor):

    def pay(self):
        print("Processing Credit Card Payment")


class UPIPayment(PaymentProcessor):

    def pay(self):
        print("Processing UPI Payment")


class PayPalPayment(PaymentProcessor):

    def pay(self):
        print("Processing PayPal Payment")
```

---

## Usage

```python
payments = [
    CreditCardPayment(),
    UPIPayment(),
    PayPalPayment()
]

for payment in payments:
    payment.pay()
```

### Output

```
Processing Credit Card Payment
Processing UPI Payment
Processing PayPal Payment
```

---

# Why Is This Better?

Suppose tomorrow the company wants to support **Bitcoin**.

We simply create another class.

```python
class BitcoinPayment(PaymentProcessor):

    def pay(self):
        print("Processing Bitcoin Payment")
```

Nothing else changes.

No existing class needs modification.

This is exactly what OCP recommends.

---

# Real-world Analogy

Think about a smartphone.

Initially it contains:

- Camera
- Calculator
- Browser

Later, you install:

- WhatsApp
- Instagram
- Spotify

Notice:

The operating system was **extended**.

It wasn't rewritten every time you installed a new application.

Similarly, software should allow new functionality without modifying stable code.

---

# Advantages of OCP

- Reduces bugs.
- Easier feature addition.
- Protects existing code.
- Improves scalability.
- Encourages abstraction and polymorphism.

---

# Best Practices

✔ Use inheritance and polymorphism.

✔ Program against abstractions.

✔ Avoid long `if-else` chains for behavior selection.

✔ Add new functionality through new classes.

---

# Common Beginner Mistakes

❌ Repeatedly modifying existing classes.

❌ Large switch/if-else statements.

❌ Tight coupling between business logic and implementations.

---

# Interview Tip

A common interview question is:

> **How do inheritance and polymorphism help implement OCP?**

Answer:

A parent abstraction defines common behavior, while child classes provide new implementations. New functionality is added by creating new child classes instead of modifying existing ones.

---

# Liskov Substitution Principle (LSP)

## Definition

The **Liskov Substitution Principle (LSP)** states that:

> **Objects of a child class should be replaceable with objects of the parent class without changing the correctness of the program.**

In simple words,

> **A child class must behave like its parent promises.**

If replacing the parent with the child causes the application to fail, LSP has been violated.

---

# Why Do We Need LSP?

Continuing our shopping system...

We already created different payment methods.

```
PaymentProcessor
       │
 ┌─────┴──────────────┐
 │        │           │
Credit   UPI      PayPal
```

Suppose our checkout process expects **any PaymentProcessor**.

If replacing one payment class with another breaks the checkout flow, the design is incorrect.

---

# Bad Design (Violates LSP)

```python
from abc import ABC, abstractmethod

class PaymentProcessor(ABC):

    @abstractmethod
    def pay(self):
        pass


class CreditCardPayment(PaymentProcessor):

    def pay(self):
        print("Credit Card Payment Successful")


class BrokenPayment(PaymentProcessor):

    def pay(self):
        raise Exception("Payment Failed")
```

Usage

```python
payment = BrokenPayment()

payment.pay()
```

Output

```
Exception:
Payment Failed
```

Although `BrokenPayment` inherits from `PaymentProcessor`, it does not behave as a valid payment processor.

The parent class promises:

```
Every payment processor can process payments.
```

The child breaks that promise.

---

# Good Design (Follows LSP)

```python
from abc import ABC, abstractmethod

class PaymentProcessor(ABC):

    @abstractmethod
    def pay(self):
        pass


class CreditCardPayment(PaymentProcessor):

    def pay(self):
        print("Credit Card Payment Successful")


class UPIPayment(PaymentProcessor):

    def pay(self):
        print("UPI Payment Successful")


class PayPalPayment(PaymentProcessor):

    def pay(self):
        print("PayPal Payment Successful")
```

Usage

```python
payments = [
    CreditCardPayment(),
    UPIPayment(),
    PayPalPayment()
]

for payment in payments:
    payment.pay()
```

Output

```
Credit Card Payment Successful
UPI Payment Successful
PayPal Payment Successful
```

Every child class behaves correctly.

The checkout process never needs to know which payment processor it receives.

---

# Another Popular Example

Bad Design

```
Bird
 │
 ├── Sparrow
 └── Penguin
```

If `Bird` defines

```python
fly()
```

then

```python
Penguin.fly()
```

fails.

Penguins cannot fly.

Instead

```
Bird
 │
 ├── FlyingBird
 │      │
 │   Sparrow
 │   Eagle
 │
 └── Penguin
```

Now no child violates the parent contract.

---

# Real-world Analogy

Imagine a TV remote.

Every television from different manufacturers should respond to the basic buttons:

- Power
- Volume
- Channel

If one TV throws an error when you press the Power button, it cannot truly replace another TV in the same setup.

That violates LSP.

Similarly, subclasses must honor the behavior expected from their parent class.

---

# Advantages of LSP

- Improves reliability.
- Makes inheritance safer.
- Supports runtime polymorphism.
- Reduces unexpected behavior.
- Makes systems easier to extend.

---

# Best Practices

✔ Child classes should preserve parent behavior.

✔ Avoid overriding methods to completely change their meaning.

✔ Use inheritance only when there is a true **IS-A** relationship.

---

# Common Beginner Mistakes

❌ Using inheritance simply to reuse code.

❌ Throwing exceptions in overridden methods because the child cannot perform the parent's behavior.

❌ Breaking assumptions made by the parent class.

---

# Interview Tip

A common interview question is:

> **How is LSP different from OCP?**

**OCP** focuses on **adding new functionality without modifying existing code.**

**LSP** focuses on ensuring that **new child classes behave correctly wherever the parent class is expected.**

Without LSP, polymorphism becomes unreliable.

---

# Key Takeaways

### Open/Closed Principle

- Extend software through new classes.
- Avoid modifying stable code.
- Use abstraction and polymorphism.

### Liskov Substitution Principle

- Child classes must honor the parent's contract.
- Replacing a parent with a child should never break the application.
- Use inheritance only when the relationship is logically correct.

---

# Interface Segregation Principle (ISP)

## Definition

The **Interface Segregation Principle (ISP)** states that:

> **A class should not be forced to depend on methods that it does not use.**

In simple terms:

> **Prefer small, focused interfaces instead of one large interface containing unrelated operations.**

In Python, we do not have a dedicated `interface` keyword like Java. Interfaces can be represented using **Abstract Base Classes (ABC)**, protocols, or similar abstractions.

---

# Why Do We Need ISP?

Continuing with our **Online Shopping System**, suppose we create one interface for all payment-related operations:

- Pay
- Refund
- EMI Payment

However, not every payment method supports all these operations.

For example:

```
Credit Card
├── Pay
├── Refund
└── EMI


UPI
├── Pay
└── Refund


Gift Card
└── Pay
```

If we put all three operations into one interface, every payment class will be forced to implement methods it may not support.

This creates unnecessary dependencies and violates ISP.

---

# Bad Design (Violates ISP)

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
```

Now consider a gift card.

```python
class GiftCardPayment(PaymentService):

    def pay(self):
        print("Payment completed using Gift Card")

    def refund(self):
        raise NotImplementedError(
            "Gift Card refund is not supported"
        )

    def pay_emi(self):
        raise NotImplementedError(
            "Gift Card EMI is not supported"
        )
```

### Usage

```python
payment = GiftCardPayment()

payment.pay()
payment.pay_emi()
```

### Output

```text
Payment completed using Gift Card

NotImplementedError:
Gift Card EMI is not supported
```

The problem is not that the exception exists.

The real problem is that `GiftCardPayment` was **forced to implement methods that do not belong to its capabilities**.

---

# Good Design (Follows ISP)

Instead of creating one large interface, divide it into smaller interfaces.

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
```

Now classes implement only the capabilities they actually support.

---

## Credit Card

Credit cards support all three operations.

```python
class CreditCardPayment(
    Payable,
    Refundable,
    EMICompatible
):

    def pay(self):
        print("Credit Card Payment Successful")

    def refund(self):
        print("Credit Card Refund Successful")

    def pay_emi(self):
        print("Credit Card EMI Payment Successful")
```

---

## UPI

Suppose UPI supports payment and refund but not EMI in our application.

```python
class UPIPayment(Payable, Refundable):

    def pay(self):
        print("UPI Payment Successful")

    def refund(self):
        print("UPI Refund Successful")
```

---

## Gift Card

Suppose a gift card supports only payment.

```python
class GiftCardPayment(Payable):

    def pay(self):
        print("Gift Card Payment Successful")
```

---

# Usage

```python
credit_card = CreditCardPayment()
upi = UPIPayment()
gift_card = GiftCardPayment()

credit_card.pay()
credit_card.pay_emi()

upi.pay()
upi.refund()

gift_card.pay()
```

### Output

```text
Credit Card Payment Successful
Credit Card EMI Payment Successful
UPI Payment Successful
UPI Refund Successful
Gift Card Payment Successful
```

---

# Why Is This Better?

Now every class depends only on the functionality it actually requires.

```text
                 Payable
                /   |   \
               /    |    \
        CreditCard UPI  GiftCard


              Refundable
               /      \
              /        \
      CreditCard       UPI


            EMICompatible
                  |
                  |
             CreditCard
```

`GiftCardPayment` is no longer forced to implement:

```python
refund()
pay_emi()
```

because it does not support those operations.

---

# Real-world Analogy

Consider a multifunction office machine.

A large interface might require:

```text
Machine
├── print()
├── scan()
├── fax()
└── photocopy()
```

But a basic printer can only:

```text
print()
```

It should not be forced to implement:

```text
scan()
fax()
photocopy()
```

A better design separates the capabilities:

```text
Printable
└── print()

Scannable
└── scan()

Faxable
└── fax()
```

Devices implement only the capabilities they support.

---

# Advantages of ISP

- Prevents unnecessary dependencies.
- Creates smaller and focused interfaces.
- Makes classes easier to understand.
- Improves maintainability.
- Improves testability.
- Reduces unnecessary implementations.

---

# Best Practices

- Keep interfaces small and focused.
- Separate unrelated behaviors.
- Do not force classes to implement unsupported operations.
- Design interfaces around client requirements.
- Prefer multiple focused abstractions over one large abstraction.

---

# Interview Tip

A common interview question is:

> **What is a "fat interface"?**

A **fat interface** contains too many unrelated methods and forces implementing classes to depend on operations they do not need.

ISP recommends splitting such an interface into smaller, focused interfaces.

---

# Dependency Inversion Principle (DIP)

## Definition

The **Dependency Inversion Principle (DIP)** states that:

> **High-level modules should not depend on low-level modules. Both should depend on abstractions.**

It also states:

> **Abstractions should not depend on details. Details should depend on abstractions.**

This principle is mainly concerned with reducing **tight coupling** between classes.

---

# First Understand High-Level and Low-Level Modules

Consider our shopping application.

The checkout system contains:

```text
OrderService
```

Its responsibility is to handle the business process of placing an order.

This is a **high-level module**.

The actual payment might be performed using:

```text
CreditCardPayment
UPIPayment
PayPalPayment
```

These are implementation details and can be considered **lower-level modules** in this design.

The high-level business logic should not be tightly connected to one specific implementation.

---

# Bad Design (Violates DIP)

Suppose `OrderService` directly creates a credit card payment object.

```python
class CreditCardPayment:

    def pay(self, amount):
        print(
            f"₹{amount} paid using Credit Card"
        )


class OrderService:

    def __init__(self):

        # Tight coupling
        self.payment = CreditCardPayment()

    def place_order(self, amount):

        print("Creating Order")

        self.payment.pay(amount)

        print("Order Placed")
```

### Usage

```python
order_service = OrderService()

order_service.place_order(2000)
```

### Output

```text
Creating Order
₹2000 paid using Credit Card
Order Placed
```

The program works.

But there is a design problem.

---

# What Is the Problem?

`OrderService` directly depends on:

```text
CreditCardPayment
```

The dependency looks like:

```text
OrderService
      |
      |
      v
CreditCardPayment
```

Now suppose the company decides to use UPI.

We must modify:

```python
OrderService
```

Again, if the company adds PayPal, we modify it again.

The high-level business logic is therefore tightly coupled to a low-level payment implementation.

---

# Good Design (Follows DIP)

We introduce an abstraction between them.

```text
                 PaymentProcessor
                  (Abstraction)
                       ▲
                       |
              -------------------
              |                 |
     CreditCardPayment      UPIPayment


                       ▲
                       |
                  OrderService
```

Now `OrderService` depends on the abstraction.

---

## Step 1 — Create the Abstraction

```python
from abc import ABC, abstractmethod


class PaymentProcessor(ABC):

    @abstractmethod
    def pay(self, amount):
        pass
```

---

## Step 2 — Create Concrete Implementations

```python
class CreditCardPayment(PaymentProcessor):

    def pay(self, amount):
        print(
            f"₹{amount} paid using Credit Card"
        )


class UPIPayment(PaymentProcessor):

    def pay(self, amount):
        print(
            f"₹{amount} paid using UPI"
        )
```

---

## Step 3 — Make the High-Level Class Depend on the Abstraction

```python
class OrderService:

    def __init__(self, payment_processor):

        # Dependency is provided from outside
        self.payment_processor = payment_processor

    def place_order(self, amount):

        print("Creating Order")

        self.payment_processor.pay(amount)

        print("Order Placed")
```

Notice that `OrderService` does **not** create:

```python
CreditCardPayment()
```

or

```python
UPIPayment()
```

It simply expects something capable of processing a payment.

---

# Usage with Credit Card

```python
credit_card = CreditCardPayment()

order_service = OrderService(credit_card)

order_service.place_order(2000)
```

### Output

```text
Creating Order
₹2000 paid using Credit Card
Order Placed
```

---

# Usage with UPI

We only change the object supplied to `OrderService`.

```python
upi = UPIPayment()

order_service = OrderService(upi)

order_service.place_order(2000)
```

### Output

```text
Creating Order
₹2000 paid using UPI
Order Placed
```

Notice something very important:

```python
class OrderService:
```

did not change.

---

# Understanding the Dependency

### Before DIP

```text
OrderService
     |
     | directly depends on
     v
CreditCardPayment
```

This creates **tight coupling**.

---

### After DIP

```text
               PaymentProcessor
                (Abstraction)
                ▲            ▲
                |            |
                |            |
       CreditCardPayment   UPIPayment

                ▲
                |
          OrderService
```

Conceptually, both the high-level policy (`OrderService`) and the concrete payment implementations are designed around the `PaymentProcessor` abstraction.

`OrderService` no longer needs to know which concrete payment processor is being used.

---

# Dependency Injection

Notice this line:

```python
def __init__(self, payment_processor):
```

Instead of creating the dependency inside the class:

```python
self.payment = CreditCardPayment()
```

we provide it from outside:

```python
order_service = OrderService(credit_card)
```

This technique is called **Dependency Injection (DI)**.

---

# DIP vs Dependency Injection

These concepts are related but they are not identical.

### Dependency Inversion Principle

DIP is a **design principle**.

It tells us:

> Depend on abstractions rather than concrete implementations.

### Dependency Injection

Dependency Injection is a **technique** commonly used to achieve loose coupling and help implement DIP.

Instead of:

```python
class OrderService:

    def __init__(self):
        self.payment = CreditCardPayment()
```

we use:

```python
class OrderService:

    def __init__(self, payment):
        self.payment = payment
```

and inject the dependency:

```python
payment = CreditCardPayment()

service = OrderService(payment)
```

---

# Why Is DIP Important for Testing?

Suppose we want to test `OrderService`.

We don't want the test to make a real payment.

We can create a fake implementation.

```python
class FakePayment(PaymentProcessor):

    def pay(self, amount):
        print(f"Fake payment of ₹{amount}")
```

Now:

```python
fake_payment = FakePayment()

order_service = OrderService(fake_payment)

order_service.place_order(2000)
```

### Output

```text
Creating Order
Fake payment of ₹2000
Order Placed
```

The business logic can now be tested without connecting to a real payment gateway.

This is one of the major practical benefits of DIP.

---

# Real-world Analogy

Think about a laptop charger.

Your laptop does not need to know:

```text
Power Plant
      ↓
Transformer
      ↓
Electric Grid
      ↓
Wall Socket
```

The laptop depends on a standard **charging interface**.

Different power sources can provide electricity as long as they satisfy that interface.

Similarly:

```text
OrderService
```

doesn't need to understand:

```text
Credit Card
UPI
PayPal
Net Banking
```

It only needs a payment processor that follows the expected contract.

---

# Advantages of DIP

- Reduces tight coupling.
- Makes implementations replaceable.
- Makes unit testing easier.
- Improves maintainability.
- Supports extensible architecture.
- Makes future changes easier.
- Encourages abstraction.

---

# Best Practices

- Depend on abstractions rather than concrete classes.
- Inject dependencies instead of creating them inside business classes.
- Keep high-level business logic independent of infrastructure details.
- Use Abstract Base Classes or protocols where an explicit contract is useful.
- Avoid unnecessary abstractions when only one simple implementation exists and no variation is expected.

---

# Common Beginner Mistakes

❌ Creating dependencies directly inside classes.

```python
self.database = MySQL()
```

❌ Making business logic depend directly on frameworks or infrastructure.

❌ Creating abstractions for every single class even when they provide no design benefit.

❌ Confusing Dependency Inversion with Dependency Injection.

---

# Interview Tip

A very common interview question is:

> **What is the difference between DIP and Dependency Injection?**

The answer is:

**DIP is a design principle**, while **Dependency Injection is a technique that can be used to implement loosely coupled designs and support DIP.**

Another common question is:

> **Why should high-level modules depend on abstractions?**

Because concrete implementations frequently change. Depending on stable abstractions allows implementations to be replaced without modifying the high-level business logic.

---

# ISP vs DIP

These two principles can initially look similar, but they solve different problems.

| ISP | DIP |
|-----|-----|
| Focuses on interface size | Focuses on dependency direction |
| Avoids unnecessary methods | Avoids tight coupling |
| Splits large interfaces | Introduces useful abstractions |
| Classes depend only on needed operations | High-level logic avoids concrete implementation dependencies |

---

# Key Takeaways

## Interface Segregation Principle

- Do not force classes to implement methods they do not need.
- Prefer small, focused interfaces.
- Different classes can implement different combinations of capabilities.

## Dependency Inversion Principle

- High-level modules should not depend directly on low-level implementations.
- Both should be designed around abstractions.
- Concrete implementations should satisfy those abstractions.
- Dependency Injection is a common technique for supplying dependencies.
- DIP reduces coupling and greatly improves testability.

---

# SOLID Principles Working Together

By now, we have learned each SOLID principle individually. However, in real-world software development, these principles are **not used in isolation**. They complement each other to create software that is flexible, maintainable, and scalable.

Consider an **Online Shopping System**.

```
                     Customer
                         │
                         ▼
                  Order Service
                         │
        ┌────────────────┼────────────────┐
        │                │                │
        ▼                ▼                ▼
 Payment Processor   Invoice Service   Email Service
        │
        ▼
 -------------------------------
 │             │               │
 ▼             ▼               ▼
Credit Card   UPI          PayPal
```

Now let's see where each SOLID principle fits.

### Single Responsibility Principle (SRP)

Each class has only one responsibility.

```
OrderService
│
└── Manage Orders

PaymentProcessor
│
└── Process Payments

InvoiceService
│
└── Generate Invoices

EmailService
│
└── Send Confirmation Emails
```

Each class changes for only one reason.

---

### Open/Closed Principle (OCP)

Suppose the company wants to introduce **Apple Pay**.

Instead of modifying existing payment classes, we simply add:

```python
class ApplePayPayment(PaymentProcessor):

    def pay(self, amount):
        print(f"₹{amount} paid using Apple Pay")
```

No existing code needs modification.

---

### Liskov Substitution Principle (LSP)

Any payment method should work wherever a `PaymentProcessor` is expected.

```
PaymentProcessor
        │
 ┌──────┼───────────┐
 │      │           │
 ▼      ▼           ▼
UPI   CreditCard  PayPal
```

The checkout process should work regardless of which payment implementation is used.

---

### Interface Segregation Principle (ISP)

Not every payment method supports the same operations.

```
Payable
│
├── Credit Card
├── UPI
└── Gift Card

Refundable
│
├── Credit Card
└── UPI

EMICompatible
│
└── Credit Card
```

Each class implements only the capabilities it actually supports.

---

### Dependency Inversion Principle (DIP)

`OrderService` should not depend directly on a concrete payment implementation.

```
                 PaymentProcessor
                      ▲
      ┌───────────────┼───────────────┐
      │               │               │
      ▼               ▼               ▼
CreditCardPayment  UPIPayment   PayPalPayment
                      ▲
                      │
               OrderService
```

The high-level business logic depends on an abstraction, allowing payment methods to be replaced without changing `OrderService`.

---

# How the Principles Complement Each Other

| Principle | Main Goal |
|-----------|-----------|
| SRP | Keep classes focused on a single responsibility. |
| OCP | Add new features without modifying existing code. |
| LSP | Ensure child classes behave correctly wherever the parent is expected. |
| ISP | Keep interfaces small and focused. |
| DIP | Reduce coupling by depending on abstractions. |

Together, these principles encourage software that is modular, extensible, and easier to maintain.

---

# Advantages of SOLID

Applying SOLID principles provides several long-term benefits.

- Improves code readability.
- Reduces tight coupling.
- Encourages high cohesion.
- Makes applications easier to extend.
- Simplifies unit testing.
- Improves maintainability.
- Supports scalable software architecture.
- Reduces the likelihood of introducing bugs when adding new features.
- Enables multiple developers to work on different modules independently.

---

# Disadvantages of SOLID

Although SOLID offers many advantages, it also introduces certain trade-offs.

- More classes and abstractions may be required.
- Initial design takes more time.
- Can increase complexity for very small projects.
- Requires a good understanding of object-oriented design.
- Overusing abstractions may lead to unnecessary code if the application is simple.

---

# Best Practices

To apply SOLID effectively:

- Keep classes focused on one responsibility.
- Prefer composition over inheritance when appropriate.
- Program against abstractions rather than concrete implementations.
- Use inheritance only when there is a genuine **IS-A** relationship.
- Design small, meaningful interfaces.
- Avoid large conditional (`if-else`) blocks when polymorphism is a better solution.
- Apply SOLID where it provides value; avoid unnecessary abstractions in simple scripts.

---

# Common Mistakes

Developers who are new to SOLID often make the following mistakes:

- Applying SOLID to very small programs where it adds unnecessary complexity.
- Creating too many classes without a clear purpose.
- Using inheritance only to reuse code instead of representing an **IS-A** relationship.
- Confusing **Dependency Injection** with the **Dependency Inversion Principle**.
- Assuming every class must have an interface or abstract base class.
- Ignoring readability in the pursuit of strict adherence to SOLID.

---

# Real-world Applications

SOLID principles are widely used in modern software development.

| Domain | Example Applications |
|---------|----------------------|
| Web Development | Django, Flask, FastAPI |
| Enterprise Applications | ERP, CRM Systems |
| Banking | Internet Banking, Payment Gateways |
| E-commerce | Amazon, Flipkart, Shopify |
| Healthcare | Hospital Management Systems |
| Desktop Applications | IDEs, Office Software |
| Mobile Development | Android, iOS Applications |
| Cloud & Microservices | Service-oriented architectures |
| Game Development | Game Engines and AI Systems |

Many modern frameworks and architectures encourage or naturally support SOLID principles.

---

# Summary

The SOLID principles provide a practical guide for designing high-quality object-oriented software.

Rather than focusing on language syntax, SOLID emphasizes **how classes should be designed and how they should interact**.

By following these principles:

- Classes become easier to understand.
- Software becomes easier to extend.
- Dependencies become more manageable.
- Testing becomes simpler.
- Applications become more maintainable over time.

When combined with Object-Oriented Programming concepts such as **encapsulation**, **inheritance**, **polymorphism**, and **abstraction**, SOLID enables developers to build software that is robust, scalable, and easier to evolve as requirements change.

---

# Quick Revision

| Principle | Remember This |
|-----------|---------------|
| **S** | One class → One responsibility |
| **O** | Extend existing behavior without modifying existing code |
| **L** | Child classes must honor the parent class contract |
| **I** | Create small, focused interfaces |
| **D** | Depend on abstractions, not concrete implementations |

---

# Frequently Asked Interview Questions

### 1. What is SOLID?

SOLID is a collection of five object-oriented design principles that help developers build maintainable, extensible, and loosely coupled software.

---

### 2. Which SOLID principle is the easiest to violate?

The **Single Responsibility Principle (SRP)** is commonly violated when a class performs multiple unrelated tasks.

---

### 3. What is the difference between OCP and DIP?

- **OCP** focuses on extending software without modifying existing code.
- **DIP** focuses on reducing dependencies by programming against abstractions.

---

### 4. Does Python support interfaces?

Python does not have a dedicated `interface` keyword. Similar behavior can be achieved using **Abstract Base Classes (ABC)** or **Protocols** from the `typing` module.

---

### 5. Is Dependency Injection the same as Dependency Inversion?

No.

- **Dependency Inversion Principle (DIP)** is a design principle.
- **Dependency Injection (DI)** is a technique commonly used to achieve loose coupling and support DIP.

---

# References

## Official Documentation

1. Python Software Foundation. **abc — Abstract Base Classes**  
   https://docs.python.org/3/library/abc.html

2. Python Software Foundation. **The Python Tutorial – Classes**  
   https://docs.python.org/3/tutorial/classes.html

3. Python Software Foundation. **PEP 8 – Style Guide for Python Code**  
   https://peps.python.org/pep-0008/

---