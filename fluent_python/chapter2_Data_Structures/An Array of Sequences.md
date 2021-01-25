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

# Example 2-18 Bisect bisect

get the index of the sequence

```python
def grade(score, breakpoints=[60, 70, 80, 90], grades='FDCBA'):
    i = bisect.bisect(breakpoints, score)
    return grades[i]

print([grade(score) for score in [33, 99, 77, 70, 89, 90, 100]])
```

# Example 2-19 Insort keeps a sorted sequence always sorted

```
import bisect
import random
SIZE=7
random.seed(1729)
my_list = []
for i in range(SIZE):
 new_item = random.randrange(SIZE*2)
 bisect.insort(my_list, new_item)
 print('%2d ->' % new_item, my_list)
 [0,2,6,7,8,10,10]
```



# MemoryView

## Example 2-21  Changing the value of an array item by poking one of its bytes

*A memoryview is essentially a generalized NumPy array structure in Python itself (without the math). It allows you to share memory between data-structures (things like PIL images, SQLlite databases, NumPy arrays, etc.) without first copying. This is very important for large data sets.*

```python
>>> numbers = array.array('h', [-2, -1, 0, 1, 2])
>>> memv = memoryview(numbers) ➊
>>> len(memv)
5
>>> memv[0] ➋
-2
>>> memv_oct = memv.cast('B') ➌
>>> memv_oct.tolist() ➍
[254, 255, 255, 255, 0, 0, 1, 0, 2, 0]
>>> memv_oct[5] = 4 ➎
>>> numbers
array('h', [-2, -1, 1024, 1, 2]) 
```

# numpy

a.transpose 转置

# Deque

## Example 2-23

```python
>>> from collections import deque
>>> dq = deque(range(10), maxlen=10) ➊
>>> dq
deque([0, 1, 2, 3, 4, 5, 6, 7, 8, 9], maxlen=10)
>>> dq.rotate(3) ➋
>>> dq
deque([7, 8, 9, 0, 1, 2, 3, 4, 5, 6], maxlen=10)
>>> dq.rotate(-4)
>>> dq
deque([1, 2, 3, 4, 5, 6, 7, 8, 9, 0], maxlen=10)
>>> dq.appendleft(-1) ➌
>>> dq
deque([-1, 1, 2, 3, 4, 5, 6, 7, 8, 9], maxlen=10)
>>> dq.extend([11, 22, 33]) ➍
>>> dq
deque([3, 4, 5, 6, 7, 8, 9, 11, 22, 33], maxlen=10)
>>> dq.extendleft([10, 20, 30, 40]) ➎
>>> dq
deque([40, 30, 20, 10, 3, 4, 5, 6, 7, 8], maxlen=10)
```

➊ maxlen 是一个可选参数，代表这个队列可以容纳的元素的数量，而且一旦设定，这个 属性就不能修改了。

 ➋ 队列的旋转操作接受一个参数 n，当 n > 0 时，队列的最右边的 n 个元素会被移动到队 列的左边。当 n < 0 时，最左边的 n 个元素会被移动到右边。

 ➌ 当试图对一个已满（len(d) == d.maxlen）的队列做尾部添加操作的时候，它头部的元 素会被删除掉。注意在下一行里，元素 0 被删除了。

 ➍ 在尾部添加 3 个元素的操作会挤掉 -1、1 和 2。 

➎ extendleft(iter) 方法会把迭代器里的元素逐个添加到双向队列的左边，因此迭代器里 的元素会逆序出现在队列里。