---
title: Analyzing some environmental data
teaching: 40
exercises: 20
questions:
- "How can I process tabular data files in Python?"
objectives:
- "Explain what a library is and what libraries are used for."
- "Import a Python library and use the functions it contains."
- "Read tabular data from a file into a program."
- "Select individual values and subsections from data."
- "Perform operations on arrays of data."
keypoints:
- "Import a library into a program using `import libraryname`."
- "Use the `numpy` library to work with arrays in Python."
- "The expression `array.shape` gives the shape of an array."
- "Use `array[x, y]` to select a single element from a 2D array."
- "Array indices start at 0, not 1."
- "Use `low:high` to specify a `slice` that includes the indices from `low` to `high-1`."
- "Use `# some kind of explanation` to add comments to programs."
- "Use `numpy.mean(array)`, `numpy.max(array)`, and `numpy.min(array)` to calculate simple statistics."
- "Use `numpy.mean(array, axis=0)` or `numpy.mean(array, axis=1)` to calculate statistics across the specified axis."
---

Words are useful, but what's more useful are the sentences and stories we build with them.
Similarly, while a lot of powerful, general tools are built into Python,
specialized tools built up from these basic units live in
[libraries]({{ page.root }}/reference.html#library)
that can be called upon when needed.

## Loading data into Python

To begin processing the wavedata, we need to load it into Python.
We can do that using a library called
[NumPy](https://numpy.org/doc/stable "NumPy Documentation"), which stands for Numerical Python.
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
numpy.loadtxt(fname='isles-of-scilly-wavenet-2d.csv', delimiter=',')
~~~
{: .language-python}

~~~
array([[0.93, 0.91, 0.99, ..., 1.42, 1.61, 1.47],
       [1.34, 1.2 , 1.26, ..., 1.49, 1.55, 1.66],
       [1.65, 1.44, 1.36, ..., 1.14, 1.26, 1.33],
       ...,
       [4.23, 4.42, 4.56, ..., 6.11, 6.63, 6.6 ],
       [6.91, 6.98, 7.83, ..., 7.82, 7.82, 7.49],
       [7.07, 7.03, 6.78, ..., 5.52, 5.24, 5.8 ]])
~~~
{: .output}

The expression `numpy.loadtxt(...)` is a
[function call]({{ page.root }}/reference.html#function-call)
that asks Python to run the [function]({{ page.root }}/reference.html#function) `loadtxt` which
belongs to the `numpy` library.
The dot notation in Python is used most of all as an object attribute/property specifier or for invoking its method. `object.property` will give you the object.property value,
`object_name.method()` will invoke on object_name method.

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
data = numpy.loadtxt(fname='isles-of-scilly-wavenet-2d.csv', delimiter=',', skiprows=1)
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
[[0.93 0.91 0.99 ... 1.42 1.61 1.47]
 [1.34 1.2  1.26 ... 1.49 1.55 1.66]
 [1.65 1.44 1.36 ... 1.14 1.26 1.33]
 ...
 [4.23 4.42 4.56 ... 6.11 6.63 6.6 ]
 [6.91 6.98 7.83 ... 7.82 7.82 7.49]
 [7.07 7.03 6.78 ... 5.52 5.24 5.8 ]]
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

> ## Data Type
>
> A Numpy array contains one or more elements
> of the same type. The `type` function will only tell you that
> a variable is a NumPy array but won't tell you the type of
> thing inside the array.
> We can find out the type
> of the data contained in the NumPy array.
>
> ~~~
> print(data.dtype)
> ~~~
> {: .language-python}
>
> ~~~
> float64
> ~~~
> {: .output}
>
> This tells us that the NumPy array's elements are
> [floating-point numbers]({{ page.root }}/reference.html#floating-point-number).
{: .callout}

With the following command, we can see the array's [shape]({{ page.root }}/reference.html#shape):

~~~
print(data.shape)
~~~
{: .language-python}

~~~
(446, 24)
~~~
{: .output}

The output tells us that the `data` array variable contains 21440 rows and 7 columns. When we
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
first value in data: 0.93
~~~
{: .output}

~~~
print('middle value in data:', data[223, 12])
~~~
{: .language-python}

~~~
middle value in data: 1.09
~~~
{: .output}

The expression `data[10720, 3]` accesses the element at row 10720, column 3. While this expression may
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
An index like `[223, 12]` selects a single element of an array,
but we can select whole sections as well.
For example,
we can select the wavedata from the mornings for the first 10 days like this:

~~~
print(data[0:10, 0:12])
~~~
{: .language-python}

~~~
[[0.93 0.91 0.99 0.94 0.98 0.93 0.87 0.83 0.84 0.83 0.83 0.87]
 [1.34 1.2  1.26 1.33 1.37 1.31 1.52 1.57 1.43 1.5  1.34 1.4 ]
 [1.65 1.44 1.36 1.14 1.2  1.26 1.1  1.02 1.05 0.89 0.88 0.89]
 [1.64 1.83 1.99 2.07 2.08 2.35 2.31 2.43 2.29 2.41 2.34 2.81]
 [4.35 4.28 4.03 3.94 3.9  3.71 3.51 3.59 3.47 3.79 3.73 3.79]
 [3.94 4.23 4.6  4.51 4.38 4.57 4.42 4.54 4.   4.07 3.61 3.62]
 [4.58 4.61 4.55 4.62 4.68 4.36 4.9  4.59 4.72 5.03 4.76 4.85]
 [4.07 4.26 4.63 4.33 4.3  4.17 4.65 4.2  4.65 4.43 3.74 3.65]
 [3.15 3.09 2.87 2.83 2.97 2.9  2.86 2.8  2.68 2.69 2.59 2.79]
 [3.13 3.23 3.89 4.17 4.28 4.95 5.14 5.17 5.07 5.31 5.3  4.91]]
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
[[3.94 4.23 4.6  4.51 4.38 4.57 4.42 4.54 4.   4.07 3.61 3.62]
 [4.58 4.61 4.55 4.62 4.68 4.36 4.9  4.59 4.72 5.03 4.76 4.85]
 [4.07 4.26 4.63 4.33 4.3  4.17 4.65 4.2  4.65 4.43 3.74 3.65]
 [3.15 3.09 2.87 2.83 2.97 2.9  2.86 2.8  2.68 2.69 2.59 2.79]
 [3.13 3.23 3.89 4.17 4.28 4.95 5.14 5.17 5.07 5.31 5.3  4.91]]
~~~
{: .output}

We also don't have to include the upper and lower bound on the slice.  If we don't include the lower
bound, Python uses 0 by default; if we don't include the upper, the slice runs to the end of the
axis, and if we don't include either (i.e., if we use ':' on its own), the slice includes
everything:

~~~
small = data[:2, 12:] # afternoon data from first 2 days
print('small subset of data is:')
print(small)
~~~
{: .language-python}
The above example selects rows 0 through 1 (i.e. 0th and 1st) and columns 5 through to the end of the array.

~~~
small subset of data is:
[[0.91 0.86 0.86 0.96 1.   1.   1.16 1.24 1.25 1.42 1.61 1.47]
 [1.37 1.42 1.27 1.17 1.23 1.22 1.41 1.48 1.61 1.49 1.55 1.66]]
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
nan
~~~
{: .output}

Ah! We have NaNs in our data - this is not an uncommon situation with real-life observational data. We have two
possible solutions:

 - replace the NaNs with a value (e.g. mean of column or mean of row) - NumPy has methods to help with this
 - use NunPy's `nanmean` function

~~~
print(numpy.nanmean(data))
~~~
{: .language-python}

~~~
2.7978422577329223
~~~
{: .output}

`mean` and `nanmean` are both [functions]({{ page.root }}/reference.html#function) that takes
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
maxval, minval, stdval = numpy.nanmax(data), numpy.nanmin(data), numpy.nanstd(data)

print('max wave height (excluding NaNs):', maxval)
print('min wave height (excluding NaNs):', minval)
print('wave height standard deviation (excluding NaNs):', stdval)
~~~
{: .language-python}

Here we've assigned the return value from `numpy.max(data[:31,6])` to the variable `day1max`, the value
from `numpy.min(data[:31,6])` to `day1min`, and so on.

~~~
max wave height (excluding NaNs): 9.2
min wave height (excluding NaNs): 0.33
wave height standard deviation (excluding NaNs): 1.4554801518585112
~~~
{: .output}

> ## Mystery Functions in IPython
>
> How did we know what functions NumPy has and how to use them?
> If you are working in IPython or in a Jupyter Notebook, there is an easy way to find out.
> If you type the name of something followed by a dot, then you can use
> [tab completion]({{ page.root }}/reference.html#tab-completion)
> (e.g. type `numpy.` and then press <kbd>Tab</kbd>)
> to see a list of all functions and attributes that you can use. After selecting one, you
> can also add a question mark (e.g. `numpy.cumprod?`), and IPython will return an
> explanation of the method! This is the same as doing `help(numpy.cumprod)`.
> Similarly, if you are using the "plain vanilla" Python interpreter, you can type `numpy.`
> and press the <kbd>Tab</kbd> key twice for a listing of what is available. You can then use the
> `help()` function to see an explanation of the function you're interested in,
> for example: `help(numpy.cumprod)`.
{: .callout}

We could also create a new temporary array of the data we want,
then ask it to do the calculation:

~~~
day_1 = data[0, :] # 0 on the first axis (rows), everything on the second (columns)
print('maximum wave height for day 1:', numpy.max(day_1)) # note we can use numpy.max here if we know there are no NaNs in the data
~~~
{: .language-python}

~~~
maximum wave height for day 1: 1.61
~~~
{: .output}

Everything in a line of code following the '#' symbol is a
[comment]({{ page.root }}/reference.html#comment) that is ignored by Python.
Comments allow programmers to leave explanatory notes for other
programmers or their future selves.

We don't actually need to store the row in a variable of its own.
Instead, we can combine the selection and the function call:

~~~
print('maximum wave height for day 1:', numpy.max(data[0, :]))
~~~
{: .language-python}

~~~
maximum wave height for day 1: 1.61
~~~
{: .output}

What if we need the maximum inflammation for each patient over all days (as in the
next diagram on the left) or the average for each day (as in the
diagram on the right)? As the diagram below shows, we want to perform the
operation across an axis:

![Per-patient maximum inflammation is computed row-wise across all columns using
numpy.max(data, axis=1). Per-day average inflammation is computed column-wise across all rows using
numpy.mean(data, axis=0).](../fig/python-operations-across-axes.png)

To support this functionality,
most array functions allow us to specify the axis we want to work on.
If we ask for the average across axis 0 (rows in our 2D example),
we get:

~~~
print(numpy.mean(data, axis=0))
~~~
{: .language-python}

~~~
[2.77298206 2.76988789 2.78100897 2.79625561 2.80480899 2.82852018
 2.82278027 2.81230942 2.8182287  2.79439462 2.77721973 2.76695067
 2.76636771 2.77544843 2.7638427  2.79567265 2.81172646 2.8126009
 2.82834081 2.83363229 2.82076233 2.81183857 2.79876404 2.78381166]
~~~
{: .output}

As a quick check,
we can ask this array what its shape is:

~~~
print(numpy.mean(data, axis=0).shape)
~~~
{: .language-python}

~~~
(24,)
~~~
{: .output}

The expression `(24,)` tells us we have an N×1 vector,
so this is the average inflammation per day for all patients.
If we average across axis 1 (columns in our 2D example), we get:

~~~
print(numpy.mean(data, axis=1))
~~~
{: .language-python}

~~~
[1.02041667 1.39375    1.0675     3.10333333 3.935      4.195
 4.70083333 4.02333333 2.78708333 4.57083333 2.89708333 2.39916667
 2.55833333 3.02666667 3.235      3.1175     2.27       1.82
 ...
~~~
{: .output}

which is the average inflammation per patient across all days.


> ## Slicing Strings
>
> A section of an array is called a [slice]({{ page.root }}/reference.html#slice).
> We can take slices of character strings as well:
>
> ~~~
> element = 'oxygen'
> print('first three characters:', element[0:3])
> print('last three characters:', element[3:6])
> ~~~
> {: .language-python}
>
> ~~~
> first three characters: oxy
> last three characters: gen
> ~~~
> {: .output}
>
> What is the value of `element[:4]`?
> What about `element[4:]`?
> Or `element[:]`?
>
> > ## Solution
> > ~~~
> > oxyg
> > en
> > oxygen
> > ~~~
> > {: .output}
> {: .solution}
>
> What is `element[-1]`?
> What is `element[-2]`?
>
> > ## Solution
> > ~~~
> > n
> > e
> > ~~~
> > {: .output}
> {: .solution}
>
> Given those answers,
> explain what `element[1:-1]` does.
>
> > ## Solution
> > Creates a substring from index 1 up to (not including) the final index,
> > effectively removing the first and last letters from 'oxygen'
> {: .solution}
>
> How can we rewrite the slice for getting the last three characters of `element`,
> so that it works even if we assign a different string to `element`?
> Test your solution with the following strings: `carpentry`, `clone`, `hi`.
>
> > ## Solution
> > ~~~
> > element = 'oxygen'
> > print('last three characters:', element[-3:])
> > element = 'carpentry'
> > print('last three characters:', element[-3:])
> > element = 'clone'
> > print('last three characters:', element[-3:])
> > element = 'hi'
> > print('last three characters:', element[-3:])
> > ~~~
> > {: .language-python}
> > ~~~
> > last three characters: gen
> > last three characters: try
> > last three characters: one
> > last three characters: hi
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

> ## Thin Slices
>
> The expression `element[3:3]` produces an
> [empty string]({{ page.root }}/reference.html#empty-string),
> i.e., a string that contains no characters.
> If `data` holds our array of patient data,
> what does `data[3:3, 4:4]` produce?
> What about `data[3:3, :]`?
>
> > ## Solution
> > ~~~
> > array([], shape=(0, 0), dtype=float64)
> > array([], shape=(0, 40), dtype=float64)
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

> ## Stacking Arrays
>
> Arrays can be concatenated and stacked on top of one another,
> using NumPy's `vstack` and `hstack` functions for vertical and horizontal stacking, respectively.
>
> ~~~
> import numpy
>
> A = numpy.array([[1,2,3], [4,5,6], [7, 8, 9]])
> print('A = ')
> print(A)
>
> B = numpy.hstack([A, A])
> print('B = ')
> print(B)
>
> C = numpy.vstack([A, A])
> print('C = ')
> print(C)
> ~~~
> {: .language-python}
>
> ~~~
> A =
> [[1 2 3]
>  [4 5 6]
>  [7 8 9]]
> B =
> [[1 2 3 1 2 3]
>  [4 5 6 4 5 6]
>  [7 8 9 7 8 9]]
> C =
> [[1 2 3]
>  [4 5 6]
>  [7 8 9]
>  [1 2 3]
>  [4 5 6]
>  [7 8 9]]
> ~~~
> {: .output}
>
> Write some additional code that slices the first and last columns of `A`,
> and stacks them into a 3x2 array.
> Make sure to `print` the results to verify your solution.
>
> > ## Solution
> >
> > A 'gotcha' with array indexing is that singleton dimensions
> > are dropped by default. That means `A[:, 0]` is a one dimensional
> > array, which won't stack as desired. To preserve singleton dimensions,
> > the index itself can be a slice or array. For example, `A[:, :1]` returns
> > a two dimensional array with one singleton dimension (i.e. a column
> > vector).
> >
> > ~~~
> > D = numpy.hstack((A[:, :1], A[:, -1:]))
> > print('D = ')
> > print(D)
> > ~~~
> > {: .language-python}
> >
> > ~~~
> > D =
> > [[1 3]
> >  [4 6]
> >  [7 9]]
> > ~~~
> > {: .output}
> {: .solution}
>
> > ## Solution
> >
> > An alternative way to achieve the same result is to use Numpy's
> > delete function to remove the second column of A.
> >
> > ~~~
> > D = numpy.delete(A, 1, 1)
> > print('D = ')
> > print(D)
> > ~~~
> > {: .language-python}
> >
> > ~~~
> > D =
> > [[1 3]
> >  [4 6]
> >  [7 9]]
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

> ## Change In Inflammation
>
> The wavedata data is _longitudinal_ in the sense that each row represents a
> series of observations relating to one "individual" (in this case, an individual is a day).  This means that
> the change in inflammation over time is a meaningful concept.
> Let's find out how to calculate changes in the data contained in an array
> with NumPy.
>
> The `numpy.diff()` function takes an array and returns the differences
> between two successive values. Let's use it to examine the changes
> each day across the first week of patient 3 from our inflammation dataset.
>
> ~~~
> day4_morning = data[3, :12] # day 4 because of the 0 indexing
> print(day4_morning)
> ~~~
> {: .language-python}
>
> ~~~
>  [1.64 1.83 1.99 2.07 2.08 2.35 2.31 2.43 2.29 2.41 2.34 2.81]
> ~~~
> {: .output}
>
> Calling `numpy.diff(day4_morning)` would do the following calculations
>
> ~~~
> [ 1.83 - 1.64, 1.99 - 1.83, 2.07 - 1.99, 2.08 - 2.07, 2.35 - 2.08, 2.31 - 2.35, 2.43 - 2.31, 2.29 - 2.43, 2.41 - 2.29, 2.34 - 2.41, 2.81 - 2.34 ]
> ~~~
> {: .language-python}
>
> and return the 11 difference values in a new array.
>
> ~~~
> numpy.diff(day4_morning)
> ~~~
> {: .language-python}
>
> ~~~
> array([ 0.19,  0.16,  0.08,  0.01,  0.27, -0.04,  0.12, -0.14,  0.12,
>       -0.07,  0.47])
> ~~~
> {: .output}
>
> Note that the array of differences is shorter by one element (length 11).
>
> When calling `numpy.diff` with a multi-dimensional array, an `axis` argument may
> be passed to the function to specify which axis to process. When applying
> `numpy.diff` to our 2D inflammation array `data`, which axis would we specify?
>
> > ## Solution
> > Since the row axis (0) is patients, it does not make sense to get the
> > difference between two arbitrary patients. The column axis (1) is in
> > days, so the difference is the change in inflammation -- a meaningful
> > concept.
> >
> > ~~~
> > numpy.diff(data, axis=1)
> > ~~~
> > {: .language-python}
> {: .solution}
>
> If the shape of an individual data file is `(60, 40)` (60 rows and 40
> columns), what would the shape of the array be after you run the `diff()`
> function and why?
>
> > ## Solution
> > The shape will be `(60, 39)` because there is one fewer difference between
> > columns than there are columns in the data.
> {: .solution}
>
> How would you find the largest change in inflammation for each patient? Does
> it matter if the change in inflammation is an increase or a decrease?
>
> > ## Solution
> > By using the `numpy.max()` function after you apply the `numpy.diff()`
> > function, you will get the largest difference between days.
> >
> > ~~~
> > numpy.max(numpy.diff(data, axis=1), axis=1)
> > ~~~
> > {: .language-python}
> >
> > ~~~
> > array([  7.,  12.,  11.,  10.,  11.,  13.,  10.,   8.,  10.,  10.,   7.,
> >          7.,  13.,   7.,  10.,  10.,   8.,  10.,   9.,  10.,  13.,   7.,
> >         12.,   9.,  12.,  11.,  10.,  10.,   7.,  10.,  11.,  10.,   8.,
> >         11.,  12.,  10.,   9.,  10.,  13.,  10.,   7.,   7.,  10.,  13.,
> >         12.,   8.,   8.,  10.,  10.,   9.,   8.,  13.,  10.,   7.,  10.,
> >          8.,  12.,  10.,   7.,  12.])
> > ~~~
> > {: .language-python}
> >
> > If inflammation values *decrease* along an axis, then the difference from
> > one element to the next will be negative. If
> > you are interested in the **magnitude** of the change and not the
> > direction, the `numpy.absolute()` function will provide that.
> >
> > Notice the difference if you get the largest _absolute_ difference
> > between readings.
> >
> > ~~~
> > numpy.max(numpy.absolute(numpy.diff(data, axis=1)), axis=1)
> > ~~~
> > {: .language-python}
> >
> > ~~~
> > array([ 12.,  14.,  11.,  13.,  11.,  13.,  10.,  12.,  10.,  10.,  10.,
> >         12.,  13.,  10.,  11.,  10.,  12.,  13.,   9.,  10.,  13.,   9.,
> >         12.,   9.,  12.,  11.,  10.,  13.,   9.,  13.,  11.,  11.,   8.,
> >         11.,  12.,  13.,   9.,  10.,  13.,  11.,  11.,  13.,  11.,  13.,
> >         13.,  10.,   9.,  10.,  10.,   9.,   9.,  13.,  10.,   9.,  10.,
> >         11.,  13.,  10.,  10.,  12.])
> > ~~~
> > {: .language-python}
> >
> {: .solution}
{: .challenge}

{% include links.md %}
