---
title: "Libraries"
teaching: 5
exercises: 0
questions:
- "How can I use software that other people have written?"
- "How can I find out what that software does?"
objectives:
- "Explain what software libraries are and why programmers create and use them."
- "Write programs that import and use modules from Python's standard library."
- "Find and read documentation for the standard library interactively (in the interpreter) and online."
keypoints:
- "Most of the power of a programming language is in its libraries."
- "A program must import a library module in order to use it."
- "Use `help` to learn about the contents of a library module."
- "Import specific items from a library to shorten programs."
- "Create an alias for a library when importing it to shorten programs."
---
## Most of the power of a programming language is in its libraries.

*   A *library* is a collection of files (called *modules*) that contains
    functions for use by other programs.
    *   May also contain data values (e.g., numerical constants) and other things.
    *   Library's contents are supposed to be related, but there's no way to enforce that.
*   The Python [standard library][stdlib] is an extensive suite of modules that comes
    with Python itself.
*   Many additional libraries are available from [PyPI][pypi] (the Python Package Index).
*   We will see later how to write new libraries.

> ## Libraries and modules
>
> A library is a collection of modules, but the terms are often used
> interchangeably, especially since many libraries only consist of a single
> module, so don't worry if you mix them.
{: .callout}


## A program must import a library module before using it.

*   Use `import` to load a library module into a program's memory.
*   Then refer to things from the module as `module_name.thing_name`.
    *   Python uses `.` to mean "part of".
*   Using `math`, one of the modules in the standard library:

~~~
import math

print('pi is', math.pi)
print('cos(pi) is', math.cos(math.pi))
~~~
{: .language-python}
~~~
pi is 3.141592653589793
cos(pi) is -1.0
~~~
{: .output}

*   Have to refer to each item with the module's name.
    *   `math.cos(pi)` won't work: the reference to `pi`
        doesn't somehow "inherit" the function's reference to `math`.

## Use `help` to learn about the contents of a library module.

*   Works just like help for a function.

~~~
help(math)
~~~
{: .language-python}
~~~
Help on module math:

NAME
    math

MODULE REFERENCE
    http://docs.python.org/3/library/math

    The following documentation is automatically generated from the Python
    source files.  It may be incomplete, incorrect or include features that
    are considered implementation detail and may vary between Python
    implementations.  When in doubt, consult the module reference at the
    location listed above.

DESCRIPTION
    This module is always available.  It provides access to the
    mathematical functions defined by the C standard.

FUNCTIONS
    acos(x, /)
        Return the arc cosine (measured in radians) of x.
⋮ ⋮ ⋮
~~~
{: .output}

## Import specific items from a library module to shorten programs.

*   Use `from ... import ...` to load only specific items from a library module.
*   Then refer to them directly without library name as prefix.

~~~
from math import cos, pi

print('cos(pi) is', cos(pi))
~~~
{: .language-python}
~~~
cos(pi) is -1.0
~~~
{: .output}

## Create an alias for a library module when importing it to shorten programs.

*   Use `import ... as ...` to give a library a short *alias* while importing it.
*   Then refer to items in the library using that shortened name.

~~~
import math as m

print('cos(pi) is', m.cos(m.pi))
~~~
{: .language-python}
~~~
cos(pi) is -1.0
~~~
{: .output}

*   Commonly used for libraries that are frequently used or have long names.
    *   E.g., the `matplotlib` plotting library is often aliased as `mpl`.
*   But can make programs harder to understand,
    since readers must learn your program's aliases.

> ## Locating the Right Module (demonstrated)
>
> You want to select a random character from a string:
>
> ~~~
> bases = 'ACTTGCTTGAC'
> ~~~
> {: .language-python}
>
> 1. Which [standard library][stdlib] module could help you?
> 2. Which function would you select from that module? Are there alternatives?
> 3. Try to write a program that uses the function.
>
> > ## Solution
> >
> > The [random module][randommod] seems like it could help you.
> >
> > The string has 11 characters, each having a positional index from 0 to 10.
> > You could use either `random.randrange` or `random.randint` functions
> > to get a random integer between 0 and
> > 10, and then pick out the character at that position:
> >
> > ~~~
> > from random import randrange
> >
> > random_index = randrange(len(bases))
> > print(bases[random_index])
> > ~~~
> > {: .language-python}
> >
> > or more compactly:
> >
> > ~~~
> > from random import randrange
> >
> > print(bases[randrange(len(bases))])
> > ~~~
> > {: .language-python}
> >
> > Perhaps you found the `random.sample` function? It allows for slightly
> > less typing:
> >
> > ~~~
> > from random import sample
> >
> > print(sample(bases, 1)[0])
> > ~~~
> > {: .language-python}
> >
> > Note that this function returns a list of values. We will learn about
> > lists in [episode 11]({{ page.root }}/11-lists/).
> >
> > There's also other functions you could use, but with more convoluted
> > code as a result.
> {: .solution}
{: .challenge}


> ## When Is Help Available?
>
> When a colleague of yours types `help(math)`,
> Python reports an error:
>
> ~~~
> NameError: name 'math' is not defined
> ~~~
> {: .error}
>
> What has your colleague forgotten to do?
>
> > ## Solution
> >
> > Importing the math module (`import math`)
> {: .solution}
{: .challenge}

[pypi]: https://pypi.python.org/pypi/
[stdlib]: https://docs.python.org/3/library/
[randommod]: https://docs.python.org/3/library/random.html
[pep8-imports]: https://pep8.org/#imports
