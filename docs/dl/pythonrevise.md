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
