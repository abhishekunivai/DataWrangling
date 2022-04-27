#**Data Wrangling**

Data wrangling can be defined as the process of cleaning, organizing, and transforming raw data into the desired format for analysts to use for prompt decision-making. Also known as data cleaning or data munging, data wrangling enables businesses to tackle more complex data in less time, produce more accurate results, and make better decisions. 

Some examples of data wrangling include:

1. Merging multiple data sources into a single dataset for analysis.
2. Identifying gaps in data (for example, empty cells in a spreadsheet) and either filling or deleting them.
3. Deleting data that’s either unnecessary or irrelevant to the project you’re working on.
4. Identifying extreme outliers in data and either explaining the discrepancies or removing them so that analysis can take place.

In this course we're going to understand how to perform *Data Wrangling* in python. But before we proceed further, let us revisit some basic of Python to brush up our coding skills.

##**1. Introduction to Basic Python**

###1.1 Basic Datatypes

In this section, we will go over simple data types in Python. These are some of the
essential building blocks for handling information in Python. The data types we will
learn are strings, integers, floats, and other non–whole number types.

####**1.1.1 Strings**

A *string* is basically text and it is denoted by
using quotes (Single or double). Strings can contain numbers, letters, and symbols. Essentially, in Python, strings are arrays of bytes representing Unicode characters.

An example of a String is:

*'cat'*

*'This is a string.'*

*'5'*

*'walking'*

*'$GOObarBaz340 '*


```python
'An example of a string'
```




    'An example of a string'



**Assigning & Printing a String**


```python
x = 'hello' #Assigning a string to a variable.
```


```python
x
```




    'hello'




```python
print(x)
```

    hello


Another example of printing:


```python
num = '12'
name = 'Sam'
```


```python
#Format 1

print('My number is: {one}, and my name is: {two}'.format(one=num,two=name))
```

    My number is: 12, and my name is: Sam



```python
#Format 2

print('My number is: {}, and my name is: {}'.format(num,name))
```

    My number is: 12, and my name is: Sam


**Using split() in Python**

If you look at the string **'cat,dog,horse'**, it looks like it is a list saved in a string. It’s actually a single value, but with the Python string’s built-in split method we can divide the string into smaller pieces by splitting it on the comma character, like so:



```python
#use .split() to split the string based on a delimiter
'cat,dog,horse'.split(',')
```




    ['cat', 'dog', 'horse']



We can split a string against any separator which needs to be specified within the brackets.

#####Q1 String slicing
Write a Python function to get a string made of its first three characters of a specified string. If the length of the string is less than 3 then return the original string.

first_three('ipy') -> ipy

first_three('python') -> pyt



```python
"""Solution"""
def first_three(str):
	return str[:3] if len(str) > 3 else str

print(first_three('ipy'))
print(first_three('python'))
print(first_three('py'))
```

    ipy
    pyt
    py


#####Q2 String Sorting
Write a Python program to sort a string lexicographically.


```python
def lexicographi_sort(s):
    return sorted(sorted(s), key=str.upper)

print(lexicographi_sort('w3resource'))
print(lexicographi_sort('quickbrown'))
```

    ['3', 'c', 'e', 'e', 'o', 'r', 'r', 's', 'u', 'w']
    ['b', 'c', 'i', 'k', 'n', 'o', 'q', 'r', 'u', 'w']


#####Q3 String cleaning
Write a Python program to remove a newline in Python. 



```python
str1='Python Exercises\n'
print(str1)
print("-"*20)
print(str1.rstrip())
print("-"*20)
str1='\nPython Exercises\n'
print(str1)
print("-"*20)
print(str1.strip())
```

    Python Exercises
    
    --------------------
    Python Exercises
    --------------------
    
    Python Exercises
    
    --------------------
    Python Exercises


#####Q4 Count Occurences
Write a Python program to count occurrences of a substring in a string.


```python
str1 = 'The quick brown fox jumps over the lazy dog.'

print("Count of Fox: ",str1.lower().count("fox"))
print("Count of The: ",str1.lower().count("the"))
```

    Count of Fox:  1
    Count of The:  2


#####Q5 Reverse String
Write a Python program to reverse a string. 



```python
def reverse_string(str1):
    return ''.join(reversed(str1))
print()
print(reverse_string("abcdef"))
print(reverse_string("Python Exercises."))
print()
```

    
    fedcba
    .sesicrexE nohtyP
    


####**1.1.2 Integer**



An *integer* is a whole number. 

Example: 5, 0, -10, 100, -9999, 25842

If you enter those into your Python interpreter, the interpreter will return them back to you.

Notice in the string example in the previous section, we had a '5'. If a number is entered within quotes, Python will process the value as a string. In the following
example, the first value and second value are not equal:

To test this, enter the following into your interpreter:




```python
5 == '5'

```




    False



In the previous statement, we asked Python whether 5 the integer was the same as '5' the string. What did Python return? **False.**

Basically, the numbers stored as Strings are characters and you cannot peroform calculations on characters. We need numbers for that. 



####**1.1.3 Floats**

A *float* value is a decimal value.

When a non–whole number is used in Python, it defaults to turning the value into a float. A float uses the built-in floating-point data type for your Python version. This means Python stores an approximation of the numeric value—an approximation that reflects only a certain level of precision.

Notice the difference between the following two numbers when you enter them into
your Python interpreter:


```python
2
2.0
```



####**1.1.4 Basic Operations on Numbers - INT & Float** 

Now, let's see some basic operations that can be performed on Integers.


```python
#Addition

x = 10 + 56
y = 0.5 + 9.9

print(x)
print(y)
```

    66
    10.4



```python
#Subtraction

x = 23 - 47
y = 81.9 - 66.75

print(x)
print(y)
```

    -24
    15.150000000000006



```python
#Multiplication

x = 61 * 10
y = 9.65 * 0.25

print(x)
print(y)
```

    610
    2.4125



```python
#Division

x = 100 / 25
y = 100.0/12.5

print(x)
print(y)
```

    4.0
    8.0



```python
#Modulus for Remainder

x = 30 % 10
y = 999.99 % 2.50

print(x)
print(y)
```

    0
    2.490000000000009



```python
#Power Indices

x = 5 ** 3
y = 17.5 ** 0.1

print(x)
print(y)
```

    125
    1.331385445092909



```python
#Brackets for BODMAS

x = (2 + 3) * (5 + 2.5)

print(x)
```

    37.5


#####1.1.4.1 Integer Exercises

#####Q1 Integer Sum
Write a Python program to sum of the first n positive integers. 


```python
"""
Solution
"""
n = int(input("Input a number: "))
sum_num = (n * (n + 1)) / 2
print("Sum of the first", n ,"positive integers:", sum_num)
```

    Input a number: 5
    Sum of the first 5 positive integers: 15.0


#####Q2 Sum of All Divisors
Write a Python program to returns sum of all divisors of a number.
Test Data:

If number = 8

If number = 12

Expected Output:

7

16 


```python
"""
Solution
"""
def sum_div(number):
    divisors = [1]
    for i in range(2, number):
        if (number % i)==0:
            divisors.append(i)
    return sum(divisors)
print(sum_div(8))
print(sum_div(12))
```

    7
    16


#####Q3 Difference of Natural Numbers
Write a Python program to calculate the difference between the squared sum of first n natural numbers and the sum of squared first n natural numbers.(default value of number=2). 

Test Data: 
If sum_difference(12) 

Expected Output : 5434 




```python
"""
Solution
"""
def sum_difference(n=2):
    sum_of_squares = 0
    square_of_sum = 0
    for num in range(1, n+1):
        sum_of_squares += num * num
        square_of_sum += num

    square_of_sum = square_of_sum ** 2

    return square_of_sum - sum_of_squares


print(sum_difference(12))

```

    5434


#####Q4 Raising Base to Power

Write a Python program to calculate the sum of all digits of the base to the specified power. 

Test Data: If power_base_sum(2, 100) 

Expected Output : 115


```python
"""
Solution
"""
def power_base_sum(base, power):
    return sum([int(i) for i in str(pow(base, power))])


print(power_base_sum(2, 100))
print(power_base_sum(8, 10))
```

    115
    37


#####Q5 Abundant & Excessive Numbers

Write a Python program to find out, if the given number is abundant. 

Note: In number theory, an abundant number or excessive number is a number for which the sum of its proper divisors is greater than the number itself. 

The integer 12 is the first abundant number. Its proper divisors are 1, 2, 3, 4 and 6 for a total of 16. 

Test Data: 
If is_abundant(12) 

If is_abundant(13) 

Expected Output: True/False


```python
"""
Solution
"""
def is_abundant(n):
    fctr_sum = sum([fctr for fctr in range(1, n) if n % fctr == 0])
    return fctr_sum > n
print(is_abundant(12))
print(is_abundant(13))
```

    True
    False



```python

```

#####1.1.4.2 Float Exercises

#####Q1 Convert Distance Measurements
Write a Python program to convert the distance (in feet) to inches, yards, and miles.


```python
"""
Solution
"""
d_ft = int(input("Input distance in feet: "))
d_inches = d_ft * 12
d_yards = d_ft / 3.0
d_miles = d_ft / 5280.0

print("The distance in inches is %i inches." % d_inches)
print("The distance in yards is %.2f yards." % d_yards)
print("The distance in miles is %.2f miles." % d_miles)

```

#####Q2 Parsing String to Float & INT

Write a Python program to parse a string to Float or Integer.

Test Data

n = "246.2458"


```python
"""
Solution
"""
n = "246.2458"
print(float(n))
print(int(float(n)))
```

#####Q3 Floating Point Numbers
Write a Python program to round a floating-point number to specified number decimal places.


```python
"""
Solution
"""
number = 212.374
d_places = int(input("Input number of desired decimal places "))
print('\nThe number comes to %f' % number)
print(f'The trimmed number comes to %.{d_places}f' % number)
```

    Input number of desired decimal places 1
    
    The number comes to 212.374000
    The trimmed number comes to 212.4


#####Q4 NaN & Infinity 
Write a Python program to illustrate NaN & Infinity values using float.


```python
"""
Solution
"""
# for infinity
print(float("InF"))
print(float("InFiNiTy"))
 
# for NaN
print(float("nan"))
print(float("NaN"))
```

    inf
    inf
    nan
    nan


#####Q5 Calculate Hypotenuse
Write a Python program to calculate the hypotenuse of a right angled triangle.


```python
"""
Solution
"""
from math import sqrt
print("Input lengths of shorter triangle sides:")
a = float(input("a: "))
b = float(input("b: "))
c = sqrt(a**2 + b**2)
print("The length of the hypotenuse is:", c )
```

####**1.1.5 List**



A list is a group of values that have some relationship in common. You use a list in Python similarly to how you would use it in normal language. In Python, you can
create a list of items by placing them within square brackets([]) and separating them with commas.

Let’s make a list of groceries in Python:


```python
['milk', 'lettuce', 'eggs']
```




    ['milk', 'lettuce', 'eggs']



You can make lists of any Python data type, or any mixture of data types (i.e., floats and strings).


```python
['hi',1,1,2.5]
```




    ['hi', 1, 1, 2.5]



You can also create lists of lists. Let’s say we have a list of names for our animals:


```python
cat_names = ['Walter', 'Ra']
dog_names = ['Joker', 'Simon', 'Ellie', 'Lishka', 'Fido']
horse_names = ['Mr. Ed']
animal_names = [cat_names, dog_names, horse_names]
```


```python
print(animal_names)
```

    [['Walter', 'Ra'], ['Joker', 'Simon', 'Ellie', 'Lishka', 'Fido'], ['Mr. Ed']]


#####Q1 Reverse a list in Python
list1 = [100, 200, 300, 400, 500]


```python
"""
Solution
"""

list1 = [100, 200, 300, 400, 500]

#Solution 1 
list1 = [100, 200, 300, 400, 500]
list1.reverse()
print(list1)

#Solution 2
list1 = [100, 200, 300, 400, 500]
list1 = list1[::-1]
print(list1)


```

    [500, 400, 300, 200, 100]
    [500, 400, 300, 200, 100]


#####Q2 Concatenate two lists index-wise
list1 = ["M", "na", "i", "Ke"]

list2 = ["y", "me", "s", "lly"]

Expected Output 

['My', 'name', 'is', 'Kelly']


```python
"""
Solution
"""
list1 = ["M", "na", "i", "Ke"] 
list2 = ["y", "me", "s", "lly"]
list3 = [i + j for i, j in zip(list1, list2)]
print(list3)
```

    ['My', 'name', 'is', 'Kelly']


#####Q3 Turn every item of a list into its square
numbers = [1, 2, 3, 4, 5, 6, 7]

Expected Output

[1, 4, 9, 16, 25, 36, 49]



```python
"""
Solution
"""
#Solution 1
numbers = [1, 2, 3, 4, 5, 6, 7]
# result list
res = []
for i in numbers:
    # calculate square and add to the result list
    res.append(i * i)
print(res)

#Solution 2
numbers = [1, 2, 3, 4, 5, 6, 7]
res = [x * x for x in numbers]
print(res)
```

    [1, 4, 9, 16, 25, 36, 49]
    [1, 4, 9, 16, 25, 36, 49]


#####Q4 Concatenate two lists in the following order

list1 = ["Hello ", "take "]

list2 = ["Dear", "Sir"]

Expected Output

['Hello Dear', 'Hello Sir', 'take Dear', 'take Sir']



```python
"""
Solution
"""
list1 = ["Hello ", "take "]
list2 = ["Dear", "Sir"]

res = [x + y for x in list1 for y in list2]
print(res)
```

    ['Hello Dear', 'Hello Sir', 'take Dear', 'take Sir']


#####Q5 Iterate both lists simultaneously
First one in same order, reverse order of second list

list1 = [10, 20, 30, 40]

list2 = [100, 200, 300, 400]

Expected output:

10 400

20 300

30 200

40 100


```python
"""
Solution
"""
list1 = [10, 20, 30, 40]
list2 = [100, 200, 300, 400]

for x, y in zip(list1, list2[::-1]):
    print(x, y)
```

    10 400
    20 300
    30 200
    40 100


####**1.1.6 Dictionary**


A *dictionary* is a collection of data which is ordered*, changeable and do not allow duplicates. 

Unlike other data types that hold only a single value as an element, Dictionary holds key:value pair. Key-value is provided in the dictionary to make it more optimized. 


```python
# Creating a dictionary with integer keys

Dict = {1: 'Geeks', 2: 'For', 3: 'Geeks'}
print(Dict)
```

    {1: 'Geeks', 2: 'For', 3: 'Geeks'}


We can also access individual elements of the dictionary via their keys.


```python
print(Dict[2])
```

    For


#####Q1 Convert two lists into a dictionary
keys = ['Ten', 'Twenty', 'Thirty']

values = [10, 20, 30]

Expected output:

{'Ten': 10, 'Twenty': 20, 'Thirty': 30}


```python
"""
Solution
"""
#Solution 1

keys = ['Ten', 'Twenty', 'Thirty']
values = [10, 20, 30]

res_dict = dict(zip(keys, values))
print(res_dict)

#Solution 2
keys = ['Ten', 'Twenty', 'Thirty']
values = [10, 20, 30]

# empty dictionary
res_dict = dict()

for i in range(len(keys)):
    res_dict.update({keys[i]: values[i]})
print(res_dict)
```

    {'Ten': 10, 'Twenty': 20, 'Thirty': 30}
    {'Ten': 10, 'Twenty': 20, 'Thirty': 30}


#####Q2 Merge two Python dictionaries into one
dict1 = {'Ten': 10, 'Twenty': 20, 'Thirty': 30}

dict2 = {'Thirty': 30, 'Fourty': 40, 'Fifty': 50}

Expected Output 

{'Ten': 10, 'Twenty': 20, 'Thirty': 30, 'Fourty': 40, 'Fifty': 50}



```python
"""
Solution
"""
#Solution 1
dict1 = {'Ten': 10, 'Twenty': 20, 'Thirty': 30}
dict2 = {'Thirty': 30, 'Fourty': 40, 'Fifty': 50}

dict3 = {**dict1, **dict2}
print(dict3)

#Solution 2
dict1 = {'Ten': 10, 'Twenty': 20, 'Thirty': 30}
dict2 = {'Thirty': 30, 'Fourty': 40, 'Fifty': 50}

dict3 = dict1.copy()
dict3.update(dict2)
print(dict3)
```

    {'Ten': 10, 'Twenty': 20, 'Thirty': 30, 'Fourty': 40, 'Fifty': 50}
    {'Ten': 10, 'Twenty': 20, 'Thirty': 30, 'Fourty': 40, 'Fifty': 50}


#####Q3 Print the value of key ‘physics’ from the below dict

sampleDict = {
    "class": {
        "student": {
            "name": "Mike",
            "marks": {
                "physics": 70,
                "history": 80
            }
        }
    }
}

Expected Output

70



```python
"""
Solution
"""
sampleDict = {
    "class": {
        "student": {
            "name": "Mike",
            "marks": {
                "physics": 70,
                "history": 80
            }
        }
    }
}

print(sampleDict['class']['student']['marks']['physics'])
```

    70


#####Q4 Initialize dictionary with default values

employees = ['Kelly', 'Emma']

defaults = {"designation": 'Developer', "salary": 8000}

Expected Output

{'Kelly': {'designation': 'Developer', 'salary': 8000},
'Emma': {'designation': 'Developer', 'salary': 8000}}



```python
"""
Solution
"""
employees = ['Kelly', 'Emma']
defaults = {"designation": 'Developer', "salary": 8000}

res = dict.fromkeys(employees, defaults)
print(res)


```

    {'Kelly': {'designation': 'Developer', 'salary': 8000}, 'Emma': {'designation': 'Developer', 'salary': 8000}}


#####Q5 Create a dictionary by extracting the keys from a given dictionary

sample_dict = {
    "name": "Kelly",
    "age": 25,
    "salary": 8000,
    "city": "New york"}

Keys to extract

keys = ["name", "salary"]

Expected output:

{'name': 'Kelly', 'salary': 8000}



```python
"""
Solution
"""
sampleDict = { 
  "name": "Kelly",
  "age":25, 
  "salary": 8000, 
  "city": "New york" }

keys = ["name", "salary"]

newDict = {k: sampleDict[k] for k in keys}
print(newDict)
```

    {'name': 'Kelly', 'salary': 8000}


####**1.1.7 Indexing in Python**

Since we have learnt about the various data types, let us move on to learning how to index & slice them to retrieve our relevant data.

**List**




```python
my_list = ['a', 'b', 'c', 'd'] 

#Indexing starts from 0
```


```python
my_list[1]
```




    'b'




```python
my_list[1:]

#Prints from the X:Y with X being included and Y excluded.
```




    ['b', 'c', 'd']




```python
nest = [1,2,3,[4,5,['target']]]
```


```python
nest[3][2][0]

#Retrieving data from a nested List
```




    'target'



**String**


```python
s = "Hey there! I'm learning Python!"
```


```python
s[0:3]

#Extracting Hey
```




    'Hey'




```python
s.split()
```




    ['Hey', 'there!', "I'm", 'learning', 'Python!']



**Dictionary**


```python
d = {'key1':'item1','key2':'item2'}
```


```python
d['key2']
```




    'item2'



#####Q1 Replace list’s item with new value if found, replace only first occurance
Replace 20 with 200

list1 = [5, 10, 15, 20, 25, 50, 20]

Expected output:

[5, 10, 15, 200, 25, 50, 20]


```python
"""
Solution
"""
#Solution

list1 = [5, 10, 15, 20, 25, 50, 20]

# get the first occurrence index
index = list1.index(20)

# update item present at location
list1[index] = 200
print(list1)
```

    [5, 10, 15, 200, 25, 50, 20]


#####Q2 Remove all occurrences of a specific item from a list.
Remove 20

list1 = [5, 20, 15, 20, 25, 50, 20]

Expected Output 

[5, 15, 25, 50]



```python
"""
Solution
"""
#Solution 1
list1 = [5, 20, 15, 20, 25, 50, 20]

def remove_value(sample_list, val):
    return [i for i in sample_list if i != val]

res = remove_value(list1, 20)
print(res)

#Solution 2
list1 = [5, 20, 15, 20, 25, 50, 20]

while 20 in list1:
    list1.remove(20)
print(list1)
```

    [5, 15, 25, 50]
    [5, 15, 25, 50]


#####Q3 Get the key of a minimum value from the following dictionary

sample_dict = {
  'Physics': 82,
  'Math': 65,
  'history': 75
}

Expected Output

Math



```python
"""
Solution
"""
sample_dict = {
    'Physics': 82,
    'Math': 65,
    'history': 75
}
print(min(sample_dict, key=sample_dict.get))
```

    Math


#####Q4 Change value of a key in a nested dictionary

Change Brad's Salary to 8500

sample_dict = {
    'emp1': {'name': 'Jhon', 'salary': 7500},
    'emp2': {'name': 'Emma', 'salary': 8000},
    'emp3': {'name': 'Brad', 'salary': 500}
}

Expected Output

{
   'emp1': {'name': 'Jhon', 'salary': 7500},
   'emp2': {'name': 'Emma', 'salary': 8000},
   'emp3': {'name': 'Brad', 'salary': 8500}
}



```python
"""
Solution
"""
sample_dict = {
    'emp1': {'name': 'Jhon', 'salary': 7500},
    'emp2': {'name': 'Emma', 'salary': 8000},
    'emp3': {'name': 'Brad', 'salary': 6500}
}

sample_dict['emp3']['salary'] = 8500
print(sample_dict)


```

    {'emp1': {'name': 'Jhon', 'salary': 7500}, 'emp2': {'name': 'Emma', 'salary': 8000}, 'emp3': {'name': 'Brad', 'salary': 8500}}


#####Q5 Find the last position of a given substring

find the last position of a substring “Emma” in a given string.

str1 = "Emma is a data scientist who knows Python. Emma works at google."


Expected output:

Last occurrence of Emma starts at index 43




```python
"""
Solution
"""
str1 = "Emma is a data scientist who knows Python. Emma works at google."
print("Original String is:", str1)

index = str1.rfind("Emma")
print("Last occurrence of Emma starts at index:", index)
```

    Original String is: Emma is a data scientist who knows Python. Emma works at google.
    Last occurrence of Emma starts at index: 43


####**1.1.8 What can various Data Types do?**

Each of the basic data types can do a variety of things. Here is a list of the data types
we’ve learned about so far, followed by examples of the kinds of actions you can tell
them to do:

• Strings
1. Change case
2.  Strip space off the end of a string 
3. Split a string

• Integers and decimals
1. Add and subtract
2. Simple math

• Lists
1. Add to or subtract from the list
2. Remove the last item of the list
3. Reorder the list
4. Sort the list

• Dictionaries
1. Add a key/value pair
2. Set a new value to the corresponding key
3. Look up a value by the key

###**1.2 Defining Functions**

Just like the pre-defined functions in python, we can also define our own functions in python to reduce the load of our code and avoid writing the same chunk of code again & again. 

The format for the same: 


```python
def my_func(param1='default'):
    """
    Docstring goes here.
    """
    print(param1)
```


```python
my_func()
```

    default



```python
my_func('new param')
```

    new param


Now that we know how this works, let's define a function to return the square of a number. 


```python
def square(x):
    return x**2
```


```python
out = square(5)
```


```python
print(out)
```

    25




#####Q1 Create a function in Python

Write a program to create a function that takes two arguments, name and age, and print their value.


```python
"""
Solution
"""
def func1(name, age):
    print(name, age)

func1("Ben", 25)
```

    Ben 25


#####Q2 Create a function with variable length of arguments

Write a program to create function func1() to accept a variable length of arguments and print their value.

Note: Create a function in such a way that we can pass any number of arguments to this function and the function should process them and display each argument’s value.

.

Output

call function with 3 arguments

func1(20, 40, 60)

call function with 2 arguments

func1(80, 100)


Printing values

20

40

60


Printing values

80

100



```python
"""
Solution
"""
def func1(*args):
    for i in args:
        print(i)

func1(20, 40, 60)
func1(80, 100)
```

    20
    40
    60
    80
    100


#####Q3 Return multiple values from a function

Write a program to create function calculation() such that it can accept two variables and calculate addition and subtraction. Also, it must return both addition and subtraction in a single return call.

def calculation(a, b):
    # Your Code

res = calculation(40, 10)
print(res)

Expected Output

50, 30



```python
"""
Solution
"""
#Solution 1
def calculation(a, b):
    addition = a + b
    subtraction = a - b
    return addition, subtraction

res = calculation(40, 10)
print(res)

#Solution 2
def calculation(a, b):
    return a + b, a - b

# get result in tuple format
# unpack tuple
add, sub = calculation(40, 10)
print(add, sub)
```

    (50, 30)


#####Q4 Create a function with default argument

Write a program to create a function show_employee() using the following conditions.

- It should accept the employee’s name and salary and display both.

- If the salary is missing in the function call then assign default value 9000 to salary

showEmployee("Ben", 12000)

showEmployee("Jessa")

Expected Output

Name: Ben salary: 12000
Name: Jessa salary: 9000


```python
"""
Solution
"""

def show_employee(name, salary=9000):
    print("Name:", name, "salary:", salary)

show_employee("Ben", 12000)
show_employee("Jessa")


```

    Name: Ben salary: 12000
    Name: Jessa salary: 9000


#####Q5 Create an inner function to calculate the addition in the following way

- Create an outer function that will accept two parameters, a and b
- Create an inner function inside an outer function that will calculate the addition of a and b
- At last, an outer function will add 5 into addition and return it





```python
"""
Solution
"""

# outer function
def outer_fun(a, b):

    # inner function
    def addition(a, b):
        return a + b

    # call inner function from outer function
    add = addition(a, b)
    # add 5 to the result
    return add + 5

result = outer_fun(5, 10)
print(result)
```

    20


###**1.3 Exercises**

#####Q1 Use Python to calculate 7 to the power of 4?


```python
#Write your code here


```

#####Q2 Split this string into a list.


```python
s = "Hi there Sam!"
```


```python
#Write your code here
```

#####Q3 Given the variables, use *format()* to print the following string:



```python
planet = "Earth"
diameter = 12742
```


```python
#Print


```

#####Q4 Given this nested list, use indexing to grab the word "hello"


```python
lst = [1,2,[3,4],[5,[100,200,['hello']],23,11],1,7]
```


```python
#Write your code here


```

#####Q5 Given this nest dictionary grab the word "hello". Be prepared, this will be tricky.


```python
d = {'k1':[1,2,3,{'tricky':['oh','man','inception',{'target':[1,2,3,'hello']}]}]}
```


```python
#Write your code here


```

#####Q6 Create a function that grabs the email website domain 
from a string in the form:

    user@domain.com
    
So for example, passing "user@domain.com" would return: domain.com


```python
#Write your code here

def domainGet(email):
    return email.split('@')[-1]
```


```python
domainGet('user@domain.com')
```




    'domain.com'



#####Q7 Create a basic function that returns True if the word 'dog' is contained in the input string. Don't worry about edge cases like a punctuation being attached to the word dog, but do account for capitalization.


```python
#define your function here

def findDog(st):
    return 'dog' in st.lower().split()
```


```python
findDog('Is there a Dog here?')
```




    True



#####Q8 Create a function that counts the number of times the word "dog" occurs in a string. Again ignore edge cases.


```python
#define ypur function here

def countDog(st):
    count = 0
    for word in st.lower().split():
        if word == 'dog':
            count += 1
    return count
```


```python
countDog('This dog runs faster than the other dog dude!')
```




    2



Let's complete this module with a tricky question. Don't worry if you're not able to solve it right now, eventually you'll be able to. 

#####Q9 **Final Problem**

You are driving a little too fast, and a police officer stops you. Write a function
  to return one of 3 possible results: "No ticket", "Small ticket", or "Big Ticket". 
  If your speed is 60 or less, the result is "No Ticket". If speed is between 61 
  and 80 inclusive, the result is "Small Ticket". If speed is 81 or more, the result is "Big    Ticket". Unless it is your birthday (encoded as a boolean value in the parameters of the function) -- on your birthday, your speed can be 5 higher in all 
  cases.


```python
#Define your function here

def caught_speeding(speed, is_birthday):
    
    if is_birthday:
        speeding = speed - 5
    else:
        speeding = speed
    
    if speeding > 80:
        return 'Big Ticket'
    elif speeding > 60:
        return 'Small Ticket'
    else:
        return 'No Ticket'
```


```python
caught_speeding(81,True)
```




    'Small Ticket'




```python
caught_speeding(81,False)
```




    'Big Ticket'



**Great Job!**
