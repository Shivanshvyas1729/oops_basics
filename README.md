# YT-MLOPS-OOPS-Tut
This repo will cover end to end tutorial for Python OOPS.

<details>
  <summary>1. self 1.1 </summary>

### What is `self` in Python?

`self` represents the **current object (instance)** of a class.

When you create an object from a class, Python automatically passes that object as the first argument to the class methods. By convention, we call this argument `self`.

You do **not** pass `self` manually. Python does it behind the scenes.

`self` allows each object to access and store its own data (attributes) and call its own methods.

### How it works

When you write:

```python
sam = employee()
```

Python internally does something similar to:

```python
employee.__init__(sam)
```

Here, the object `sam` is automatically passed to the `__init__()` method as `self`.

That's why inside the constructor:

```python
self.id = 123
self.salary = 50000
self.designation = "SDE"
```

the attributes are attached to the specific object (`sam`).

---

### Example

```python
# initiate a class
class employee:

    # constructor
    def __init__(self):
        print("self id:", id(self))

        self.id = 123
        self.salary = 50000
        self.designation = "SDE"

    def travel(self):
        print("self id inside method:", id(self))
        print("Employee is now travelling to Delhi")


# create an object
sam = employee()

print("sam object id:", id(sam))

# call method
sam.travel()
```

### Output (example)

```python
self id: 140234567890128
sam object id: 140234567890128
self id inside method: 140234567890128
Employee is now travelling to Delhi
```

Notice that the ID of `self` and the ID of `sam` are the same. This proves that `self` refers to the object that was created.

### Key Points

1. `self` refers to the current object (instance).
2. When an object is created, Python automatically passes that object to `__init__()` as `self`.
3. When a method is called using an object, Python automatically passes that object as `self`.

Example:

```python
sam.travel()
```

is internally equivalent to:

```python
employee.travel(sam)
```

Here, `sam` is automatically passed as `self`.

So, **`self` is simply a reference to the object that is currently using the class, allowing the object to access its own attributes and methods.**



</details>


<details><summary>self 1.2</summary>


```python
# initiate a class
class Employee:

    # constructor
    def __init__(self):
        print(f"Object received as self -> {id(self)}")

        self.id = 123
        self.salary = 50000
        self.designation = "SDE"

    def travel(self):
        print(f"travel() called by object -> {id(self)}")
        print("Employee is now travelling to Delhi")


# Creating first object
sam = Employee()
print(f"sam object id -> {id(sam)}")

print("-" * 40)

# Creating second object
shaktiman = Employee()
print(f"shaktiman object id -> {id(shaktiman)}")
```

### Possible Output

```text
Object received as self -> 2345678901120
sam object id -> 2345678901120
----------------------------------------
Object received as self -> 2345678913456
shaktiman object id -> 2345678913456
```

### Explanation

When we create:

```python
sam = Employee()
```

Python internally does:

```python
Employee.__init__(sam)
```

So `self` refers to `sam`.

The IDs are the same because both `self` and `sam` are references to the **same object**.

Later, when we create:

```python
shaktiman = Employee()
```

Python creates a **new object in a different memory location (RAM)** and internally does:

```python
Employee.__init__(shaktiman)
```

Now `self` refers to `shaktiman`.

Since `shaktiman` is a completely new object, its memory address (ID) is different from `sam`.

### Visual Representation

```text
sam  --------------------> Object A
                             id = 101

self (during sam creation) -> Object A
                              id = 101


shaktiman -------------> Object B
                           id = 202

self (during shaktiman creation) -> Object B
                                    id = 202
```

### One-line Definition

**`self` is a reference to the current object being created or used. Every time a new object is created, Python automatically passes that object's reference as `self`, so `self` points to a different memory location for different objects.**

</details>





<details>
  <summary>2. GetterEncapsulation, Getters, Setters & Static Methods</summary>
  
  # Python OOP Notes: Encapsulation, Getters, Setters & Static Methods



<details>
  <summary>code
  </summary>



# File 1: `oops_proj.py`

```python
class chatbook:

    # Static (Class) Variable
    # Shared among all objects
    # Used to generate unique IDs
    __user_id = 1

    def __init__(self):

        # Assign current user ID to the object
        self.id = chatbook.__user_id

        # Increment static ID for the next object
        chatbook.__user_id += 1

        # Private attribute (Encapsulation)
        self.__name = "Default User"

        # Public attributes
        self.username = ''
        self.password = ''
        self.loggedin = False

        # self.menu()

    # Static Method
    # Returns the current value of the static variable
    @staticmethod
    def get_id():
        return chatbook.__user_id

    # Static Method
    # Updates the static variable
    @staticmethod
    def set_id(val):
        chatbook.__user_id = val

    # Getter
    # Returns the private attribute __name
    def get_name(self):
        return self.__name

    # Setter
    # Updates the private attribute __name
    def set_name(self, value):
        self.__name = value
```

---

# File 2: `main.py`

```python
# Import the chatbook class
from oops_proj import chatbook

# Create first object
user1 = chatbook()

# Print the unique ID assigned to the object
print(user1.id)







# ----------------------------
# Static Method Example
# ----------------------------

# Update the shared static variable
# chatbook.set_id(10)

# Create another object
# user2 = chatbook()
# print(user2.id)

# Create third object
# user3 = chatbook()
# print(user3.id)





# ----------------------------
# Getter & Setter Example
# ----------------------------

# Read private attribute using getter
# print(user1.get_name())

# Update private attribute using setter
# user1.set_name("Agent X")

# Read updated value
# print(user1.get_name())
```


</details>


# 1. Encapsulation

## Definition

**Encapsulation** is the process of **hiding the internal data of a class** and allowing controlled access through methods.

Instead of allowing everyone to directly modify important data, we protect it.

### Why?

* Prevent accidental changes
* Add validation before changing data
* Make code more secure
* Improve maintainability

---

# 2. Public vs Private Attributes

## Public Attribute

Accessible from anywhere.

```python
class Student:
    def __init__(self):
        self.name = "Rahul"
```

Usage

```python
s = Student()

print(s.name)

s.name = "Aman"
```

No protection.

---

## Private Attribute

Use double underscore (`__`).

```python
class Student:

    def __init__(self):
        self.__name = "Rahul"
```

Now,

```python
print(s.__name)
```

gives

```
AttributeError
```

Python hides it using **name mangling**.

Internally,

```
__name
```

becomes

```
_Student__name
```

Although it can still be accessed internally, developers are expected **not** to access it directly.

---

# Example from your code

```python
class chatbook:

    def __init__(self):
        self.__name = "Default User"
```

Here,

```
__name
```

is private.

So this is **wrong**

```python
user1.__name
```

Instead use a getter.

---

# 3. Getter

A getter **returns** the value of a private attribute.

Your code

```python
def get_name(self):
    return self.__name
```

Usage

```python
print(user1.get_name())
```

Output

```
Default User
```

Flow

```
Object
   ↓
get_name()
   ↓
returns __name
```

---

# 4. Setter

A setter **updates** a private attribute.

Your code

```python
def set_name(self, value):
    self.__name = value
```

Usage

```python
user1.set_name("Agent X")
```

Now

```python
print(user1.get_name())
```

Output

```
Agent X
```

---

## Why not modify directly?

Without a setter

```python
user1.__name = ""
```

or

```python
user1.__name = 123
```

may store invalid values.

A setter lets you validate first.

Example

```python
def set_name(self, value):

    if len(value) > 0:
        self.__name = value
```

Now

```
Empty names cannot be stored.
```

---

# Getter vs Setter

| Getter                | Setter               |
| --------------------- | -------------------- |
| Reads data            | Changes data         |
| Returns value         | Updates value        |
| Usually no validation | Validation is common |

---

# 5. Static Attribute

## Definition

A **static attribute** belongs to the **class**, not individual objects.

There is only **one copy**, shared by every object.

Your code

```python
class chatbook:

    __user_id = 1
```

Notice

It is **outside** `__init__()`.

That makes it a class variable (static attribute).

---

# Why is it needed?

Suppose every user should receive a unique ID.

User 1

```
ID = 1
```

User 2

```
ID = 2
```

User 3

```
ID = 3
```

The counter must be shared across all objects.

---

# What happens inside `__init__`

```python
self.id = chatbook.__user_id
```

Current value

```
1
```

So

```
user1.id = 1
```

Then

```python
chatbook.__user_id += 1
```

becomes

```
2
```

Next object

```
user2.id = 2
```

Then

```
3
```

and so on.

---

## Visualization

Initially

```
chatbook.__user_id = 1
```

Create first object

```
user1.id = 1

chatbook.__user_id = 2
```

Create second object

```
user2.id = 2

chatbook.__user_id = 3
```

Create third object

```
user3.id = 3

chatbook.__user_id = 4
```

---

# Why not keep it inside `__init__`?

Suppose

```python
class chatbook:

    def __init__(self):

        self.user_id = 1
```

Every object starts with

```
1
```

Result

```
user1.id = 1

user2.id = 1

user3.id = 1
```

No unique IDs.

---

# Static Method

A **static method** works with **class-level data** and **doesn't require an object (`self`)**.

Python uses the `@staticmethod` decorator.

Your code

```python
@staticmethod
def get_id():
    return chatbook.__user_id
```

Notice

* No `self`
* Uses the class name directly

---

# Calling a static method

Recommended

```python
chatbook.get_id()
```

Output

```
2
```

(after one object is created)

---

# Another static method

```python
@staticmethod
def set_id(val):
    chatbook.__user_id = val
```

Usage

```python
chatbook.set_id(10)
```

Now

Next object

```python
user2 = chatbook()
```

gets

```
ID = 10
```

because the shared counter was changed.

---

# Why use `@staticmethod`?

Because these methods don't depend on a specific object.

Example

Changing

```
chatbook.__user_id
```

is a class-level operation.

So

```
Class
 ↓
Static Method
 ↓
Static Variable
```

---

# Why use `chatbook.__user_id` instead of `self.__user_id`?

`self` refers to an **individual object**.

Static variables belong to the **class**.

Therefore

Correct

```python
chatbook.__user_id
```

Not recommended

```python
self.__user_id
```

Using the class name makes it clear that you're working with shared class data.

---

# Complete Flow of Your Program

```python
user1 = chatbook()
```

Inside constructor

```
chatbook.__user_id = 1

↓

user1.id = 1

↓

chatbook.__user_id += 1

↓

chatbook.__user_id = 2
```

Then

```python
print(user1.id)
```

Output

```
1
```

---

If later

```python
user2 = chatbook()
```

then

```
user2.id = 2
```

---

# Summary

### Encapsulation

* Hides internal data
* Protects important information
* Achieved using private attributes (`__variable`)

### Getter

* Reads private data
* Safe way to access values

### Setter

* Updates private data
* Can perform validation before updating

### Static Attribute

* Shared by all objects
* Defined outside `__init__`
* Only one copy exists

### Static Method

* Belongs to the class
* Uses `@staticmethod`
* Doesn't require `self`
* Accesses or modifies class-level data

---

<img width="808" height="222" alt="image" src="https://github.com/user-attachments/assets/19a0752a-05f6-4560-aaa5-84e659d1d65f" />

----

<img width="746" height="196" alt="image" src="https://github.com/user-attachments/assets/64b1fb83-f04d-4c89-b584-53c2eb97a86c" />



# Interview Questions

**Q1. What is encapsulation?**
Encapsulation is the process of hiding a class's internal data and exposing it only through controlled methods like getters and setters.

**Q2. Why do we use getters and setters?**
They provide controlled access to private attributes and allow validation before reading or modifying data.

**Q3. What is a static attribute?**
A static attribute (class variable) belongs to the class itself and is shared among all objects.

**Q4. What is a static method?**
A static method belongs to the class, doesn't take `self`, and is typically used to work with class-level data.

**Q5. Why is `__user_id` declared outside `__init__()`?**
Because it needs to be shared across every object so each new object gets a unique ID. If it were inside `__init__()`, every object would start with the same value.

</details>





<details><summary>3. Inheritance & super() Keyword 
</summary>

Since you're creating **GitHub README notes** that follow your teacher's lecture, I recommend structuring them exactly like your Encapsulation notes: definition → examples → code explanation → summary → interview questions.

# Suggested Title

**Python OOP Notes: Inheritance & `super()` Keyword**

---

# Table of Contents

1. Inheritance
2. Parent Class and Child Class
3. Basic Inheritance
4. Method Overriding
5. The `super()` Keyword
6. Constructor Inheritance
7. Why use `super()`?
8. Complete Flow
9. Summary
10. Interview Questions

---

# 1. Inheritance

## Definition

**Inheritance** is an Object-Oriented Programming (OOP) concept that allows one class (**child class**) to inherit the attributes and methods of another class (**parent class**).

Instead of writing the same code multiple times, we can write it once in the parent class and reuse it in child classes.

---

## Why use Inheritance?

* Promotes code reusability.
* Reduces code duplication.
* Makes programs easier to maintain.
* Allows extending existing functionality.

---

# 2. Parent Class and Child Class

## Parent (Base) Class

The class whose properties are inherited.

```python
class Animal:
    pass
```

---

## Child (Derived) Class

The class that inherits from another class.

```python
class Dog(Animal):
    pass
```

Here,

* `Animal` → Parent class
* `Dog` → Child class

---

# 3. Basic Inheritance

## Parent Class

```python
class Animal:

    def __init__(self, name):
        self.name = name

    def speak(self):
        print(f"{self.name} makes a sound.")
```

---

## Child Class

```python
class Dog(Animal):

    def speak(self):
        print(f"{self.name} barks.")
```

Notice

```python
class Dog(Animal)
```

means

> Dog inherits everything from Animal.

---

## What does Dog inherit?

It inherits

* Attributes
* Methods

except **private members** (created using `__`).

---

# Creating Objects

```python
animal = Animal("Generic Animal")
animal.speak()
```

Output

```text
Generic Animal makes a sound.
```

---

```python
dog = Dog("Buddy")
dog.speak()
```

Output

```text
Buddy barks.
```

---

# 4. Method Overriding

A child class can define a method with the **same name** as the parent class.

This is called **Method Overriding**.

Example

Parent

```python
def speak(self):
    print("Makes a sound.")
```

Child

```python
def speak(self):
    print("Barks.")
```

Now,

```python
dog.speak()
```

calls

```text
Dog.speak()
```

instead of

```text
Animal.speak()
```

The parent's method is overridden.

---

# 5. The `super()` Keyword

## Definition

The `super()` function allows a child class to access the parent class's methods and constructor.

It is mainly used for

* Calling the parent's constructor.
* Calling the parent's methods.

---

# Constructor Inheritance

Your code

```python
class Animal:

    def __init__(self):
        self.name = "Buddy"
```

Child

```python
class Dog(Animal):

    def __init__(self, breed):
        super().__init__()
        self.breed = breed
```

---

## Why use `super().__init__()`?

If the child class defines its own constructor,

```python
def __init__(self):
```

Python **does not automatically call** the parent's constructor.

Without

```python
super().__init__()
```

the parent attributes are never initialized.

---

## Example

Without `super()`

```python
class Dog(Animal):

    def __init__(self, breed):
        self.breed = breed
```

Now

```python
dog = Dog("Golden Retriever")
```

Trying

```python
print(dog.name)
```

gives

```text
AttributeError
```

because

```python
self.name
```

was never created.

---

With `super()`

```python
class Dog(Animal):

    def __init__(self, breed):
        super().__init__()
        self.breed = breed
```

Now

```python
dog.name
```

works.

Output

```text
Buddy
```

---

# Calling Parent Methods

Your code

```python
def speak(self):
    super().speak()
    print(f"{self.name} barks. It is a {self.breed}.")
```

First,

```python
super().speak()
```

calls

```python
Animal.speak()
```

which prints

```text
Buddy makes a sound.
```

Then

```python
print(...)
```

prints

```text
Buddy barks. It is a Golden Retriever.
```

---

# Complete Flow

```python
dog = Dog("Golden Retriever")
```

↓

Dog constructor starts

↓

```python
super().__init__()
```

↓

Animal constructor runs

↓

```python
self.name = "Buddy"
```

↓

Back to Dog constructor

↓

```python
self.breed = "Golden Retriever"
```

↓

Object creation complete

---

Now

```python
dog.speak()
```

↓

```python
super().speak()
```

↓

Animal.speak()

↓

```text
Buddy makes a sound.
```

↓

Dog.speak()

↓

```text
Buddy barks. It is a Golden Retriever.
```

---

# Why use `super()`?

* Reuses parent code.
* Avoids rewriting constructors.
* Allows extending parent functionality.
* Keeps parent and child classes connected.
* Makes code easier to maintain.

---

# Difference Between Inheritance and `super()`

| Inheritance                          | `super()`                           |
| ------------------------------------ | ----------------------------------- |
| Child gets parent's properties       | Accesses parent methods/constructor |
| Achieved using `class Child(Parent)` | Achieved using `super()`            |
| Used for code reuse                  | Used to extend parent functionality |

---

# Summary

### Inheritance

* Child class inherits attributes and methods from parent class.
* Promotes code reuse.
* Reduces duplication.

### Method Overriding

* Child class defines a method with the same name as the parent.
* Child implementation replaces the parent's implementation.

### `super()`

* Calls the parent constructor.
* Calls parent methods.
* Helps extend existing functionality.

---

# Interview Questions

### Q1. What is inheritance?

Inheritance is an OOP feature that allows one class to inherit the attributes and methods of another class, promoting code reuse.

---

### Q2. What is a parent class?

A parent (base) class is the class whose properties and methods are inherited by another class.

---

### Q3. What is a child class?

A child (derived) class inherits the properties and methods of the parent class and can also add or modify functionality.

---

### Q4. What is method overriding?

Method overriding occurs when a child class defines a method with the same name as a method in the parent class, replacing the parent's implementation.

---

### Q5. What is the `super()` keyword?

`super()` is used inside a child class to access the parent class's constructor or methods.

---

### Q6. Why do we use `super().__init__()`?

When a child class has its own constructor, `super().__init__()` ensures that the parent class's constructor also runs, initializing parent attributes.

---

### Q7. Can a child class access private attributes of the parent?

No. Private attributes (declared using `__`) are name-mangled and are not directly accessible in the child class. Public and protected members can be inherited.

</details>
