## **PEP 8 Summary: Python Style Guide**

**PEP 8** is Python’s official **style guide** that provides **conventions for writing clean, readable, and consistent code**. It helps
improve code maintainability and collaboration. Below is a **concise summary** of its key points:

---

### **1. Code Layout**

- **Indentation:** Use **4 spaces per indentation level** (no tabs).
    - This is only true if you're not using a modern IDE - modern IDEs like PyCharm or vscode converts tabs to spaces automatically under
      the hood.
- **Line length:** Limit lines to **79 characters** (72 for docstrings).
    - This is more of a practical guideline rooted in the fact that with 79 characters the code is perfectly readable in old terminal
      emulators.
- **Blank lines:**
    - Separate top-level functions and class definitions with **two blank lines**.
    - Use **one blank line** to separate methods within a class.
    - Most IDE's have either automatic linters that enforces this on save or shortcuts that handles this (Alt+Shift+L in PyCharm for
      example)
- **Imports:**
    - Place imports at the top of the file.
    - Use **one import per line**.
    - Follow the order:
        1. **Standard library imports**
        2. **Third-party imports**
        3. **Local application imports**

---

### **2. Naming Conventions**

- **Variables & Functions:** `snake_case` (e.g., `calculate_total_price`)
- **Classes:** `PascalCase` (e.g., `ApiAuthenticator`)
- **Constants:** `UPPER_CASE_WITH_UNDERSCORES`
- **Private methods or attributes:** Prefix with an underscore (`_protected_method`, `__private_method`)
- **Avoid**:
    - Names that shadow built-in functions (`list`, `dict`, `id`).
    - Single-character names, except for counters (such as `i`, `j` in loops).
        - Generally - no single-character variable names.

---

### **3. Whitespace Usage**

- **Around Operators:**
    - ✅ `x = a + b`
    - ❌ `x=a+b`
- **Inside Brackets & Parentheses:**
    - ✅ `my_list = [1, 2, 3]`
    - ❌ `my_list = [ 1,2,3 ]`
- **After Commas:**
    - ✅ `func(a, b, c)`
    - ❌ `func(a,b,c)`

---

### **4. Comments & Docstrings**

- **Use comments sparingly** and make them meaningful.
- **Inline comments:** Place at least **two spaces before** `#`:

```python
x = 42  # This is an example of using two spaces after your code before placing a comment.
```

- **Block comments:** Explain complex logic **above** the code block.

```python
# Check if the user has the required permissions before proceeding.
# If the user is an admin, allow full access; otherwise, restrict actions.
if user.is_admin:
    grant_full_access()
else:
    restrict_access()
```

- **Docstrings:**
    - Used for **modules, functions, classes, methods**.
    - Use **triple-double quotes**:

```python
def multiply_numbers(param1, param2):
    """
    Compute the sum of two numbers.

    This function takes two numerical parameters and returns their sum.
    It does not perform any type checking, so ensure the inputs are valid numbers.

    Args:
        param1 (int or float): The first number.
        param2 (int or float): The second number.

    Returns:
        int or float: The sum of param1 and param2.
    """
    return param1 * param2
```
Real world example - not strict doc-strings but more useful for objects IMO.
```python
class SshUtils:  
    def __init__(self, profile_folder, descriptive_name: str = None, keyfile_name="id_rsa", passphrase=None):
        """  
        Creates an SSH key-pair inside playbooks/profile folder with name `key_name`.pub for public, and
        `key_name` for private.  
        
        Usage example:
        ssh_utils = SshUtils(profile_folder="test_profile", key_name="id_rsa", passphrase="Password1234!")        
        ssh_utils.create_ssh_key_pair(key_bits=4096)
        print(ssh_utils.read_public_key())  
        
        Passphrase is optional and can be omitted.
        """
        self.key_dir = os.path.expanduser(PathManager().active_profile_dir / ".ssh")
        self.key_name = keyfile_name
        self.descriptive_name = descriptive_name
        self.passphrase = passphrase
        self.priv_key_path = Path(self.key_dir).joinpath(self.key_name)
        self.pub_key_path = self.priv_key_path.with_suffix(".pub")
```

---

### **5. Best Practices**

- **Boolean Comparisons:**
    - ✅ `if is_valid:`
    - ❌ `if is_valid == True:`
- **Avoid Mutable Defaults:**

```python
# Bad 
def append_to_list(value, my_list=[]):
    my_list.append(value)
    return my_list


# Good
def append_to_list(value, my_list=None):
    if my_list is None:
        my_list = []
    my_list.append(value)
    return my_list
    `
```

- **Use `is` for `None` comparisons:**
    - ✅ `if x is None:`
    - ❌ `if x == None:`
- **Use `with` for file handling:**
    - the `with` imperative is a context-manager in Python and automatically handles closing the file handle so you don't accidentially
      drown your system with open file handles.
        - The lesson: always use context-managers when you have the option, they're a great safeguard and makes your code more pythonic!

```python
with open("file.txt", "r") as f:
    content = f.read()
```

---

### **6. Object-Oriented Programming (OOP)**

- Class methods should use `@classmethod` and `@staticmethod` decorators where applicable.
- Use **`self`** for instance methods and **`cls`** for class methods.
- Keep class attributes private (`_attr` or `__attr`).

---

### **7. Exceptions & Error Handling**

- **Use exceptions instead of returning error codes**:

```python
try:
    result = 10 / x
except ZeroDivisionError as e:
    print(f"Error: {e}")
    `
```

- **Use specific exception types** (avoid catching `Exception` unless necessary).
    - `Exception` is the base-class that all other exceptions inherit from in Python, this means that it will catch any exception - this is
      rarely what you wan't and will give you a lot of headaches!

---

### **8. String Formatting**

- Prefer **f-strings** (Python 3.6+):

```python
name = "Alice"
print(f"Hello, {name}!")
`

import math

print(f"Pi is approximately {math.pi:0.99})  # Prints Pi with 99 decimal points.
      >> > "Pi is approximately 3.141592653589793115997963468544185161590576171875"
```

- Avoid `+` for string concatenation.
    - Don't do: `"Pi is a mathematical constant defined as " + str(math.pi) + ". It's apprixmiately equal to 3.14"`

The old way is to use `"this is a string".format(name)`. It is only useful under very specific scenarious and with f-strings, you can do a
lot of really neat stuff.

---

## **Conclusion**

Following **PEP 8** ensures **clean, consistent, and professional Python code**. Many tools like **`flake8`**, **`black`**, and **`pylint`**
help enforce PEP 8 automatically, but for some things it's necessary that you make it a practice to always follow the standard

This goes for things like proper casing of variables, functions and classes and indentation (whitespace) for example, while other things
like line length (which are inherited from the widths of classic terminal emulators) are somewhat more flexible and then again you have
string formatting where there are exceptions to the rule and then on the other hand we have stuff like import order which can be automated
with tools like `isort` which are similar in nature to `black` and `flake8`.

So in summary - following PEP8 makes your code cleaner which in turn makes it more readable for other people - code is foremost meant to be
read by people and only secondarily read by computers - if that was not true, we would still be using machine language, but we're not
machines, we're humans, so we write clean code.

## **Exercises**

No exercises, but try to return to this chapter once in a while and refresh your memory on different topics every now and then.