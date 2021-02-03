# dict Comprehensions

dict Comprehension like liscomps.We could add filter into comprehensions

```python
>>> country_code = {country: code for code, country in DIAL_CODES} 
>>> country_code
{'China': 86, 'India': 91, 'Bangladesh': 880, 'United States': 1, 'Pakistan': 92, 'Japan': 81, 'Russia': 7, 'Brazil': 55, 'Nigeria': 234, 'Indonesia': 62} 
>>> {code: country.upper() for country, code in country_code.items() ... if code < 66}
{1: 'UNITED STATES', 55: 'BRAZIL', 62: 'INDONESIA', 7: 'RUSSIA'}
```

##  用setdefault 处理找不到的key

```python



my_dict.setdefault(key,[]).append(new_value)

...is the same as runing...

if key not in my_dict:
    my_dict[key]=[]
mydict[key].append(new_value)

...except that the latter code performs at least two searches for key—three if it’s not found—while setdefault does it all with a single lookup.

```



## Mappings with Flexible Key Lookup 

## 映射的弹性键查询

### defaultdict：处理找不到的键的一个选择

在用户创建 defaultdict 对象的时候，就需要给它配置一个为找不到的键创造默认值的方法

```
dd = defaultdict(list) 
```



