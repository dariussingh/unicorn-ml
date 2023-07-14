---
layout: default
title: Numeric Types and Operations
parent: Python
nav_order: 2
---

# Numeric Types and Operations

## Numeric types
Python supports arithmetic operations and hence we can use python as a calculator. There are three distinct numeric types: integers, floating point numbers, and complex numbers. Integers (`int`) as the names suggests, represents integers, floating point numbers (`float`) represents real numbers and complex numbers (`complex`) represents complex numbers and has a real and imaginary part, which is each a floating point number. To extract the real and imaginary parts of a complex number z, we can use `z.real` and `z.imag`. The standard library includes addition numeric types `fractions.Fraction`, for rational numbers, and `decimal.Decimal`, for float point numbers with user-definable precision.

```python{% raw %}
>>> type(7)
int
>>> type(7.0)
float
>>> type(3.14)
float
>>> type(22 / 7)
float
>>> type(1 + 2j)
complex
>>> type(10 + 5J)
complex
>>> (10 + 5J).real
10.0
>>> (10 + 5J).imag
5.0
{% endraw %}```

## Operations

### Numeric operations
Here is a table of operations available in python:

| Operation         | Result                                                                |
|:------------------|:----------------------------------------------------------------------|
| `x + y`           | sum of x and y                                                        |
| `x - y`           | difference of x and y                                                 |
| `x * y`           | product of x and y                                                    |
| `x / y`           | quotient of x and y                                                   |
| `x // y`          | integer division of x and y                                           |
| `x % y`           | modulus of x and y                                                    |
| `-x`              | x negated                                                             |
| `+x`              | x unchanged                                                           |
| `abs(x)`          | absolute value of x                                                   |
| `int(x)`          | x converted to integer                                                |
| `float(x)`        | x converted to floating point                                         |
| `complex(re, im)` | a complex number with real part _re_ and, \n and imaginary part _im_. |
| `c.conjugate()`   | conjugate of a complex number _c_                                     |
| `divmod(x, y)`    | the pair `(x // y, x % y)`                                            |
| `pow(x, y)`       | x to the power y                                                      |
| `x ** y`          | x to the power y                                                      |

Now let's do some simple calculations using python.

```python{% raw %}
>>> 2 + 2
4
>>> 50 - 5*6
20
>>> (50 - 5*6) / 4
5.0
>>> 8/5 # division always returns a floating point number
1.6
{% endraw %}```

Division (`/`) always returns a float. To do floor division and get an integer result you can use the `//` operator; to calculate the remainder you can use `%`.

```python{% raw %}
>>> 17 / 3 # classic division returns a float
5.666666666666667
>>> 17 //3 # floor division discards the fractional part
5
>>> 17 % 3 # the % operator returns the remainder of the division
2
>>> 5 * 3 + 2 # floored quotient * divisor + remainder
17
{% endraw %}```

The equal sign (`=`) can be used to assign a value to a variable. 

```python{% raw %}
>>> x = 2
>>> y = 3
>>> x ** y
8
>>> pow(x, y)
8
>>> -x
-2
>>> +y
3
>>> divmod(x, y)
(0, 2)
>>> abs(-x)
2
>>> float(x)
2.0
>>> int(y / x)
1
>>> z = complex(x, y)
>>> z
(2+3j)
>>> z.conjugate()
(2-3j)
{% endraw %}```

There is full support for floating point; operators with mixed type operands convert the integer operand to floating point.

```python{% raw %}
>>> 4 * 3.75 - 1
14.0
{% endraw %}```

In interactive mode, the last printed expression is assigned to the variable `_`.

```python{% raw %}
>>> tax = 12.5 / 100
>>> price = 100.50
>>> price * tax
12.5625
>>> price + _
113.0625
>>> round(_, 2)
113.06
{% endraw %}```

### Boolean operations
These are the Boolean operations, ordered by ascending priority.

| Operation   | Result                               |
|:------------|:-------------------------------------|
| `x or y`    | if x is true, then x, else y         |
| `x and y`   | if x is false, then x, else y        |
| `not x`     | if x is false, then true, else false |

For example:
```python{% raw %}
>>> False and False
False
>>> False and True
False
>>> True and True
True
>>> False or False
False
>>> False or True
True
>>> True or True
True
>>> not True
False
{% endraw %}```

### Comparison operations
There are eight comparison operations in python. They have the same priority (which is higher than that of Boolean operations). Comparisons can be chained arbitrarily; for example, `x < y <= z` is equivalent to `x < y and y <= z`, except that y is evaluated only once (but in both cases z is not evaluated at all when x < y is found to be false).

| Operation | Result                   |
|:----------|:-------------------------|
| `<`       | strictly less than       |
| `<=`      |  less than or equal      |
| `>`       | strictly greater than    |
| `>=`      |  greater than or equal   |
| `==`      |  equal                   |
| `!=`      |  not equal               |
| `is`      |  object identity         |
| `is not`  |  negated object identity |

For example:

```python{% raw %}
>>> 10 < 11
True
>>> 12 <= 11
False
>>> 10 > 10
False
>>> 10 >= 10
True
>>> 5 == 5
True
>>> 5 != 5
False
{% endraw %}```

The `is` keyword is used to test object identity i.e. to test whether two variables belong to the same object. For example: 

```python{% raw %}
>>> x = 10
>>> y = 10
>>> x == y
True
>>> x is y
True
{% endraw %}```

But we see that this does not hold when we define lists (you will learn more about lists in the upcoming sections).

```python{% raw %}
>>> list_a = [1, 2, 3]
>>> list_b = [1, 2, 3]
>>> list_a == list_b
True
>>> list_a is list_b
False
{% endraw %}```

### Bitwise operations
Bitwise operations only make sense for integers. The priorities of the binary bitwise operations are all lower than the numeric operations and higher than the comparisons; the unary operation `~` has the same priority as the other unary numeric operations (`+` and `-`).

The bitwise operations sorted in ascending priority are:

| Operation | Result                            |
|:----------|:----------------------------------|
| `x | y`   | bitwise _or_ of x and y           |
| `x ^ y`   | bitwise _exclusive or_ of x and y |
| `x & y`   | bitwise _and_ of x and y          |
| `x << n`  | x shifted left by n bits          |
| `x >> n`  | x shifted right by n bits         |
| `~x`      | the bits of x inverted            |

The `bin()` function can be used to convert a number from it's integer value to its binary value.

The bitwise OR operator `|` performs logical disjunction. For each corresponding pair of bits, it returns a one if atleast one of them is switched on.

```python{% raw %}
>>> a = 156
>>> bin(a)
'0b10011100'
>>> b = 52
>>> bin(b)
'0b110100'
>>> a | b
188
>>> bin(a | b)
'0b10111100'
{% endraw %}```

The bitwise AND operator `&` performs logical conjunction. For each corresponding pair of bits occupying the same position, it returns a one only when both bits are switched on.

```python{% raw %}
>>> a = 156
>>> bin(a)
'0b10011100'
>>> b = 52
>>> bin(b)
'0b110100'
>>> a & b
20
>>> bin(a & b)
'0b10100'
{% endraw %}```

The bitwise XOR operator `^` performs exclusive disjunction on bit pairs. Each bit pair must contain opposing bit values to produce one.

```python{% raw %}
>>> a = 156
>>> bin(a)
'0b10011100'
>>> b = 52
>>> bin(b)
'0b110100'
>>> a ^ b
168
>>> bin(a ^ b)
'0b10101000'
{% endraw %}```

The bitwise NOT operator `~` performs logical negation on a given number by flipping all of its bits.

```python{% raw %}
>>> a = 156
>>> bin(a)
'0b10011100'
>>> ~a
-157
>>> bin(~a)
'-0b10011101'
>>> ~a & 255
99
>>> bin(~a & 255)
'0b1100011'
{% endraw %}```

{: .note }
Unsigned data types don't let you store negative numbers such as -157 because there is no space for a sign in regular bit pattern.

Python does not support unsigned integers natively. That means all numbers have an implicit sign attached to them whether you specify one or not. In the above, instead of the expected output that is 99 we get -157, to fix this we use a bitmask.

The bitwise left shift operator `<<` moves the bits of its first operand to the left by the number of places specified in its second operand. It also takes care of inserting enough zero bits to fill the gap that arises on the right edge of the new bit pattern.

```python{% raw %}
>>> a = 39
>>> bin(a)
'0b100111'
>>> a << 2
156
>>> bin(a << 2)
'0b10011100'
>>> a << 3
312
>>> bin(a << 3)
'0b100111000'
{% endraw %}```

The bitwise right shift operator `>>` moves the bits of its first operand to the right by the number of places specified in its second operand.

```python{% raw %}
>>> a = 39
>>> bin(a)
'0b100111'
>>> a >> 2
9
>>> bin(a >> 2)
'0b1001'
>>> a >> 3
4
>>> bin(a >> 3)
'0b100'
{% endraw %}```

### Assignment operations
The following are the assignment operations in python.

| Operation | Result                  |
|:----------|:------------------------|
| `x = 10`  | assigns x a value of 10 |
| `x += y`  | `x = x + y`             |
| `x -= y`  | `x = x - y`             |
| `x *= y`  | `x = x * y`             |
| `x /= y`  | `x = x / y`             |
| `x %= y`  | `x = x % y`             |
| `x **= y` | `x = x ** y`            |
| `x &= y`  | `x = x & y`             |
| `x |= y`  | `x = x | y`             |
| `x ^= y`  | `x = x ^ y`             |
| `x >>= y` | `x = x >> y`            |
| `x <<= y` | `x = x << y`            |

For example:

```python{% raw %}
>>> c = 10
>>> print(c)
10
>>> c += 5
>>> print(c)
15
>>> c -= 6
>>> print(c)
9
>>> c *= 2
>>> print(c)
18
>>> c /= 3
>>> print(c)
6.0
>>> c %= 5
>>> print(c)
1.0
>>> c //= 1 + 10
>>> print(c)
1.0
>> c += 9
>> c **= 10
>>> print(c)
10000000000
{% endraw %}```