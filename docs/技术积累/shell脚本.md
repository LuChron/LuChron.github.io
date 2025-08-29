## 1 Shell 脚本

Shell 脚本（shell script），是一种为 shell 编写的脚本程序。

## 2 Shell 环境

Shell 编程跟 JavaScript 编程一样，只要有一个能编写代码的文本编辑器和一个能解释执行的脚本解释器就可以了。

Linux 的 Shell 种类众多，常见的有：

- Bourne Shell（/usr/bin/sh或/bin/sh）
- Bourne Again Shell（/bin/bash）
- C Shell（/usr/bin/csh）
- K Shell（/usr/bin/ksh）
- Shell for Root（/sbin/sh）
- ……

我们这里关注的是 Bas。Bash 也是大多数Linux 系统默认的 Shell。

在一般情况下，人们并不区分 Bourne Shell 和 Bourne Again Shell，所以，像 **#!/bin/sh**，它同样也可以改为 **#!/bin/bash**。

==**#!** 告诉系统其后路径所指定的程序即是解释此脚本文件的 Shell 程序。==

## 3 第一个shell脚本

打开文本编辑器(可以使用 vi/vim 命令来创建文件)，新建一个文件 test.sh，扩展名为 sh（sh代表shell），扩展名并不影响脚本执行.。

输入一些代码，第一行一般是这样：

```bash
#!/bin/bash
echo "Hello World !"
```

**#!** 是一个约定的标记，它告诉系统这个脚本需要什么解释器来执行，即使用哪一种 Shell。

echo 命令用于向窗口输出文本。

### 3.1 运行 Shell 脚本有两种方法：

**1、作为可执行程序**

将上面的代码保存为 test.sh，并 cd 到相应目录：

```shell
chmod +x ./test.sh  #使脚本具有执行权限
./test.sh  #执行脚本
```

注意，一定要写成 **./test.sh**，而不是 **test.sh**，运行其它二进制的程序也一样，直接写 test.sh，linux 系统会去 PATH 里寻找有没有叫 test.sh 的，而只有 /bin, /sbin, /usr/bin，/usr/sbin 等在 PATH 里，你的当前目录通常不在 PATH 里，所以写成 test.sh 是会找不到命令的，要用 ./test.sh 告诉系统说，就在当前目录找。

**2、作为解释器参数**

这种运行方式是，直接运行解释器，其参数就是 shell 脚本的文件名，如：

```shell
/bin/sh test.sh
#或者
sh test.sh
```

这种方式运行的脚本，不需要在第一行指定解释器信息，写了也没用。

## 4 shell变量

### 4.1 命名规则

- **只包含字母、数字和下划线：** 变量名可以包含字母（大小写敏感）、数字和下划线 **_**，不能包含其他特殊字符。
- **不能以数字开头：** 变量名不能以数字开头，但可以包含数字。
- **避免使用 Shell 关键字：** 不要使用Shell的关键字（例如 if、then、else、fi、for、while 等）作为变量名，以免引起混淆。
- **使用大写字母表示常量：** 习惯上，常量的变量名通常使用大写字母，例如 **PI=3.14**。
- **避免使用特殊符号：** 尽量避免在变量名中使用特殊符号，因为它们可能与 Shell 的语法产生冲突。
- **避免使用空格：** 变量名中不应该包含空格，因为空格通常用于分隔命令和参数。

比如：

```bash
RUNOOB="www.runoob.com"
LD_LIBRARY_PATH="/bin/"
_var="123"
var2="abc"
```

但是注意，和平常的格式化美观不同：这里==避免等号两边使用空格==

除了显式地直接赋值，还可以用语句给变量赋值，如：

```bash
for file in `ls /etc`
或
for file in $(ls /etc)
```

以上语句将 /etc 下目录的文件名循环出来。

### 4.2 使用变量

使用一个定义过的变量，只要在变量名前面加美元符号即可，如

```bash
your_name="tom"
echo $your_name
your_name="alibaba"
echo $your_name
```

使用 readonly 命令可以将变量定义为只读变量，只读变量的值不能被改变。

### 4.3 只读变量

下面的例子尝试更改只读变量，结果报错：

```bash
#!/bin/bash

myUrl="https://www.google.com"
readonly myUrl
myUrl="https://www.runoob.com"
```

上述运行时编译器会报错。

### 4.4 删除变量

使用 unset 命令可以删除变量。语法：

```
unset variable_name
```

变量被删除后不能再次使用。unset 命令不能删除只读变量。

### 4.5 变量类型

Shell 支持不同类型的变量，其中一些主要的类型包括：

**字符串变量：** 在 Shell中，变量通常被视为字符串。你可以使用单引号 **'** 或双引号 **"** 来定义字符串，例如：

```shell
my_string='Hello, World!'
或者
my_string="Hello, World!"
```

**整数变量**： 在一些Shell中，你可以使用 **declare** 或 **typeset** 命令来声明整数变量。这样的变量只包含整数值，例如：

```shell
declare -i my_integer=42
```

这样的声明告诉 Shell 将 my_integer 视为整数，如果尝试将非整数值赋给它，Shell会尝试将其转换为整数。

**数组变量：** Shell 也支持数组，允许你在一个变量中存储多个值。数组可以是整数索引数组或关联数组。

```shell
my_array=(1 2 3 4 5)
```

或者关联数组：

```shell
declare -A associative_array
associative_array["name"]="John"
associative_array["age"]=30
```

**环境变量：** 这些是由操作系统或用户设置的特殊变量，用于配置 Shell 的行为和影响其执行环境。

例如，PATH 变量包含了操作系统搜索可执行文件的路径：

```
echo $PATH
```

**特殊变量：** 有一些特殊变量在 Shell 中具有特殊含义，例如 **$0** 表示脚本的名称，**$1**, **$2**, 等表示脚本的参数。

**$#**表示传递给脚本的参数数量，**$?** 表示上一个命令的退出状态等。

### 4.6 Shell 字符串

字符串是shell编程中最常用最有用的数据类型（除了数字和字符串，也没啥其它类型好用了），字符串可以用单引号，也可以用双引号，也可以不用引号。

```shell
str='this is a string'
```

单引号字符串的限制：

- 单引号里的任何字符都会原样输出，==单引号字符串中的变量是无效的；==
- 单引号字符串中不能出现单独一个的单引号（对单引号使用转义符后也不行），但可成对出现，作为字符串拼接使用。

体会一下这个区别。比如：

```bash
your_name="runoob"
# 使用双引号拼接
greeting="hello, "$your_name" !"
greeting_1="hello, ${your_name} !"
echo $greeting  $greeting_1

# 使用单引号拼接
greeting_2='hello, '$your_name' !'
greeting_3='hello, ${your_name} !'
echo $greeting_2  $greeting_3
```

```bash
hello, runoob ! hello, runoob !
hello, runoob ! hello, ${your_name} !
```

> 其他的一些用法：
>
> ###### 获取字符串长度
>
> ```bash
> string="abcd"
> echo \${#string}   # 输出 4
> ```
>
> 变量为字符串时，**`${#string}`** 等价于 **`${#string[0]}`**
>
> ###### 提取子字符串
>
> 以下实例从字符串第 **2** 个字符开始截取 **4** 个字符：
>
> ```bash
> string="runoob is a great site"
> echo ${string:1:4} # 输出 unoo
> ```
>
> **注意**：第一个字符的索引值为 **0**。
>
> ###### 查找子字符串
>
> 查找字符 **i** 或 **o** 的位置(哪个字母先出现就计算哪个)：
>
> ```bash
> string="runoob is a great site"
> echo `expr index "$string" io`  # 输出 4
> ```
>
> **注意：** 以上脚本中 **`** 是反引号，而不是单引号 **'**，不要看错了哦。

bash支持一维数组（不支持多维数组），并且没有限定数组的大小。

类似于 C 语言，数组元素的下标由 0 开始编号。获取数组中的元素要利用下标，下标可以是整数或算术表达式，其值应大于或等于 0。

### 4.7 shell数组

在 Shell 中，用括号来表示数组，数组元素用"空格"符号分割开。定义数组的一般形式为：

```shell
数组名=(值1 值2 ... 值n)
```

例如：

```shell
array_name=(value0 value1 value2 value3)
```

或者

```shell
array_name=(
value0
value1
value2
value3
)
```

还可以单独定义数组的各个分量：

```shell
array_name[0]=value0
array_name[1]=value1
array_name[n]=valuen
```

可以不使用连续的下标，而且下标的范围没有限制。

### 4.7.1 读取数组

读取数组元素值的一般格式是：

```shell
${数组名[下标]}
```

例如：

```shell
valuen=${array_name[n]}
```

使用 **@** 符号可以获取数组中的所有元素，例如：

```shell
echo ${array_name[@]}
```

### 4.8 获取数组的长度

获取数组长度的方法与获取字符串长度的方法相同，例如：

```bash
# 取得数组元素的个数
length=\${#array_name[@]}
# 或者
length=\${#array_name[*]}
# 取得数组单个元素的长度
length=\${#array_name[n]}
```

### 4.9 注释

以 **#** 开头的行就是注释，会被解释器忽略。

通过每一行加一个 **#** 号设置多行注释，像这样：

```bash
#--------------------------------------------
# 这是一个注释
# author：Lucien
#--------------------------------------------
##### 用户配置区 开始 #####
#
#
# 这里可以添加脚本描述信息
# 
#
##### 用户配置区 结束  #####
```

## 5  Shell 传递参数

我们可以在执行 Shell 脚本时，向脚本传递参数，脚本内获取参数的格式为 **$n**，**n** 代表一个数字，**1** 为执行脚本的第一个参数，**2** 为执行脚本的第二个参数。

例如可以使用 **$1、$2** 等来引用传递给脚本的参数，其中 **$1** 表示第一个参数，**$2** 表示第二个参数，依此类推。

以下实例我们向脚本传递三个参数，并分别输出，其中 **$0** 为执行的文件名（包含文件路径）：

```bash
#!/bin/bash
# author:菜鸟教程
# url:www.runoob.com

echo "Shell 传递参数实例！";
echo "执行的文件名：$0";
echo "第一个参数为：$1";
echo "第二个参数为：$2";
echo "第三个参数为：$3";
```

运行：

```bash
$ chmod +x test.sh 
$ ./test.sh 1 2 3
Shell 传递参数实例！
执行的文件名：./test.sh
第一个参数为：1
第二个参数为：2
第三个参数为：3
```

| 参数处理 | 说明                                                         |
| :------- | :----------------------------------------------------------- |
| $#       | 传递到脚本的参数个数                                         |
| $*       | 以一个单字符串显示所有向脚本传递的参数。 如"$*"用「"」括起来的情况、以"$1 $2 … $n"的形式输出所有参数。 |
| $$       | 脚本运行的当前进程ID号                                       |
| $!       | 后台运行的最后一个进程的ID号                                 |
| $@       | 与$*相同，但是使用时加引号，并在引号中返回每个参数。 如"$@"用「"」括起来的情况、以"$1" "$2" … "$n" 的形式输出所有参数。 |
| $-       | 显示Shell使用的当前选项，与[set命令](https://www.runoob.com/linux/linux-comm-set.html)功能相同。 |
| $?       | 显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误。 |

## 6 shell 运算符

### 6.1 算数运算符

下表列出了常用的算术运算符，假定变量 a 为 10，变量 b 为 20：

| +    | 加法                                          | `expr $a + $b` 结果为 30。    |
| ---- | --------------------------------------------- | ----------------------------- |
| -    | 减法                                          | `expr $a - $b` 结果为 -10。   |
| *    | 乘法                                          | `expr $a \* $b` 结果为  200。 |
| /    | 除法                                          | `expr $b / $a` 结果为 2。     |
| %    | 取余                                          | `expr $b % $a` 结果为 0。     |
| =    | 赋值                                          | a=$b 把变量 b 的值赋给 a。    |
| ==   | 相等。用于比较两个数字，相同则返回 true。     | `[ $a == $b ] `返回 false。   |
| !=   | 不相等。用于比较两个数字，不相同则返回 true。 | `[ $a != $b ] `返回 true。    |

条件表达式要放在方括号之间，并且要有空格，例如: **``[$a==$b]``** 是错误的，必须写成 **`[ $a == $b ]`**。

### 6.2 关系运算符

下表列出了常用的关系运算符，假定变量 a 为 10，变量 b 为 20：

| 运算符 | 说明                                                  | 举例                         |
| :----- | :---------------------------------------------------- | :--------------------------- |
| -eq    | 检测两个数是否相等，相等返回 true。                   | `[ $a -eq $b ] `返回 false。 |
| -ne    | 检测两个数是否不相等，不相等返回 true。               | `[ $a -ne $b ] `返回 true。  |
| -gt    | 检测左边的数是否大于右边的，如果是，则返回 true。     | `[ $a -gt $b ]` 返回 false。 |
| -lt    | 检测左边的数是否小于右边的，如果是，则返回 true。     | `[ $a -lt $b ] `返回 true。  |
| -ge    | 检测左边的数是否大于等于右边的，如果是，则返回 true。 | `[ $a -ge $b ] `返回 false。 |
| -le    | 检测左边的数是否小于等于右边的，如果是，则返回 true。 | `[ $a -le $b ] `返回 true。  |

### 6.3 布尔运算符

下表列出了常用的布尔运算符，假定变量 a 为 10，变量 b 为 20：

| 运算符 | 说明                                                | 举例                                       |
| :----- | :-------------------------------------------------- | :----------------------------------------- |
| !      | 非运算，表达式为 true 则返回 false，否则返回 true。 | [ ! false ] 返回 true。                    |
| -o     | 或运算，有一个表达式为 true 则返回 true。           | `[ $a -lt 20 -o $b -gt 100 ]` 返回 true。  |
| -a     | 与运算，两个表达式都为 true 才返回 true。           | `[ $a -lt 20 -a $b -gt 100 ] `返回 false。 |

> 这些是常用的，其他略。可查看菜鸟教程。

## 7 Shell echo 

`echo` 是一个内置的 Shell 命令，用于在标准输出（通常是终端）显示一行文本或变量的值。

**命令格式：**

```shell
echo [选项] [字符串]
```

为什么需要 echo？

- **信息反馈**：向用户显示脚本执行状态或结果
- **调试工具**：输出变量值或执行位置，帮助调试脚本
- **交互界面**：创建简单的用户交互界面
- **文件生成**：快速生成配置文件或脚本

| `\n` | 换行           |
| ---- | -------------- |
| `\t` | 水平制表符     |
| `\v` | 垂直制表符     |
| `\b` | 退格           |
| `\r` | 回车           |
| `\\` | 反斜杠字符本身 |

## 8 Shell test 命令

`test` 命令是 Shell 内置的条件判断工具，用于评估表达式并返回布尔值（真/假），它通常与 `if` 语句结合使用，是 Shell 脚本中实现逻辑控制的基础。

Shell 中的 test 命令用于检查某个条件是否成立，它可以进行数值、字符和文件三个方面的测试。

### 语法格式

```shell
test EXPRESSION
# 或
[ EXPRESSION ]  # 注意方括号内必须有空格
```

`test` 命令最常用于检查文件属性，以下是常用文件测试选项：

| 操作符 | 描述         | 示例                   |
| :----- | :----------- | :--------------------- |
| -e     | 文件是否存在 | `[ -e file.txt ]`      |
| -f     | 是普通文件   | `[ -f /path/to/file ]` |
| -d     | 是目录       | `[ -d /path/to/dir ]`  |
| -r     | 可读         | `[ -r file.txt ]`      |
| -w     | 可写         | `[ -w file.txt ]`      |
| -x     | 可执行       | `[ -x script.sh ]`     |
| -s     | 文件大小 >0  | `[ -s logfile ]`       |
| -L     | 是符号链接   | `[ -L symlink ]`       |

例子：

```bash
#!/bin/bash

file="/etc/passwd"

if [ -e "$file" ]; then
    echo "$file 存在"
    if [ -r "$file" ]; then
        echo "并且可读"
    fi
else
    echo "$file 不存在"
fi
```

## 9 shell流程控制

if 语句语法格式：

```bash
if condition
then
    command1 
    command2
    ...
    commandN 
fi
```

写成一行（适用于终端命令提示符）：

```bash
if [ $(ps -ef | grep -c "ssh") -gt 1 ]; then echo "true"; fi
```

末尾的 **fi** 就是 **if** 倒过来拼写，后面还会遇到类似的。

### 9.1 if else

if else 语法格式：

```bash
if condition
then
    command1 
    command2
    ...
    commandN
else
    command
fi
```

### 9.2 if else-if else

if else-if else 语法格式：

```bash
if condition1
then
    command1
elif condition2 
then 
    command2
else
    commandN
fi
```

if else 的 **[...]** 判断语句中大于使用 **-gt**，小于使用 **-lt**。

```bash
if [ "$a" -gt "$b" ]; then
    ...
fi
```

如果使用 **((...))** 作为判断语句，大于和小于可以直接使用 **>** 和 **<**。

```bash
if (( a > b )); then
    ...
fi
```

### 9.3 for 循环

与其他编程语言类似，Shell支持for循环。

for循环一般格式为：

```bash
for var in item1 item2 ... itemN
do
    command1
    command2
    ...
    commandN
done
```

写成一行：

```bash
for var in item1 item2 ... itemN; do command1; command2… done;
```

当变量值在列表里，for 循环即执行一次所有命令，使用变量名获取列表中的当前取值。命令可为任何有效的 shell 命令和语句。in 列表可以包含替换、字符串和文件名。

in列表是可选的，如果不用它，for循环使用命令行的位置参数。

```bash
for loop in 1 2 3 4 5
do
    echo "The value is: $loop"
done
```

输出：

```bash
The value is: 1
The value is: 2
The value is: 3
The value is: 4
The value is: 5
```

### 9.4 while 语句

while 循环用于不断执行一系列命令，也用于从输入文件中读取数据。其语法格式为：

```bash
while condition
do
    command
done
```

### 9.5 until 循环

until 循环执行一系列命令直至条件为 true 时停止。until 循环与 while 循环在处理方式上刚好相反。

until 语法格式:

```bash
until condition
do
    command
done
```

### 9.6 case ... esac 语句

**case ... esac** 为多选择语句，与其他语言中的 switch ... case 语句类似，是一种多分支选择结构，每个 case 分支用右圆括号开始，用两个分号 **;;** 表示 break，即执行结束，跳出整个 case ... esac 语句，esac（就是 case 反过来）作为结束标记。

可以用 case 语句匹配一个值与一个模式，如果匹配成功，执行相匹配的命令。

**case ... esac** 语法格式如下：

```bash
case 值 in
模式1)
    command1
    command2
    ...
    commandN
    ;;
模式2)
    command1
    command2
    ...
    commandN
    ;;
esac
```

实例：

```bash
echo '输入 1 到 4 之间的数字:'
echo '你输入的数字为:'
read aNum
case $aNum in
    1)  echo '你选择了 1'
    ;;
    2)  echo '你选择了 2'
    ;;
    3)  echo '你选择了 3'
    ;;
    4)  echo '你选择了 4'
    ;;
    *)  echo '你没有输入 1 到 4 之间的数字'
    ;;
esac
```

### 9.7 跳出循环

在循环过程中，有时候需要在未达到循环结束条件时强制跳出循环，Shell 使用两个命令来实现该功能：**break** 和 **continue**。

#### 9.7.1 break 命令

break 命令允许跳出所有循环（终止执行后面的所有循环）。

下面的例子中，脚本进入死循环直至用户输入数字大于5。要跳出这个循环，返回到shell提示符下，需要使用break命令。

```bash
#!/bin/bash
while :
do
    echo -n "输入 1 到 5 之间的数字:"
    read aNum
    case $aNum in
        1|2|3|4|5) echo "你输入的数字为 $aNum!"
        ;;
        *) echo "你输入的数字不是 1 到 5 之间的! 游戏结束"
            break
        ;;
    esac
done
```

#### 9.7.2 continue 命令

continue 命令与 break 命令类似，只有一点差别，它不会跳出所有循环，仅仅跳出当前循环。

## 10 Shell 函数

### 10.1 函数定义

linux shell 可以用户定义函数，然后在shell脚本中可以随便调用。

shell中函数的定义格式如下：

```bash
[ function ] funname [()]

{
    action;
    [return int;]
}
```

说明：

- 1、可以带 **function fun()** 定义，也可以直接 **fun()** 定义,不带任何参数。
- 2、参数返回，可以显示加：**return** 返回，如果不加，将以最后一条命令运行结果，作为返回值。 **return** 后跟数值 **n(0-255)**.

下面的例子定义了一个函数并进行调用：

```bash
#!/bin/bash

funWithReturn(){
    echo "这个函数会对输入的两个数字进行相加运算..."
    echo "输入第一个数字: "
    read aNum
    echo "输入第二个数字: "
    read anotherNum
    echo "两个数字分别为 $aNum 和 $anotherNum !"
    return $(($aNum+$anotherNum))
}
funWithReturn
echo "输入的两个数字之和为 $? !"
```

输出：

```bash
这个函数会对输入的两个数字进行相加运算...
输入第一个数字: 
1
输入第二个数字: 
2
两个数字分别为 1 和 2 !
输入的两个数字之和为 3 !
```

函数返回值在调用该函数后通过 **$?** 来获得。

**注意：**所有函数在使用前必须定义。这意味着必须将函数放在脚本开始部分，直至shell解释器首次发现它时，才可以使用。调用函数仅使用其函数名即可。

**注意：** **return** 语句只能返回一个介于 0 到 255 之间的整数，而两个输入数字的和可能超过这个范围。

### 10.2 函数参数

在Shell中，调用函数时可以向其传递参数。在函数体内部，通过 $n 的形式来获取参数的值，例如，$1表示第一个参数，$2表示第二个参数...

```bash
#!/bin/bash

funWithParam(){
    echo "第一个参数为 $1 !"
    echo "第二个参数为 $2 !"
    echo "第十个参数为 $10 !"
    echo "第十个参数为 ${10} !"
    echo "第十一个参数为 ${11} !"
    echo "参数总数有 $# 个!"
    echo "作为一个字符串输出所有参数 $* !"
}
funWithParam 1 2 3 4 5 6 7 8 9 34 73
```

## 11 Shell 输入/输出重定向

大多数系统命令从你的终端接受输入并将所产生的输出发送回到您的终端。一个命令通常从一个叫标准输入的地方读取输入，默认情况下，这恰好是你的终端。同样，一个命令通常将其输出写入到标准输出，默认情况下，这也是你的终端。

重定向命令列表如下：

| 命令            | 说明                                               |
| :-------------- | :------------------------------------------------- |
| command > file  | 将输出重定向到 file。                              |
| command < file  | 将输入重定向到 file。                              |
| command >> file | 将输出以追加的方式重定向到 file。                  |
| n > file        | 将文件描述符为 n 的文件重定向到 file。             |
| n >> file       | 将文件描述符为 n 的文件以追加的方式重定向到 file。 |
| n >& m          | 将输出文件 m 和 n 合并。                           |
| n <& m          | 将输入文件 m 和 n 合并。                           |
| << tag          | 将开始标记 tag 和结束标记 tag 之间的内容作为输入。 |

> 需要注意的是文件描述符 0 通常是标准输入（STDIN），1 是标准输出（STDOUT），2 是标准错误输出（STDERR）。

### 11.1 输出重定向

重定向一般通过在命令间插入特定的符号来实现。特别的，这些符号的语法如下所示:

```bash
command1 > file1
```

上面这个命令执行command1然后将输出的内容存入file1。

注意任何file1内的已经存在的内容将被新内容替代。如果要将新内容添加在文件末尾，请使用>>操作符。

执行下面的 who 命令，它将命令的完整的输出重定向在用户文件中(users):

```bash
$ who > users
```

执行后，并没有在终端输出信息，这是因为输出已被从默认的标准输出设备（终端）重定向到指定的文件。

你可以使用 cat 命令查看文件内容：

```bash
$ cat users
_mbsetupuser console  Oct 31 17:35 
tianqixin    console  Oct 31 17:35 
tianqixin    ttys000  Dec  1 11:33 
```

==输出重定向会覆盖文件内容==

如果不希望文件内容被覆盖，可以使用 >> 追加到文件末尾，例如：

### 11.2 输入重定向

和输出重定向一样，Unix 命令也可以从文件获取输入，语法为：

```bash
command1 < file1
```

这样，本来需要从键盘获取输入的命令会转移到文件读取内容。

注意：输出重定向是大于号(>)，输入重定向是小于号(<)。

接着以上实例，我们需要统计 users 文件的行数,执行以下命令：

```bash
$ wc -l users
       2 users
```

也可以将输入重定向到 users 文件：

```bash
$  wc -l < users
       2 
```

注意：上面两个例子的结果不同：第一个例子，会输出文件名；第二个不会，因为它仅仅知道从标准输入读取内容。

```bash
command1 < infile > outfile
```

同时替换输入和输出，执行command1，从文件infile读取内容，然后将输出写入到outfile中。

