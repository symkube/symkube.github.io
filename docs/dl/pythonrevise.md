## f-string
使用`{}`把表达式插入一个f-string

调试语法糖：
```py
print(f"{x=}, {y=}")
# 输出: x=10, y=20
```

如果需要在 f-string 的结果中包含花括号本身，需要使用双花括号 `{{` 和 `}}`。

多行 F-strings：

```python
    name = "David"
    profession = "Engineer"
    message = (
        f"Name: {name}\n"
        f"Profession: {profession}"
    )
    print(message)
    # 输出:
    # Name: David
    # Profession: Engineer
```
或者使用三引号：
```python
    message = f"""
    Name: {name}
    Profession: {profession}
    """
    print(message)
    # 输出 (注意前导空格):
    #
    #     Name: David
    #     Profession: Engineer
    #
```

**易错点：**

1.  **引号的嵌套：** 如果 f-string 本身用双引号 `"` 包裹，那么在 `{}` 内部的字符串字面值应该用单引号 `'`，反之亦然。
    ```python
    # 正确
    data = {"key": "value"}
    print(f"The value is {data['key']}")

    # 错误 (会导致 SyntaxError)
    # print(f"The value is {data["key"]}") # 内部的双引号会提前闭合 f-string

    # 正确 (另一种方式)
    print(f'The value is {data["key"]}')
    ```

2.  **反斜杠 `\` 的使用：** 在 f-string 的表达式部分，不能直接使用反斜杠 `\` (例如用于换行符 `\n` 或其他转义序列)。
    ```python
    # 错误
    # print(f"Newline: {\n}") # SyntaxError: f-string expression part cannot include a backslash

    # 正确 (将转义字符放在表达式之外，或者表达式本身返回一个包含转义字符的字符串)
    print(f"Newline: {'\n'}Hello")
    print(f"Hello\nWorld")
    ```

3.  **忘记 `f` 前缀：** 如果忘记了 `f`，那么 `{}` 将被视为普通字符，不会进行求值。
    ```python
    name = "Eve"
    print("Hello, {name}")
    # 输出: Hello, {name} (而不是 Hello, Eve)
    ```

## 拷贝

`[:]` (切片), list(), copy.copy() 都会进行浅拷贝

## 切片

基本语法

切片的基本语法是使用方括号 [] 并在其中指定索引，但与单个索引不同，切片使用冒号 : 来分隔起始索引、结束索引和可选的步长：

sequence[start:stop:step]
start (起始索引，可选):

切片将从这个索引开始。
这个索引处的元素会被包含在切片结果中。
如果省略，默认为 0 (序列的开头)。
可以是负数，表示从末尾开始计数 (-1 是最后一个元素，-2 是倒数第二个，以此类推)。
stop (结束索引，可选):

切片将在这个索引之前结束。
这个索引处的元素不会被包含在切片结果中。
如果省略，默认为序列的长度 (直到序列的末尾)。
可以是负数。

创建新对象： 切片操作通常会创建一个新的序列对象（对于列表、元组、字符串等内置类型，这是一个浅拷贝）。原始序列不会被修改。
索引越界安全： 与单个索引不同，切片对于超出范围的 start 或 stop 索引通常是安全的，它会尽其所能返回一个有效的切片（可能是空的）。例如，如果列表只有5个元素，my_list[0:100] 仍然会返回整个列表，而不会报错。

setdefault 在键不存在时设置默认值并返回默认值。在键存在时，返回现有值。

