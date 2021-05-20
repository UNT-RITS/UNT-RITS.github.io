# Python Useful Code Samples

Here are a few Python code samples useful when you work on Talon HPC.

**All Python code is for Python 3!**

## Reverse

```python
''' reversing string with special case of slice step param '''

a = 'abcdefghijklmnopqrstuvwxyz'
print(a[::-1])

''' iterating eover stirng reversly efficiantly '''
for char in reversed(a):
  print(char)
  
print([1,2,3,4,5][::-1])
```


## List to String

```python
a = ["Python", "is", "awesome!"]
print(" ".join(a))


>> Python is awesome!
```

## Chained Functions

```python
def prod(a,b):
  return a*b

def sum(a,b):
  return a+b

a, b = 3, 10

print((prod if a < b else sum)(a,b))


>> 30
```

## Checking Words are [Anagrams](https://en.wikipedia.org/wiki/Anagram)

```python
# imports
from collections import Counter

str1 = "cat"
str2 = "tac"

Counter(str1) == Counter(str2)


>> True
```

## Concatenate Lists

```python
a = [1,2,3,4]

b = [5,6,7]

c = [*a, *b]

print(c)


>> [1, 2, 3, 4, 5, 6, 7]
```

## Copy Lists

```python
from copy import deepcopy

a = [[1,2,3,4], [1,2,54,76,87]]

b = deepcopy(a)

b[0][3] = 999

print(a,b)

# good for nested listst


>> [[1, 2, 3, 4], [1, 2, 54, 76, 87]] [[1, 2, 3, 999], [1, 2, 54, 76, 87]]
```

## Safe dictionary get

```python
a = {1:'a', 3:'v', 99:'B'}

print(a.get(1, 'None'))
print(a.get(98, 'None'))


>> a
>> None
```

## Statement for-else

```python
a = [1,2,3,4,5,6]

for i in a:
  if i == 0:
    break
else:
  print("Did not reach loop!")
  
  
>> Did not reach loop!
```


## Single-line for

```python
a = [1,2,3,-1]
[0 if i < 0 else i for i in a]


>> [1, 2, 3, 0]
```


## Merge dictionaries

```python
d1 = {'a':1}
d2 = {'b':34}

print({**d1, **d2})


>> {'a': 1, 'b': 34}
```

## Sorting Dictionary

```python
mydict = {'carl':40, 'alan':2, 'bob':1, 'danny':0}

# How to sort a dict by value Python 3>
sort = {key:value for key, value in sorted(mydict.items(), key=lambda kv: (kv[1], kv[0]))}
print(sort)

# How to sort a dict by key Python 3>
sort = {key:mydict[key] for key in sorted(mydict.keys())}
print(sort)


>> {'danny': 0, 'bob': 1, 'alan': 2, 'carl': 40}
>> {'alan': 2, 'bob': 1, 'carl': 40, 'danny': 0}
```


## 

```python

```
