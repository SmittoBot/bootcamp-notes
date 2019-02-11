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

## Django
* Django overview:
  * User requests a URL
  * This goes to `urls.py` file, which calls `views.py` file
  * This calls `models.py`, which interacts with database and feeds back to `views.py`
  * views.py uses html/css/js templates to fill out view, then sent back to user
