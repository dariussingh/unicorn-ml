---
layout: default
title: Introduction
parent: Python
nav_order: 1
---

# Introduction

## What is python?
Python is an interpreted, object-oriented, high-level programming language with dynamic semantics. Its high-level built in data structures, combined with dynamic typing and dynamic binding, make it very attractive for Rapid Application Development, as well as for use as a scripting or glue language to connect existing components together. Python's simple, easy to learn syntax emphasizes readability and therefore reduces the cost of program maintenance. Python supports modules and packages, which encourages program modularity and code reuse. The Python interpreter and the extensive standard library are available in source or binary form without charge for all major platforms, and can be freely distributed.

Python is
- __Interpreted__: Programs are executed directly, no compilation and linking of programs is needed. The interpreter can be used interactively while writing programs.
- __Object-oriented__: It organizes software design around data, or objects rather than functions and logic.
- __High-level__: It has a strong abstraction from the details of machine language and uses natural language elements.

This tutorial assumes you have access to a system with python installed on it. If you do not have access to such a system, you can follow a [step-by-step guide](https://wiki.python.org/moin/BeginnersGuide/Download) on how to download and install python onto your system.

Let's write our first line of python code.
```python{% raw %}
>>> print("Hello World!")
Hello World!
{% endraw %}```
We have used the built-in `print()` function to print the string `Hello world!` on our screen. You will learn more about functions and strings in the upcoming sections.


## Comments
__Comments__ in python start with the hash `#` character and extend to the end of the physical line. A comment may appear a the start of a line or following whitespace or code, but not within a string literal. Comments are used to clarify code and are not interpreted by python.

```python{% raw %}
# this is a comment
spam = 1 # and this is the second comment
        # ... now a third
text = "# This is not a comment because it is inside quotes."
{% endraw %}```


