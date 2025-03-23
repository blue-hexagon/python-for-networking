# **Understanding `int()`**

This tutorial introduces **integers (`int`) in Python**, a fundamental data type you'll use **frequently** in networking scripts, automation, and calculations.

---

## **📌 Integers in Python**

```python
if __name__ == '__main__':  
    """ 
    Integers (`int`) are one of the most fundamental datatypes in Python.
    You'll work with them *a lot*. They are simple in nature and form the 
    starting point for understanding Python's datatypes.
    """

    # Basic integer assignment
    this_is_an_int = 256  
    this_is_also_an_int = int(256)  # These two are equivalent.
    
    # Initializing an integer to zero using `int()`
    this_just_initializes_to_the_number_zero = int()  
    print(this_just_initializes_to_the_number_zero)  # Output: 0  

    # Strings and type conversion
    this_is_not_an_int_its_a_string = "256"  
    but_with_type_conversion_we_can_turn_it_into_an_int = int(this_is_not_an_int_its_a_string)  # Converts to an integer

    # Comparison of integer creation methods
    if this_is_an_int == this_is_also_an_int:  
        print('Takeaway: You can create integers using direct assignment or int(). '
              'Additionally, `int()` can perform type conversions, as demonstrated with `int("256")`.')  
  
    # int() can also convert binary strings into their decimal equivalents
    for bits in range(8, 32, 8):  
        """
        This for-loop runs three times:
        - First iteration: bits = 8
        - Second iteration: bits = 16
        - Third iteration: bits = 32
        
        The range() function works as:
        range(start, stop, step)
        - You can specify only `start`, or `start` and `stop`, or all three.
        """

        val = int("1" * bits, 2)  # Creates a binary string (e.g., "11111111") and converts it to decimal
        print(val)  

        # The second argument in int() (here: 2) defines the base.
        # Try reasoning about the output in your head before running the script!
```

---

## **📝 Exercises**

These exercises will **challenge your understanding of `int()` and `range()`**.

### **Exercise 1: Fun with Negative Ranges**

#### **Steps:**

1. Create a **main function**.
2. Inside the function, **write a `for` loop** using `range()`.
    - It should **start at -15**, **end at -16**, and **decrease by 3 each time** (`step = -3`).
3. Inside the loop, **print the current integer**.
4. Run the script and **predict what will happen**.
5. Compare the output with your expectation.
6. **Why did this happen?** Play around with different values to find out!

#### **Hints:**

```python
def main():
    for num in range(-15, -16, -3):
        print(num)

if __name__ == "__main__":
    main()
```

- What happens when the **range "ends before it starts"**?
- Change `range(-15, -30, -3)`, then `range(-15, -10, -3)`, and observe.

---

### **Exercise 2: Understanding `int()`**

#### **Steps:**

1. **Create a main function**.
2. **Create a string variable** that holds `"11"`. Name it anything.
    
    ```python
    my_var = "11"
    ```
    
3. **Create a new variable** equal to the first one:
    
    ```python
    my_new_var = my_var
    ```
    
4. **Print the new variable** using the `print()` function:
    
    ```python
    print(my_new_var)  # Output: "11"
    ```
    
5. **Now convert it into an integer** using `int()`:
    
    ```python
    print(int(my_new_var, 10))  # Explicit base 10 conversion
    ```
    
6. **Try removing `,10` and print again**:
    
    ```python
    print(int(my_new_var))  # What happens?
    ```
    
7. **Try changing `,10` to `,2`** and print again:
    
    ```python
    print(int(my_new_var, 2))  # What happens?
    ```
    
8. **Play around with different bases** to deepen your understanding!

#### **Hints:**

- What happens if `"11"` is interpreted as **base-10**?
- What happens if `"11"` is interpreted as **base-2** (binary)?
- Try using **different string values**:
    - `"100"` as base-2?
    - `"A"` as base-16?

---

## **🎯 Takeaways**

✔ `int()` can **initialize integers** (`int()` → `0`).  
✔ `int()` can **convert strings to numbers** (`int("123")` → `123`).  
✔ `int()` can **convert binary, octal, and hexadecimal** (`int("FF", 16)` → `255`).  
✔ `range(start, stop, step)` lets you **iterate over sequences** dynamically.


