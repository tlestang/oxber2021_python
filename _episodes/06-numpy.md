---
title: Analyzing Patient Data
teaching: 10
exercises: 0
questions:
- "How can I process tabular data files in Python?"
- "How can I visualize tabular data in Python?"
- "How can I group several plots together?"
objectives:
- "Explain what a library is and what libraries are used for."
- "Import a Python library and use the functions it contains."
- "Read tabular data from a file into a program."
- "Select individual values and subsections from data."
- "Perform operations on arrays of data."
- "Plot simple graphs from data."
- "Group several graphs in a single figure."
keypoints:
- "Import a library into a program using `import libraryname`."
- "Use the `numpy` library to work with arrays in Python."
- "The expression `array.shape` gives the shape of an array."
- "Use `array[x, y]` to select a single element from a 2D array."
- "Array indices start at 0, not 1."
- "Use `low:high` to specify a `slice` that includes the indices from `low` to `high-1`."
- "Use `numpy.mean(array)`, `numpy.max(array)`, and `numpy.min(array)` to calculate simple statistics."
- "Use the `pyplot` module from the `matplotlib` library for creating simple visualizations."
---

Words are useful, but what's more useful are the sentences and stories we build with them.
Similarly, while a lot of powerful, general tools are built into Python,
specialized tools built up from these basic units live in
[libraries]({{ page.root }}/reference.html#library)
that can be called upon when needed.

## Loading data into Python

To begin processing inflammation data, we need to load it into Python.
We can do that using a library called
[NumPy](http://docs.scipy.org/doc/numpy/ "NumPy Documentation"), which stands for Numerical Python.
In general, you should use this library when you want to do fancy things with lots of numbers,
especially if you have matrices or arrays. To tell Python that we'd like to start using NumPy,
we need to [import]({{ page.root }}/reference.html#import) it:

~~~
import numpy
~~~
{: .language-python}

Importing a library is like getting a piece of lab equipment out of a storage locker and setting it
up on the bench. Libraries provide additional functionality to the basic Python package, much like
a new piece of equipment adds functionality to a lab space. Just like in the lab, importing too
many libraries can sometimes complicate and slow down your programs - so we only import what we
need for each program.

Once we've imported the library, we can ask the library to read our data file for us:

~~~
numpy.loadtxt(fname='inflammation-01.csv', delimiter=',')
~~~
{: .language-python}

~~~
array([[ 0.,  0.,  1., ...,  3.,  0.,  0.],
       [ 0.,  1.,  2., ...,  1.,  0.,  1.],
       [ 0.,  1.,  1., ...,  2.,  1.,  1.],
       ...,
       [ 0.,  1.,  1., ...,  1.,  1.,  1.],
       [ 0.,  0.,  0., ...,  0.,  2.,  0.],
       [ 0.,  0.,  1., ...,  1.,  1.,  0.]])
~~~
{: .output}

The expression `numpy.loadtxt(...)` is a
[function call]({{ page.root }}/reference.html#function-call)
that asks Python to run the [function]({{ page.root }}/reference.html#function) `loadtxt` which
belongs to the `numpy` library.
This [dotted notation]({{ page.root }}/reference.html#dotted-notation)
is used everywhere in Python: the thing that appears before the dot contains the thing that
appears after.

As an example, John Smith is the John that belongs to the Smith family.
We could use the dot notation to write his name `smith.john`,
just as `loadtxt` is a function that belongs to the `numpy` library.

`numpy.loadtxt` has two [parameters]({{ page.root }}/reference.html#parameter): the name of the file
we want to read and the [delimiter]({{ page.root }}/reference.html#delimiter) that separates values
on a line. These both need to be character strings
(or [strings]({{ page.root }}/reference.html#string) for short), so we put them in quotes.

Since we haven't told it to do anything else with the function's output,
the [notebook]({{ page.root }}/reference.html#notebook) displays it.
In this case,
that output is the data we just loaded.
By default,
only a few rows and columns are shown
(with `...` to omit elements when displaying big arrays).
Note that, to save space when displaying NumPy arrays, Python does not show us trailing zeros,
so `1.0` becomes `1.`.

Our call to `numpy.loadtxt` read our file
but didn't save the data in memory.
To do that,
we need to assign the array to a variable. In a similar manner to how we assign a single
value to a variable, we can also assign an array of values to a variable using the same syntax.
Let's re-run `numpy.loadtxt` and save the returned data:

~~~
data = numpy.loadtxt(fname='inflammation-01.csv', delimiter=',')
~~~
{: .language-python}

This statement doesn't produce any output because we've assigned the output to the variable `data`.
If we want to check that the data have been loaded,
we can print the variable's value:

~~~
print(data)
~~~
{: .language-python}

~~~
[[ 0.  0.  1. ...,  3.  0.  0.]
 [ 0.  1.  2. ...,  1.  0.  1.]
 [ 0.  1.  1. ...,  2.  1.  1.]
 ...,
 [ 0.  1.  1. ...,  1.  1.  1.]
 [ 0.  0.  0. ...,  0.  2.  0.]
 [ 0.  0.  1. ...,  1.  1.  0.]]
~~~
{: .output}

Now that the data are in memory,
we can manipulate them.
First,
let's ask what [type]({{ page.root }}/reference.html#type) of thing `data` refers to:

~~~
print(type(data))
~~~
{: .language-python}

~~~
<class 'numpy.ndarray'>
~~~
{: .output}

The output tells us that `data` currently refers to
an N-dimensional array, the functionality for which is provided by the NumPy library.
These data correspond to arthritis patients' inflammation.
The rows are the individual patients, and the columns
are their daily inflammation measurements.

With the following command, we can see the array's [shape]({{ page.root }}/reference.html#shape):

~~~
print(data.shape)
~~~
{: .language-python}

~~~
(60, 40)
~~~
{: .output}

The output tells us that the `data` array variable contains 60 rows and 40 columns. When we
created the variable `data` to store our arthritis data, we did not only create the array; we also
created information about the array, called [members]({{ page.root }}/reference.html#member) or
attributes. This extra information describes `data` in the same way an adjective describes a noun.
`data.shape` is an attribute of `data` which describes the dimensions of `data`. We use the same
dotted notation for the attributes of variables that we use for the functions in libraries because
they have the same part-and-whole relationship.

If we want to get a single number from the array, we must provide an
[index]({{ page.root }}/reference.html#index) in square brackets after the variable name, just as we
do in math when referring to an element of a matrix.  Our inflammation data has two dimensions, so
we will need to use two indices to refer to one specific value:

~~~
print('first value in data:', data[0, 0])
~~~
{: .language-python}

~~~
first value in data: 0.0
~~~
{: .output}

~~~
print('middle value in data:', data[30, 20])
~~~
{: .language-python}

~~~
middle value in data: 13.0
~~~
{: .output}

The expression `data[30, 20]` accesses the element at row 30, column 20. While this expression may
not surprise you,
 `data[0, 0]` might.
Programming languages like Fortran, MATLAB and R start counting at 1
because that's what human beings have done for thousands of years.
Languages in the C family (including C++, Java, Perl, and Python) count from 0
because it represents an offset from the first value in the array (the second
value is offset by one index from the first value). This is closer to the way
that computers represent arrays (if you are interested in the historical
reasons behind counting indices from zero, you can read
[Mike Hoye's blog post](http://exple.tive.org/blarg/2013/10/22/citation-needed/)).
As a result,
if we have an M×N array in Python,
its indices go from 0 to M-1 on the first axis
and 0 to N-1 on the second.
It takes a bit of getting used to,
but one way to remember the rule is that
the index is how many steps we have to take from the start to get the item we want.

!["data" is a 3 by 3 numpy array containing row 0: ['A', 'B', 'C'], row 1: ['D', 'E', 'F'], and
row 2: ['G', 'H', 'I']. Starting in the upper left hand corner, data[0, 0] = 'A', data[0, 1] = 'B',
data[0, 2] = 'C', data[1, 0] = 'D', data[1, 1] = 'E', data[1, 2] = 'F', data[2, 0] = 'G',
data[2, 1] = 'H', and data[2, 2] = 'I',
in the bottom right hand corner.](../fig/python-zero-index.svg)

> ## In the Corner
>
> What may also surprise you is that when Python displays an array,
> it shows the element with index `[0, 0]` in the upper left corner
> rather than the lower left.
> This is consistent with the way mathematicians draw matrices
> but different from the Cartesian coordinates.
> The indices are (row, column) instead of (column, row) for the same reason,
> which can be confusing when plotting data.
{: .callout}

## Slicing data
An index like `[30, 20]` selects a single element of an array,
but we can select whole sections as well.
For example,
we can select the first ten days (columns) of values
for the first four patients (rows) like this:

~~~
print(data[0:4, 0:10])
~~~
{: .language-python}

~~~
[[ 0.  0.  1.  3.  1.  2.  4.  7.  8.  3.]
 [ 0.  1.  2.  1.  2.  1.  3.  2.  2.  6.]
 [ 0.  1.  1.  3.  3.  2.  6.  2.  5.  9.]
 [ 0.  0.  2.  0.  4.  2.  2.  1.  6.  7.]]
~~~
{: .output}

The [slice]({{ page.root }}/reference.html#slice) `0:4` means, "Start at index 0 and go up to,
but not including, index 4". Again, the up-to-but-not-including takes a bit of getting used to,
but the rule is that the difference between the upper and lower bounds is the number of values in
the slice.

We don't have to start slices at 0:

~~~
print(data[5:10, 0:10])
~~~
{: .language-python}

~~~
[[ 0.  0.  1.  2.  2.  4.  2.  1.  6.  4.]
 [ 0.  0.  2.  2.  4.  2.  2.  5.  5.  8.]
 [ 0.  0.  1.  2.  3.  1.  2.  3.  5.  3.]
 [ 0.  0.  0.  3.  1.  5.  6.  5.  5.  8.]
 [ 0.  1.  1.  2.  1.  3.  5.  3.  5.  8.]]
~~~
{: .output}

We also don't have to include the upper and lower bound on the slice.  If we don't include the lower
bound, Python uses 0 by default; if we don't include the upper, the slice runs to the end of the
axis, and if we don't include either (i.e., if we use ':' on its own), the slice includes
everything:

~~~
small = data[:3, 36:]
print('small is:')
print(small)
~~~
{: .language-python}
The above example selects rows 0 through 2 and columns 36 through to the end of the array.

~~~
small is:
[[ 2.  3.  0.  0.]
 [ 1.  1.  0.  1.]
 [ 2.  2.  1.  1.]]
~~~
{: .output}

## Analyzing data

NumPy has several useful functions that take an array as input to perform operations on its values.
If we want to find the average inflammation for all patients on
all days, for example, we can ask NumPy to compute `data`'s mean value:

~~~
print(numpy.mean(data))
~~~
{: .language-python}

~~~
6.14875
~~~
{: .output}

`mean` is a [function]({{ page.root }}/reference.html#function) that takes
an array as an [argument]({{ page.root }}/reference.html#argument).

> ## Not All Functions Have Input
>
> Generally, a function uses inputs to produce outputs.
> However, some functions produce outputs without
> needing any input. For example, checking the current time
> doesn't require any input.
>
> ~~~
> import time
> print(time.ctime())
> ~~~
> {: .language-python}
>
> ~~~
> Sat Mar 26 13:07:33 2016
> ~~~
> {: .output}
>
> For functions that don't take in any arguments,
> we still need parentheses (`()`)
> to tell Python to go and do something for us.
{: .callout}

Let's use three other NumPy functions to get some descriptive values about the dataset.
We'll also use multiple assignment,
a convenient Python feature that will enable us to do this all in one line.

~~~
maxval, minval, stdval = numpy.max(data), numpy.min(data), numpy.std(data)

print('maximum inflammation:', maxval)
print('minimum inflammation:', minval)
print('standard deviation:', stdval)
~~~
{: .language-python}

Here we've assigned the return value from `numpy.max(data)` to the variable `maxval`, the value
from `numpy.min(data)` to `minval`, and so on.

~~~
maximum inflammation: 20.0
minimum inflammation: 0.0
standard deviation: 4.61383319712
~~~
{: .output}

## Visualizing data
The mathematician Richard Hamming once said, "The purpose of computing
is insight, not numbers," and the best way to develop insight is often
to visualize data.  Visualization deserves an entire lecture of its
own, but we can explore a few features of Python's `matplotlib`
library here.  While there is no official plotting library,
`matplotlib` is the _de facto_ standard.  

Let's take a look at the average inflammation over time:

~~~
ave_inflammation = numpy.mean(data, axis=0)
ave_plot = matplotlib.pyplot.plot(ave_inflammation)
matplotlib.pyplot.show()
~~~
{: .language-python}

![A line graph showing the average inflammation across all patients over a 40-day period.](../fig/inflammation-01-average.svg)

Here, we have put the average inflammation per day across all patients in the variable
`ave_inflammation`, then asked `matplotlib.pyplot` to create and display a line graph of those
values.  

### Grouping plots
You can group similar plots in a single figure using subplots.
This script below uses a number of new commands. The function `matplotlib.pyplot.figure()`
creates a space into which we will place all of our plots. The parameter `figsize`
tells Python how big to make this space. Each subplot is placed into the figure using
its `add_subplot` [method]({{ page.root }}/reference.html#method). The `add_subplot` method takes 3
parameters. The first denotes how many total rows of subplots there are, the second parameter
refers to the total number of subplot columns, and the final parameter denotes which subplot
your variable is referencing (left-to-right, top-to-bottom). Each subplot is stored in a
different variable (`axes1`, `axes2`, `axes3`). Once a subplot is created, the axes can
be titled using the `set_xlabel()` command (or `set_ylabel()`).
Here are our three plots side by side:

~~~
import numpy
import matplotlib.pyplot

data = numpy.loadtxt(fname='inflammation-01.csv', delimiter=',')

fig = matplotlib.pyplot.figure(figsize=(10.0, 3.0))

axes1 = fig.add_subplot(1, 3, 1)
axes2 = fig.add_subplot(1, 3, 2)
axes3 = fig.add_subplot(1, 3, 3)

axes1.set_ylabel('average')
axes1.plot(numpy.mean(data, axis=0))

axes2.set_ylabel('max')
axes2.plot(numpy.max(data, axis=0))

axes3.set_ylabel('min')
axes3.plot(numpy.min(data, axis=0))

fig.tight_layout()

matplotlib.pyplot.savefig('inflammation.png')
matplotlib.pyplot.show()
~~~
{: .language-python}

![Three line graphs showing the daily average, maximum and minimum inflammation over a 40-day period.](../fig/inflammation-01-group-plot.svg)

The [call]({{ page.root }}/reference.html#function-call) to `loadtxt` reads our data,
and the rest of the program tells the plotting library
how large we want the figure to be,
that we're creating three subplots,
what to draw for each one,
and that we want a tight layout.
(If we leave out that call to `fig.tight_layout()`,
the graphs will actually be squeezed together more closely.)

The call to `savefig` stores the plot as a graphics file. This can be
a convenient way to store your plots for use in other documents, web
pages etc. The graphics format is automatically determined by
Matplotlib from the file name ending we specify; here PNG from
'inflammation.png'. Matplotlib supports many different graphics
formats, including SVG, PDF, and JPEG.

> ## Importing libraries with shortcuts
>
> In this lesson we use the `import matplotlib.pyplot`
> [syntax]({{ page.root }}/reference.html#syntax)
> to import the `pyplot` module of `matplotlib`. However, shortcuts such as
> `import matplotlib.pyplot as plt` are frequently used.
> Importing `pyplot` this way means that after the initial import, rather than writing
> `matplotlib.pyplot.plot(...)`, you can now write `plt.plot(...)`.
> Another common convention is to use the shortcut `import numpy as np` when importing the
> NumPy library. We then can write `np.loadtxt(...)` instead of `numpy.loadtxt(...)`,
> for example.
>
> Some people prefer these shortcuts as it is quicker to type and results in shorter
> lines of code - especially for libraries with long names! You will frequently see
> Python code online using a `pyplot` function with `plt`, or a NumPy function with
> `np`, and it's because they've used this shortcut. It makes no difference which
> approach you choose to take, but you must be consistent as if you use
> `import matplotlib.pyplot as plt` then `matplotlib.pyplot.plot(...)` will not work, and
> you must use `plt.plot(...)` instead. Because of this, when working with other people it
> is important you agree on how libraries are imported.
{: .callout}

{% include links.md %}
