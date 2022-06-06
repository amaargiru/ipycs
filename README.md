## **Interactive Python Cheatsheet**<br>in Jupiter notebook format

You can download [IPYCS Jupiter notebook](https://github.com/amaargiru/ipycs/blob/main/PYCS.ipynb) with code cells that allows you to edit and write new code, with full syntax highlighting. The results that are returned from this computation are then displayed in the notebook as the cell’s output.

## Data structures

### List


```python
import bisect

a = []  # Empty list

a: list[int] = [10, 20]
b: list[int] = [30, 40]
a.append(50)  # Add item
b.insert(2, 60)  # Inserts item at index
print(a, b)

a += b
print(f"Add: {a}")

b = list(reversed(a))  # reversed() returns reversed iterator, not list
a.reverse()
print(f"Reverse: {a}, {b}")

b = sorted(a)  # Returns a new sorted list
a.sort()  # Modifies the list in-place and has no return value
print(f"Sort: {a}, {b}")

print(bisect.bisect(a, 20))  # Locate the insertion point for value in a list to maintain sorted order

bisect.insort(a, 12)  # Insert value in a list in sorted order
print(a)

s: str = "A whole string"
list_of_chars: list = list(s)
print(list_of_chars)
list_of_words: list = s.split()
print(list_of_words)

i: int = list_of_chars.index("w")  # Returns index of the first occurrence or raises ValueError
print(i)
list_of_chars.remove("w")  # Removes first occurrence of the item or raises ValueError
e = list_of_chars.pop(9)  # Removes and returns item at index or from the end.
print(list_of_chars, e)
a.clear()  # Removes all items
```

    [10, 20, 50] [30, 40, 60]
    Add: [10, 20, 50, 30, 40, 60]
    Reverse: [60, 40, 30, 50, 20, 10], [60, 40, 30, 50, 20, 10]
    Sort: [10, 20, 30, 40, 50, 60], [10, 20, 30, 40, 50, 60]
    2
    [10, 12, 20, 30, 40, 50, 60]
    ['A', ' ', 'w', 'h', 'o', 'l', 'e', ' ', 's', 't', 'r', 'i', 'n', 'g']
    ['A', 'whole', 'string']
    2
    ['A', ' ', 'h', 'o', 'l', 'e', ' ', 's', 't', 'i', 'n', 'g'] r
    

### Dictionary


```python
d = {}  # Empty dictionary

d: dict[str, str] = {"Italy": "Pizza", "US": "Hot-Dog", "China": "Dim Sum"}  # Creates a dictionary

k = ["Italy", "US", "China"]  # Creates a dictionary from two collections
v = ["Pizza", "Hot-Dog", "Dim Sum"]
d = dict(zip(k, v))

k = d.keys()  # Collection of keys that reflects changes
v = d.values()  # Collection of values that reflects changes
k_v = d.items()  # Collection of key-value tuples that reflects changes

print(d)
print(k)
print(v)
print(k_v)

print(f"Mapping: {k.mapping['Italy']}")

d.update({"China": "Dumplings"})  # Adds item or replace one with matching keys
print(f"Replace item: {d}")

c = d["China"]  # Read value
print(f"Read item: {c}")

try:
    v = d.pop("Spain")  # Removes item or raises KeyError
except KeyError:
    print("Dictionary key doesn't exist")

b = {k: v for k, v in d.items() if "a" in k}  # Returns a dictionary, filtered by keys
print(b)
c = {k: v for k, v in d.items() if len(v) >= 7}  # Returns a dictionary, filtered by values
print(c)

d.clear() # Removes all items
```

    {'Italy': 'Pizza', 'US': 'Hot-Dog', 'China': 'Dim Sum'}
    dict_keys(['Italy', 'US', 'China'])
    dict_values(['Pizza', 'Hot-Dog', 'Dim Sum'])
    dict_items([('Italy', 'Pizza'), ('US', 'Hot-Dog'), ('China', 'Dim Sum')])
    Mapping: Pizza
    Replace item: {'Italy': 'Pizza', 'US': 'Hot-Dog', 'China': 'Dumplings'}
    Read item: Dumplings
    Dictionary key doesn't exist
    {'Italy': 'Pizza', 'China': 'Dumplings'}
    {'US': 'Hot-Dog', 'China': 'Dumplings'}
    

### defaultdict

The *defaultdict* will create any items that you try to access (provided of course they do not exist yet) without throws a KeyError.


```python
from collections import defaultdict

dd = defaultdict(int)  # defaultdict
print(dd[10])  # print int(), thus 0

dd = {}  # "Regular" dictionary
# print(dd[10])  # throws KeyError
```

    0
    

### Counter

A Counter is a dict subclass for counting hashable objects, it is a collection where elements are stored as dictionary keys and their counts are stored as dictionary values.


```python
from collections import Counter

shirts_colors = ["red", "white", "blue", "white", "white", "black", "black"]
c = Counter(shirts_colors)
print(c)

c["blue"] += 1
print(f"After shopping: {c}")
```

    Counter({'white': 3, 'black': 2, 'red': 1, 'blue': 1})
    After shopping: Counter({'white': 3, 'blue': 2, 'black': 2, 'red': 1})
    

### Set


```python
big_cities: set["str"] = {"New-York", "Los Angeles", "Ottawa"}
american_cities: set["str"] = {"Chicago", "New-York", "Los Angeles"}

big_cities |= {"Sydney"}  # Add item (or you can use add())
american_cities |= {"Salt Lake City", "Seattle"}  # Add set (or you can use update())

print(big_cities, american_cities)

union_cities: set["str"] = big_cities | american_cities  # Or union()
intersected_cities: set["str"] = big_cities & american_cities  # Or intersection()
dif_cities: set["str"] = big_cities - american_cities  # Or difference()
symdif_cities: set["str"] = big_cities ^ american_cities  # Or symmetric_difference()

issub: bool = big_cities <= union_cities  # Or issubset()
issuper: bool = american_cities >= dif_cities  # Or issuperset()

print(union_cities)
print(intersected_cities)
print(dif_cities)
print(symdif_cities)

print(issub, issuper)

big_cities.add("London")  # Add items

big_cities.remove("Ottawa")  # Removes an item from the set if it is present or raises KeyError
big_cities.discard("Los Angeles")  # Remove an item from the set if it is present without raising KeyError
big_cities.pop()  # Remove and return a random item from the set or raises KeyError
big_cities.clear()  # Removes all items from the set
```

    {'New-York', 'Ottawa', 'Sydney', 'Los Angeles'} {'New-York', 'Chicago', 'Seattle', 'Salt Lake City', 'Los Angeles'}
    {'Chicago', 'Salt Lake City', 'New-York', 'Ottawa', 'Seattle', 'Los Angeles', 'Sydney'}
    {'New-York', 'Los Angeles'}
    {'Ottawa', 'Sydney'}
    {'Ottawa', 'Chicago', 'Seattle', 'Salt Lake City', 'Sydney'}
    True False
    

### Frozen Set

Frozen set is just an immutable and hashable version of a set object. Frozen set can be used as key in Dictionary or as element of another set.


```python
s = frozenset({"New-York", "Los Angeles", "Ottawa"})
```

### Tuple  
Tuple is an immutable and hashable list


```python
a = (2, 3)
b = ("Boson", "Higgs", 1.56e-22)

print(a, b)
```

    (2, 3) ('Boson', 'Higgs', 1.56e-22)
    

### Named Tuple
Subclass of tuple with named elements


```python
from collections import namedtuple

rectangle = namedtuple('rectangle', 'length width')
r = rectangle(length = 1, width = 2)

print(r)
print(r.length)
print(r.width)
print(r._fields)
```

    rectangle(length=1, width=2)
    1
    2
    ('length', 'width')
    

### Enum


```python
from enum import Enum, auto
import random

class Currency(Enum):
    euro = 1
    us_dollar = 2
    yuan = auto()

# If there are no numeric values before auto(), it returns 1, otherwise it returns an increment of the last numeric value

local_currency = Currency.us_dollar  # Returns a member
print(local_currency)

local_currency = Currency["us_dollar"]  # Returns a member or raises KeyError
print(local_currency)

local_currency = Currency(2)  # Returns a member or raises ValueError
print(local_currency)

print(local_currency.name)
print(local_currency.value)

list_of_members = list(Currency)
member_names    = [e.name for e in Currency]
member_values   = [e.value for e in Currency]
random_member   = random.choice(list(Currency))

print(list_of_members, "\n",
      member_names, "\n",
      member_values, "\n",
      random_member)
```

    Currency.us_dollar
    Currency.us_dollar
    Currency.us_dollar
    us_dollar
    2
    [<Currency.euro: 1>, <Currency.us_dollar: 2>, <Currency.yuan: 3>] 
     ['euro', 'us_dollar', 'yuan'] 
     [1, 2, 3] 
     Currency.us_dollar
    

### Range


```python

r1: range = range(11)  # Creates a sequence of numbers from 0 to 10
r2: range = range(5, 21) # Creates a sequence of numbers from 5 to 20
r3: range = range(20, 9, -2)  # Creates a sequence of numbers from 20 to 10 with step 2

print("To exclusive: ", end="")
for i in r1:
  print(f"{i} ", end="")

print("\nFrom inclusive to exclusive: ", end="")
for i in r2:
  print(f"{i} ", end="")

print("\nFrom inclusive to exclusive with step: ", end="")
for i in r3:
  print(f"{i} ", end="")

print(f"\nFrom = {r3.start}")
print(f"To = {r3.stop}")
```

    To exclusive: 0 1 2 3 4 5 6 7 8 9 10 
    From inclusive to exclusive: 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 
    From inclusive to exclusive with step: 20 18 16 14 12 10 
    From = 20
    To = 9
    

### Dataclass  
Decorator that automatically generates init(), repr() and eq() special methods


```python
from dataclasses import dataclass
from decimal import *
from datetime import datetime

@dataclass
class Transaction:
    value: Decimal
    issuer: str = "Default Bank"
    dt: datetime = datetime.now()

t1 = Transaction(value=1000_000, issuer="Deutsche Bank", dt = datetime(2022, 1, 1, 12))
t2 = Transaction(1000)

print(t1)
print(t2)
```

    Transaction(value=1000000, issuer='Deutsche Bank', dt=datetime.datetime(2022, 1, 1, 12, 0))
    Transaction(value=1000, issuer='Default Bank', dt=datetime.datetime(2022, 5, 26, 17, 56, 14, 318575))
    

Objects can be made immutable with *frozen=True*.


```python
from dataclasses import dataclass

@dataclass(frozen=True)
class User:
    name: str
    account: int

```

### Deque

A thread-safe list with efficient appends and pops from either side.


```python
from collections import deque
d = deque([1, 2, 3, 4], maxlen=1000)

d.append(5)  # Add element to the right side of the deque
d.appendleft(0)  # Add element to the left side of the deque by appending elements from iterable

d.extend([6, 7])  # Extend the right side of the deque
d.extendleft([-1, -2])  # Extend the left side of the deque
print(d)

a = d.pop()  # Remove and return an element from the right side of the deque. Can raise an IndexError
b = d.popleft()  # Remove and return an element from the left side of the deque. Can raise an IndexError
print(a, b)
print(d)
```

    deque([-2, -1, 0, 1, 2, 3, 4, 5, 6, 7], maxlen=1000)
    7 -2
    deque([-1, 0, 1, 2, 3, 4, 5, 6], maxlen=1000)
    

### Queue

The queue module implements multi-producer, multi-consumer FIFO queues. It is especially useful in threaded programming when information must be exchanged safely between multiple threads. For LIFO queue use LifoQueue. For a priority queue use PriorityQueue.


```python
from queue import Queue
q = Queue(maxsize=1000)

q.put("eat", block=True, timeout=10)  # Put an element to the queue with 10 seconds timeuot, block if necessary until a free slot is available
q.put("sleep")  # Default values block=True, timeout=None
q.put("code")
q.put_nowait("repeat")  # Equivalent to put("repeat", block=False). Put an element on the queue if a free slot is immediately available, else raise the queue.Full exception
print(q.queue)

a = q.get(block=True, timeout=10)  # Remove and return an item from the queue
b = q.get()  # Default values block=True, timeout=None
c = q.get_nowait()  # Equivalent to get(False)
print(a, b, c, q.queue)
```

    deque(['eat', 'sleep', 'code', 'repeat'])
    eat sleep code deque(['repeat'])
    

### Array  
Object type that can only hold numbers of a predefined type.


```python
from array import array

a1 = array("l", [1, 2, 3, -4])  # Array from collection of numbers
a2 = array("b", b"1234567890")  # Array from bytes object
b = bytes(a2)

print(a1)
print(a2[0])
print(b)

print(a1.index(-4))  # Returns an index of a member or raises ValueError
```

    array('l', [1, 2, 3, -4])
    49
    b'1234567890'
    3
    

### Generator

Any function that contains a yield statement returns a generator.


```python
def count(start, step):
    current = start
    while True:
        yield current
        current += step

c = count(100, 10)

print(next(c))
print(next(c))
print(next(c))
```

    100
    110
    120
    

## String


```python
se: str = ""  # Empty string
si: str = str(12345)  # Creates the string from int
sj: str = " ".join(["Follow", "the", "white", "rabbit"])  # Joins items using string as a separator
print(f"Joined string: {sj}")

is_contains: bool = "rabbit" in sj  # Checks if string contains a substring
is_startswith = sj.startswith("Foll")
is_endswith = sj.endswith("bbit")
print(f"is_contains = {is_contains}, is_startswith = {is_startswith}, is_endswith = {is_endswith}")

sr: str  = sj.replace("rabbit", "sheep")  # Replaces substrings. Also you can use times:  sr: str  = sj.replace("rabbit", "sheep", times)
print(f"After replace: {sr}")

i1 = sr.find("rabbit")  # Returns start index of the first match or -1
i2 = sr.index("sheep")  #  Returns start index of the first match or raises ValueError
print(f"Start index of 'rabbit' is {i1}, start index of 'sheep' is {i2}")

d = str.maketrans({"a" : "x", "b" : "y", "c" : "z"})
st  = "abc".translate(d)
print(f"Translate string: {st}")
```

    Joined string: Follow the white rabbit
    is_contains = True, is_startswith = True, is_endswith = True
    After replace: Follow the white sheep
    Start index of 'rabbit' is -1, start index of 'sheep' is 17
    Translate string: xyz
    

### lower(), upper(), capitalize() and title()


```python
s: str = "camelCase string"

print(s.lower())
print(s.upper())
print(s.capitalize())
print(s.title())
```

    camelcase string
    CAMELCASE STRING
    Camelcase string
    Camelcase String
    

### Property Methods

```text
+---------------+----------+----------+----------+----------+----------+
|               | [ !#$%…] | [a-zA-Z] |  [½¼¾]   |  [²³¹]   |  [0-9]   |
+---------------+----------+----------+----------+----------+----------+
| isprintable() |   yes    |   yes    |   yes    |   yes    |   yes    |
| isalnum()     |          |   yes    |   yes    |   yes    |   yes    |
| isnumeric()   |          |          |   yes    |   yes    |   yes    |
| isdigit()     |          |          |          |   yes    |   yes    |
| isdecimal()   |          |          |          |          |   yes    |
+---------------+----------+----------+----------+----------+----------+
```

*isspace()* checks for *[ \t\n\r\f\v\x1c-\x1f\x85…]*

### strip()


```python
s: str = "  ~~##A big blahblahblah##~~  "

s = s.strip()  # Strips all whitespace characters from both ends
print(s)

s = s.strip("~#")  # Strips all passed characters from both ends
print(s)

s = s.lstrip(" A")  # Strips all passed characters from left end
print(s)

s = s.rstrip("habl")  # Strips all passed characters from right end
print(s)

```

    ~~##A big blahblahblah##~~
    A big blahblahblah
    big blahblahblah
    big 
    

### split()


```python
s1: str = "Follow the white rabbit, Neo"

c1 = s1.split()  # Splits on one or more whitespace characters
print(c1)

c2 = s1.split(sep=", ", maxsplit=1)  # Splits on "sep" str at most "maxsplit" times
print(c2)

s2: str = "Beware the Jabberwock, my son!\n The jaws that bite, the claws that catch!"

c3 = s2.splitlines(keepends=False)  # On [\n\r\f\v\x1c-\x1e\x85\u2028\u2029] and \r\n.
print(c3)

# split() vs rsplit()

c4 = s2.split(maxsplit=2)
c5 = s2.rsplit(maxsplit=2)

print(c4, c5)
```

    ['Follow', 'the', 'white', 'rabbit,', 'Neo']
    ['Follow the white rabbit', 'Neo']
    ['Beware the Jabberwock, my son!', ' The jaws that bite, the claws that catch!']
    ['Beware', 'the', 'Jabberwock, my son!\n The jaws that bite, the claws that catch!'] ['Beware the Jabberwock, my son!\n The jaws that bite, the claws', 'that', 'catch!']
    

## Regex

Argument flags=re.IGNORECASE can be used with all functions


```python
import re

s1: str = "123 abc ABC 456"

m1 = re.search("[aA]", s1)  # Searches for first occurrence of the pattern; search() return None if it can't find a match
print(m1)
print(m1.group(0))

m2 = re.match("[aA]", s1)  # Searches at the beginning of the text; match() return None if it can't find a match
print(m2)

c1: list = re.findall("[aA]", s1)  # Returns all occurrences as strings
print(c1)

def replacer(s):  # replacer() can be a function that accepts a match object and returns a string
    return chr(ord(s[0]) + 1)  # Next symbol in alphabet

s2 = re.sub("\w", replacer, s1)  # Substitutes all occurrences with 'replacer'
print(s2)

c2 = re.split("\d", s1)
print(c2)

iter = re.finditer("\D", s1)  # Returns all occurrences as match objects

for ch in iter:
    print(ch.group(0), end= "")
```

    <re.Match object; span=(4, 5), match='a'>
    a
    None
    ['a', 'A']
    234 bcd BCD 567
    ['', '', '', ' abc ABC ', '', '', '']
     abc ABC 

### Match Object


```python
import re

m3 = re.match(r"(\w+) (\w+)", "John Connor, leader of the Resistance")

s3: str = m3.group(0)  # Returns the whole match
s4: str = m3.group(1)  # Returns part in the first bracket
t1: tuple = m3.groups()  # Returns all bracketed parts
start: int = m3.start()  # Returns start index of the match
end: int = m3.end()  # Returns exclusive end index of the match
t2: tuple[int, int] = m3.span()  # Return the 2-tuple (start, end)

print (f"{s3}\n {s4}\n {t1}\n {start}\n {end}\n {t2}\n")
```

    John Connor
     John
     ('John', 'Connor')
     0
     11
     (0, 11)
    
    

### JSON

Human-readable text format to store and transmit data objects.


```python
import json

d: dict = {1: "Lemon", 2: "Apple", 3: "Banana!"}

object_as_string: str = json.dumps(d, indent=2)
print(object_as_string)

restored_object = json.loads(object_as_string)

# Write object to JSON file
with open("1.json", 'w', encoding='utf-8') as file:
    json.dump(d, file, indent=2)

# Read object from JSON file
with open("1.json", encoding='utf-8') as file:
    restored_from_file = json.load(file)
    
print(restored_from_file)

```

    {
      "1": "Lemon",
      "2": "Apple",
      "3": "Banana!"
    }
    {'1': 'Lemon', '2': 'Apple', '3': 'Banana!'}
    

### Pickle

Binary file format to store and transmit data objects.


```python
import pickle

d: dict = {1: "Lemon", 2: "Apple", 3: "Banana!"}

# Write object to binary file
with open("1.bin", "wb") as file:
    pickle.dump(d, file)

# Read object from file
with open("1.bin", "rb") as file:
    restored_from_file = pickle.load(file)

print(restored_from_file)
```

    {1: 'Lemon', 2: 'Apple', 3: 'Banana!'}
    

### Bytes

Bytes object is an immutable sequence of single bytes. Mutable version is called bytearray.


```python

### Encode
b1 = bytes([1, 2, 3, 4])  # Ints must be in range from 0 to 255
b2 = "The String".encode('utf-8')
b3 = (-1024).to_bytes(4, byteorder='big', signed=True)  # byteorder="big"/"little"/"sys.byteorder", signed=False/True
b4 = bytes.fromhex('FEADCA')  # Hex pairs can be separated by spaces
b5 = bytes(range(10,30,2))

print(b1, b2, b3, b4, b5)

### Decode
c: list = list(b"\xfc\x00\x00\x00\x00\x01")  # Returns ints in range from 0 to 255
s: str = b'The String'.decode("utf-8")
b: int = int.from_bytes(b"\xfc\x00", byteorder='big', signed=False)  # byteorder="big"/"little"/"sys.byteorder", signed=False/True
s2: str = b"\xfc\x00\x00\x00\x00\x01".hex(" ")  # Returns a string of hexadecimal pairs, hex pairs can be separated by spaces

print(c, s, b, s2)

with open("1.bin", "wb") as file:  # Write bytes to file
    file.write(b1)

with open("1.bin", "rb") as file:  # Read bytes from file
    b6 = file.read()

print(b6)
```

    b'\x01\x02\x03\x04' b'The String' b'\xff\xff\xfc\x00' b'\xfe\xad\xca' b'\n\x0c\x0e\x10\x12\x14\x16\x18\x1a\x1c'
    [252, 0, 0, 0, 0, 1] The String 64512 fc 00 00 00 00 01
    b'\x01\x02\x03\x04'
    

### Struct

Module that performs conversions between a sequence of numbers and a bytes object. System’s type sizes and byte order are used by default.


```python
from struct import pack, unpack, iter_unpack

b = pack(">hhll", 1, 2, 3, 4)
print(b)

t = unpack(">hhll", b)
print(t)

i = pack("ii", 1, 2) * 5
print(i)

print(list(iter_unpack('ii', i)))
```

    b'\x00\x01\x00\x02\x00\x00\x00\x03\x00\x00\x00\x04'
    (1, 2, 3, 4)
    b'\x01\x00\x00\x00\x02\x00\x00\x00\x01\x00\x00\x00\x02\x00\x00\x00\x01\x00\x00\x00\x02\x00\x00\x00\x01\x00\x00\x00\x02\x00\x00\x00\x01\x00\x00\x00\x02\x00\x00\x00'
    [(1, 2), (1, 2), (1, 2), (1, 2), (1, 2)]
    

## Datetime

Module *datetime* provides *date*, *time*, *datetime* and *timedelta*. All are immutable and hashable

### Constructors


```python
from datetime import date, time, datetime, timedelta

d: date = date(year=1964, month=9, day=2)
t: time  = time(hour=12, minute=30, second=0, microsecond=0, tzinfo=None, fold=0)
dt: datetime = datetime(year=1964, month=9, day=2, hour=10, minute=30, second=0)
td: timedelta = timedelta(weeks=1, days=1, hours=12, minutes=13, seconds=14)

print (f"{d}\n {t}\n {dt}\n {td}")
```

    1964-09-02
     12:30:00
     1964-09-02 10:30:00
     8 days, 12:13:14
    

### Now


```python
from datetime import date, time, datetime
import pytz

d: date  = date.today()
dt1: datetime = datetime.today()
dt2: datetime = datetime.utcnow()
dt3: datetime = datetime.now(pytz.timezone('US/Pacific'))

print (f"{d}\n {dt1}\n {dt2}\n {dt3}")

```

    2022-06-05
     2022-06-05 18:21:30.733274
     2022-06-05 13:21:30.733273
     2022-06-05 06:21:30.733273-07:00
    

### Timezone


```python
from datetime import date, time, datetime, timedelta, tzinfo
from dateutil.tz import UTC, tzlocal, gettz, datetime_exists, resolve_imaginary

tz1: tzinfo = UTC  # UTC timezone

tz2: tzinfo = tzlocal()  # Local timezone
tz3: tzinfo = gettz()  # Local timezone

tz4: tzinfo = gettz("America/Chicago")  # "Asia/Kolkata" etc. See full list at en.wikipedia.org/wiki/List_of_tz_database_time_zones

local_dt = datetime.today()
utc_dt = local_dt.astimezone(UTC)  # Convert local datetime to UTC datetime

print (f"{tz1}\n {tz2}\n {tz3}\n {tz4}\n {local_dt}\n {utc_dt}")
```

    tzutc()
     tzlocal()
     tzlocal()
     tzfile('US/Central')
     2022-06-05 18:21:30.790123
     2022-06-05 13:21:30.790123+00:00
    

### Encode

Python uses the Unix Epoch: "1970-01-01 00:00 UTC"


```python
from datetime import datetime
from dateutil.tz import tzlocal

dt1: datetime = datetime.fromisoformat("2021-10-04 00:05:23.555+00:00")  # Raises ValueError
dt2: datetime = datetime.strptime("21/10/04 17:30", "%d/%m/%y %H:%M")   # Datetime from str, according to format (https://docs.python.org/3/library/datetime.html#strftime-and-strptime-format-codes)
dt3: datetime = datetime.fromordinal(100000)  # 100000th day after 1.1.0001
dt4: datetime = datetime.fromtimestamp(20_000_000.01)  # Local datetime from seconds since the Epoch

tz2: tzinfo = tzlocal()
dt5: datetime = datetime.fromtimestamp(300_000_000, tz2)  # Aware datetime from seconds since the Epoch

print (f"{dt1}\n {dt2}\n {dt3}\n {dt4}\n {dt5}")
```

    2021-10-04 00:05:23.555000+00:00
     2004-10-21 17:30:00
     0274-10-16 00:00:00
     1970-08-20 16:33:20.010000
     1979-07-05 10:20:00+05:00
    

### Decode


```python
from datetime import datetime

dt1: datetime = datetime.today()

s1: str = dt1.isoformat()
s2: str = dt1.strftime("%d/%m/%y %H:%M")  # Outputting datetime object to string (format: https://docs.python.org/3/library/datetime.html#strftime-and-strptime-format-codes)
i: int = dt1.toordinal()  # Days since Gregorian NYE 1, ignoring time and tz
a: float = dt1.timestamp()  # Seconds since the Epoch

print (f"{dt1}\n {s1}\n {s2}\n {i}\n {a}")
```

    2022-06-05 18:21:30.931110
     2022-06-05T18:21:30.931110
     05/06/22 18:21
     738311
     1654435290.93111
    

### Arithmetics


```python
from datetime import date, time, datetime, timedelta
from dateutil.tz import UTC, tzlocal, gettz, datetime_exists, resolve_imaginary

d: date  = date.today()
dt1: datetime = datetime.today()
dt2: datetime = datetime(year=1981, month=12, day=2)
td1: timedelta = timedelta(days=5)
td2: timedelta = timedelta(days=1)

d = d + td1  # date = date ± timedelta
dt3 = dt1 - td1  # datetime = datetime ± timedelta

td3 = dt1 - dt2  # timedelta = datetime - datetime

td4 = 10 * td1  # timedelta = const * timedelta
c: float = td1/td2  # timedelta/timedelta

print (f"{d}\n {dt3}\n {td3}\n {td4}\n {c}")
```

    2022-06-10
     2022-05-31 18:21:30.979967
     14795 days, 18:21:30.979967
     50 days, 0:00:00
     5.0
    

## File

### Open

Open the file and return a corresponding file object.


```python
f = open("f.txt", mode='r', encoding="utf-8", newline=None)

print(f.read())
```

    Hello from file!
    


*encoding=None* means that the default encoding is used, which is platform dependent. Best practice is to use *encoding="utf-8"* whenever possible.  
*newline=None* means all different end of line combinations are converted to '\n' on read, while on write all '\n' characters are converted to system's default line separator.  
*newline=""* means no conversions take place, but input is still broken into chunks by readline() and readlines() on every "\n", "\r" and "\r\n".  

### Modes

"r" - Read (default)  
"w" - Write (truncate)  
"x" - Write or fail if the file already exists  
"a" - Append  
"w+" - Read and write (truncate)  
"r+" - Read and write from the start  
"a+" - Read and write from the end  
"t" - Text mode (default)  
"b" - Binary mode (`'br'`, `'bw'`, `'bx'`, …)  

### Exceptions

*FileNotFoundError* can be raised when reading with "r" or "r+".  
*FileExistsError* can be raised when writing with "x".  
*IsADirectoryError* and *PermissionError* can be raised by any.  
*OSError* is the parent class of all listed exceptions.  

### Read from file


```python
with open("f.txt", encoding="utf-8") as f:
    chars = f.read(5)  # Reads chars/bytes or until EOF
    print(chars)

    f.seek(0)  # Moves to the start of the file. Also seek(offset) and seek(±offset, anchor), where anchor is 0 for start, 1 for current position and 2 for end

    lines: list[str] = f.readlines()  # Also readline()
    print(lines)
```

    Hello
    ['Hello from file!']
    

### Write to file


```python
with open("f.txt", "w", encoding="utf-8") as f:
    f.write("Hello from file!")  # Also f.writelines(<collection>)
    # f.flush() for flushes write buffer; runs every 4096/8192 B
```

## Paths


```python
from os import getcwd, path, listdir, scandir, stat
from pathlib import Path

s1:str = getcwd()  # Returns the current working directory
print(s1)

s2:str = path.abspath("f.txt")  # Returns absolute path
print(s2)

s3: str = path.basename(s2)  # Returns final component of the path
s4: str = path.dirname(s2)  # Returns path without the final component
t1: tuple = path.splitext(s2)  # Splits on last period of the final component
print(s3, s4, t1)

p = Path(s2)
st = p.stat()
print(st)

b1: bool = p.exists()
b2: bool = p.is_file()
b3: bool = p.is_dir()
print(b1, b2, b3)

c: list = listdir(path=s1)  # Returns filenames located at path
print(c)

s5: str = p.stem  # Returns final component without extension
s6: str  = p.suffix  # Returns final component's extension
t2: tuple = p.parts  # Returns all components as strings
print(s5, s6, t2)
```

    c:\Works\amaargiru\ipycs
    c:\Works\amaargiru\ipycs\f.txt
    f.txt c:\Works\amaargiru\ipycs ('c:\\Works\\amaargiru\\ipycs\\f', '.txt')
    os.stat_result(st_mode=33206, st_ino=25051272927278718, st_dev=3628794147, st_nlink=1, st_uid=0, st_gid=0, st_size=16, st_atime=1654514538, st_mtime=1654514457, st_ctime=1654437943)
    True True False
    ['.git', '.gitignore', 'convert_nb_to_md.bat', 'f.txt', 'LICENSE', 'pycallgraph3.png', 'PYCS.ipynb', 'README.md']
    f .txt ('c:\\', 'Works', 'amaargiru', 'ipycs', 'f.txt')
    

## Data querying

### Sum, Count, Min, Max


```python
a: list[int] = [1, 2, 3, 4, 5, 2, 2]

s = sum(a)
print(s)

c = a.count(2)  # Returns number of occurrences
print(c)

mn = min(a)
print(mn)

mx = max(a)
print(mx)
```

    19
    3
    1
    5
    

### Pairwise


```python
import itertools

a = [1, 2, 3, 4, 5]
p = itertools.pairwise(a)  # Returns successive overlapping pairs

print(list(p))
```

    [(1, 2), (2, 3), (3, 4), (4, 5)]
    

### Encryption and Decryption


```python
import hashlib

# pip install pycryptodomex
from Cryptodome import Random
from Cryptodome.Cipher import AES
from Cryptodome.Util.Padding import pad
from Cryptodome.Util.Padding import unpad

def encrypt_data(password: str, raw_data: bytes) -> bytes:
    res = bytes()
    try:
        key = hashlib.sha256(password.encode()).digest()
        align_raw = pad(raw_data, AES.block_size)
        iv = Random.new().read(AES.block_size)
        cipher = AES.new(key, AES.MODE_CBC, iv)
        ciphered_data = cipher.encrypt(align_raw)
        res = iv + ciphered_data
    except Exception as e:
        print(f"Encrypt error: {str(e)}")
    return res

def decrypt_data(password: str, encrypted_data: bytes) -> bytes:
    res = bytes()
    try:
        key = hashlib.sha256(password.encode()).digest()
        iv = encrypted_data[:AES.block_size]
        ciphered_data = encrypted_data[AES.block_size:]
        cipher = AES.new(key, AES.MODE_CBC, iv)
        decrypt_data = cipher.decrypt(ciphered_data)
        res = unpad(decrypt_data, AES.block_size)
    except Exception as e:
        print(f"Decrypt error: {str(e)}")
    return res

def encrypt_file(src_file: str, dst_file: str, password: str) -> bool:
    try:
        with open(src_file, "rb") as reader, open(dst_file, "wb") as writer:
            data = reader.read()
            data_enc = encrypt_data(password, data)
            writer.write(data_enc)
            writer.flush()
            print(f"{src_file} encrypted into {dst_file}")
        return True
    except Exception as e:
        print(f"Encrypt_file error: {str(e)}")
        return False

def decrypt_file(src_file: str, dst_file: str, password: str) -> bool:
    try:
        with open(src_file, "rb") as reader, open(dst_file, "wb") as writer:
            data = reader.read()
            data_decrypt = decrypt_data(password, data)
            writer.write(data_decrypt)
            writer.flush()
            print(f"{src_file} decrypted into {dst_file}")
        return True
    except Exception as e:
        print(f"Decrypt file error: {str(e)}")
        return False

if __name__ == '__main__':
    mes: bytes = bytes("A am the Message", "utf-8")
    passw: str = "h3AC3TsU8TECvyCqd5Q5WUag5uXLjct2"
    print(f"Original message: {mes}")

    # Encrypt message
    enc: bytes = encrypt_data(passw, mes)
    print(f"Encrypted message: {enc}")

    # Decrypt message
    dec: bytes = decrypt_data(passw, enc)
    print(f"Decrypted message: {dec}")

```

    Original message: b'A am the Message'
    Encrypted message: b"\xb3\x0f\xce~LX\x83\t=\xa7\xc3\xd3\xdc\x91\xe6\xb3\xce$i\x1dr\x19\xd6\xeb\xc3\xcc\xf9yLQ\xb2=\xd3|\x147\xc0\x1d\xa9\x92\xbb\xe7\x86R\xe07'\x8d"
    Decrypted message: b'A am the Message'
    

## Exceptions

### Catching exceptions

Basic Example


```python
a: float = 0
b: float = 0

try:
    b: float = 1/a
except ZeroDivisionError as e:
    print(f"Error: {e}")
```

    Error: division by zero
    

More complex example. Code inside the *else* block will only be executed if *try* block had no exceptions. Code inside the *finally* block will always be executed (unless a signal is received).


```python
import traceback

a: float = 0
b: float = 0

try:
    b: float = 1/a
except ZeroDivisionError as e:
    print(f"Error: {e}")
except ArithmeticError as e:
    print(f"We have a bit more complicated problem: {e}")
except Exception as serious_problem:  # Catch all exceptions
    print(f"I don't really know what is going on: {traceback.print_exception(serious_problem)}")
else:
    print("No errors!")
finally:
    print("This part is always called")
```

    Error: division by zero
    This part is always called
    

### Raising Exceptions


```python
from decimal import *

def div(a: Decimal, b: Decimal) -> Decimal:
    if b == 0:
        raise ValueError("Second argument must be non-zero")
    return a/b


try:
    c: Decimal = div(1, 0)
except ValueError:
    print("We have ValueError, as a planned!")
    # raise # We can re-raise exception
```

    We have ValueError, as a planned!
    

### Built-in Exceptions
```text
BaseException
 +-- SystemExit                   # Raised by the sys.exit() function
 +-- KeyboardInterrupt            # Raised when the user press the interrupt key (ctrl-c)
 +-- Exception                    # User-defined exceptions should be derived from this class
      +-- ArithmeticError         # Base class for arithmetic errors
      |    +-- ZeroDivisionError  # Dividing by zero
      +-- AttributeError          # Attribute is missing
      +-- EOFError                # Raised by input() when it hits end-of-file condition
      +-- LookupError             # Raised when a look-up on a collection fails
      |    +-- IndexError         # A sequence index is out of range
      |    +-- KeyError           # A dictionary key or set element is missing
      +-- NameError               # An object is missing
      +-- OSError                 # Errors such as “file not found”
      |    +-- FileNotFoundError  # File or directory is requested but doesn't exist
      +-- RuntimeError            # Error that don't fall into other categories
      |    +-- RecursionError     # Maximum recursion depth is exceeded
      +-- StopIteration           # Raised by next() when run on an empty iterator
      +-- TypeError               # An argument is of wrong type
      +-- ValueError              # When an argument is of right type but inappropriate value
           +-- UnicodeError       # Encoding/decoding strings to/from bytes fails
```

### Exits by raising SystemExit exception


```python
import sys

# sys.exit()  # Exits with exit code 0 (success)
# sys.exit(777)  # Exits with passed exit code
```

### User-defined Exceptions


```python
class MyException(Exception):
    pass

raise MyException("My car is broken")
```


    ---------------------------------------------------------------------------

    MyException                               Traceback (most recent call last)

    c:\Works\amaargiru\ipycs\PYCS.ipynb Cell 92' in <cell line: 4>()
          <a href='vscode-notebook-cell:/c%3A/Works/amaargiru/ipycs/PYCS.ipynb#ch0000089?line=0'>1</a> class MyException(Exception):
          <a href='vscode-notebook-cell:/c%3A/Works/amaargiru/ipycs/PYCS.ipynb#ch0000089?line=1'>2</a>     pass
    ----> <a href='vscode-notebook-cell:/c%3A/Works/amaargiru/ipycs/PYCS.ipynb#ch0000089?line=3'>4</a> raise MyException("My car is broken")
    

    MyException: My car is broken


### Exception Object

```python
arguments = <name>.args
exc_type = <name>.__class__
filename = <name>.__traceback__.tb_frame.f_code.co_filename
func_name = <name>.__traceback__.tb_frame.f_code.co_name
line = linecache.getline(filename, <name>.__traceback__.tb_lineno)
error_msg = ''.join(traceback.format_exception(exc_type, <name>, <name>.__traceback__))
```

## Math

### Basic Math


```python
from math import pi

a: float = pi ** 2  # Or pow(pi, 2)
print(f"Power: {a}")

b: float = round(pi, 2)
print(f"Round: {b}")

c: int = round(256, -2)
print(f"Int round: {c}")

d: float = abs(-pi)
print(f"Abs: {d}")

e: float = abs(10+10j)  # Or e: float = abs(complex(real=10, imag=10))
print(f"Complex abs: {e}")

```

    Power: 9.869604401089358
    Round: 3.14
    Int round: 300
    Abs: 3.141592653589793
    Complex abs: 14.142135623730951
    

### Bitwise Operators


```python
a: int = 0b01010101
b: int = 0b10101010

print(f"And: 0b{a&b:08b}")
print(f"Or: 0b{a|b:08b}")
print(f"Xor: 0b{a^b:08b}")
print(f"Left shift: 0b{a << 4:08b}")
print(f"Right shift: 0b{b >> 4:08b}")
print(f"Not: 0b{~a:08b}")
```

    And: 0b00000000
    Or: 0b11111111
    Xor: 0b11111111
    Left shift: 0b10101010000
    Right shift: 0b00001010
    Not: 0b-1010110
    

### Bit count


```python
a: int = 4242
print(f"{a} in binary format: 0b{a:b}")

c = a.bit_count()  # Returns the number of ones in the binary representation of the absolute value of the integer
print(f"Bit count: {c}")
```

    4242 in binary format: 0b1000010010010
    Bit count: 4
    

### Fractions


```python
from fractions import Fraction

f = Fraction("0.2").as_integer_ratio()

print(f)
```

    (1, 5)
    

### Euclidean distance between two points


```python
import math

p1 = (0.22, 1, 12)
p2 = (-0.12, 3, 7)

print(math.dist(p1, p2))
```

    5.39588732276722
    

## Random


```python
import random

rf: float = random.random()  # A float inside [0, 1)
print(f"Single float random: {rf}")

ri: int = random.randint(1, 10)  # An int inside [from, to]
print(f"Single int random: {ri}")

rb = random.randbytes(10)
print(f"Random bytes: {rb}")

rc: str = random.choice(["Alice", "Bob", "Maggie", "Madhuri Dixit"])
print(f"Random choice: {rc}")

rs: str = random.sample([1, 2, 3, 4, 5, 6, 7, 8, 9, 10], 5)
print(f"Random list without duplicates: {rs}")

a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
print(f"List before shuffle: {a}")
random.shuffle(a)
print(f"List after shuffle: {a}")

```

    Single float random: 0.9024807633898538
    Single int random: 7
    Random bytes: b'>\xe0^\x16PX\xf8E\xf8\x98'
    Random choice: Bob
    Random list without duplicates: [5, 10, 3, 6, 1]
    List before shuffle: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    List after shuffle: [10, 4, 6, 5, 1, 8, 3, 9, 7, 2]
    

## Profiling

### Stopwatch


```python
from time import time
start_time = time()

j: int = 0
for i in range(10_000_000):  # Long operation
    j = i ** 2

duration = time() - start_time
print(f"{duration} seconds")
```

    2.2923033237457275 seconds
    

### High performance


```python
from time import perf_counter
start_time = perf_counter()

j: int = 0
for i in range(10_000_000):  # Long operation
    j = i ** 2

duration = perf_counter() - start_time
print(f"{duration} seconds")
```

    2.3540456001646817 seconds
    

### timeit

Try to avoid a number of common traps for measuring execution times


```python
from timeit import timeit

def long_pow():
    j: int = 0
    for i in range(1000_000):  # Long operation
        j = i ** 2

timeit("long_pow()", number=10, globals=globals(), setup='pass')
```




    1.8552540000528097



### Call Graph

Generates a PNG image of the call graph with highlighted bottlenecks


```python
from pycallgraph3 import PyCallGraph
from pycallgraph3.output import GraphvizOutput

def long_pow():
    j: int = 0
    for i in range(1000_000):  # Long operation
        j = i ** 2

def short_pow():
    j: int = 0
    for i in range(1000):  # Short operation
        j = i ** 2

with PyCallGraph(output=GraphvizOutput()):
    # Code to be profiled
    long_pow()
    short_pow()
    # This will generate a file called pycallgraph3.png
```

<img src="pycallgraph3.png" style="height:400px">

## Sources  
[docs.python.org](https://docs.python.org/)  
[Comprehensive Python Cheatsheet](https://github.com/gto76/python-cheatsheet)  
[Python Cheatsheet](https://github.com/wilfredinni/python-cheatsheet)  
["The Hitchhiker’s Guide to Python"](https://docs.python-guide.org/)  
[Joel Grus, "Data Science from Scratch"](https://github.com/joelgrus/data-science-from-scratch)  
["Python 3 Patterns, Recipes and Idioms"](https://python-3-patterns-idioms-test.readthedocs.io/en/latest/index.html)  
["Python Notes for Professionals"](https://goalkicker.com/PythonBook/)  
[Mark Lutz, "Learning Python"](https://drive.google.com/file/d/0B2Y-n6IlHYliSXZxMk0xT0NSY1E/preview)  
