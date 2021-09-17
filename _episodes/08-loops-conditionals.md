---
title: "Loops and conditional statements"
teaching: 7
exercises: 3
questions:
- "How can I make a program repeat instructions?"
- "How can programs do different things for different data?"
objectives:
- "Explain what for loops are normally used for."
- "Trace the execution of a simple (unnested) loop and correctly state the values of variables in each iteration."
- "Write simple for loops, e.g. the aggregate values."
- "Correctly write programs that use if and else statements and simple logial expressions."
keypoints:
- "A *for loop* executes commands once for each value in a collection."
- "A `for` loop is made up of a collection, a loop variable, and a body."
- "The first line of the `for` loop must end with a colon, and the body must be indented."
- "Indentation is always meaningful in Python."
- "Loop variables can be called anything (but it is strongly advised to have a meaningful name to the looping variable)."
- "The body of a loop can contain many statements."
- "Use `range` to iterate over a sequence of numbers."
- "Use `if` statements to control whether or not a block of code is executed."
- "Use `else` to execute a block of code when an `if` condition is *not* true."
- "Use `elif` to specify additional tests."
- "Conditions are tested once, in order."
---

## Python lists

We create a list by putting values inside square brackets and
separating the values with commas:

~~~
odds = [1, 3, 5, 7]
print('odds are:', odds)
~~~
{: .language-python}

~~~
odds are: [1, 3, 5, 7]
~~~
{: .output}

We can access elements of a list using indices -- numbered positions of elements in the list.
These positions are numbered starting at 0, so the first element has an index of 0.

~~~
print('first element:', odds[0])
print('last element:', odds[3])
print('"-1" element:', odds[-1])
~~~
{: .language-python}

~~~
first element: 1
last element: 7
"-1" element: 7
~~~
{: .output}

Yes, we can use negative numbers as indices in Python. When we do so, the index `-1` gives us the
last element in the list, `-2` the second to last, and so on.
Because of this, `odds[3]` and `odds[-1]` point to the same element here.

There is one important difference between lists and strings:
we can change the values in a list,
but we cannot change individual characters in a string.
For example:

~~~
names = ['Curie', 'Darwing', 'Turing']  # typo in Darwin's name
print('names is originally:', names)
names[1] = 'Darwin'  # correct the name
print('final value of names:', names)
~~~
{: .language-python}

~~~
names is originally: ['Curie', 'Darwing', 'Turing']
final value of names: ['Curie', 'Darwin', 'Turing']
~~~
{: .output}

works, but:

~~~
name = 'Darwin'
name[0] = 'd'
~~~
{: .language-python}

~~~
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-8-220df48aeb2e> in <module>()
      1 name = 'Darwin'
----> 2 name[0] = 'd'

TypeError: 'str' object does not support item assignment
~~~
{: .error}

does not.

## Nested lists

~~~
fields_and_names = [['Physics', Natural history', 'Computer Science'], ['Curie', 'Darwin', 'Turing']]  
~~~
{: .language-python}

## Append to a list

~~~
l = [1, 2, 3]
l.append("a string")
print(l)
~~~
{: .language-python}

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

## Use `if` statements to control whether or not a block of code is executed.

*   An `if` statement (more properly called a *conditional* statement)
    controls whether some block of code is executed or not.
*   Structure is similar to a `for` statement:
    *   First line opens with `if` and ends with a colon
    *   Body containing one or more statements is indented (usually by 4 spaces)

~~~
mass = 3.54
if mass > 3.0:
    print(mass, 'is large')

mass = 2.07
if mass > 3.0:
    print (mass, 'is large')
~~~
{: .language-python}
~~~
3.54 is large
~~~
{: .output}

## Conditionals are often used inside loops.

*   Not much point using a conditional when we know the value (as above).
*   But useful when we have a collection to process.

~~~
masses = [3.54, 2.07, 9.22, 1.86, 1.71]
for m in masses:
    if m > 3.0:
        print(m, 'is large')
~~~
{: .language-python}
~~~
3.54 is large
9.22 is large
~~~
{: .output}

## Use `else` to execute a block of code when an `if` condition is *not* true.

*   `else` can be used following an `if`.
*   Allows us to specify an alternative to execute when the `if` *branch* isn't taken.

~~~
masses = [3.54, 2.07, 9.22, 1.86, 1.71]
for m in masses:
    if m > 3.0:
        print(m, 'is large')
    else:
        print(m, 'is small')
~~~
{: .language-python}
~~~
3.54 is large
2.07 is small
9.22 is large
1.86 is small
1.71 is small
~~~
{: .output}

## Use `elif` to specify additional tests.

*   May want to provide several alternative choices, each with its own test.
*   Use `elif` (short for "else if") and a condition to specify these.
*   Always associated with an `if`.
*   Must come before the `else` (which is the "catch all").

~~~
masses = [3.54, 2.07, 9.22, 1.86, 1.71]
for m in masses:
    if m > 9.0:
        print(m, 'is HUGE')
    elif m > 3.0:
        print(m, 'is large')
    else:
        print(m, 'is small')
~~~
{: .language-python}
~~~
3.54 is large
2.07 is small
9.22 is HUGE
1.86 is small
1.71 is small
~~~
{: .output}

## Conditions are tested once, in order.

*   Python steps through the branches of the conditional in order, testing each in turn.
*   So ordering matters.

~~~
grade = 85
if grade >= 70:
    print('grade is C')
elif grade >= 80:
    print('grade is B')
elif grade >= 90:
    print('grade is A')
~~~
{: .language-python}
~~~
grade is C
~~~
{: .output}

*   Does *not* automatically go back and re-evaluate if values change.

~~~
velocity = 10.0
if velocity > 20.0:
    print('moving too fast')
else:
    print('adjusting velocity')
    velocity = 50.0
~~~
{: .language-python}
~~~
adjusting velocity
~~~
{: .output}

*   Often use conditionals in a loop to "evolve" the values of variables.

~~~
velocity = 10.0
for i in range(5): # execute the loop 5 times
    print(i, ':', velocity)
    if velocity > 20.0:
        print('moving too fast')
        velocity = velocity - 5.0
    else:
        print('moving too slow')
        velocity = velocity + 10.0
print('final velocity:', velocity)
~~~
{: .language-python}
~~~
0 : 10.0
moving too slow
1 : 20.0
moving too slow
2 : 30.0
moving too fast
3 : 25.0
moving too fast
4 : 20.0
moving too slow
final velocity: 30.0
~~~
{: .output}

> ## Compound Relations Using `and`, `or`, and Parentheses
>
> Often, you want some combination of things to be true.  You can combine
> relations within a conditional using `and` and `or`.  Continuing the example
> above, suppose you have
>
> ~~~
> mass     = [ 3.54,  2.07,  9.22,  1.86,  1.71]
> velocity = [10.00, 20.00, 30.00, 25.00, 20.00]
>
> i = 0
> for i in range(5):
>     if mass[i] > 5 and velocity[i] > 20:
>         print("Fast heavy object.  Duck!")
>     elif mass[i] > 2 and mass[i] <= 5 and velocity[i] <= 20:
>         print("Normal traffic")
>     elif mass[i] <= 2 and velocity[i] <= 20:
>         print("Slow light object.  Ignore it")
>     else:
>         print("Whoa!  Something is up with the data.  Check it")
> ~~~
> {: .language-python}
>
> Just like with arithmetic, you can and should use parentheses whenever there
> is possible ambiguity.  A good general rule is to *always* use parentheses
> when mixing `and` and `or` in the same condition.  That is, instead of:
>
> ~~~
> if mass[i] <= 2 or mass[i] >= 5 and velocity[i] > 20:
> ~~~
> {: .language-python}
>
> write one of these:
>
> ~~~
> if (mass[i] <= 2 or mass[i] >= 5) and velocity[i] > 20:
> if mass[i] <= 2 or (mass[i] >= 5 and velocity[i] > 20):
> ~~~
> {: .language-python}
>
> so it is perfectly clear to a reader (and to Python) what you really mean.
{: .callout}

> ## Trimming Values
>
> Fill in the blanks so that this program creates a new list
> containing zeroes where the original list's values were negative
> and ones where the original list's values were positive.
>
> ~~~
> original = [-1.5, 0.2, 0.4, 0.0, -1.3, 0.4]
> result = ____
> for value in original:
>     if ____:
>         result.append(0)
>     else:
>         ____
> print(result)
> ~~~
> {: .language-python}
>
> ~~~
> [0, 1, 1, 1, 0, 1]
> ~~~
> {: .output}
> > ## Solution
> >
> > ~~~
> > original = [-1.5, 0.2, 0.4, 0.0, -1.3, 0.4]
> > result = []
> > for value in original:
> >     if value < 0.0:
> >         result.append(0)
> >     else:
> >         result.append(1)
> > print(result)
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}


