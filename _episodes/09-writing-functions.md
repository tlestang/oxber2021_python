---
title: "Writing Functions"
teaching: 6
exercises: 4
questions:
- "How can I create my own functions?"
objectives:
- "Explain and identify the difference between function definition and function call."
- "Write a function that takes a small, fixed number of arguments and produces a single result."
keypoints:
- "Break programs down into functions to make them easier to understand."
- "Define a function using `def` with a name, parameters, and a block of code."
- "Defining a function does not run it."
- "Arguments in call are matched to parameters in definition."
- "Functions may return a result to their caller using `return`."
---

## Define a function using `def` with a name, parameters, and a block of code.

*   Begin the definition of a new function with `def`.
*   Followed by the name of the function.
    *   Must obey the same rules as variable names.
*   Then *parameters* in parentheses.
    *   Empty parentheses if the function doesn't take any inputs.
    *   We will discuss this in detail in a moment.
*   Then a colon.
*   Then an indented block of code.

~~~
def print_greeting():
    print('Hello!')
~~~
{: .language-python}

## Defining a function does not run it.

*   Defining a function does not run it.
    *   Like assigning a value to a variable.
*   Must call the function to execute the code it contains.

~~~
print_greeting()
~~~
{: .language-python}
~~~
Hello!
~~~
{: .output}

## Arguments in call are matched to parameters in definition.

*   Functions are most useful when they can operate on different data.
*   Specify *parameters* when defining a function.
    *   These become variables when the function is executed.
    *   Are assigned the arguments in the call (i.e., the values passed to the function).
    *   If you don't name the arguments when using them in the call, the arguments will be matched to
parameters in the order the parameters are defined in the function.

~~~
def print_date(year, month, day):
    joined = str(year) + '/' + str(month) + '/' + str(day)
    print(joined)

print_date(1871, 3, 19)
~~~
{: .language-python}
~~~
1871/3/19
~~~
{: .output}

Or, we can name the arguments when we call the function, which allows us to
specify them in any order:
~~~
print_date(month=3, day=19, year=1871)
~~~
{: .language-python}
~~~
1871/3/19
~~~
{: .output}

*   Via [Twitter](https://twitter.com/minisciencegirl/status/693486088963272705):
    `()` contains the ingredients for the function
    while the body contains the recipe.

## Functions may return a result to their caller using `return`.

*   Use `return ...` to give a value back to the caller.
*   May occur anywhere in the function.
*   But functions are easier to understand if `return` occurs:
    *   At the start to handle special cases.
    *   At the very end, with a final result.

~~~
def average(values):
    if len(values) == 0:
        return None
    return sum(values) / len(values)
~~~
{: .language-python}

~~~
a = average([1, 3, 4])
print('average of actual values:', a)
~~~
{: .language-python}
~~~
average of actual values: 2.6666666666666665
~~~
{: .output}

> ## Order of Operations
>
> 1. What's wrong in this example?
>
>     ~~~
>     result = print_time(11, 37, 59)
>
>     def print_time(hour, minute, second):
>        time_string = str(hour) + ':' + str(minute) + ':' + str(second)
>        print(time_string)
>     ~~~
>     {: .language-python}
> 
> 2. After fixing the problem above, explain why running this example code:
>
>     ~~~
>     result = print_time(11, 37, 59)
>     print('result of call is:', result)
>     ~~~
>     {: .language-python}
>
>     gives this output:
>
>     ~~~
>     11:37:59
>     result of call is: None
>     ~~~
>     {: .output}
>
> 3. Why is the result of the call `None`?
>
> > ## Solution
> > 
> > 1. The problem with the example is that the function `print_time()` is defined *after* the call to the function is made. Python
> > doesn't know how to resolve the name `print_time` since it hasn't been defined yet and will raise a `NameError` e.g.,
> > `NameError: name 'print_time' is not defined`
> >
> > 2. The first line of output `11:37:59` is printed by the first line of code, `result = print_time(11, 37, 59)` that binds the value 
> > returned by invoking `print_time` to the variable `result`. The second line is from the second print call to print the contents 
> > of the `result` variable.
> >
> > 3. `print_time()` does not explicitly `return` a value, so it automatically returns `None`.
> >
> {: .solution}
{: .challenge}

> ## Encapsulation of an If/Print Block
>
> The code below will run on a label-printer for chicken eggs.  A digital scale will report a chicken egg mass (in grams) 
> to the computer and then the computer will print a label.  
>
> Please re-write the code so that the if-block is folded into a function.
>
> ~~~
> import random
> for i in range(10):
>
>     # simulating the mass of a chicken egg
>     # the (random) mass will be 70 +/- 20 grams
>     mass = 70 + 20.0 * (2.0 * random.random() - 1.0)
>
>     print(mass)
>    
>     # egg sizing machinery prints a label
>     if mass >= 85:
>        print("jumbo")
>     elif mass >= 70:
>        print("large")
>     elif mass < 70 and mass >= 55:
>        print("medium")
>     else:
>        print("small")
> ~~~
> {: .language-python}
>
>
> The simplified program follows.  What function definition will make it functional?
>
> ~~~
> # revised version
> import random
> for i in range(10):
>
>     # simulating the mass of a chicken egg
>     # the (random) mass will be 70 +/- 20 grams
>     mass = 70 + 20.0 * (2.0 * random.random() - 1.0)
>
>     print(mass, print_egg_label(mass))    
>
> ~~~
> {: .language-python}
>
>
> 1. Create a function definition for `print_egg_label()` that will work with the revised program above.  Note, the function's return value will be significant. Sample output might be `71.23 large`.
> 2. A dirty egg might have a mass of more than 90 grams, and a spoiled or broken egg will probably have a mass that's less than 50 grams.  Modify your `print_egg_label()` function to account for these error conditions. Sample output could be `25 too light, probably spoiled`.
>
> > ## Solution
> >
> > ~~~
> > def print_egg_label(mass):
> >     #egg sizing machinery prints a label
> >     if mass >= 90:
> >         return "warning: egg might be dirty"
> >     elif mass >= 85:
> >         return "jumbo"
> >     elif mass >= 70:
> >         return "large"
> >     elif mass < 70 and mass >= 55:
> >         return "medium"
> >     elif mass < 50:
> >         return "too light, probably spoiled"
> >     else:
> >         return "small"
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

## Break programs down into functions to make them easier to understand.

*   Human beings can only keep a few items in working memory at a time.
*   Understand larger/more complicated ideas by understanding and combining pieces.
    *   Components in a machine.
    *   Lemmas when proving theorems.
*   Functions serve the same purpose in programs.
    *   *Encapsulate* complexity so that we can treat it as a single "thing".
*   Also enables *re-use*.
    *   Write one time, use many times.
