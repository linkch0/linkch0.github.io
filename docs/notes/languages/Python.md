---
icon: material/language-python
tags: [Updating]
comments: true
---

# Python

## sys

1. `sys.byteorder`: An indicator of the native byte order. Edianness output `little` or `big`.

## fileinput

1. Create an instance of the [`FileInput`](https://docs.python.org/3.8/library/fileinput.html?highlight=fileinput#fileinput.FileInput) class.

    使用`readline()`方法读取一行输入：

    ```python
    >>> import fileinput
    >>> stdin = fileinput.input()
    >>> stdin.readline()
    hello world
    'hello world\n'
    >>> stdin.readline()
    
    '\n'
    ```

## Built-in Functions

1. `exec()`: This function supports dynamic execution of Python code. _object_ must be either a string or a code object. If it is a string, the string is parsed as a suite of Python statements which is then executed (unless a syntax error occurs).

    输入一行字符串并作为 Python 语句执行：

    ```python
    >>> import fileinput
    >>> stdin = fileinput.input()
    >>> exec(stdin.readline())
    x = 1; y = 2;
    >>> x, y
    (1, 2)
    >>> exec(stdin.readline())
    arr = [1, 2, 3, 4, 5]
    >>> arr
    [1, 2, 3, 4, 5]
    ```

2. `globals()`: Return a dictionary representing the current global symbol table. This is always the dictionary of the current module (inside a function or method, this is the module where it is defined, not the module from which it is called).

    全局符号表

    ```python
    >>> a, b, c = 1, 2, 3
    >>> globals()['a'] = -1
    >>> globals()
    {'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <class '_frozen_importlib.BuiltinImporter'>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>, 'a': -1, 'b': 2, 'c': 3}
    ```

3. `ord(c)`: Given a string representing one Unicode character, return an integer representing the Unicode code point of that character `c`. `chr(i)`: Return the string representing a character whose Unicode code point is the integer `i`.

    Unicode 字符与编码相互转换

    ```python
    >>> ord('a'), chr(97), ord('0'), chr(48)
    (97, 'a', 48, '0')
    ```

4. `format(value[, format_spec])`: Convert a value to a “formatted” representation, as controlled by format_spec. `bin(x)`: Convert an integer number to a binary string prefixed with “0b”. `oct(x)`: Convert an integer number to an octal string prefixed with “0o”. `hex(x)`: Convert an integer number to a lowercase hexadecimal string prefixed with “0x”.

    ```python
    >>> bin(14), oct(14), hex(14)
    ('0b1110', '0o16', '0xe')
    >>> format(14, '#b'), format(14, 'b')
    ('0b1110', '1110')
    >>> f'{14:#b}', f'{14:b}'
    ('0b1110', '1110')
    >>> f'{14:#x}', f'{14:x}'
    ('0xe', 'e')
    >>> f'{14:#o}', f'{14:o}'
    ('0o16', '16')
    ```

## IPython Tips

1.   如果你不确定 function, class, or method 的使用方法，打印 `__doc__` 属性，查看文档，或者在 IPython 中语句末尾加上一个 question mark `?` ，两个 `??` 查看更详细的内容

     ```python
     In [17]: print(spark.read.__doc__)
     
         Interface used to load a :class:`DataFrame` from external storage systems
         (e.g. file systems, key-value stores, etc). Use :attr:`SparkSession.read`
         to access this.
     
         .. versionadded:: 1.4.0
     
         .. versionchanged:: 3.4.0
             Supports Spark Connect.
     
     
     In [18]: spark.read?
     Type:        property
     String form: <property object at 0x104841b20>
     Docstring:
     Returns a :class:`DataFrameReader` that can be used to read data
     in as a :class:`DataFrame`.
     
     .. versionadded:: 2.0.0
     
     .. versionchanged:: 3.4.0
         Supports Spark Connect.
     
     Returns
     -------
     :class:`DataFrameReader`
     
     Examples
     --------
     >>> spark.read
     <...DataFrameReader object ...>
     
     Write a DataFrame into a JSON file and read it back.
     
     >>> import tempfile
     >>> with tempfile.TemporaryDirectory() as d:
     ...     # Write a DataFrame into a JSON file
     ...     spark.createDataFrame(
     ...         [{"age": 100, "name": "Hyukjin Kwon"}]
     ...     ).write.mode("overwrite").format("json").save(d)
     ...
     ...     # Read the JSON file as a DataFrame.
     ...     spark.read.format('json').load(d).show()
     +---+------------+
     |age|        name|
     +---+------------+
     |100|Hyukjin Kwon|
     +---+------------+
     ```
