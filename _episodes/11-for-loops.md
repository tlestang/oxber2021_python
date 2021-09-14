---
title: "For Loops"
teaching: 10
exercises: 15
questions:
- "How can I make a program do many things?"
objectives:
- "Explain what for loops are normally used for."
- "Trace the execution of a simple (unnested) loop and correctly state the values of variables in each iteration."
- "Write for loops that use the Accumulator pattern to aggregate values."
keypoints:
- "A *for loop* executes commands once for each value in a collection."
- "A `for` loop is made up of a collection, a loop variable, and a body."
- "The first line of the `for` loop must end with a colon, and the body must be indented."
- "Indentation is always meaningful in Python."
- "Loop variables can be called anything (but it is strongly advised to have a meaningful name to the looping variable)."
- "The body of a loop can contain many statements."
- "Use `range` to iterate over a sequence of numbers."
- "The Accumulator pattern turns many values into one."
---
## A *for loop* executes commands once for each value in a collection.

*   Doing calculations on the values in a list one by one
    is as painful as working with `pressure_001`, `pressure_002`, etc.
*   A *for loop* tells Python to execute some statements once for each value in a list,
    a character string,
    or some other collection.
*   "for each thing in this group, do these operations"

~~~
for number in [2, 3, 5]:
    print(number)
~~~
{: .language-python}

*   This `for` loop is equivalent to:

~~~
print(2)
print(3)
print(5)
~~~
{: .language-python}

*   And the `for` loop's output is:

~~~
2
3
5
~~~
{: .output}

## A `for` loop is made up of a collection, a loop variable, and a body.

~~~
for number in [2, 3, 5]:
    print(number)
~~~
{: .language-python}

*   The collection, `[2, 3, 5]`, is what the loop is being run on.
*   The body, `print(number)`, specifies what to do for each value in the collection.
*   The loop variable, `number`, is what changes for each *iteration* of the loop.
    *   The "current thing".
* The first line of the `for` loop must end with a colon, and the body must be indented.
    *   Any consistent indentation is legal, but almost everyone uses four spaces.

## Loop variables can be called anything.

*   As with all variables, loop variables are:
    *   Created on demand.
    *   Meaningless: their names can be anything at all.

~~~
for kitten in [2, 3, 5]:
    print(kitten)
~~~
{: .language-python}

## The body of a loop can contain many statements.

*   But no loop should be more than a few lines long.
*   Hard for human beings to keep larger chunks of code in mind.

~~~
primes = [2, 3, 5]
for p in primes:
    squared = p ** 2
    cubed = p ** 3
    print(p, squared, cubed)
~~~
{: .language-python}
~~~
2 4 8
3 9 27
5 25 125
~~~
{: .output}

## Use `range` to iterate over a sequence of numbers.

*   The built-in function [`range`](https://docs.python.org/3/library/stdtypes.html#range) produces a sequence of numbers.
    *   *Not* a list: the numbers are produced on demand
        to make looping over large ranges more efficient.
*   `range(N)` is the numbers 0..N-1
    *   Exactly the legal indices of a list or character string of length N

~~~
print('a range is not a list: range(0, 3)')
for number in range(0, 3):
    print(number)
~~~
{: .language-python}
~~~
a range is not a list: range(0, 3)
0
1
2
~~~
{: .output}

> ## Practice Accumulating (demoed)
>
> Fill in the blanks in each of the programs below
> to produce the indicated result.
>
> ~~~
> # Total length of the strings in the list: ["red", "green", "blue"] => 12
> total = 0
> for word in ["red", "green", "blue"]:
>     ____ = ____ + len(word)
> print(total)
> ~~~
> {: .language-python}
> > ## Solution
> > ~~~
> > total = 0
> > for word in ["red", "green", "blue"]:
> >     total = total + len(word)
> > print(total)
> > ~~~
> > {: .language-python}
> {: .solution}

> ## Cumulative Sum
>
> Reorder and properly indent the lines of code below
> so that they print a list with the cumulative sum of data.
> The result should be `[1, 3, 5, 10]`.
>
> ~~~
> cumulative.append(total)
> for number in data:
> cumulative = []
> total += number
> total = 0
> print(cumulative)
> data = [1,2,2,5]
> ~~~
> {: .language-python}
> > ## Solution
> > ~~~
> > total = 0
> > data = [1,2,2,5]
> > cumulative = []
> > for number in data:
> >     total += number
> >     cumulative.append(total)
> > print(cumulative)
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

> ## Identifying Variable Name Errors
>
> 1. Read the code below and try to identify what the errors are
>    *without* running it.
> 2. Run the code and read the error message.
>    What type of `NameError` do you think this is?
>    Is it a string with no quotes, a misspelled variable, or a
>    variable that should have been defined but was not?
> 3. Fix the error.
> 4. Repeat steps 2 and 3, until you have fixed all the errors.
>
> ~~~
> for number in range(10):
>     # use a if the number is a multiple of 3, otherwise use b
>     if (Number % 3) == 0:
>         message = message + a
>     else:
>         message = message + "b"
> print(message)
> ~~~
> {: .language-python}
> > ## Solution
> > - Python variable names are case sensitive: `number` and `Number` refer to different variables.
> > - The variable `message` needs to be initialized as an empty string.
> > - We want to add the string `"a"` to `message`, not the undefined variable `a`.
> >
> > ~~~
> > message = ""
> > for number in range(10):
> >     # use a if the number is a multiple of 3, otherwise use b
> >     if (number % 3) == 0:
> >         message = message + "a"
> >     else:
> >         message = message + "b"
> > print(message)
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

