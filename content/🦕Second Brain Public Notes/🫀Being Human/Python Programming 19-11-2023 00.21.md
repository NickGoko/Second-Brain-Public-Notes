---
tags:
  - computer-science/python
---
### Dive Deeper into Python Data Structures
- **Lists**
    - Lists are ordered collections of items, which can be of different data types.
    - They are mutable, meaning you can change, add, and remove elements after the list is created.
    - Common operations on lists include:
        - Accessing elements by index
        - Slicing lists to extract subsets of elements
        - Modifying elements using index assignment
        - Appending, inserting, and removing elements
        - Sorting and reversing lists
    - Lists are created using square brackets `[]` and elements are separated by commas.
- **Tuples**
    - Tuples are similar to lists but are immutable, meaning they cannot be changed after creation.
    - They are commonly used for grouping related data together, such as coordinates or RGB color values.
    - Tuples are created using parentheses `()` and elements are separated by commas.
    - Common operations include accessing elements by index and unpacking tuples into variables.
- **Dictionaries**
    - Dictionaries are unordered collections of key-value pairs.
    - They <mark style="background: #BBFABBA6;">are mutable and allow you to store and retrieve values based on keys rather than numerical indices</mark>.
    - Keys must be unique and immutable (such as strings, numbers, or tuples), while values can be of any data type.
    - Common operations include adding, accessing, and modifying key-value pairs, as well as iterating over keys, values, or items.
    - Dictionaries are created using curly braces `{}` with key-value pairs separated by colons `:` and items separated by commas.

- **Sets**
    - Sets are <mark style="background: #FFB86CA6;">unordered collections of unique elements</mark>.
    - They are mutable, meaning you can add and remove elements, but the elements themselves are immutable.
    - Sets do not allow duplicate elements, and they are particularly useful for mathematical operations like union, intersection, difference, and symmetric difference.
    - Sets are created using curly braces `{}`, similar to dictionaries, but without key-value pairs. Alternatively, you can use the `set()` constructor with an iterable.
    - Common operations on sets include adding and removing elements, checking membership, and performing set operations like union, intersection, and difference.
- **Frozensets**
    - Frozensets are similar to sets but are immutable, meaning once created, they cannot be changed.
    - Frozensets are useful in scenarios where you need an immutable set, such as using sets as keys in dictionaries or as elements in other sets.
    - Frozensets are created using the `frozenset()` constructor with an iterable.
    - Common operations on frozensets include checking membership and performing set operations, but since they are immutable, they do not support operations that modify the frozenset itself, such as adding or removing elements.


- **Defining Functions**
    - Functions are blocks of reusable code that perform a specific task.
    - They help in organizing code, promoting reusability, and making code more modular and readable.
    - In Python, functions are defined using the `def` keyword followed by the function name and parentheses containing any parameters.
    - Parameters are inputs that a function can accept. They can be optional or required, and they are specified within the parentheses.
    - Functions may or may not return a value. If a function returns a value, it typically uses the `return` statement to send the result back to the caller.
    - A function definition consists of a header and a block of code. The header includes the function name and parameters, while the block of code contains the function's implementation.
    - Once defined, functions can be called from anywhere in the code by using the function name followed by parentheses containing any arguments.
    - It's good practice to provide a docstring, a string literal that describes what the function does, immediately after the function header. Docstrings help in documenting the purpose, usage, and behavior of the function.
    - Functions can also have default parameter values, allowing some parameters to be optional.
    - Python functions support recursion, meaning a function can call itself either directly or indirectly.

### Error Handling and Debugging:

#### Handling Exceptions:
- **Definition**:
  - Error handling is a mechanism used to manage and respond to unexpected errors or exceptions that occur during program execution.
  - Exceptions are runtime errors that disrupt the normal flow of program execution.
- **Try-Except Block**:
  - Python provides a `try-except` block for handling exceptions.
  - Syntax:
    ```python
    try:
        # Code that may raise an exception
    except ExceptionType as e:
        # Handle the exception
    ```
- **Common Exception Types**:
  - `ZeroDivisionError`: Raised when division or modulo by zero occurs.
  - `TypeError`: Raised when an operation or function is applied to an object of inappropriate type.
  - `ValueError`: Raised when a function receives an argument of correct type but with an inappropriate value.
  - `FileNotFoundError`: Raised when a file or directory is requested but cannot be found.
- **Exception Handling Strategies**:
  - Specific Exception Handling: Handle specific exceptions individually.
  - Generic Exception Handling: Handle all exceptions with a generic `except` block.
  - Raising Exceptions: Raise custom exceptions using the `raise` statement.
  
#### Using Debugging Tools and Techniques:
- **Print Statements**:
  - Insert print statements at strategic points in the code to inspect variable values and control flow.
- **Debugger**:
  - Use Python's built-in debugger (`pdb`) or external IDEs with debugging capabilities.
  - Set breakpoints to pause execution at specific lines of code and inspect variables.
- **Logging**:
  - Use the `logging` module to log messages at different severity levels during program execution.
  - Logging allows for more detailed inspection of program behavior compared to print statements.
- **Unit Tests**:
  - Write unit tests to systematically test individual components of code and identify errors.
  - Unit tests help catch bugs early in the development process and ensure code reliability.
  
#### Summary:
- Error handling allows programs to gracefully handle unexpected errors or exceptions that occur during execution.
- Python provides a `try-except` block for handling exceptions, allowing developers to respond to errors appropriately.
- Common debugging techniques include using print statements, debugging tools like `pdb`, logging, and writing unit tests.
  
#### Facts:
- Error handling is essential for managing unexpected errors or exceptions that occur during program execution.
- Python's `try-except` block allows developers to gracefully handle exceptions and prevent program crashes.
- Debugging tools like `pdb`, logging, and unit tests help identify and fix errors in Python code.

### File I/O Operations:

#### Reading and Writing Files:
- **File Modes**:
  - Python supports various file modes for reading, writing, and appending data to files.
  - Common file modes include `'r'` for reading, `'w'` for writing, and `'a'` for appending.
- **Opening and Closing Files**:
  - Use the `open()` function to open a file and obtain a file object.
  - Syntax:
    ```python
    file = open('filename.txt', mode)
    ```
  - Always remember to close files using the `close()` method to release system resources.
- **Reading from Files**:
  - Use the `read()` method to read the entire contents of a file as a single string.
  - Alternatively, use the `readline()` or `readlines()` methods to read one line or all lines from a file, respectively.
- **Writing to Files**:
  - Use the `write()` method to write data to a file.
  - Syntax:
    ```python
    file.write('data')
    ```
  - Always remember to close the file after writing.
  
#### Working with CSV Files:
- **CSV (Comma-Separated Values)**:
  - CSV files store tabular data in plain text format, with each line representing a row and fields separated by commas.
  - Python's `csv` module provides functions to read from and write to CSV files.
  - Use `csv.reader()` to read data from a CSV file and `csv.writer()` to write data to a CSV file.

#### Working with JSON Files:
- **JSON (JavaScript Object Notation)**:
  - JSON files store data in a structured format similar to Python dictionaries.
  - Python's `json` module provides functions to encode Python objects as JSON strings and decode JSON strings into Python objects.
  - Use `json.dump()` to write data to a JSON file and `json.load()` to read data from a JSON file.

#### Working with XML Files:
- **XML (eXtensible Markup Language)**:
  - XML files store structured data using custom tags and attributes.
  - Python's `xml.etree.ElementTree` module provides functions to parse and manipulate XML data.
  - Use `ElementTree.parse()` to parse an XML file and `ElementTree.Element()` to create XML elements.

#### Summary:
- Python provides built-in support for reading from and writing to various file formats, including plain text, CSV, JSON, and XML.
- File I/O operations involve opening files, reading or writing data, and closing files to release system resources.
- The `csv`, `json`, and `xml.etree.ElementTree` modules provide convenient functions for working with CSV, JSON, and XML files, respectively.

#### Facts:
- File I/O operations are fundamental for reading and writing data to files in Python.
- CSV, JSON, and XML are common file formats used for storing and exchanging structured data.
- Python's built-in modules (`csv`, `json`, `xml.etree.ElementTree`) provide convenient functions for working with these file formats.
### 1. Define Classes and Objects:
- **Classes**: 
  - Classes are blueprints for creating objects in Python.
  - They define the properties (attributes) and behaviors (methods) that objects of that class will have.
  - Classes encapsulate data for the objects and the methods to manipulate that data.

- **Objects**:
  - Objects are instances of classes.
  - Each object represents a specific instance of the class, with its own unique data and behavior.
  - Objects are created based on the structure defined by the class.
#### Definition:
- **Instances of Classes**:
  - <mark style="background: #FFB86CA6;">Objects are instances of classes in Python</mark>.
  - They <mark style="background: #FFF3A3A6;">represent specific occurrences or instances of the class structure</mark>.
- **Unique Data and Behavior**:
  - <mark style="background: #FFF3A3A6;">Each object possesses its own unique set of data and behavior, distinct from other objects of the same class</mark>.
- **Creation**:
  - <mark style="background: #BBFABBA6;">Objects are created based on the blueprint provided by the class definition</mark>.

#### Key Points:
- **Instantiation**:
  - The process of creating an object from a class is called instantiation.
- **Attributes and Methods**:
  - Objects inherit attributes and methods from their class, allowing them to access data and perform actions defined within the class.
- **State and Behavior**:
  - Objects encapsulate both state (represented by attributes) and behavior (represented by methods), making them self-contained entities.
- **Example**:
  ```python
  class Person:
      def __init__(self, name, age):
          self.name = name   # Attribute
          self.age = age     # Attribute
          
      def greet(self):
          print(f"Hello, my name is {self.name} and I am {self.age} years old.")   # Method
  
  # Creating objects (instances) of the Person class
  person1 = Person("Alice", 30)
  person2 = Person("Bob", 25)
  
  # Each object has its own unique data and behavior
  person1.greet()  # Output: Hello, my name is Alice and I am 30 years old.
  person2.greet()  # Output: Hello, my name is Bob and I am 25 years old.
  ```

#### Importance:
- **Modularity**:
  - Objects promote modularity by encapsulating data and behavior within self-contained units, enhancing code organization and maintainability.
- **Reusability**:
  - Objects can be reused across different parts of a program, reducing redundancy and facilitating code reuse.
- **Abstraction**:
  - Objects abstract away complex implementation details, allowing users to interact with them through well-defined interfaces (methods).
- **Scalability**:
  - Objects support scalability by enabling the creation of multiple instances of a class, each serving a specific purpose within a larger system.

### 2. Relationship Between Classes and Objects:
- **Class-Object Relationship**:
  - A class serves as a template or blueprint for creating objects.
  - Objects are instances of a class, meaning they are specific realizations of that class.
  - Each object inherits the attributes and methods defined in the class but can have its own unique data.

### 3. Creating Instances of a Class (Objects):
- **Instantiation**:
  - Instantiation is the process of creating objects from a class.
  - To create an object, you use the class name followed by parentheses, optionally passing arguments if the class has an `__init__` method.

```python
# Example of creating instances of a class
class MyClass:
    pass

# Creating objects (instances) of MyClass
obj1 = MyClass()
obj2 = MyClass()
```

### 4. Attributes and Methods in Classes:
- **Attributes**:
  - Attributes are variables that belong to a class or an object.
  - They represent the data associated with the class or object.
  - Attributes can be accessed using dot notation (`object.attribute`).

- **Methods**:
  - Methods are functions defined within a class.
  - They represent the behaviors or actions that objects of the class can perform.
  - Methods can access and manipulate the attributes of the class or object.

```python
# Example of attributes and methods in a class
class Person:
    # Class attribute
    species = 'Human'
    
    # Constructor method
    def __init__(self, name, age):
        # Instance attributes
        self.name = name
        self.age = age
    
    # Method to introduce the person
    def introduce(self):
        print(f"Hello, my name is {self.name} and I am {self.age} years old.")

# Creating an instance of the Person class
person1 = Person("Alice", 30)

# Accessing attributes and calling methods
print(person1.name)    # Output: Alice
print(person1.age)     # Output: 30
person1.introduce()    # Output: Hello, my name is Alice and I am 30 years old.
```


### Attributes vs. Methods:

#### Attributes:
- **Definition**: 
  - <mark style="background: #FFB86CA6;">Attributes are variables that belong to a class</mark> or an object.
- **Role**:
  - Attributes store data associated with the class or object.
  - They represent the state or characteristics of the class or object.
- **Access**:
  - Attributes can be accessed using dot notation (`object.attribute`).
- **Example**:
  ```python
  class Car:
      def __init__(self, make, model):
          self.make = make   # Attribute
          self.model = model # Attribute
  ```

#### Methods:
- **Definition**:
  - <mark style="background: #FFB86CA6;">Methods are functions defined within a class.</mark>
- **Role**:
  - Methods represent behaviors or actions that objects of the class can perform.
  - They operate on the data stored in the attributes of the class or object.
- **Access**:
  - Methods can be called using dot notation (`object.method()`).
- **Example**:
  ```python
  class Car:
      def start_engine(self):
          print("Engine started") # Method
  
      def stop_engine(self):
          print("Engine stopped") # Method
  ```

### Role of Attributes in Storing Data:
- **Data Storage**:
  - Attributes play a crucial role in storing data within objects.
  - They represent the state of objects by holding values that describe their characteristics or properties.
- **Example**:
  ```python
  class Person:
      def __init__(self, name, age):
          self.name = name   # Attribute
          self.age = age     # Attribute
  ```

### Methods as Functions Defined Within a Class:
- **Functionality**:
  - Methods encapsulate functionality related to the class.
  - They define the behavior of objects and enable them to perform specific actions or tasks.
- **Encapsulation**:
  - Methods provide a way to encapsulate related operations within the class, promoting modularity and code organization.
- **Example**:
  ```python
  class Calculator:
      def add(self, x, y):
          return x + y   # Method
  
      def subtract(self, x, y):
          return x - y   # Method
  ```

### Inheritance:

#### Definition:
- **Concept**:
  - Inheritance is a fundamental concept in object-oriented programming (OOP) where a new class (subclass or child class) can inherit attributes and methods from an existing class (superclass or parent class).
- **Hierarchy**:
  - It establishes a hierarchical relationship between classes, allowing subclasses to inherit the properties of their superclass.
- **Importance**:
  - Inheritance promotes code reuse, modularity, and extensibility by enabling the creation of specialized classes based on existing ones.

#### Superclass and Subclass:
- **Superclass (Parent Class)**:
  - The superclass is the existing class from which attributes and methods are inherited.
  - It serves as the base or template for creating more specialized classes.
- **Subclass (Child Class)**:
  - The subclass is the new class that inherits attributes and methods from the superclass.
  - It can add additional features or modify existing ones while retaining the behavior of the superclass.

#### Inheriting Attributes and Methods:
- **Attributes**:
  - Subclasses inherit attributes (instance variables) defined in the superclass, gaining access to the same data.
  - They can also define their own unique attributes.
- **Methods**:
  - Subclasses inherit methods (functions) from the superclass, allowing them to perform the same actions.
  - They can override inherited methods to customize behavior or add new methods to extend functionality.

#### Method Overriding and super():
- **Method Overriding**:
  - Subclasses can override methods inherited from the superclass by redefining them with the same name.
  - This allows subclasses to customize behavior without modifying the superclass.
- **super() Function**:
  - The `super()` function allows subclasses to call methods from the superclass, facilitating method overriding.
  - It provides a way to access and invoke superclass methods within the context of the subclass.

#### Example:
```python
class Animal:
    def speak(self):
        return "Animal speaks"

class Dog(Animal):  # Dog inherits from Animal
    def speak(self):  # Method overriding
        return "Dog barks"

# Creating instances
animal = Animal()
dog = Dog()

# Inheritance in action
print(animal.speak())  # Output: Animal speaks
print(dog.speak())     # Output: Dog barks
```

#### Importance:
- **Code Reuse**:
  - Inheritance promotes code reuse by allowing subclasses to inherit attributes and methods from their superclass, reducing redundancy.
- **Modularity**:
  - It enhances modularity by facilitating the creation of specialized classes that build upon existing ones, promoting a hierarchical organization of code.
- **Extensibility**:
  - Inheritance enables the extension of class functionality by adding new features or modifying existing ones in subclasses, enhancing the flexibility and scalability of the codebase.
- **Polymorphism**:
  - It supports polymorphism, allowing objects of subclasses to be treated as objects of their superclass, promoting flexibility and interoperability in object interactions.

In summary, inheritance is a powerful mechanism in OOP that fosters code reuse, modularity, and extensibility by establishing relationships between classes and enabling the propagation of attributes and methods across class hierarchies. It plays a crucial role in designing flexible and maintainable software systems.

### Polymorphism:

#### Definition:
- **Ability for Objects to Take on Multiple Forms**:
  - Polymorphism allows objects to be treated as instances of their superclass or any subclasses, enabling them to exhibit different behaviors based on their specific types.
- **Method Overriding and Overloading**:
  - Polymorphism is implemented through method overriding and overloading, where methods in subclasses can replace or extend methods inherited from their superclass.

#### Key Concepts:
- **Method Overriding**:
  - Subclasses can provide a specific implementation of a method that is already defined in their superclass.
  - The overridden method in the subclass takes precedence over the method in the superclass when invoked on an object of the subclass.
- **Method Overloading**:
  - Method overloading involves defining multiple methods with the same name but different parameter lists within a class or its subclasses.
  - The appropriate method is selected based on the number or type of arguments provided during method invocation.
- **Benefits**:
  - **Code Flexibility**:
    - Polymorphism enhances code flexibility by allowing different objects to respond differently to the same method invocation, based on their specific types.
  - **Code Reusability**:
    - Polymorphism promotes code reusability by enabling the same method name to be used across different classes, facilitating modular design and maintenance.
  - **Enhanced Readability**:
    - Polymorphic code is often more readable and intuitive, as it reflects the natural behavior of objects in the real world, leading to clearer and more concise code.

#### Example:
```python
class Animal:
    def speak(self):
        print("Animal speaks")

class Dog(Animal):
    def speak(self):
        print("Dog barks")

class Cat(Animal):
    def speak(self):
        print("Cat meows")

# Polymorphic behavior
def make_speak(animal):
    animal.speak()

# Objects of different types exhibiting polymorphic behavior
animal1 = Animal()
animal2 = Dog()
animal3 = Cat()

make_speak(animal1)  # Output: Animal speaks
make_speak(animal2)  # Output: Dog barks
make_speak(animal3)  # Output: Cat meows
```

#### Importance:
- **Flexibility**:
  - Polymorphism allows for flexible and extensible code, enabling objects to behave in different ways based on their specific types.
- **Extensibility**:
  - Polymorphism facilitates the addition of new subclasses with specialized behavior without modifying existing code, promoting modular design and scalability.
- **Encapsulation**:
  - Polymorphism encourages encapsulation by separating the implementation details of individual classes, leading to more modular, maintainable, and reusable code.

In summary, polymorphism enables objects to exhibit different behaviors based on their specific types, promoting code flexibility, reusability, and extensibility in object-oriented programming. By embracing polymorphism, developers can write more modular, maintainable, and expressive code that better models real-world scenarios.


### Advanced Python Concepts:

#### Decorators:

##### Definition:
- **Function Decorators**:
  - Decorators are a powerful feature in Python that allow you to dynamically modify the behavior of functions or methods.
  - They are implemented using functions themselves, and they modify or enhance the behavior of other functions or methods without changing their actual code.
  
##### Key Concepts:
- **Decorator Syntax**:
  - Decorators are applied using the `@decorator_name` syntax, which is placed before the definition of the function to be decorated.
- **Higher-order Functions**:
  - Decorators are implemented as higher-order functions, which are functions that take another function as an argument and return a new function.
- **Common Use Cases**:
  - **Logging**:
    - Decorators can be used to log function calls, providing useful information for debugging and monitoring.
  - **Authentication and Authorization**:
    - Decorators can enforce authentication and authorization checks before allowing access to certain functions or methods.
  - **Performance Monitoring**:
    - Decorators can measure the execution time of functions and provide performance metrics.
  - **Caching**:
    - Decorators can cache the results of function calls to improve performance by avoiding redundant computation.
  
#### Generators:

##### Definition:
- **Generator Functions**:
  - Generators are a special type of iterable in Python that allow you to generate a sequence of values on-the-fly using a simple and memory-efficient syntax.
  - They are implemented using generator functions, which are functions that contain one or more `yield` statements.
  
##### Key Concepts:
- **Lazy Evaluation**:
  - Generators use lazy evaluation, which means that they produce values only when requested, conserving memory and improving performance.
- **Iterators**:
  - Generators are also iterators, meaning they support iteration protocols like `for` loops and can be consumed using functions like `next()`.
- **Infinite Sequences**:
  - Generators can produce infinite sequences of values, making them suitable for scenarios where you need to work with large or potentially infinite datasets.
- **Memory Efficiency**:
  - Generators are memory-efficient because they generate values on-the-fly and do not store the entire sequence in memory at once.
  
#### Context Managers:

##### Definition:
- **Resource Management**:
  - Context managers are used for resource management, ensuring that resources like files, database connections, or locks are properly acquired and released.
  - They are implemented using the `with` statement in Python.
  
##### Key Concepts:
- **`__enter__` and `__exit__` Methods**:
  - Context managers define `__enter__` and `__exit__` methods that are called when entering and exiting the context, respectively.
  - The `__enter__` method is responsible for acquiring resources, while the `__exit__` method is responsible for releasing resources and handling exceptions.
- **`with` Statement**:
  - The `with` statement is used to create a context managed by a context manager, ensuring that resources are properly managed even in the presence of exceptions.
- **Common Use Cases**:
  - **File Handling**:
    - Context managers can be used to automatically close files after they have been used, ensuring that resources are released properly.
  - **Database Connections**:
    - Context managers can be used to manage database connections, ensuring that connections are closed when they are no longer needed.
  - **Thread Synchronization**:
    - Context managers can be used to acquire and release locks for thread synchronization, preventing race conditions and deadlocks.

#### Regular Expressions:

##### Definition:
- **Pattern Matching**:
  - Regular expressions (regex) are a powerful tool for pattern matching and text manipulation in Python.
  - They provide a concise and flexible syntax for searching, extracting, and replacing text based on specified patterns.
  
##### Key Concepts:
- **Pattern Syntax**:
  - Regular expressions consist of special characters and symbols that define patterns to be matched against text.
- **Match Objects**:
  - Regular expression operations return match objects, which contain information about the match including the matched text and its location in the input string.
- **Common Operations**:
  - **Search**:
    - Search for a pattern within a string, returning the first match found.
  - **Match**:
    - Determine if the entire string matches a given pattern.
  - **Substitution**:
    - Replace occurrences of a pattern in a string with specified text.
  - **Splitting**:
    - Split a string into substrings based on a specified pattern.
- **Performance Considerations**:
  - Regular expressions can be powerful but may also be computationally expensive, especially for complex patterns or large input strings.
  - Care should be taken to optimize regular expressions for performance-critical applications.

#### Facts:
- Decorators enhance the functionality of functions by modifying or extending their behavior dynamically.
- Generators produce values on-the-fly using lazy evaluation, conserving memory and improving performance.
- Context managers ensure proper resource management by acquiring and releasing resources automatically within a defined context.
- Regular expressions provide a powerful tool for pattern matching and text manipulation based on specified patterns.

### Encapsulation:

#### Definition:
- **Bundling of Data and Methods**:
  - Encapsulation refers to the bundling of data (attributes) and methods (functions) that operate on the data within a single unit, typically a class in object-oriented programming.
  - It allows for the organization of related functionality and data into a cohesive and self-contained unit.

#### Importance:
- **Information Hiding**:
  - Encapsulation facilitates information hiding by restricting access to certain components of the class, thereby preventing direct modification of internal data and ensuring data integrity.
  - It hides the implementation details of a class from external users, allowing changes to be made to the internal structure without affecting external code that interacts with the class.
- **Code Organization**:
  - Encapsulation promotes code organization and modularity by grouping related functionality and data together within a class.
  - It helps in managing complexity by breaking down large systems into smaller, more manageable units that can be understood and maintained independently.

#### Access Modifiers:
- **Public**:
  - Public members (attributes and methods) are accessible from outside the class and can be freely accessed and modified by external code.
  - They are typically used for functionality that is intended to be part of the public interface of the class.
- **Private**:
  - Private members are accessible only within the class itself and cannot be accessed or modified from outside the class.
  - They are typically used for internal implementation details that should not be exposed to external users.
  - In Python, private members are indicated by prefixing the attribute or method name with double underscores (`__`).
- **Protected**:
  - Protected members are accessible within the class itself and its subclasses (derived classes), but not from outside the class hierarchy.
  - They are typically used when certain attributes or methods need to be accessible to subclasses but hidden from external code.
  - In Python, protected members are indicated by prefixing the attribute or method name with a single underscore (`_`), although this is more of a convention than a strict enforcement.

#### Example:
```python
class EncapsulatedClass:
    def __init__(self):
        self.__private_attr = 10  # Private attribute
        self._protected_attr = 20  # Protected attribute
        self.public_attr = 30  # Public attribute

    def get_private_attr(self):
        return self.__private_attr

    def set_private_attr(self, value):
        self.__private_attr = value

# Creating an object of the EncapsulatedClass
obj = EncapsulatedClass()

# Accessing public attribute
print(obj.public_attr)  # Output: 30

# Accessing private attribute (will raise an AttributeError)
# print(obj.__private_attr)

# Accessing protected attribute
print(obj._protected_attr)  # Output: 20

# Accessing private attribute using getter method
print(obj.get_private_attr())  # Output: 10

# Modifying private attribute using setter method
obj.set_private_attr(50)
print(obj.get_private_attr())  # Output: 50
```

#### Facts:
- Encapsulation bundles data and methods within a single unit (class), promoting information hiding and code organization.
- Access modifiers like public, private, and protected control the visibility and accessibility of class members, ensuring proper encapsulation and data integrity.
- Encapsulation helps manage complexity by breaking down systems into smaller, self-contained units with well-defined interfaces.

### Class Relationships:

#### Aggregation:
- **Definition**:
  - Aggregation is a type of class relationship where one class (the whole or container) contains references to other classes (the parts or components), but the contained classes do not depend on the container class for their existence.
  - It represents a "has-a" relationship, where the container class "has" instances of the contained class.
- **Example**:
  - A `Library` class may contain references to multiple `Book` objects. The `Book` objects exist independently of the `Library`, and they can be removed from the `Library` without being destroyed.
- **Benefits**:
  - Allows for modular design by breaking down complex systems into smaller, reusable components.
  - Promotes code reusability and flexibility by enabling the reuse of existing classes in different contexts.
  
#### Composition:
- **Definition**:
  - Composition is a stronger form of aggregation where the lifetime of the contained objects is tightly coupled to the lifetime of the container object.
  - It represents a "part-of" relationship, where the contained objects are integral parts of the container object and cannot exist independently.
- **Example**:
  - A `Car` class may contain instances of `Engine`, `Wheel`, and `Chassis` classes. The `Engine`, `Wheel`, and `Chassis` objects are created and destroyed along with the `Car`.
- **Benefits**:
  - Ensures better control over the lifetime of contained objects, preventing orphaned objects and resource leaks.
  - Simplifies memory management by automatically deallocating resources when the container object is destroyed.

#### Association:
- **Definition**:
  - Association represents a relationship between two classes where one class uses or interacts with another class.
  - It can be a one-to-one, one-to-many, or many-to-many relationship.
- **Example**:
  - A `Student` class may be associated with a `School` class, indicating that a student attends a particular school.
- **Benefits**:
  - Enables communication and collaboration between objects by allowing them to exchange messages and share data.
  - Facilitates the modeling of real-world relationships and behaviors in object-oriented systems.

#### Summary:
- Aggregation and composition are two types of class relationships that represent "has-a" and "part-of" relationships, respectively.
- Aggregation allows for independent existence of contained objects, while composition tightly couples the lifetime of contained objects to the container object.
- Association represents a usage or interaction relationship between classes, enabling communication and collaboration between objects.
  
#### Facts:
- Aggregation and composition are types of class relationships that model "has-a" and "part-of" relationships, respectively.
- Association represents a usage or interaction relationship between classes, facilitating communication and collaboration between objects.
- Aggregation promotes code reusability and modular design, while composition ensures better control over the lifetime of contained objects.

### Design Patterns:

#### Singleton Pattern:
- **Definition**:
  - The Singleton pattern ensures that a class has only one instance and provides a global point of access to that instance.
  - It is useful when exactly one object is needed to coordinate actions across the system.
- **Example**:
  - A `Logger` class that manages system logs. It ensures that there is only one instance of the `Logger` throughout the application.
- **Implementation**:
  - Use a static method to control access to the single instance.
  - Lazily instantiate the instance the first time it is requested.
- **Benefits**:
  - Provides a single point of access to a shared resource, such as a configuration or logging object.
  - Guarantees that there is only one instance of the class, reducing resource consumption and preventing conflicts.

#### Factory Pattern:
- **Definition**:
  - The Factory pattern provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created.
  - It is useful when the creation process is complex or when the specific subclass to be instantiated is unknown at runtime.
- **Example**:
  - A `ShapeFactory` class that creates instances of different geometric shapes such as `Circle`, `Rectangle`, and `Triangle`.
- **Implementation**:
  - Define a common interface or superclass for the objects to be created.
  - Create a factory class with methods for creating instances of the objects.
- **Benefits**:
  - Encapsulates object creation, making the code more maintainable and flexible.
  - Decouples the client code from the concrete classes, allowing for easier extensibility and modification.

#### Observer Pattern:
- **Definition**:
  - The Observer pattern defines a one-to-many dependency between objects, where changes in one object (the subject or publisher) trigger updates in other objects (the observers or subscribers).
  - It is useful for implementing distributed event handling systems or building loosely coupled systems.
- **Example**:
  - An `EventDispatcher` class that notifies registered listeners about changes or events in the system.
- **Implementation**:
  - Define interfaces for subjects and observers to establish a contract.
  - Allow observers to register or unregister themselves with the subject.
- **Benefits**:
  - Promotes loose coupling between objects, allowing for easier maintenance and modification.
  - Enables the creation of reusable components that can be independently developed and tested.

#### Summary:
- Design patterns such as Singleton, Factory, and Observer provide solutions to common design problems in object-oriented systems.
- Singleton ensures a single instance of a class, Factory encapsulates object creation, and Observer facilitates communication between objects.
- Each design pattern has specific use cases and benefits, contributing to the overall maintainability, flexibility, and scalability of the software system.

#### Facts:
- Design patterns such as Singleton, Factory, and Observer address common design challenges in object-oriented programming.
- Singleton ensures that a class has only one instance, Factory encapsulates object creation, and Observer facilitates communication between objects.
- Each design pattern has its specific use cases and implementation strategies, contributing to the overall robustness and flexibility of software systems.