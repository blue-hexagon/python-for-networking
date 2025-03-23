## **Python: From Absolute Beginner to Expert**
### *A Crashcourse into Python for Network Engineers*

#### **Absolute Beginner (The Basics)**

- **A. Python Syntax & Basics**
    - [[A1. My first Python application]]
    - [[A2. Variable Scopes]]
    - [[A3. Understanding indentation, comments, and PEP 8 style guide]]
- **B. Data Types & Variables**
    - [[B1. Integers, floats, strings, booleans]]
    - Type conversion (`int()`, `str()`, `float()`, `bool()`)
- **C. Operators**
    - Arithmetic (`+`, `-`, `*`, `/`, `//`, `%`, `**`)
    - Comparison (`==`, `!=`, `<`, `>`, `<=`, `>=`)
    - Logical (`and`, `or`, `not`)
- **D. Control Flow**
    - `if`, `elif`, `else` statements
    - Loops: `for`, `while`
    - `break`, `continue`, `pass`
- **E. Functions**
    - Defining functions (`def my_function()`)
    - Function arguments and return values
    - Default parameters, keyword arguments
    - Forcing function calls to use args or kwargs: `*`,`/` 
- **F. Basic Data Structures**
    - Lists (`list.append()`, `list.pop()`, slicing)
    - Tuples (immutable sequences)
    - Dictionaries (`dict.keys()`, `dict.values()`)
    - Sets (`set.add()`, `set.remove()`)

### **Final Chapter Exercises**
* Create a function that accepts an IP address and returns the numerical (base-10) value as a single integer.

* Create a function that takes an IP address and returns the class of IP address (i.e. A, B, C etc.)
	* Hint: you can use the function you previously created above as an aid.

* Create a simple CLI that continuously asks for an IP address and prints the IP address class.
	* Hint: use `input()`
		* Does the function `input` take any arguments? What does its signature look like?
	* Extra assingment: Make the app crash by entering the wrong input, and then implement input sanitation/validation so the app can't be crashed by entering any wrong input.
		* Did you get it right? Try your best to crash the app by.

* Now make it so that when the user enters a valid IP address, the program calls the windows (cmd) ping command and prints the output to the CLI and then goes back to the CLI you wrote, so that a user can use your CLI as a special ping-tool.
	* Hint: use `subprocess`
---
#### **Intermediate (Building Proficiency)**

- **Advanced Data Structures**
    - Nested lists and dicts
    - Deque (`collections.deque`)
    - DefaultDict (`collections.defaultdict`)
- **String Manipulation**
    - String formatting (`f-strings`, `.format()`)
    - String methods (`.split()`, `.join()`, `.replace()`, regex)
- **File Handling**
    - Reading & writing files (`open()`, `with` statement)
    - JSON and CSV parsing (`json`, `csv` modules)
- **Exception Handling**
    - `try`, `except`, `finally`, `raise`
    - Custom exceptions
- **List Comprehensions & Generators**
    - `[x**2 for x in range(10)]`
    - Generator functions (`yield`)
- **Lambda Functions & Functional Programming**
    - `map()`, `filter()`, `reduce()`
    - `lambda` expressions
- **Modules & Packages**
    - `import`, `from module import`
    - Creating and using modules
    - Virtual environments (`venv`)

---

#### **Advanced (Mastery Level)**

- **Object-Oriented Programming (OOP)**
    - Classes, Objects
    - Inheritance, Polymorphism, Encapsulation
    - Dunder (`__init__`, `__str__`, `__repr__`)
    - Abstract classes (`ABC` module)
- **Concurrency & Parallelism**
    - Multithreading (`threading` module)
    - Multiprocessing (`multiprocessing` module)
    - Async programming (`asyncio`, `await`, `async`)
- **Metaprogramming**
    - Decorators (`@staticmethod`, `@classmethod`, custom decorators)
    - Metaclasses (`type`, `__new__`)
- **Networking & Sockets**
    - `socket` programming (TCP/UDP)
    - `asyncio` for networking
- **Regular Expressions**
    - `re` module for pattern matching
- **Databases & ORMs**
    - SQLite, PostgreSQL, MySQL (`sqlite3`, `psycopg2`, `SQLAlchemy`)
    - ORMs like Django ORM, SQLAlchemy
- **Unit Testing & Test-Driven Development (TDD)**
    - `unittest` module
    - `pytest`
    - Mocking (`unittest.mock`)
- **Logging & Debugging**
    - `logging` module (`log.debug()`, `log.info()`, `log.warning()`)
    - Debugging (`pdb`, `breakpoints()`)
- **Working with APIs**
    - `requests`, `http.client`
    - RESTful API consumption (`requests.get()`, `requests.post()`)

---

#### **Expert (Deep Dive into Specializations)**

- **Design Patterns in Python**
    - Singleton, Factory, Observer, Decorator patterns
- **Advanced Algorithms & Data Structures**
    - Graphs (`networkx`)
    - Trees (Binary Trees, BST)
    - Dynamic Programming
    - Sorting & Searching (`heapq`, `bisect`)
- **Performance Optimization**
    - Profiling (`cProfile`, `line_profiler`)
    - Memory management (`gc`, `sys.getsizeof()`)
    - Cython, Numba, PyPy for performance boost
- **Security & Cryptography**
    - Hashing (`hashlib`, `bcrypt`)
    - Encryption (`pycryptodome`, `cryptography`)
    - Secure coding practices
- **Building CLI Tools**
    - `argparse`, `click`
    - Creating command-line utilities
- **Web Development**
    - Flask & Django frameworks
    - WebSockets (`websockets`, `socket.io`)
- **Machine Learning & AI**
    - `numpy`, `pandas`, `scikit-learn`, `tensorflow`
    - Deep Learning models
- **DevOps & Automation**
    - Docker, Kubernetes
    - CI/CD pipelines
    - Infrastructure as Code (`Ansible`, `Terraform`)
- **Low-Level Python & C Extensions**
    - `ctypes`, `Cython`
    - Interfacing with C/C++ code
- **Distributed Systems & P2P Networks**
    - `zmq`, `grpc`
    - Building decentralized applications