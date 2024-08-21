# ![Python Pre-Work - Error Handling in Python](./assets/hero.png)

## Error Handling in Python ( 25 min )

As you continue with Python, you’ll no doubt encounter a variety of errors fed back to you by the interpreter. When your program halts with an error message, this is an indication that something is wrong with the code. Learning to understand these messages — and what to do next — is an essential part of becoming a proficient programmer.

## Topics

- Troubleshooting Common Errors
- Using the Try-Except Code to Handle Errors
- Raising Errors in Your Own Code

### **Learning Objectives**

By the end of this lesson, you'll be able to:

- Troubleshoot the three most common Python programming errors.
- Determine when to use the`try-except` exception to bypass errors.
- Explain why you might use the `raise` keyword.

## Introduction

There are many different types of errors and exceptions in Python. The good news is, their names (for the most part) provide insight into the reason why the code failed to run.

Throughout the lesson, we'll cover a few of the most common errors, what each means, and how to troubleshoot each.

## Try it out in Repl.it!

Create a new [Repl.it](https://replit.com/new/python3) for this lesson called `Error_Handling_In_Python`. As you go through this lesson, try out the examples in your Repl to see how they work.

## How Do I Know There is an Error?

First things first, before we learn about individual errors, we need to know how Python communicates with us about said errors. It will communicate with us in whatever we're using to run our code (e.g. Repl.it or your terminal).

```bash
hello

# NameError: name 'hello' is not defined
```

Depending on your development environment, sometimes the error message may contain additional information, but the error itself `NameError: name 'hello' is not defined` will be contained within.

```plaintext
Traceback (most recent call last):
  File "/home/runner/Error_Handling_In_Python/main.py", line 1, in <module>
    hello
NameError: name 'hello' is not defined. Did you mean: 'help'?
```

Always read error messages carefully to determine the cause of the error.

## NameError

One basic type of error is a `NameError`. A `NameError` is thrown when the variable that’s referred to doesn’t exist in the _namespace_ — in other words, when we try to access a variable that we haven't defined yet.

### Try it out in Repl.it!

```bash
hello

# NameError: name 'hello' is not defined
```

We can fix this by declaring a variable named `hello`, which would allow us to avoid the error:

```bash
hello = True
print(hello)

# True
```

## SyntaxError

`SyntaxError` quite possibly the most common type of error.

A `SyntaxError` indicates that something you wrote doesn't follow the proper syntax of Python. A `SyntaxError` means we've mistyped something and as a result, Python doesn't understand.

For example, if we failed to place a colon after an `if` statement condition, we’d see something like this:

### Try it out in Repl.it!

```bash
if hello
    print('hello exists')

# SyntaxError: invalid syntax
```

Sometimes error messages will include clues about the location of the error in the code.

```plaintext
  File "/home/runner/Error_Handling_In_Python/main.py", line 1
    if hello
            ^
SyntaxError: expected ':'
```

An arrow (`^`) under the offending section of code indicates where the problem occurred.

The fix? Simply put the colon in its proper place:

```python
if hello:
    print('hello exists')

# hello exists
```

## TypeError

`TypeError` occurs when we try to do manipulate data types in a way that python does not permit. Like adding a string and an integer or trying to get the length of an integer.

### Try it out in Repl.it!

```python
12.0 + 'twelve'

# TypeError: unsupported operand type(s) for +: 'float' and 'str'
```

The `TypeError` already tells us that the error is related to Python data types. In this case, the message is clear (although it does contain a fair amount of jargon). Basically, this error message is telling us "hey, you can’t use the operand `+` with a float and a string."

## Error Types Summary

| Error Name    | What does it mean?                                                          | How can I fix it?                                                                                                                       |
| ------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `NameError`   | We're trying to access a variable that we haven't defined yet.              | Double check that the variable you're trying to access is correct. If it is, ensure you've defined that variable prior to accessing it. |
| `SyntaxError` | We've written something that doesn't follow the proper syntax of Python.    | Double check the syntax in the line(s) where Python indicates there is an error. This is indicated by the error message.                |
| `TypeError`   | We're trying to manipulate data types in a way that Python does not permit. | Read the helper text Python included with the `TypeError` and double check what you're asking Python to do.                             |

## Break the Shackles!

What if we _want_ to do something that throws an error in Python? We can actually write logic that tells Python what to do in the case of an error. Exceptions are our ticket to breaking free from Python errors.

## For Example

Let's say in the example below, we wanted to convert the list of strings into floats.

```python
str_to_float = ['2.1', '2.3', '7,5', '$12.12', '8.9', '5%', '33.1']
```

Normally, the program would get to the `,` in `7,5` and stop running entirely with an error – Python can't convert certain characters like commas into floats.

However, we can get around this by writing a function that loops through a string checking to see if each character has a comma, dollar sign, or percentage. If it does, then that character is marked as corrupted.

Then, we convert all the characters that are not corrupted to floats and add them to a list. If the character is corrupted, we add `None`. We used logic to get around the error!

### Try it out in Repl.it!

```python
str_to_float = ['2.1', '2.3', '7,5', '$12.12', '8.9', '5%', '33.1']

floats = []
bad_characters = ',$%'
for number in str_to_float:
    corrupted = False
    for bad_character in bad_characters:
        if bad_character in number:
            corrupted = True
            break  # Exit the inner loop if a bad character is found
    if corrupted:
        floats.append(None)
    else:
        floats.append(float(number))

print(floats)

# [2.1, 2.3, None, None, 8.9, None, 33.1]
```

Once we’ve executed the code block, `floats` should be `[2.1, 2.3, None, None, 8.9, None, 33.1]`.

## But What If...

But what if instead of just seven strings like in the previous example, we had millions of different strings that we wanted to convert? What if some of them had characters other than just commas, dollar signs and percentages that could break the `float` function?

It would be impossible to look through every element in a program and come up with the logic to ensure the process doesn’t throw an error. And even if it were possible, our code could quickly become bloated with condition after condition that needed to be met.

## Let's Use Try-Except This Time

Luckily, we can wait for `float` to break and _then_ take action. The basic syntax for handling exceptions uses the keywords `try` and `except`.

Here’s how we can use them given the previous example:

```python
str_to_float = ['2.1', '2.3', '7,5', '$12.12', '8.9', '5%', '33.1']

floats = []
for number in str_to_float:
    try:
        floats.append(float(number))
    except:
        floats.append(None)

print(floats)

# [2.1, 2.3, None, None, 8.9, None, 33.1]
```

The code above simply catches _any_ exception that could occur in the `try` statement.

Just like before, we initialize an empty list to hold the converted numbers. Now, as we iterate through the `str_to_float` list, we use the `try` and `except` syntax to handle errors. First, `try` attempts the code inside of its block. If that code successfully runs, `except` is skipped. Alternatively, if the code in the `try` block throws an exception, the code inside of the `except` block will run instead.

There are many exceptions –see the full list [here](https://docs.python.org/3/library/exceptions.html) – for now, we'll stick with the most common.

## Getting Specific

It may be more useful to be specific about the type of error on which you want to act.

Fortunately, we can chain multiple `except` statements together _and_ write out the specific type of exception we want each `except` statement to target (hence the keyword `target`).

```python
try:
    # Code
except TypeError as e:
    # Code to run on TypeError.
except (NameError, ValueError) as e:
    # Code to run if NameError or ValueError is thrown.
except Exception as e:
    # All other exceptions.
```

Splitting the `except` statement into multiple sections delineated by error type improves the flexibility of your code in the face of uncertain errors.

## Pro Tip

As you begin to use Python packages outside of its built-in functionality, you will notice that some of them have their own custom error types and exceptions. Google will be your best friend as you learn Python and additional packages.

`What does the ____ error in Python mean?`

## Raise

Exceptions let us circumvent errors in python. `Raise` lets us throw errors that wouldn't normally occur! So in a way, they're kind of opposites.

The `raise` keyword can be used to alert a user of a specific error type. As an example, we can write a function that will raise an error if `4` is entered but will otherwise print the number.

### Try it out in Repl.it!

```python
def no_four(number):
    if number == 4:
        raise ValueError('No fours allowed!!')
    else:
        print('Number:', number)
```

When the error is raised, the string entered as an argument to `ValueError` is the message that’s returned to the user:

```python
no_four(4)

# ValueError: No fours allowed!!

no_four(2)

# Number: 2
```

## Review

This introduction to error handling should help you debug your own code and understand Python’s error messages, and help you write your own exception logic.

[Errors & Exceptions](https://docs.python.org/3/tutorial/errors.html)

We’ve only scratched the surface when it comes to the types of **exceptions** that can occur; there are many built-in types for a wide range of scenarios and problems.

For a full list of the built-in exception types and their explanations, [consult this page in the official Python 3 documentation.](https://docs.python.org/3/library/exceptions.html)

<br>

<hr>

<a href="./assets/error-handling.pdf" target="_blank" download="error-handling.pdf" class="ant-btn" data-trackable="true" data-track-category="study guide" data-track-section="lesson page" data-track-action="download study guide"><span role="img" class="anticon"><svg viewBox="0 0 16 16" width="1em" height="1em" fill="currentColor" aria-hidden="true" focusable="false" class=""><g class="download_svg__nc-icon-wrapper"><path d="M8 12c.3 0 .5-.1.7-.3L14.4 6 13 4.6l-4 4V0H7v8.6l-4-4L1.6 6l5.7 5.7c.2.2.4.3.7.3z"></path><path data-color="color-2" d="M1 14h14v2H1z"></path></g></svg></span><span> Download Study Guide</span></a>

<br>
