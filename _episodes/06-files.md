---
title: Analyzing Data from Multiple Files
teaching: 20
exercises: 0
questions:
- "How can I do the same operations on many different files?"
objectives:
- "Use a library function to get a list of filenames that match a wildcard pattern."
- "Write a `for` loop to process multiple files."
keypoints:
- "Use `glob.glob(pattern)` to create a list of files whose names match a pattern."
- "Use `*` in a pattern to match zero or more characters, and `?` to match any single character."
---

When working with real datasets, we may not always have everything in a single file.
We need a way to get a list of all the files in our `data` directory whose names start with `wave-` and end with `.csv`.
The following library will help us to achieve this:
~~~
import glob
~~~
{: .language-python}

The `glob` library contains a function, also called `glob`,
that finds files and directories whose names match a pattern.
We provide those patterns as strings:
the character `*` matches zero or more characters,
while `?` matches any one character.
We can use this to get the names of all the CSV files in the current directory:

~~~
print(glob.glob('waves_*.csv'))
~~~
{: .language-python}

~~~
['waves_10s.csv', 'waves_00s.csv', 'waves_80s.csv', 'waves_90s.csv']
~~~
{: .output}

These files show waveheight data from some years in the decades indicated in the filename. As these examples show,
`glob.glob`'s result is a list of file and directory paths in arbitrary order.
This means we can loop over it
to do something with each filename in turn.
In our case,
the "something" we want to do is generate a set of plots for each file in our waveheight dataset.

If we want to start by analyzing just the first three files in alphabetical order, we can use the
`sorted` built-in function to generate a new sorted list from the `glob.glob` output:

~~~
import glob
import numpy
import matplotlib.pyplot

filenames = sorted(glob.glob('waves_*.csv'))
filenames = filenames[0:3]

for filename in filenames:
    print(filename)
    
    data = numpy.loadtxt(fname=filename, delimiter=',')
    number_of_rows = data.shape[0]
    number_of_years = number_of_rows//12

    # need to reshape the data for plotting
    data = numpy.reshape(data[:,2], [number_of_years,12])
    
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
    matplotlib.pyplot.show()
~~~
{: .language-python}

~~~
waves-00.csv
~~~
{: .output}

![Output from the first iteration of the for loop. Three line graphs showing the average,
maximum and minimum waveheight in the 2000s.](
../fig/waves_loop_1.svg)

~~~
waves-10s.csv
~~~
{: .output}

![Output from the second iteration of the for loop. Three line graphs showing the average,
maximum and minimum waveheight in the 2010s.](../fig/waves_loop_2.svg)

~~~
waves-80s.csv
~~~
{: .output}

![Output from the third iteration of the for loop. Three line graphs showing the average,
maximum and minimum waveheight in the 1980s.](../fig/waves_loop_3.svg)


Looking at these three decades, we can see similarities - with the average value representing a smooth climate with clear annual cycle. 
There are differences year on year, and the minimum and maximum data tend to be more variable than the mean.

> ## Different types of division
>
> You might have noticed that we calculated the number of years when reshaping the data, rather
> than using 10 for each decade. This was useful here because the file containing data from the 2010s 
> only has data from 6 years, but each one of these years did contain data for every month. If any year had missing data
> from any month, we would have needed to have done some additional preprocessing.
> 
> When we divided by 12 to get the number of years, we used `//` - you might have expected us just to use `/`.
> Python creates a float as a result from a division operation using `/`, even if both inputs are integers:
>
> ~~~
> type(10/2)
> ~~~
> {: .language-python}
>
> ~~~
> float
> ~~~
> {: .output}
> 
> However, if you use a float value as an array index, you get an error (even if it refers to a whole number).
> `//` is Python's integer division operator - meaning that the result will always be an integer:
>
> ~~~
> type(10//2)
> ~~~
> {: .language-python}
>
> ~~~
> int
> ~~~
> {: .output}
>
> If the result would normally result in a floating-point number, the actual result will instead be an integer rounded towards minus infinity:
>
> ~~~
> print(19/4)
> print(19//4)
> ~~~
> {: .language-python}
>
> ~~~
> 4.75
> 4
> ~~~
> {: .output}
{: .callout}

Sometimes, plots can help us spot patterns in data, or problems with data.

Let's load `waves_90s.csv`:

~~~
data = numpy.loadtxt(fname = "waves_90s.csv", delimiter=',')
~~~
{: .language-python}

If we try and take the mean for the entire year, we'll see that there must be NaNs:

~~~
numpy.mean(data[:,2])
~~~
{: .language-python}

~~~
nan
~~~
{: .output}

If we had only plotted the reshaped data, we would see white squares where there are NaNs in the data:

~~~
matplotlib.pyplot.imshow(data)
matplotlib.pyplot.show()
~~~
{: .language-python}

![1990s data highlighting NaNs](../fig/1990s_nans.svg)

We can clearly see that there must have been some problem with the collection of data in the first 6 months of 1994.
Apart from that, the rest of the data looks relatively sensible, with low wave heights in the summer months of the decade, and 
higher wave heights in the winter months of the decade. This means that we have no reason not to trust the rest of the dataset. 

There are other ways that we could have determined where the missing data is. The Numpy function `isnan` will tell us whether 
any given value is NaN; if we give it an `ndarray`, it will return an `ndarray` of the same shape with boolean values (`True` or `False`)
showing if the value at that index was a NaN. `argwhere` will return the indices for an `ndarray` of booleans where the value is `True`.

~~~
numpy.argwhere(numpy.isnan(data))
~~~
{: .language-python}

~~~
array([[4, 0],
       [4, 1],
       [4, 2],
       [4, 3],
       [4, 4],
       [4, 5]])
~~~
{: .output}

There are almost always multiple ways to achieve the same result in programming, and often the choice as to which method
to use comes down to personal preference. Some people might prefer to look at patterns in plots, while others may be happy to 
look at summary statistics and aggregate values from tabular data to come to the same conclusion.

> ## Plotting Differences
>
> Plot the difference between the average monthly waveheights in the 1980s and 1990s
> Can you do this using glob, without specifying the filenames explicitly in the code?
>
> > ## Solution
> > ~~~
> > import glob
> > import numpy
> > import matplotlib.pyplot
> >
> > filenames = sorted(glob.glob('waves_*.csv'))
> >
> > data0 = numpy.loadtxt(fname=filenames[2], delimiter=',')
> > data1 = numpy.loadtxt(fname=filenames[3], delimiter=',')
> >
> > number_of_rows0 = data0.shape[0]
> > number_of_years0 = number_of_rows0//12 
> > data0 = numpy.reshape(data0[:,2], [number_of_years0,12])
> >
> > number_of_rows1 = data1.shape[0]
> > number_of_years1 = number_of_rows1//12 
> > data1 = numpy.reshape(data1[:,2], [number_of_years1,12])
> >
> > fig = matplotlib.pyplot.figure(figsize=(10.0, 3.0))
> >
> > matplotlib.pyplot.ylabel('Difference in average')
> > matplotlib.pyplot.plot(numpy.mean(data0, axis=0) - numpy.mean(data1, axis=0))
> >
> > fig.tight_layout()
> > matplotlib.pyplot.show()
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}
 
Congratulations! We've investigated the wave data and spotted some trends, and identified bad / missing data.
Now that we understand what is in the model data set, and trust that it is realistic, we can use it to make practical decisions about things like boat operations

{% include links.md %}
