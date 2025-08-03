# Programming

## What is programming?

Programming is the process of designing, writing, testing, debugging, and maintaining the source code of computer programs. It is a set of instructions that tell a computer what to do and how to do it.

Programming languages are the languages used to write the source code of programs. There are many programming languages, each with its own syntax, structure, and rules. The four most popular programming languages used in FRC include [Python](https://www.python.org/), [Java](https://www.java.com/en/download/help/whatis_java.html), [C++](https://www.w3schools.com/cpp/cpp_intro.asp), and [LabVIEW](https://www.ni.com/en-us/shop/labview.html).

## Why do programming languages exist?

Programming languages exist to provide a way for humans to communicate instructions to computers in a manner that they can understand and execute.

Computers are essentially machines that perform operations based on a set of instructions. However, computers do not understand natural language like humans do, so programming languages provide a way for us to write code in a structured, formal syntax that the computer can interpret and execute.

Programming languages have evolved over time to become more user-friendly, easier to read, and capable of abstracting complex concepts into simple, high-level constructs. This makes it easier for humans to write and understand code, and allows for the creation of more complex programs.

Additionally, programming languages serve as a means of communication between developers, enabling them to share, reuse, and build upon each other's code.

In summary, programming languages exist to provide a bridge between human language and the language of computers, enabling us to create software that can perform a wide range of tasks and solve complex problems.

## What is Syntax

Syntax is the set of rules and constructs that define how code is written in a particular programming language. This includes things like variable declaration, function definition, and control structures.

### Python Syntax

Python uses indentation to define code blocks, instead of brackets. The standard indentation is four spaces, although tabs and any other space size will work, as long as it is consistent. Each logical line of code must have the same indentation. The following code is an example of proper indentation.
```python
def function():
    if True:
        print("Hello World")
        if False:
            print("This won't run")
    print("This will run")
```

The following code is an example of improper indentation.
```python
def function():
    if True:
        print("Hello World")
    if False:
        print("This won't run")
    print("This will run")
```
### Variables

Variables are used to store data values. Python has no command for declaring a variable. A variable is created the moment you first assign a value to it. Variables do not need to be declared with any particular type, and can even change type after they have been set.
```python
x = 5
y = "John"
print(x)
print(y)
```
### Comments

Comments can be used to explain Python code. Comments can be used to make the code more readable. They can also be used to prevent execution when testing code.
```python
#This is a comment.
print("Hello, World!") #This is also a comment.
```
### Data Types

Python has the following data types built-in by default, in these categories:

* Text Type: `str`
* Numeric Types: `int`, `float`, `complex`
* Sequence Types: `list`, `tuple`, `range`
* Mapping Type: `dict`
* Set Types: `set`, `frozenset`
* Boolean Type: `bool`
* Binary Types: `bytes`, `bytearray`, `memoryview`

### Strings

Strings in Python are surrounded by either single quotation marks, or double quotation marks.
```python
x = "Hello World"
# is the same as
x = 'Hello World'
```

Strings can be output to screen using the `print()` function.
```python
x = "Hello World"
print(x)
```

### Numbers

Python supports two types of numbers - integers and floating point numbers. (It also supports complex numbers, which will not be explained in this document.) To define an integer, use the following syntax:
```python
x = 1
y = 35656222554887711
z = -3255522
```

To define a floating point number, you may use one of the following notations:
```python
x = 1.10
y = 1.0
z = -35.59
a = 35e3
b = 12E4
c = -87.7e100
```

### Booleans

Booleans represent one of two values: `True` or `False`.
```python
print(10 > 9)
print(10 == 9)
print(10 < 9)
```

### Casting

If you want to specify the data type of a variable, this can be done with casting.
```python
x = str(3)    # x will be '3'
y = int(3)    # y will be 3
z = float(3)  # z will be 3.0
```

### Getting the Type

You can get the data type of a variable with the `type()` function.
```python
x = 5
y = "John"
print(type(x))
print(type(y))
```

### Setting the Specific Type

You can specify the data type with the following constructor functions:
```python
x = str("s1") # x will be 's1'
y = int(2)    # y will be 2
z = float(3.0)# z will be 3.0
```

# Electronics

## Types of Electronics

In the world of electronics there are two main types of electronics: analog and digital. Analog electronics are used to control things that have a continuous range of values. For example a knob on a stereo that controls the volume. Digital electronics are used to control things that have a discrete number of values. For example a light switch that can be either on or off. The on and off can be toggled in various ways, but the number of values is still discrete. These advanced digital communications are methods like I2C, Serial, and CAN.

### Analog Electronics

Some examples of analog electronics are:

* Volume control on a stereo
* Temperature control on a heater
* Steering wheel on a car
* Throttle on a motorcycle

### Digital Electronics

Some examples of digital electronics are:

* Light switch
* Motion sensor
* Doorbell
* Limit switch on a machine
* OLED display

## Electronics components in FRC

There are many categories of electronic components that are used in FRC. Some of the most common are:

* Motors and Motor Controllers
* Limit Switches and Buttons
* Pressure Sensors
* Cameras
* Relays
* Lights
* Microcontrollers
* Encoders
* Gyro/IMU
* Power Distribution
* Radio
