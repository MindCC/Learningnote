# An Array of Sequences

*Mutable sequences*

list, bytearray, array.array, collections.deque, and memoryview

*Immutable sequences*

tuple, str, and bytes



##  chr() & ord()

chr(65)

'A'

ord('A')

65

# list comprehension
## Example2-4 Cartesian product using a list comprehension

```python
>>> colors = ['black', 'white']
>>> sizes = ['S', 'M', 'L']
>>> tshirts = [(color, size) for color in colors for size in sizes]  
>>> tshirts
[('black', 'S'),
 ('black', 'M'), 
 ('black', 'L'),
 ('white', 'S'), 
 ('white', 'M'),
 ('white', 'L')]
>>> for color in colors:
... 	for size in sizes:
... 		print((color, size))
...
('black', 'S')
('black', 'M')
('black', 'L')
('white', 'S')
('white', 'M')
('white', 'L')
```

# Generator Expressions

##  Example 2-6. Cartesian product in a generator expression
```python
>>> colors = ['black', 'white']
>>> sizes = ['S', 'M', 'L']
>>> for tshirt in ('%s %s' % (c, s) for c in colors for s in sizes):  ... print(tshirt)
...
black S
black M
black L
white S
white M
white L
```

# Tuples

Another example of tuple unpacking is prefixing an argument with a star when callinga function:

```
>>> divmod(20, 8)
(2, 4)
>>> t = (20, 8)
>>> divmod(*t)
(2, 4)
>>> quotient, remainder = divmod(*t)
>>> quotient, remainder(2, 4)
```

*Python divmod() 函数接收两个数字类型（非复数）参数，返回一个包含商和余数的元组(a // b, a % b)*



### os.path.split

*the os.path.split() function builds a tuple (path, last_part) from a filesystem path*

  ```
>>> importos
>>> _, filename = os.path.split('/home/luciano/.ssh/idrsa.pub')
>>> filename
'idrsa.pub'
  ```



## Using * to grab excess items

Defining function parameters with *args to grab arbitrary excess arguments is a classicPython feature.

```
>>> a, b, *rest = range(5)
>>> a, b, rest
(0, 1, [2, 3, 4])
>>> a, b, *rest = range(3)
>>> a, b, rest(0, 1, [2])
>>> a, b, *rest = range(2)
>>> a, b, rest(0, 1, [])
```

In the context of parallel assignment, the * prefix can be applied to exactly one variable,but it can appear in any position:

```
>>> a, *body, c, d = range(5)
>>> a, body, c, d(0, [1, 2], 3, 4)
>>> *head, b, c, d = range(5)
>>> head, b, c, d([0, 1], 2, 3, 4)
```

## Nested Tuple Unpacking

 The tuple to receive an expression to unpack can have nested tuples, like (a, b, (c,d)), and Python will do the right thing if the expression matches the nesting structure

###  Example 2-8. Unpacking nested tuples to access the longitude

```
metro_areas = [
	('Tokyo', 'JP', 36.933, (35.689722, 139.691667)),  
    ('Delhi NCR', 'IN', 21.935, (28.613889, 77.208889)),
    ('Mexico City', 'MX', 20.142, (19.433333, -99.133333)),
    ('New York-Newark', 'US', 20.104, (40.808611, -74.020386)), 
    ('Sao Paulo', 'BR', 19.649, (-23.547778, -46.635833)),]
print('{:15} | {:^9} | {:^9}'.format('', 'lat.', 'long.'))
fmt = '{:15} | {:9.4f} | {:9.4f}'
for name, cc, pop, (latitude, longitude) in metro_areas:  
	if longitude <= 0: 
    	print(fmt.format(name, latitude, longitude))
    	
                |   lat.    |   long.
Mexico City     |   19.4333 |  -99.1333
New York-Newark |   40.8086 |  -74.0204
Sao Paulo       |  -23.5478 |  -46.6358
```

The ^ means right-aligned when outputting. If the width is less than the actual width of the string, the actual width will be output

