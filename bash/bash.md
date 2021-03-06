bash是我最喜欢用的脚本，bash中有一些基本的概念，对于理解较为复杂的代码非常有用，这里做一个简单的介绍。
## 基本定义
* black，空格或者是tab键
* word，被当做一个独立的单元的字符串，和编译中我们常说的token是一个概念。
* name，只有字母数字和下划线组成的word，并且这些word必须以字母或者下划线开头，也就是所不能以数字开头。
* 元字符，在没有被加引号时的一个单独的字符，用来分割word，一共有九个：`|`, `&`, `;`, `<`, `>`, `(`, `)`,`space`, `tab`
* 控制符（control operators），bash中的 control operators有10个，具体可以看文档：`||`, `&`, `&&`, `;`, `;;`, `|`, `|&`, `(`, `)`, `<newline>`

从上面可以看到，元字符和控制符是有重合的。

## 保留字（reserved words）
首先，保留字也是word，但明显比name的范围好大一点，所以保留字中有的成员并不符合name的定义，比如`!`, bash中的保留字一共有20个。
其中不满足name定义的有5个：`!`, `{`, `}`,  `[[`, 和`]]`, 保留字在bash中有特殊的含义。

#### 那么问题来了？我们之前在if语句中常用的`[`是什么？
`[` 是一个内建命令，可以通过`which`看到，显然它不是bash的关键字。那么`[` 和 `test` 什么区别呢？据说没区别，除了`[`命令的最后一个参数必须是`]`字符。

#### 为什么test是内建命令，但却还能找到这个文件？
bash中有的命令既内建模式，也有实体文件，比如`cd`，这个是bash内建的命令，但同时也有一个`cd`文件，在`/usr/bin`, 而这个cd文件的内容其实就是一个脚本，执行内建的`cd`命令。
`test`和`[`都是内建命令，但是也确实同时存在同名的文件，比如在centos下就在`/usr/bin`下，这是为什么？

## 命令 command
command是bash语法中的基本单元，每一条command都有一个返回值（return value），这个返回值通常就是这个程序执行之后的退出码（exit status）。
当然如果是因为某个信号而终止的话，那这个返回值就是128+信号值，此时这个程序没有正常执行完，也许就没有退出码。

command 一般就是一系列空格隔开的单词和重定向符号，并且由控制操作符结尾（control operator，一般就是`;`, `&`,  `&&`, `||`)

## 管道线 pipeline
bash中的pipeline是一种语法结构，pipeline由多个command构成。

## 算术求值 ARITHMETIC EVALUATION
算是求值，这个没法直接用，需要用`((`这个复合命令，命令都有一个返回值，这个复合命令的返回值就两种，0和1，所以可以用在条件表达式中，如果求值后这个值非零，那返回值就是0，如果求值后为0，那么返回值就是1。

## 条件表达式 CONDITIONAL EXPRESSIONS
条件表达式，结果就是0和1的区别，成立或者不成立。比较，可以是字串，也可以是算术，算是比较和字符串比较是对应的不同的op，只是我一直有点奇怪，算是运算的OP为什么是字母。


