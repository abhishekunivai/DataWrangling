Do This Before Lab 1
====================

What python version do you have?

This is how you can see the version in the jupyter interface

```python--cff578a9-03de-472a-962a-c37d2ba22456
import sys
print(sys.version)
```

If you've successfully completed the above install, skip to below the troubleshooting section. All of the statements there should run.

Python Libraries
----------------

Some of this code ought to be installed on your system. Check the others (commented), else we will need to install these soon!

```python--5dad1ee1-8edb-4b10-af9b-5964441fdbdd
#IPython is what you are using now to run the notebook
import IPython
print("IPython version:      %6.6s" % IPython.__version__)

# Numpy is a library for working with Arrays
import numpy as np
print("Numpy version:        %6.6s" % np.__version__)

# SciPy implements many different numerical algorithms
import scipy as sp
print("SciPy version:        %6.6s" % sp.__version__)

# Pandas makes working with data tables easier
import pandas as pd
print("Pandas version:       %6.6s" % pd.__version__)

# Module for plotting
import matplotlib
print("Matplotlib version:    %6.6s" % matplotlib.__version__)

# SciKit Learn implements several Machine Learning algorithms
import sklearn
print("Scikit-Learn version: %6.6s" % sklearn.__version__)

# # Requests is a library for getting data from the Web
# import requests
# print("requests version:     %6.6s" % requests.__version__)

# #BeautifulSoup is a library to parse HTML and XML documents
# import bs4
# print("BeautifulSoup version:%6.6s" % bs4.__version__)

# import seaborn
# print("Seaborn version:%6.6s" % seaborn.__version__)
```

If any of these libraries are missing you will need to install them and restart jupyter.

Kicking the tires
-----------------

Lets try some things, starting from very simple, to more complex.

### Hello World

The following is the incantation we like to put at the beginning of every notebook. It loads most of the stuff we will regularly use.

```python--b83087e1-cdb1-46e1-a712-42e23d89390d
# The %... is an iPython thing, and is not part of the Python language.
# In this case we're just telling the plotting library to draw things on
# the notebook, instead of on a separate window.
%matplotlib inline 
#this line above prepares the jupyter notebook for working with matplotlib

# See all the "as ..." contructs? They're just aliasing the package names.
# That way we can call methods like plt.plot() instead of matplotlib.pyplot.plot().
# notice we use short aliases here, and these are conventional in the python community

import numpy as np # imports a fast numerical programming library
import scipy as sp #imports stats functions, amongst other things
import matplotlib as mpl # this actually imports matplotlib
import matplotlib.cm as cm # allows us easy access to colormaps
import matplotlib.pyplot as plt # sets up plotting under plt
import pandas as pd #lets us handle data as dataframes
```

### Hello matplotlib

The notebook integrates nicely with Matplotlib, the primary plotting package for python. This should embed a figure of a sine wave:

```python--af578c0a-0c72-41f3-b457-a7263ada4a3a
x = np.linspace(0, 10, 30)  #array of 30 points from 0 to 10
y = np.sin(x)
z = y + np.random.normal(size=30) * .2
plt.plot(x, y, 'o-', label='A sine wave')
plt.plot(x, z, '-', label='Noisy sine')
plt.legend(loc = 'lower right')
plt.xlabel("X axis")
plt.ylabel("Y axis")           
```

### Hello Numpy

The Numpy array processing library is the basis of nearly all numerical computing in Python. Here's a 30 second crash course. For more details, consult the [Numpy User's Guide](http://docs.scipy.org/doc/numpy-dev/user/index.html)

```python--d79a5ef4-f9da-4e9d-96c0-63e459b57c41
print("Make a 3 row x 4 column array of random numbers")
x = np.random.random((3, 4))
print(x,"\n")


print("Add 1 to every element")
x = x + 1
print(x,"\n")

print("Get the element at row 1, column 2")
print(x[1, 2])

# The colon syntax is called "slicing" the array. 
print("Get the first row")
print(x[0, :])

print("Last 2 items in the first row")
print(x[0, -2:])

print("Get every 2nd item in the first row")
print(x[0, ::2])
```

Print the maximum, minimum, and mean of the array. This does **not** require writing a loop. In the code cell below, type `x.m<TAB>`, to find built-in operations for common array statistics like this

```python--c728ecb2-cf35-4d3d-aa1c-05b20302b76c
print("Max is  ", x.max())
print("Min is  ", x.min())
print("Mean is ", x.mean())
```

Call the `x.max` function again, but use the `axis` keyword to print the maximum of each row in x.

```python--29db4e10-f0b3-465e-bb39-ce7c49daef87
print(x.max(axis=1))
```

Here's a way to quickly simulate 500 coin "fair" coin tosses (where the probabily of getting Heads is 50%, or 0.5)

```python--847a95b6-58ab-4aa8-bb70-05315ce08712
x = np.random.binomial(500, .5)
print("number of heads:", x)
```

Repeat this simulation 500 times, and use the [plt.hist() function](http://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.hist) to plot a histogram of the number of Heads (1s) in each simulation

```python--c7e16106-fa74-4675-b939-58eece47472f
# 3 ways to run the simulations

# loop
heads = []
for i in range(500):
    heads.append(np.random.binomial(500, .5))

# "list comprehension"
heads = [np.random.binomial(500, .5) for i in range(500)]

# pure numpy, preferred
heads = np.random.binomial(500, .5, size=500)

histogram = plt.hist(heads, bins=10)
```