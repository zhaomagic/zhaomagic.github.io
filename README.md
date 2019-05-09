Shell基础
1.	Shell简介
Shell是一个命令行解释工具（是一个软件），它将用户输入的命令解析为内核能够理解的语言（命令）。
Shell 除了能解释用户输入的命令，将它传递给内核，还可以：调用其他程序，给其他程序传递数据或参数，并获取程序的处理结果；在多个程序之间传递数据，把一个程序的输出作为另一个程序的输入；Shell 本身也可以被其他程序调用。
由此可见，Shell 是将内核、程序和用户连接了起来。
Shell 本身支持的命令并不多，但是它可以调用其他的程序，每个程序就是一个命令，这使得 Shell 命令的数量可以无限扩展，其结果就是 Shell 的功能非常强大，完全能够胜任 Linux 的日常管理工作，如文本或字符串检索、文件的查找或创建、软件的自动部署、更改系统设置、监控服务器性能、发送报警邮件、抓取网页内容、压缩文件等。

Shell 并不是简单的堆砌命令，我们还可以在 Shell 中编程，这和使用 C/C++、Java、Python 等常见的编程语言并没有什么两样。

Shell 虽然没有 C/C++、Java、Python 等强大，但也支持了基本的编程元素，例如：
if...else 选择结构，switch...case 开关语句，for、while、until 循环；
变量、数组、字符串、注释、加减乘除、逻辑运算等概念；
函数，包括用户自定义的函数和内置函数（例如 printf、export、eval 等）。

站在这个角度讲，Shell 也是一种编程语言，它的编译器（解释器）是 Shell 这个程序。我们平时所说的 Shell，有时候是指连接用户和内核的这个程序，有时候又是指 Shell 编程。

Shell 主要用来开发一些实用的、自动化的小工具，而不是用来开发具有复杂业务逻辑的中大型软件，例如检测计算机的硬件参数、一键搭建Web开发环境、日志分析等，Shell 都非常合适。


2.	几种常见的shell
2.1.	常见的 Shell 有 sh、bash、csh、tcsh、ash 等。

默认shell：bash

bash shell 是 Linux 的默认 shell，本文档也基于 bash 编写。

bash 由 GNU 组织开发，保持了对 sh shell 的兼容性，是各种 Linux 发行版默认配置的 shell。
bash 兼容 sh 意味着，针对 sh 编写的 Shell 代码可以不加修改地在 bash 中运行。
2.2.	查看shell
Shell 是一个程序，一般都是放在/bin或者/user/bin目录下，当前 Linux 系统可用的 Shell 都记录在/etc/shells文件中。/etc/shells是一个纯文本文件，可以使用 cat 命令查看它


查看系统默认shell：
$ echo $SHELL
	/bin/bash
输出结果表明默认的 Shell 是 bash。
3.	Shell命令
3.1.	Shell提示符
启动终端模拟包或者从 Linux 控制台登录后，便可以看到 Shell 提示符，是输入 Shell 命令的地方。

对于普通用户，Base shell 默认的提示符是美元符号$；对于超级用户（root 用户），Bash Shell 默认的提示符是井号#。该符号表示 Shell 等待输入命令。

3.2.	Shell变量
在 Bash shell 中，每一个变量的值都是字符串，无论你给变量赋值时有没有使用引号，值都会以字符串的形式存储。
3.2.1.	定义变量
例：variable='value'
注意，赋值号的周围不能有空格
Shell 变量的命名规范和大部分编程语言都一样：变量名由数字、字母、下划线组成；必须以字母或者下划线开头；不能使用 Shell 里的关键字（通过 help 命令可以查看保留关键字）。

3.2.2.	使用变量
例：echo $variable   echo ${variable}
变量名外面的花括号{ }是可选的，加不加都行，加花括号是为了帮助解释器识别变量的边界，推荐给所有变量加上花括号{ }，这是个良好的编程习惯。

3.2.3.	将命令的结果赋值给变量
例：variable=`command`
variable=$(command)

第一种方式把命令用反引号包围起来，；第二种方式把命令用$()包围起来，区分更加明显，所以推荐使用这种方式。

3.2.4.	只读变量
使用 readonly 命令可以将变量定义为只读变量，只读变量的值不能被改变。

例：
variable='value'
readonly variable

3.2.5.	删除变量
使用 unset 命令可以删除变量。语法：
unset variable

3.2.6.	特殊变量
特殊变量列表
变量	含义
$0	当前脚本的文件名
$n	传递给脚本或函数的参数。n 是一个数字，表示第几个参数。例如，第一个参数是$1，第二个参数是$2。
$#	传递给脚本或函数的参数个数。
$*	传递给脚本或函数的所有参数。
$@	传递给脚本或函数的所有参数。被双引号(" ")包含时，与 $* 稍有不同，下面将会讲到。
$?	上个命令的退出状态，或函数的返回值。
$$	当前Shell进程ID。对于 Shell 脚本，就是这些脚本所在的进程ID。

$* 和 $@ 的区别：
$* 和 $@ 都表示传递给函数或脚本的所有参数，不被双引号(" ")包含时，都以"$1" "$2" … "$n" 的形式输出所有参数。

但是当它们被双引号(" ")包含时，"$*" 会将所有的参数作为一个整体，以"$1 $2 … $n"的形式输出所有参数；"$@" 会将各个参数分开，以"$1" "$2" … "$n" 的形式输出所有参数。

3.2.7.	命令行参数
运行脚本时传递给脚本的参数称为命令行参数。命令行参数用 $n 表示，例如，$1 表示第一个参数，$2 表示第二个参数，依次类推。

3.3.	Shell运算符
3.3.1.	算术运算符
原生bash不支持简单的数学运算，但是可以通过其他命令来实现，例如 awk 和 expr，expr 最常用。

expr 是一款表达式计算工具，使用它能完成表达式的求值操作。

例：
val=`expr 2 + 2`
echo "Total value : $val"

注意：
表达式和运算符之间要有空格，例如 2+2 是不对的，必须写成 2 + 2，这与我们熟悉的大多数编程语言不一样。
完整的表达式要被 ` ` 包含，注意这个字符是反引号。

算术运算符列表
运算符	说明	举例
+	加法	`expr $a + $b` 结果为 30。
-	减法	`expr $a - $b` 结果为 10。
*	乘法	`expr $a \* $b` 结果为  200。
/	除法	`expr $b / $a` 结果为 2。
%	取余	`expr $b % $a` 结果为 0。
=	赋值	a=$b 将把变量 b 的值赋给 a。
==	相等。用于比较两个数字，相同则返回 true。	[ $a == $b ] 返回 false。
!=	不相等。用于比较两个数字，不相同则返回 true。	[ $a != $b ] 返回 true。

注意：
乘号(*)前边必须加反斜杠(\)才能实现乘法运算；
条件表达式要放在方括号之间，并且要有空格，例如 [$a==$b] 是错误的，必须写成 [ $a == $b ]。
3.3.2.	关系运算符
关系运算符只支持数字，不支持字符串，除非字符串的值是数字。
关系运算符列表
运算符	说明	举例
-eq	检测两个数是否相等，相等返回 true。	[ $a -eq $b ] 返回 true。
-ne	检测两个数是否相等，不相等返回 true。	[ $a -ne $b ] 返回 true。
-gt	检测左边的数是否大于右边的，如果是，则返回 true。	[ $a -gt $b ] 返回 false。
-lt	检测左边的数是否小于右边的，如果是，则返回 true。	[ $a -lt $b ] 返回 true。
-ge	检测左边的数是否大等于右边的，如果是，则返回 true。	[ $a -ge $b ] 返回 false。
-le	检测左边的数是否小于等于右边的，如果是，则返回 true。	[ $a -le $b ] 返回 true。





3.3.3.	布尔运算符
布尔运算符列表
运算符	说明	举例
!	非运算，表达式为 true 则返回 false，否则返回 true。	[ ! false ] 返回 true。
-o	或运算，有一个表达式为 true 则返回 true。	[ $a -lt 20 -o $b -gt 100 ] 返回 true。
-a	与运算，两个表达式都为 true 才返回 true。	[ $a -lt 20 -a $b -gt 100 ] 返回 false。


3.3.4.	字符串运算符
字符串运算符列表
运算符	说明	举例
=	检测两个字符串是否相等，相等返回 true。	[ $a = $b ] 返回 false。
!=	检测两个字符串是否相等，不相等返回 true。	[ $a != $b ] 返回 true。
-z	检测字符串长度是否为0，为0返回 true。	[ -z $a ] 返回 false。
-n	检测字符串长度是否为0，不为0返回 true。	[ -z $a ] 返回 true。
str	检测字符串是否为空，不为空返回 true。	[ $a ] 返回 true。


3.3.5.	文件测试运算符
文件测试运算符用于检测 Unix 文件的各种属性。

文件测试运算符列表
操作符	说明	举例
-b file	检测文件是否是块设备文件，如果是，则返回 true。	[ -b $file ] 返回 false。
-c file	检测文件是否是字符设备文件，如果是，则返回 true。	[ -b $file ] 返回 false。
-d file	检测文件是否是目录，如果是，则返回 true。	[ -d $file ] 返回 false。
-f file	检测文件是否是普通文件（既不是目录，也不是设备文件），如果是，则返回 true。	[ -f $file ] 返回 true。
-g file	检测文件是否设置了 SGID 位，如果是，则返回 true。	[ -g $file ] 返回 false。
-k file	检测文件是否设置了粘着位(Sticky Bit)，如果是，则返回 true。	[ -k $file ] 返回 false。
-p file	检测文件是否是具名管道，如果是，则返回 true。	[ -p $file ] 返回 false。
-u file	检测文件是否设置了 SUID 位，如果是，则返回 true。	[ -u $file ] 返回 false。
-r file	检测文件是否可读，如果是，则返回 true。	[ -r $file ] 返回 true。
-w file	检测文件是否可写，如果是，则返回 true。	[ -w $file ] 返回 true。
-x file	检测文件是否可执行，如果是，则返回 true。	[ -x $file ] 返回 true。
-s file	检测文件是否为空（文件大小是否大于0），不为空返回 true。	[ -s $file ] 返回 true。
-e file	检测文件（包括目录）是否存在，如果是，则返回 true。	[ -e $file ] 返回 true。


3.4.	Shell字符串
1、获取字符串长度
string="abcd"
echo ${#string} #输出 4
2、提取子字符串
string="alibaba is a great company"
echo ${string:1:4} #输出liba
3、查找子字符串
string="alibaba is a great company"
echo `expr index "$string" is`

3.5.	Shll数组
bash支持一维数组（不支持多维数组），并且没有限定数组的大小。数组元素的下标由0开始编号。获取数组中的元素要利用下标，下标可以是整数或算术表达式，其值应大于或等于0。
1、定义数组
在Shell中，用括号来表示数组，数组元素用“空格”符号分割开。定义数组的一般形式为：
    array_name=(value1 ... valuen)
例如：
array_name=(value0 value1 value2 value3)

2、读取数组
读取数组元素值的一般格式是：
    ${array_name[index]}
例如：
valuen=${array_name[2]}

使用@ 或 * 可以获取数组中的所有元素，例如：
${array_name[*]}
${array_name[@]}

3、获取数组的长度
获取数组长度的方法与获取字符串长度的方法相同，例如：
# 取得数组元素的个数
length=${#array_name[@]}
# 或者
length=${#array_name[*]}
# 取得数组单个元素的长度
lengthn=${#array_name[n]}
3.6.	流程控制
3.6.1.	if else语句
if [ expression 1 ]
then
   Statement(s) to be executed if expression 1 is true
elif [ expression 2 ]
then
   Statement(s) to be executed if expression 2 is true
elif [ expression 3 ]
then
   Statement(s) to be executed if expression 3 is true
else
   Statement(s) to be executed if no expression is true
fi
最后必须以 fi 来结尾闭合 if，fi 就是 if 倒过来拼写，后面也会遇见。

注意：expression 和方括号([ ])之间必须有空格，否则会有语法错误。

3.6.2.	case ... esac
case ... esac 与其他语言中的 switch ... case 语句类似，是一种多分枝选择结构。

case 语句匹配一个值或一个模式，如果匹配成功，执行相匹配的命令。case语句格式如下：
case 值 in
模式1)
    command1
    command2
    command3
    ;;
模式2）
    command1
    command2
    command3
    ;;
*)
    command1
    command2
    command3
    ;;
Esac


case工作方式如上所示。取值后面必须为关键字 in，每一模式必须以右括号结束。取值可以为变量或常数。匹配发现取值符合某一模式后，其间所有命令开始执行直至 ;;。;; 与其他语言中的 break 类似，意思是跳到整个 case 语句的最后。

取值将检测匹配的每一个模式。一旦模式匹配，则执行完匹配模式相应命令后不再继续其他模式。如果无一匹配模式，使用星号 * 捕获该值，再执行后面的命令。
3.6.3.	for循环
for循环一般格式为：
for 变量 in 列表
do
    command1
    command2
    ...
    commandN
done

列表是一组值（数字、字符串等）组成的序列，每个值通过空格分隔。每循环一次，就将列表中的下一个值赋给变量。

in 列表是可选的，如果不用它，for 循环使用命令行的位置参数。

例如，顺序输出当前列表中的数字：
for loop in 1 2 3 4 5
do
    echo "The value is: $loop"
done
运行结果：
The value is: 1
The value is: 2
The value is: 3
The value is: 4
The value is: 5

3.6.4.	while循环
while循环用于不断执行一系列命令，也用于从输入文件中读取数据；命令通常为测试条件。其格式为：
while command
do
   Statement(s) to be executed if command is true
done
命令执行完毕，控制返回循环顶部，从头开始直至测试条件为假。
3.6.5.	跳出循环
Shell也使用 break 和 continue 来跳出循环。

break命令允许跳出所有循环（终止执行后面的所有循环）。
在嵌套循环中，break 命令后面还可以跟一个整数，表示跳出第几层循环。例如：
break n
表示跳出第 n 层循环。

continue命令与break命令类似，只有一点差别，它不会跳出所有循环，仅仅跳出当前循环。

同样，continue 后面也可以跟一个数字，表示跳出第几层循环。


3.7.	Shell函数
Shell 也支持函数。Shell 函数必须先定义后使用。

Shell 函数的定义格式如下：
function_name () {
    list of commands
    [ return value ]
}
如果你愿意，也可以在函数名前加上关键字 function：
function function_name () {
    list of commands
    [ return value ]
}
函数返回值，可以显式增加return语句；如果不加，会将最后一条命令运行结果作为返回值。

Shell 函数返回值只能是整数，一般用来表示函数执行成功与否，0表示成功，其他值表示失败。如果 return 其他数据，比如一个字符串，往往会得到错误提示：“numeric argument required”。

如果一定要让函数返回字符串，那么可以先定义一个变量，用来接收函数的计算结果，脚本在需要的时候访问这个变量来获得函数返回值。

像删除变量一样，删除函数也可以使用 unset 命令，不过要加上 .f 选项，如下所示：
$unset  .f  function_name
函数参数：

在Shell中，调用函数时可以向其传递参数。在函数体内部，通过 $n 的形式来获取参数的值，例如，$1表示第一个参数，$2表示第二个参数...

3.8.	输入输出重定向
1、命令输出重定向的语法为：
$ command > file
这样，输出到显示器的内容就可以被重定向到文件。

如果不希望文件内容被覆盖，可以使用 >> 追加到文件末尾，例如：
$ echo line 1  >> users

2、输入重定向
语法为：
command < file
这样，本来需要从键盘获取输入的命令会转移到文件读取内容。


3、/dev/null 文件

如果希望执行某个命令，但又不希望在屏幕上显示输出结果，那么可以将输出重定向到 /dev/null：
	 command > /dev/null
/dev/null 是一个特殊的文件，写入到它的内容都会被丢弃；如果尝试从该文件读取内容，那么什么也读不到。但是 /dev/null 文件非常有用，将命令的输出重定向到它，会起到”禁止输出“的效果。

3.9.	Shell文件包含
Shell 也可以包含外部脚本，将外部脚本的内容合并到当前脚本。

Shell 中包含脚本可以使用：
. filename
或
source filename
两种方式的效果相同，简单起见，一般使用点号(.)，但是注意点号(.)和文件名中间有一空格。


注意：被包含脚本不需要有执行权限。













