## Python for Bankers
----
### aka 
Using python and other languages to do analysis and build cool things and no longer being locked down by manual work in Microsoft products that are not repeatable, maintainable or scalable.
----
### Who is this for? 
You, if: 
* Your available tools are limited to Excel + Powerpoint, but you want something more powerful
* You've heard that Python is basically the coolest thing since the Chipotle burrito
* You studied computer science, engineering, math...or philosophy, Spanish, or pre-law...or didn't go to college. Really, as long as you want to learn to code, you can
----
### What we want to cover:
* A minimal overview of the language itself, but just to understand what the foundational concepts are. For syntax and more, Google is your friend
* Really understanding how other programming languages differ from Microsoft's VBA 
* (Most of our time) Walking through some real world examples of writing code to get data, transform data, and do analysis
----
### Topics:
1. Why is programming awesome?
2. A minute on VBA 
3. The Python story
4. Python language basics
5. Use cases
    1. Working with data from Yahoo finance/Cool graphs
    2. Data feeds from APIs: Quandl
    3. Web scraping/Information Retrieval
    4. Basic Machine Learning: Handwritten digit recognition
----
#### Why is programming awesome? 

* You can build something real. Charts, websites, apps, write code that analyzes huge amounts of data. 
* You're telling the computer exactly what to do. Going from VBA->Python->C, you're getting closer and closer to the bare metal of a computer. Controlling what is happening on a CPU with threads and processes, understanding how data is stored in memory and caches, down to the actual instructions run on different CPU architectures. 

----

* View the world and your work through a very objective lens. Code either compiles or it doesn't. It passes test cases or doesn't. There is a strong sense of objectivity and order in programming not found in anything else
* Share your code with communities around the world on Github/Gitlab, create open source projects, see your code reused, contribute to other projects. 
----
* And you can literally start programming on almost any modern computer. 
![img](./img/js_chrome.png)
Search for "Dev Tools" in Chrome to write some javascript

----
If you have a Mac, look for "Terminal" in Applications. Python is installed on all Linux operating systems (and therefore on Macs as well)

![img](./img/python_terminal.png) <!-- .element height="80%" width="80%" -->
----
### A minute on VBA
Visual Basic for Applications (VBA) is quite amazing within the context of Microsoft applications. There are many solid concepts from mainstream programming that lives in VBA. 

Bankers especially are notorious for squeezing everything possible out of VBA to automate workflows, analysis, chart creation, etc
----
### The good of VBA 
* Object oriented programming: All MS charts, cells, etc are objects with various attributes and other objects within. This is good
* For data, starting to think about using code to manipulate sequences of data, instead of dragging and button clicking
----
### The bad of VBA
* Tightly coupled to Microsoft apps. Hard to learn how code can be used in other contexts
* Not easy to develop, version control and test. Code is in Microsoft viewer in Excel/Powerpoint/Word. 
* (Important) When working with data, too often is data treated as unbounded arrays of data in Excel tables, with hard references to cells that can easily change ($B$5?)
----
### Move from this
![img](./img/vba.png) <!-- .element height="80%" width="80%" -->

----
### To this:
![img](./img/jupyter.png) <!-- .element height="70%" width="70%" -->


----
### The story of Python

https://en.wikipedia.org/wiki/Python_(programming_language)

----
### A few details
* Interpreted and high level (unlike Java, C, C++, etc)
* Written in C and can create C extensions
* "Batteries included": Very big standard library to get lots of things done quickly
* Easy to learn syntax: Has created massive community of new programmers
* Huge contributor community: There is a python package for just about anything

----
### Python basics: How to run

Mac/Linux:
```
$ python3
Python 3.7.3 (v3.7.3:ef4ec6ed12, Mar 25 2019, 16:52:21) 
[Clang 6.0 (clang-600.0.57)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> print("hello world")
hello world
>>> 
```
----
#### Running on Windows (probably your case)
The awesome folks at anaconda.com have a Python distribution that includes Python itself, a large number of common packages you'll most likely need, as well as a shell for Windows. 

Download the Anaconda distribution and open the "Anaconda prompt"
```
(base) C:\>python
Python 3.7.0 (default, June 2018, 08:04:48) [MSC v.1912 64bit (AMD64)] :: Anaconda, Inc. on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> print("hello world")
hello world
>>> 
```
----
#### Python basic syntax

* Basic types: `str`, `int`, `float`, `bool`, `list`, `set`, `dict`
* Functions: `def`
* Classes: `class`


#### Basic types

```
>>> a = 1
>>> b = 3
>>> type(a)
'<class 'int'>
>>> a+b
4
>>> a/b
0.3333333333333333
```


#### Strings
```
>>> test_string = 'Hello World'
>>> len(test_string)
11
>>> test_string.upper()
'HELLO WORLD'
>>> test_string.lower()
'hello world'
>>> test_string.replace('World', 'Galaxy')
'Hello Galaxy'
```


#### Cooler things with strings: Pattern matching

Find all the phone numbers in this text: 

> Please contact me at my office number (212-111-0909) 
or call my cell at 101-093-6543. 
If you can't reach those, 
call my manager at 212-546-1123

Create a search pattern for these phone numbers and use python's `re` library (Regular Expression) to find all matching strings


```
>>> text = '''Please contact me at my office number (212-111-0909) 
or call my cell at 101-093-6543. If you can't reach those, 
call my manager at 212-546-1123'''
# triple quotes can be used for multiline strings...
# this is a comment btw
>>> import re
>>> re.findall(r'\d{3}\-\d{3}\-\d{4}', text)
['212-111-0909', '101-093-6543', '212-546-1123']

# \d{3}\-\d{3}\-\d{4} is our pattern
# \d{3} says to match 3 consecutive numbers
# \- matches a normal hyphen. A - is a special char, 
# hence the leading \
````


### The List!

```
>>> [0,1,2,3,4,5]
[0, 1, 2, 3, 4, 5]
>>> list(range(6))
[0, 1, 2, 3, 4, 5]
>>> [i for i in range(100) if i%17==0]
[0, 17, 34, 51, 68, 85]
>>> 'strings can be split into lists of other strings'.split()
['strings', 'can', 'be', 'split', 'into', 'lists', 'of', 'other', 'strings']

>>> my_list = [1,2,3]
>>> my_list.append(4)
>>> my_list
[1, 2, 3, 4]
```


### The Dictionary
* A `dict` is a mapping of keys to values (think of how you use vlookup, but way more powerful)

```
>>> tickers = {"ford": 'F', "google": "GOOGL", 
               "microsoft": "MSFT", "tesla": "TSLA"}
>>> tickers['ford']
'F'
>>> tickers['aol']
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'aol'
>>> tickers.items()
dict_items([('ford', 'F'), ('google', 'GOOGL'), 
('microsoft', 'MSFT'), ('tesla', 'TSLA')])
```


### Manipulating data

Print tickers with price over $200

```
>>> prices = {"TSLA": 219, "MSFT": 134, "F": 9, "GOOGL": 1164}
>>> for ticker, price in prices.items():
        if price > 200:
            print(ticker)
TSLA
GOOGL
```
Ok, but not very "pythonic"


Better
```
>>> [name for name in prices if prices[name] > 200]
['TSLA', 'GOOGL']
```
Slightly more complex but also good
```
>>> list(filter(lambda name: prices[name] > 200, prices))
['TSLA', 'GOOGL']
```
