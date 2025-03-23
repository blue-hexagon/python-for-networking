## **Python Scoping: Understanding LEGB Rule & Scope Types**

In Python, **scoping** determines how variables are searched and accessed in different parts of a program. Python uses the **LEGB rule** (Local, Enclosing, Global, Built-in) to resolve variable names.

**Scoping** is fundamentally about **where a variable is accessible** in a program. When you declare a variable, **not all parts of your code can see or modify it**. The question scoping answers is:

> **"I have data or logic stored in this variable, but I need to access it somewhere else – can I access it directly, or do I need to pass it explicitly?"**

This leads to different strategies based on **where the variable is declared and where it needs to be used**. Depending on the situation, you might need to:

- Pass it as a **function argument**
- Store it as an **instance variable in a class**
- Use **closures** for state retention
- Use **global or nonlocal** (sparingly)

The main thing you should focus on right now, is understanding the rule of:
* Local scope **(L**)
* Nested scope **(E)**
* Global scope **(G)**
* Built-in scope **(B)**

---

## **The Four Scope Levels (LEGB Rule)**

Python follows a hierarchy when looking up variables:

1️⃣ **Local (L)**: Inside the current function (or lambda).  
2️⃣ **Enclosing (E)**: Inside any outer function (if using nested functions).
3️⃣ **Global (G)**: Defined at the top level of a module or file.  
4️⃣ **Built-in (B)**: Predefined Python names like `len()`, `print()`, `range()`.

Python searches for a variable in this order:  
**Local → Enclosing → Global → Built-in**

If the variable isn't found, Python raises a `NameError`.

---

## **1. Local Scope**

A variable defined inside a function is **local** to that function.

```python
def my_function():
    x = 10  # Local scope
    print(x)

my_function()
# print(x)  # ❌ NameError: x is not defined (because it's local to my_function)
```
*We'll get to exceptions later.*

---

## **2. Enclosing Scope (Nested Functions)**

If a variable isn't found in **local scope**, Python checks **enclosing functions**.

```python
def outer():
    y = 20  # Enclosing scope

    def inner():
        print(y)  # Can access y from enclosing function

    inner()

outer()
```

🔹 `**inner()**`** can access `****y****` because `****y****` is in the enclosing function ****`outer()`**.  
🔹 But **inner functions can't modify enclosing variables unless explicitly declared with ******`**nonlocal**`.

### **Modifying an Enclosing Variable with **`**nonlocal**`

```python
def outer():
    y = 20  # Enclosing scope

    def inner():
        nonlocal y  # Declaring y as nonlocal
        y += 10
        print(y)

    inner()
    print(y)  # Modified in enclosing scope

outer()
```

🔹 Without `nonlocal`, `y += 10` would create a **new local variable** instead of modifying the enclosing `y`.

---

## **3. Global Scope**

Variables defined outside functions are **global** and accessible everywhere **except when modified inside a function** (unless declared `global`).

```python
z = 30  # Global scope

def my_function():
    print(z)  # Access global variable

my_function()
print(z)  # Still accessible globally
```

**Global variables can be accessed inside functions but not modified unless declared ******`**global**`.

### **Modifying a Global Variable with **`**global**`
```python
counter = 0  # Global scope

def increment():
    global counter  # Declaring counter as global
    counter += 1  # Now modifying the global variable

increment()
print(counter)  # Output: 1
```

🔹 Without `global`, `counter += 1` would create a **new local variable**, leaving the global `counter` unchanged.

This is purely for demonstration - using `global` is usually bad practice and is often considered a [code smell](https://www.google.com/search?q=code+smell). In multithreaded programs it can cause [deadlocks](https://stackoverflow.com/questions/2143873/how-to-explain-the-deadlock-better) and it makes debugging and software testing harder and results in code that is harder to reason about and understand. 

---

## **4. Built-in Scope**

Python has **predefined functions and keywords** that exist in the **built-in scope**.

```python
print(len("Python"))  # len() is in built-in scope
```

🔹 These are **always available** from anywhere in your code, without you having to do anything! - Unless you override them, aka. shadow them (which is bad).

### **Overriding a Built-in Function (Not Recommended)**

```python
def len(x):  # Overriding built-in function
    return "Oops!"

print(len("Python"))  # Oops!
```

**Avoid naming variables/functions the same as built-in ones** to prevent unexpected behavior (this phenomenon, when done, is called `shadowing`).

---
## **Exercises**
No exercises at this point in time.