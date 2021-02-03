```python
Example 5-2. Use function through a different name, and pass function as argument 
# 通过别的名称使用函数，再把函数作为参数传递
>>> fact = factorial 
>>> fact
<function factorial at 0x...> 
>>> fact(5) 120 
>>> map(factorial, range(11)) <map object at 0x...> 
>>> list(map(fact, range(11)))
[1, 1, 2, 6, 24, 120, 720, 5040, 40320, 362880, 3628800]
```



```
示例 5-5 计算阶乘列表：map 和 filter 与列表推导比较
>>> list(map(fact, range(6))) ➊ [1, 1, 2, 6, 24, 120]
>>> [fact(n) for n in range(6)] ➋ [1, 1, 2, 6, 24, 120]
>>> list(map(factorial, filter(lambda n: n % 2, range(6)))) ➌ [1, 6, 120]
>>> [factorial(n) for n in range(6) if n % 2] ➍ [1, 6, 120] >>>
```

## Anonymous Functions

```
示例 5-7 使用 lambda 表达式反转拼写，然后依此给单词列表排序
>>> fruits = ['strawberry', 'fig', 'apple', 'cherry', 'raspberry', 'banana'] >>> sorted(fruits, key=lambda word: word[::-1]) ['banana
```

## 函数注解	

```
示例 5-15 在指定长度附近截断字符串的函数
	def clip(text, max_len=80): 
	"""在max_len前面或后面的第一个空格处截断文本
    """
	end = None
    if len(text) > max_len:
		space_before = text.rfind(' ', 0, max_len)
        if space_before >= 0: 
        	end = space_before
		else:
			space_after = text.rfind(' ', max_len) 
		if space_after >= 0: 
			end = 		space_after
	if end is None: # 没找到空格 
		end = len(text)
	return text[:end].rstrip()
	示例 5-19 有注解的 clip 函数
	def clip(text:str, max_len:'int > 0'=80) -> str: 
	"""在max_len前面或后面的第一个空格处截断文本
    """
	end = None
    if len(text) > max_len:
		space_before = text.rfind(' ', 0, max_len)
        if space_before >= 0: 
        	end = space_before
		else:
			space_after = text.rfind(' ', max_len) 
		if space_after >= 0: 
			end = 		space_after
	if end is None: # 没找到空格 
		end = len(text)
	return text[:end].rstrip()
```

函数声明中的各个参数可以在 : 之后增加注解表达式。如果参数有默认值，注解放在参数 名和 = 号之间。如果想注解返回值，在 ) 和函数声明末尾的 : 之间添加 -> 和一个表达式。 那个表达式可以是任何类型。注解中最常用的类型是类（如 str 或 int）和字符串（如 'int > 0'）。在示例 5-19 中，max_len 参数的注解用的是字符串。