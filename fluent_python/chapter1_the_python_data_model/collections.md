# collections

## namedtuple

namedtuple is a subclass that inherits from tuple.namedtype is cooler than tuple.namedtuple creates an object similar to a tuple, and the object has access properties. This object is more like a class with data properties, but the data properties are read-only.

example: 

```python
Mytuple=collections.namedtuple('Mytuple',['x','y'])
n=Mytuple(1,2)
print n.x
1
print n.y
2
```

```python
Person = collections.namedtuple('Person','name age gender')  
Bob = Person(name='Bob', age=30, gender='male')  
```

### make data to namedtuple

```python
Mytuple = namedtuple('Mytuple', ['x', 'y'])
test= [11, 22]
p = Mytuple ._make(test)
p
Mytuple (x=11, y=22)
```

# the data is read-only. If you want to update, you need to call the method_replace.

```python
>>> p
Mytuple(x=11, y=22)
>>> p.x
11
>>> p.y
22
>>> p.y=33

Traceback (most recent call last):
  File "<pyshell#16>", line 1, in <module>
    p.y=33
AttributeError: can't set attribute
>>> p._replace(y=33)
Mytuple(x=11, y=33)
>>> p
Mytuple(x=11, y=22)
>>>
```

### Convert data dictionary to namedtuple type

```
>>> d={'x':44,'y':55}
>>> dp=Mytuple(**d)
>>> dp
Mytuple(x=44, y=55)
>>> p
Mytuple(x=11, y=22)
```

### Namedtuple is most commonly used in dealing with data returned from a CSV or database. Using map() function and namedtupe to build the type_ Make() method

```python
EmployeeRecord = namedtuple('EmployeeRecord', 'name, age, title, department, paygrade')

import csv
for emp in map(EmployeeRecord._make, csv.reader(open("employees.csv", "rb"))):
    print(emp.name, emp.title)

# sqlite数据库
import sqlite3
conn = sqlite3.connect('/companydata')
cursor = conn.cursor()
cursor.execute('SELECT name, age, title, department, paygrade FROM employees')
for emp in map(EmployeeRecord._make, cursor.fetchall()):
    print(emp.name, emp.title)

# MySQL 数据库
import mysql
from mysql import connector
from collections import namedtuple
user = 'herbert'
pwd = '######'
host = '127.0.0.1'
db = 'world'
cnx = mysql.connector.connect(user=user, password=pwd, host=host,database=db)
cur.execute("SELECT Name, CountryCode, District, Population FROM CITY where CountryCode = 'CHN' AND Population > 500000")
CityRecord = namedtuple('City', 'Name, Country, Dsitrict, Population')
for city in map(CityRecord._make, cur.fetchall()):
    print(city.Name, city.Population)
```

