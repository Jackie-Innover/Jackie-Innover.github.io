# Python 编码规范 (Google)

[TOC]

## 分号

不要在行尾加分号, 也不要用分号将两条命令存放在同一样.

## 行长度

每行不超过80个字符

以下情况除外：

1. 长的导入模块语句
2. 注释里的URL

不要使用反斜杠连接行。

Python会将 [圆括号, 中括号和花括号中的行隐式的连接起来](http://docs.python.org/2/reference/lexical_analysis.html#implicit-line-joining) , 你可以利用这个特点. 如果需要, 你可以在表达式外围增加一对额外的圆括号。

```python
推荐: foo_bar(self, width, height, color='black', design=None, x='foo',
             emphasis=None, highlight=0)

     if (width == 0 and height == 0 and
         color == 'red' and emphasis == 'strong'):
```

如果一个文本字符串在一行放不下, 可以使用圆括号来实现隐式行连接:

```python
x = ('这是一个非常长非常长非常长非常长 '
     '非常长非常长非常长非常长非常长非常长的字符串')
```

在注释中，如果必要，将长的URL放在一行上。

```python
Yes:  # See details at
      # http://www.example.com/us/developer/documentation/api/content/v2.0/csv_file_name_extension_full_specification.html
No:  # See details at
     # http://www.example.com/us/developer/documentation/api/content/\
     # v2.0/csv_file_name_extension_full_specification.html
```

注意上面例子中的元素缩进; 你可以在本文的 :ref:`缩进 <indentation>`部分找到解释.

## 括号

宁缺毋滥的使用括号

除非是用于实现行连接, 否则**不要在返回语句或条件语句中使用括号**. 不过在元组两边使用括号是可以的.

```python
Yes: if foo:
         bar()
     while x:
         x = bar()
     if x and y:
         bar()
     if not x:
         bar()
     return foo
     for (x, y) in dict.items(): ...
No:  if (x):
         bar()
     if not(x):
         bar()
     return (foo)
```

## 缩进

用4个空格来缩进代码

绝对不要用tab, 也不要tab和空格混用. 对于行连接的情况, 你应该要么垂直对齐换行的元素(见 :ref:`行长度 <line_length>` 部分的示例), 或者使用4空格的悬挂式缩进(这时第一行不应该有参数):

```python
Yes:   # 与起始变量对齐
       foo = long_function_name(var_one, var_two,
                                var_three, var_four)

       # 字典中与起始值对齐
       foo = {
           long_dictionary_key: value1 +
                                value2,
           ...
       }

       # 4 个空格缩进，第一行不需要
       foo = long_function_name(
           var_one, var_two, var_three,
           var_four)

       # 字典中 4 个空格缩进
       foo = {
           long_dictionary_key:
               long_dictionary_value,
           ...
       }
No:    # 第一行有空格是禁止的
      foo = long_function_name(var_one, var_two,
          var_three, var_four)

      # 2 个空格是禁止的
      foo = long_function_name(
        var_one, var_two, var_three,
        var_four)

      # 字典中没有处理缩进
      foo = {
          long_dictionary_key:
              long_dictionary_value,
              ...
      }
```

## 空行

顶级定义之间空两行, 方法定义之间空一行

顶级定义之间空两行, 比如函数或者类定义. 方法定义, 类定义与第一个方法之间, 都应该空一行. 函数或方法中, 某些地方要是你觉得合适, 就空一行.

## 空格

按照标准的排版规范来使用标点两边的空格

括号内不要有空格.

按照标准的排版规范来使用标点两边的空格

```python
Yes: spam(ham[1], {eggs: 2}, [])
```

```python
No:  spam( ham[ 1 ], { eggs: 2 }, [ ] )
```

不要在逗号, 分号, 冒号前面加空格, 但应该在它们后面加(除了在行尾).

```python
Yes: if x == 4:
         print x, y
     x, y = y, x
```

```python
No:  if x == 4 :
         print x , y
     x , y = y , x
```

参数列表, 索引或切片的左括号前不应加空格.

```python
Yes: spam(1)
```

```python
no: spam (1)
```

```python
Yes: dict['key'] = list[index]
```

```python
No:  dict ['key'] = list [index]
```

在二元操作符两边都加上一个空格, 比如赋值(=), 比较(==, <, >, !=, <>, <=, >=, in, not in, is, is not), 布尔(and, or, not).  至于算术操作符两边的空格该如何使用, 需要你自己好好判断. 不过两侧务必要保持一致.

```python
Yes: x == 1
```

```python
No:  x<1
```

当'='用于指示关键字参数或默认参数值时, 不要在其两侧使用空格.

```python
Yes: def complex(real, imag=0.0): return magic(r=real, i=imag)
```

```python
No:  def complex(real, imag = 0.0): return magic(r = real, i = imag)
```

不要用空格来垂直对齐多行间的标记, 因为这会成为维护的负担(适用于:, #, =等):

```python
Yes:
     foo = 1000  # 注释
     long_name = 2  # 注释不需要对齐

     dictionary = {
         "foo": 1,
         "long_name": 2,
         }
```

```python
No:
     foo       = 1000  # 注释
     long_name = 2     # 注释不需要对齐

     dictionary = {
         "foo"      : 1,
         "long_name": 2,
         }
```

------

## Shebang

大部分.py文件不必以#!作为文件的开始. 根据 [PEP-394](http://www.python.org/dev/peps/pep-0394/) , 程序的main文件应该以 #!/usr/bin/python2或者 #!/usr/bin/python3开始.

(译者注: 在计算机科学中, [Shebang](http://en.wikipedia.org/wiki/Shebang_%28Unix%29) (也称为Hashbang)是一个由井号和叹号构成的字符串行(#!), 其出现在文本文件的第一行的前两个字符. 在文件中存在Shebang的情况下, 类Unix操作系统的程序载入器会分析Shebang后的内容, 将这些内容作为解释器指令, 并调用该指令, 并将载有Shebang的文件路径作为该解释器的参数. 例如, 以指令#!/bin/sh开头的文件在执行时会实际调用/bin/sh程序.)

\#!先用于帮助内核找到Python解释器, 但是在导入模块时, 将会被忽略. 因此只有被直接执行的文件中才有必要加入#!.

## 注释

确保对模块, 函数, 方法和行内注释使用正确的风格

**文档字符串**

> Python有一种独一无二的的注释方式: 使用文档字符串. 文档字符串是包, 模块, 类或函数里的第一个语句. 这些字符串可以通过对象的__doc__成员被自动提取, 并且被pydoc所用. (你可以在你的模块上运行pydoc试一把, 看看它长什么样). 我们对文档字符串的惯例是使用三重双引号"""( [PEP-257](http://www.python.org/dev/peps/pep-0257/) ). 一个文档字符串应该这样组织: 首先是一行以句号, 问号或惊叹号结尾的概述(或者该文档字符串单纯只有一行). 接着是一个空行. 接着是文档字符串剩下的部分, 它应该与文档字符串的第一行的第一个引号对齐. 下面有更多文档字符串的格式化规范.

**模块**

> 每个文件应该包含一个许可样板. 根据项目使用的许可(例如, Apache 2.0, BSD, LGPL, GPL), 选择合适的样板.

**函数和方法**

> 下文所指的函数,包括函数, 方法, 以及生成器.
>
> 一个函数必须要有文档字符串, 除非它满足以下条件:
>
> 1. 外部不可见
> 2. 非常短小
> 3. 简单明了
>
> 文档字符串应该包含函数做什么, 以及输入和输出的详细描述. 通常, 不应该描述"怎么做", 除非是一些复杂的算法. 文档字符串应该提供足够的信息, 当别人编写代码调用该函数时, 他不需要看一行代码, 只要看文档字符串就可以了. 对于复杂的代码, 在代码旁边加注释会比使用文档字符串更有意义.
>
> 关于函数的几个方面应该在特定的小节中进行描述记录， 这几个方面如下文所述. 每节应该以一个标题行开始. 标题行以冒号结尾. 除标题行外, 节的其他内容应被缩进2个空格.
>
> - Args:
>
>   列出每个参数的名字, 并在名字后使用一个冒号和一个空格, 分隔对该参数的描述.如果描述太长超过了单行80字符,使用2或者4个空格的悬挂缩进(与文件其他部分保持一致).描述应该包括所需的类型和含义.如果一个函数接受*foo(可变长度参数列表)或者**bar (任意关键字参数), 应该详细列出*foo和**bar.
>
> - Returns: (或者 Yields: 用于生成器)
>
>   描述返回值的类型和语义. 如果函数返回None, 这一部分可以省略.
>
> - Raises:
>
>   列出与接口有关的所有异常.
>
> ```python
> def fetch_bigtable_rows(big_table, keys, other_silly_variable=None):
>     """Fetches rows from a Bigtable.
>
>     Retrieves rows pertaining to the given keys from the Table instance
>     represented by big_table.  Silly things may happen if
>     other_silly_variable is not None.
>
>     Args:
>         big_table: An open Bigtable Table instance.
>         keys: A sequence of strings representing the key of each table row
>             to fetch.
>         other_silly_variable: Another optional variable, that has a much
>             longer name than the other args, and which does nothing.
>
>     Returns:
>         A dict mapping keys to the corresponding table row data
>         fetched. Each row is represented as a tuple of strings. For
>         example:
>
>         {'Serak': ('Rigel VII', 'Preparer'),
>          'Zim': ('Irk', 'Invader'),
>          'Lrrr': ('Omicron Persei 8', 'Emperor')}
>
>         If a key from the keys argument is missing from the dictionary,
>         then that row was not found in the table.
>
>     Raises:
>         IOError: An error occurred accessing the bigtable.Table object.
>     """
>     pass
> ```

**类**

> 类应该在其定义下有一个用于描述该类的文档字符串. 如果你的类有公共属性(Attributes), 那么文档中应该有一个属性(Attributes)段. 并且应该遵守和函数参数相同的格式.
>
> ```python
> class SampleClass(object):
>     """Summary of class here.
>
>     Longer class information....
>     Longer class information....
>
>     Attributes:
>         likes_spam: A boolean indicating if we like SPAM or not.
>         eggs: An integer count of the eggs we have laid.
>     """
>
>     def __init__(self, likes_spam=False):
>         """Inits SampleClass with blah."""
>         self.likes_spam = likes_spam
>         self.eggs = 0
>
>     def public_method(self):
>         """Performs operation blah."""
> ```

**块注释和行注释**

> 最需要写注释的是代码中那些技巧性的部分. 如果你在下次 [代码审查](http://en.wikipedia.org/wiki/Code_review) 的时候必须解释一下, 那么你应该现在就给它写注释. 对于复杂的操作, 应该在其操作开始前写上若干行注释. 对于不是一目了然的代码, 应在其行尾添加注释.
>
> ```python
> # We use a weighted dictionary search to find out where i is in
> # the array.  We extrapolate position based on the largest num
> # in the array and the array size and then do binary search to
> # get the exact number.
>
> if i & (i-1) == 0:        # true iff i is a power of 2
> ```
>
> 为了提高可读性, 注释应该至少离开代码2个空格.
>
> 另一方面, 绝不要描述代码. 假设阅读代码的人比你更懂Python, 他只是不知道你的代码要做什么.
>
> ```python
> # BAD COMMENT: Now go through the b array and make sure whenever i occurs
> # the next element is i+1
> ```

## 类

如果一个类不继承自其它类, 就显式的从object继承. 嵌套类也一样.

```python
Yes: class SampleClass(object):
         pass


     class OuterClass(object):

         class InnerClass(object):
             pass


     class ChildClass(ParentClass):
         """Explicitly inherits from another class already."""
No: class SampleClass:
        pass


    class OuterClass:

        class InnerClass:
            pass
```

继承自 `object` 是为了使属性(properties)正常工作, 并且这样可以保护你的代码, 使其不受Python 3000的一个特殊的潜在不兼容性影响. 这样做也定义了一些特殊的方法, 这些方法实现了对象的默认语义, 包括 `__new__, __init__, __delattr__, __getattribute__, __setattr__, __hash__, __repr__, and __str__` .

## 字符串

```python
Yes: x = a + b
     x = '%s, %s!' % (imperative, expletive)
     x = '{}, {}!'.format(imperative, expletive)
     x = 'name: %s; score: %d' % (name, n)
     x = 'name: {}; score: {}'.format(name, n)
```

```python
No: x = '%s%s' % (a, b)  # use + in this case
    x = '{}{}'.format(a, b)  # use + in this case
    x = imperative + ', ' + expletive + '!'
    x = 'name: ' + name + '; score: ' + str(n)
```

避免在循环中用+和+=操作符来累加字符串. 由于字符串是不可变的, 这样做会创建不必要的临时对象, 并且导致二次方而不是线性的运行时间. 作为替代方案, 你可以将每个子串加入列表, 然后在循环结束后用 `.join` 连接列表. (也可以将每个子串写入一个 `cStringIO.StringIO` 缓存中.)

```python
Yes: items = ['<table>']
     for last_name, first_name in employee_list:
         items.append('<tr><td>%s, %s</td></tr>' % (last_name, first_name))
     items.append('</table>')
     employee_table = ''.join(items)
```

```python
No: employee_table = '<table>'
    for last_name, first_name in employee_list:
        employee_table += '<tr><td>%s, %s</td></tr>' % (last_name, first_name)
    employee_table += '</table>'
```

在同一个文件中, 保持使用字符串引号的一致性. 使用单引号'或者双引号"之一用以引用字符串, 并在同一文件中沿用. 在字符串内可以使用另外一种引号, 以避免在字符串中使用. PyLint已经加入了这一检查.

```python
Yes:
     Python('Why are you hiding your eyes?')
     Gollum("I'm scared of lint errors.")
     Narrator('"Good!" thought a happy Python reviewer.')
```

```python
No:
     Python("Why are you hiding your eyes?")
     Gollum('The lint. It burns. It burns us.')
     Gollum("Always the great lint. Watching. Watching.")
```

为多行字符串使用三重双引号"""而非三重单引号'''. 当且仅当项目中使用单引号'来引用字符串时, 才可能会使用三重'''为非文档字符串的多行字符串来标识引用. 文档字符串必须使用三重双引号""". 不过要注意, 通常用隐式行连接更清晰, 因为多行字符串与程序其他部分的缩进方式不一致.

```python
Yes:
    print ("This is much nicer.\n"
           "Do it this way.\n")
No:
      print """This is pretty ugly.
  Don't do this.
  """
```

