# YT-MLOPS-OOPS-Tut
This repo will cover end to end tutorial for Python OOPS.

<details>
  <summary>self 1.1 </summary>

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
