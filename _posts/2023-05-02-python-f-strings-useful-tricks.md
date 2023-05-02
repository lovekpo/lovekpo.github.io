---
layout: post
title: Python - f-strings Useful Tricks
date: 2023-05-02 17:51 +0900
categories: [Python]
tags: [python]     # TAG names should always be lowercase
---
_원문 : [https://medium.com/geekculture/python-f-strings-useful-tricks-8f5cbc19f62](https://medium.com/geekculture/python-f-strings-useful-tricks-8f5cbc19f62){:target="_blank"}_

Python에서 `f-strings`을 사용한 몇가지 트릭

![Python f-string](https://miro.medium.com/v2/resize:fit:1394/format:webp/1*6dgF_sWUzuv_weZLK9DfQw.png){: width="700" height="400" }

Python `f-strings` 은 단순히 문자열을 출력하는 것보다 더 많은 것을 할 수 있습니다.

### Re-use Variable Name Again

```python
str_value = "hello，python coders"
print(f"{ str_value = }")
# str_value = 'hello，python coders'
```

### Change Output Directly

```python
num_value = 125
print(f"{num_value % 2 = }")
# num_value % 2 = 1
```

### Date formatting

```python
import datetime

today = datetime.date.today()
print(f"{today: %Y%m%d}")
#20211224
print(f"{today =: %Y%m%d}")
#today = 20211224
```

### 2/8/16 Hexadecimal Conversion

```python
>>> a = 42
>>> f"{a:b}"# Binary
'101010'
>>> f"{a:o}"# Octal
'52'
>>> f"{a:x}"# Hex, small letters
'2a'
>>> f"{a:X}"# Hex, capital letters
'2A'
>>> f"{a:c}"# ascii 码
'*'
```

### Floating Point Number Formatting

```python
>>> num_value = 223.456
>>> f'{num_value = :.2f}'
'num_value = 223.46'
>>> nested_format = ".2f"
>>> print(f'{num_value:{nested_format}}')
223.46
```

### String Alignment

```python
>>> x = 'test'
>>> f'{x:>10}'  # Right alignment
'      test'
>>> f'{x:*<10}' # Left alignment
'test******'
>>> f'{x:=^10}'# Center
'===test==='
>>> x, n = 'test', 10
>>> f'{x:~^{n}}'# Center
'~~~test~~~'
Use !s, !r
>>> x = 'test'
>>> f"{x!s}"# Same as str(x)
'test'
>>> f"{x!r}"# Same as repr(x)
"'test'"
```

### Custom Format

```python
class MyClass:
    def __format__(self, format_spec) -> str:
        print(f'MyClass __format__ called with {format_spec!r}')
        return "MyClass()"

print(f'{MyClass():bala bala  %%MYFORMAT%%}')
# Output
MyClass __format__ called with format_spec='bala bala  %%MYFORMAT%%'
MyClass()
```

### More Efficient

Python의 f-strings 는 매우 유연하고 우아하며 효율적인 문자열 출력처리 방법이기도 합니다.

```python
>>> timeit.timeit("""name = "Tony"
        age = 100
        '%s is %s.' % (name, age)""", number = 10000)
# 0.0029884499333798885

>>> timeit.timeit("""name = "Tony"
        age = 100
        '{} is {}.'.format(name, age)""", number = 10000)
# 0.003444851143285632

>>> timeit.timeit("""name = "Tony"
        age = 100
        f'{name} is {age}.'""", number = 10000)
# 0.0018234248273074627
```
