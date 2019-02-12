# Python/Django Full Stack Development

## Python
* Anaconda distribution: comes pre-packaged with additional useful libraries
* Miniconda: smaller and lighter version of Anaconda with the essentials
* `platformio-ide-terminal`: most popular terminal package for atom
* `autocomplete-python` package in atom for python code autocompletion

### Numbers/Strings
* Numbers in python: Integers and Floating Point numbers (decimal)
* Strings: can have either `'` or `"` to wrap, use one to wrap the other
* Can refer to individual characters of a String using index notation:
```
print(mystring[0])
```
* Supports negative indexing, can use `[-1]` to get last character of String
* To get all characters including and after the 2nd index and up to the 5th:
```
print(mystring[2:5])
```
* Slicing notation starts at 2, but only goes _up to_ 5, not including it!
* Step size: to skip every other character in string do 
```
print(mystring[::2])
```
* Strings are immutable, can't redefine certain indexes, can just redefine the entire variable 
* Can use `.upper()` and `.lower()` to set case of entire string, many other methods like `.capitalize()`
* Can use the `.split()` method to split each individual word on spaces into a list:
* Can specify the particular character to split on:
```
mystring.split('o')
```
* For String interpolation and formatting:
```
x = "Item One: {x}, Item Two: {y}".format(x="Big", y="Boi")
```

### Lists/Dictionaries
* Can put different data types in a List:
```
mylist = ['big',1,'boi',2,'swag']
```
* Refer to List elements with same indexing as Strings, including slicing
* Unlike Strings, Lists are mutable, can change independent elements of them
* Can user `.append()` to add a new item to the end of the list
* To add multiple new items to the end of the list, can use `extend()` method:
```
mylist.extend(['x','y','z'])
```
* Use `.pop()` to pop off the last element of the list and return that item, can also specify the index 
* Use `.reverse()` to reverse the elements of the list, no kidding! Can also use `.sort()`, etc
* Use multiple indexes to get an element from a nested list: `list[2][1]`
* List compregension:
```
matrix = [[1,2,3],[4,5,6],[7,8,9]]
first_col = [row[0] for row in matrix]
```
* Dictionaries: Python's version of Hash Tables/Objects in JS, create mappings with key-value pairs
* Can nest dictionaries, lists etc inside one another, and then call methods on the final assignment
* Existing elements are mutable, simply add new elements with:
```
mystuff['key'] = 'value'
```
* Booleans: `True` and `False` or `1` and `0`, need the capital!
* Tuples: immutable lists, such as `(1,2,3)`, can mix data types, slicing indexing etc are same as lists
* Sets: unordered collections of unique elements, adding multiple identical elements won't change it

### Control Flow 
* No type coercion in Python, `1 == "1"` will return false 
* Logical operators are `and` and `or`
* Python stresses readability due to white space, not as much `{}`, control flow statements are keyword, statement, and `:`
```
if 4<20:
 print("beast!")
```
* Use `elif` and `else` to follow up conditionals:
```
if 1>2:
 print("beast")
elif 2>3:
 print("mode")
else:
 print("swag")
```
* For loops/iterating:
```
seq = [1,2,3,4,5,6]
for item in seq:
  print(item)
```
* Tuple unpacking, iterating through tuples:
```
mypairs = [(1,2),(3,4),(5,6)]
for (tup1,tup2) in mypairs:
  print(tup1)
  print(tup2)
```
* Use `range` to define starting num, ending num, and step size. Range is a generator (function) that incrementally makes the next element:
```
for i in range(0,20,2):
  print(i)
```
* List comprehension:
```
x = [1,2,3,4]
out = [num**2 for num in x]
```

### Functions 
* Functions are formatted in snake case, can assign parameters with default values:
```
def my_func(param1='default'):
  """
  THIS IS THE DOCSTRING
  """
  print("My first python function is {a}!).format(a=param1))
  
my_func("beast")
```
* Python automatically checks for a docstring for the function, and will often display it when autocompleting depending on your IDE
* Use `type()` keyword to check for the type of the object:
```
def add_num(num1,num2):
  if type(num1) == type(num2) == type(10):
    return num1+num2 
  else:
    return "We need INTS!!"
```
* Can use `lambda` expressions for very small functions that don't require permanent declarations:
```
mylist = [1,2,3,4,5,6,7,8]
evens = filter(lambda num: num%2 == 0,mylist)
print(list(evens))
```
* Can use the `in` function to determine if an element is in a list:
```
print('x' in [1,2,3])
```

### Scope 

## Django
* Django overview:
  * User requests a URL
  * This goes to `urls.py` file, which calls `views.py` file
  * This calls `models.py`, which interacts with database and feeds back to `views.py`
  * views.py uses html/css/js templates to fill out view, then sent back to user
