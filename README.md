# Python 3

# Table of Contents
-[Control Flow]


## Control Flow
### While Loops
```py
c = 5
while c != 0:
    print(c)
    c -= 1
```
### Break
```py
while True: #Infinite loop.
    response = input()
    if int(response) % 7 == 0:
        break
```
## Strings, Collections and Iterations
### Strings and String Literals
Be aware of escape functions. Use r (raw) if need be, ie. path = r"C:etc/etc/etc"
```py
/n #New line.
string = "This is a string with a /n new line"

string.capitalize() #One of type string's functions.
```
### List
```py
list = [3,4,"Daniel"]
list.append("rich")

list("Rich")
#returns ["r","i","c","h"]
```
### Dictionary
Dictionaries map keys to value
```py
d = {'daniel':37,'maike':29}
d['daniel'] #Returns 37
d['maike']=30 #Updates the value to 30 from 29

### Bytes
Bytes are like strings. b'string'. To change bytes to string
```py
from urllib.request import urlopen
story = urlopen('http://sixty-north.com/c/t.txt')
story_words = []
for line in story:
    line_words = line.decode('utf-8').split() #.decode('utf-8') will decode bytes to string.
    for word in line_words:
        story_words.append(word)
story.close()
story_words
```
## Modularity
### __name__
Python set the value of dunder name differently depending on how the module is being used (importing or executing). Use the following under the function in the .py file.
```py
if __name__ == '__main__':
    fetch_words()
```
It is best practice to define a module (a .py file) with this so it can be imported to the Python REPL without running immediately, as __name__ == '__name__' in REPL. Imported to a text editor __name__ == '__main__'.
## Objects and Types
1. Python uses dynamic typing, ie., you dont have to declare the type.
2. Pythin uses strong typing, ie., types are not coerced to match.
3. dir() will give a list of object attributes.
4. __name__ is the name of the object.
5. __doc__ is the doc string of the object.
6. Strings have a repitition operation, *. String * integer will return copies of the string.

To see if objects are equivalent, ie., have the same value:
```py
a == b
```
To see if objects have the same reference, ie., name tag, use:
```py
a is b
```
### Function Arguments and Defaults
Args with defaults must be list after args without defaults.
```py
def banner(message, border='-') # Border has a default set.
    line = border * len(message)
    print(line)
    print(message)
    print(line)
    
>>>banner('Norwegian Blue')
>>>--------------
   Norwegian Blue
   --------------
```
Positional arguments can be placed in the defined order without specifing a key. Alternatively, referring to above, one could call banner(border='*', message = 'New Zealand'). Keys must be placed AFTER any positional arguments.
#### Mutable Default Values
Default values are only called once, so a default list that has values added to it will inherit these when using the function again. Solution: only use IMMUTABLE default values! ..Such as integers and strings. Use None in place of a list if suitable:
```py
def add_spam(menu=None)
    if menu = None:
        menu = []
        menu.append('spam')
        return menu
```
### Type Systems
```py 
def add(a, b):
    return a + b
```
This will return a + b regardless of type, but will not add different types.
### Scopes
Names are looked up in the narrowest relevant context: The LEGB rule
1. Local
2. Enclosing
3. Global
4. Built in

Rebinding global names:
```py
count = 0
def set_count(c):
    global count
    count = c
def show_count()
    print(count)
```
By using global count, when setting the count with set_count, the global count, i.e., count = 0 will change.
### Everything is an object
This can be seen by using the type() function on anything.
## Built in Collections
### Tuples
Immutable. 
```py
t = (67, 'this is a tuple', 2)

t1 = (('this is a nested tuple', 16), (67, 'this is a tuple', 2))
t[1][2] # This indexing returns 2

t = (341,) # To create a single entry tuple you must set a comma.
t = () # Although, this is how to make an empty tuple (no comma).

t = 1,2,3,4,5,6 # Returns a tuple (1,2,3,4,5,6), ie., brackets can be omitted.

def minmax(items)
    return min(items), max(items) # Returns (min, max) in a tuple.
```
#### Tuple Unpacking!
```py
lower, upper = minmax([34, 45, 12, 56, 78]) # lower returns 12, upper returns 78

(a, (b, (c,d))) = (4, (3, (2,1))) # a returns 4, b returns 3 etc.
```
#### Tuple Swapping
```py
a = 'jelly'
b = 'bean'
a, b = b, a # a returns 'bean', b 'jelly'
```
#### Create Tuple
```py
tuple('Shane') # Returns ('S','h','a','n','e')
```
#### in not in
```py
5 in (3,4,5,6,7) # Returns True
5 not in (3,4,5,6,7) # Returns False
```
### Strings
```py
'new' + 'found' + 'land' # Returns 'newfoundland'
# Better to use join() on extensive concatenation as + methods creates lots of temporaries.

#join() can also:

colors = ';'.join(['#45ff23', '#2321fa']) # Returns '#45ff23 ; #2321fa'
name = ' '.join(['Shane', 'Daniel', 'Rich']) # Returns 'Shane Daniel Rich'
```
##### Partition
```py
'unforgetable'.partition('forget') # Returns ('un', 'forget', 'able')
# Is often used with unpacking
departure, seperator, arrival = 'London:Edinburgh'.partition(':') # departure returns 'London', etc.
departure, _, arrival = 'London:Edinburgh'.partition(':') # Convention is to use _ for unused or dummy values, some Pythons programs with look for these underscores.
```
##### format() and f strings
In f strings f is placed at before the start of the string.
```py
'The age of {0} is {1}. {0} is a {occ[0]}'.format('Jim', 24, occ=('pilot', 'banker'))

import math
'Math constants: pi={m.pi:.3f}, e={m.e:.3f}'.format(m=math) # Three decimal places :.3f

f'Math constants: pi={m.pi:.3f}, e={m.e:.3f}'

value = 4 * 20
f'The value is {value}.'
```
### range() and enumerate()
```py
for i in range(5):
range(5) # Retruns range(0,5), ie., type range.
list(range(0, 10, 2)) # Returns a list with a 2 step, [0,2,4,6,8]

# Enumerate places the values in tuples with the index.
t = [2, 3, 6, 76]
for i, v in enumerate(t): # Unpacking with enumerate.
    print(f'i = {i}, v = {v}')
```
### Lists
#### Negative indices
Ie., list[-1] or list[-2] will refer to the last and seconds last item in the list.
#### Slicing and Soft Copying
```py
a_list[start:stop]
list = [1,2,3,5]
print(list[2:]) # Returns [3,5]
# The below are soft copies, in that they create a copy of the references but the items mutated, for example with an append(). Rebinding, ie replacing the list will stop this. 
list2 = list[:] # Where list is list2 is False but where list == list2, BUT, items are updated in both.
list2 = list.copy() # A more readable way to copy.
list2 = list(list) # Best way to copy, as any iterable series as a source can be passed, not just lists.
# See below:
list2 = [[9,8,7],[1,2,3]]
list5 = list2[:]
list5[1] = [99,88,77] # This rebinds and creates a new object in [1] that is not the same as list2.
list2[1].append(1000) # 1000 will therefore only be appended to list2[1]
list5[0].append(2000) # The object at [0] is still the same object in both lists, so an append of 2000 will appear in both lists.
print(list2)
print(list5)
```
#### index()
```py
w = 'the fox jumped over the dog'.split() # Returns a list of words split by a comma.
i = w.index('fox') # Searching through list for a match and returns index.
print(i)
w.count('the') # Returns 2
```
#### delete, del or remove() and insert(), extend()
```py
del list[0]
list.remove('fox')

list.insert(2, 'sheep') # Insert 'sheep' at index 2.
list.extent(['duck', 'bird']) # Adds these two items to the end of the list.
```
#### Rearranging a list, reverse(), sort() and sort(key=)
Reverse is self explanatory.
```py
list.sort(reverse=True) # Decending order. 
list.sort() # Default is acending order.
list.sort(key=len) # Sorts by length.
```
#### sorted() and reversed() 
1. They have the advantage of working on any finite iterable source object (ie., not just lists). 
2. sorted() create a new list object that is sorted, wheras reversed creates a list_reverseiterator object that can be converted to a list using the list() function.
```py
list = [1,2,6,8]
list2 = reversed(list) # Creates a list_reverseiterator object.
list(list2) # Create list and return [8,6,2,1]
```
### Dictionaries

## Pandas and Geopandas
### Functions
```py
df.apply() #Functions
```
## File and Paths
```py
from pathlib import Path

data_folder = Path("source_data/text_files/")

file_to_open = data_folder / "raw_data.txt" # If you want to add on to the path, you can use the / operator directly in your code.

print(file_to_open.read_text())


if not filename.exists():
    print("Oops, file doesn't exist!")
else:
    print("Yay, the file exists!")
```
To make paths compatible in all operating systems (windows uses the opposite slash to everythin else) use:
```py
from pathlib import Path

filename = Path("source_data/text_files/raw_data.txt")
```
Here’s an example that will open a local file in your web browser with just two lines a code:
```py
from pathlib import Path
import webbrowser

filename = Path("source_data/text_files/raw_data.txt")

webbrowser.open(filename.absolute().as_uri())
```
```py
from pathlib import Path

file_name = Path(file_path).name  # myfile.png
file_stem = Path(file_path).stem  # myfile
```
