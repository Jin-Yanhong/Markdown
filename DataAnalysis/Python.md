## 类型转换

1.  int()

    > Boolean 值 true = 1 ，false = 0 含有除数字以外的特殊字符，不能强转

2.  float()

3.  str()

4.  bool()

    > Boolean 值 true = 1 ，false = 0 含有除数字以外的特殊字符，不能强转字符串中没有内容都为`false` 列表中有数据，返回`true`,否则返回`false`

    ```python
    print(bool(0))
    print(bool(0.0))
    print(bool(''))
    print(bool(""))
    print(bool([]))
    print(bool(()))
    print(bool({}))
    ```

    以上结果均为 `false`

## 运算符

| 运算符 | 说明   |
| ------ | ------ |
| +      | 加     |
| -      | 减     |
| \*     | 乘法   |
| /      | 除法   |
| //     | 整除   |
| %      | 取余数 |
| \*\*   | 指数   |
| ()     | 小括号 |

## 输出

普通输出

```python
print()
```

格式化输出

```python
print("我的名字是%s,我的年龄是%d" % (name,age))
```

## 输入

```python
input()
```

## 字符串方法

1. len 获取长度
2. find 查找内容
3. startsWith，endsWith 判断
4. count 统计某个字母出现的次数
5. replace 内容替换
6. split 切割字符串
7. upper,lower 切换大小写
8. strip 空格处理
9. join 字符串拼接(split 的逆操作)

## 列表方法

1. append 在末尾插入元素
2. insert 在指定位置插入元素
3. extend 合并两个列表
4. in 查找
5. not in 查找
6. del 删除
7. pop 删除
8. remove 删除
9. value[start:end:step] 切片

## 字典方法

1. dict[key] 如果 key 不存在 44 则报错
2. dict.get(key)
3. dict.del 删除字典| 删除字典中的元素
4. dict.clear 清空字典
5. for key in dict.keys(): 遍历字典的 key
6. for value in dict.values(): 遍历字典的 value
7. for key,value in dict.items(): 遍历字典的 每一项

## 文件

### 文件的打开

open(filepath,mode). w,r

### 文件的关闭
