Iteration 迭代
==============

This chapter is about iteration, which is the ability to run a block of
statements repeatedly. We saw a kind of iteration, using recursion, in
Section [recursion]. We saw another kind, using a for loop, in
Section [repetition]. In this chapter we’ll see yet another kind, using
a while statement. But first I want to say a little more about variable
assignment.

这个章节主要涉及迭代，它可以实现重复运行某个代码块的功能。我们已经在「递归」
部分看到了一种利用递归的迭代方式；另一种利用 ``for`` 循环的方式我们也在「重复」
部分见识了。这个章节，我们将讨论另外一种利用 ``while`` 语句来实现的方式。
不过，首先我想再多讨论讨论有关变量赋值的问题。


Reassignment 重赋值
-------------------

As you may have discovered, it is legal to make more than one assignment
to the same variable. A new assignment makes an existing variable refer
to a new value (and stop referring to the old value).

你应该已经发现了，对同一变量的赋值是合法的。新的赋值会使得已有的变量指向
新的值（同时不再指向旧的值）。

::

    >>> x = 5
    >>> x
    5
    >>> x = 7
    >>> x
    7

The first time we display x, its value is 5; the second time, its value
is 7.

第一次显示 x 的值为 5；第二次它的值变成了 7。

Figure [fig.assign2] shows what **reassignment** looks like in a state
diagram.

图 [fig.assign2] 展示了 **重赋值** 在一个状态图中过程。


At this point I want to address a common source of confusion. Because
Python uses the equal sign (=) for assignment, it is tempting to
interpret a statement like a = b as a mathematical proposition of
equality; that is, the claim that a and b are equal. But this
interpretation is wrong.

正好我想强调一个来源普遍的问题。由于 Python 用等号（=）来赋值，所以很容易将其
理解成如 ``a = b`` 的这样的数学命题上的相等；即是说，a 的值和 b 的值是相等的。
这是种错误的理解。

First, equality is a symmetric relationship and assignment is not. For
example, in mathematics, if :math:`a=7` then :math:`7=a`. But in Python,
the statement ``a = 7`` is legal and ``7 = a`` is not.

首先，「等于」是一种对等关系，而「赋值」不是。比如说，数学上，如果 :math:`a=7`，
则 :math:`7=a`。但是在 Python 中，表述 ``a = 7`` 是合法的，``7 = a`` 则不合法。

Also, in mathematics, a proposition of equality is either true or false
for all time. If :math:`a=b` now, then :math:`a` will always equal
:math:`b`. In Python, an assignment statement can make two variables
equal, but they don’t have to stay that way:

当然，在数学中，「等于」命题不是对的就是错的。如果 :math:`a=b`，那么 :math:`a`
则是永远与 :math:`b` 相等的。在 Python 中，赋值表达式可以使得两个变量相等，
但是它们不一定保持这个相等的状态：

::

    >>> a = 5
    >>> b = a    # a and b are now equal # a 和 b 现在相等
    >>> a = 3    # a and b are no longer equal # a 和 b 不再相等
    >>> b
    5

The third line changes the value of a but does not change the value of
b, so they are no longer equal.

第三行改变了 a 的值，但是没有改变 b 的值，所以它们不再相等了。

Reassigning variables is often useful, but you should use it with
caution. If the values of variables change frequently, it can make the
code difficult to read and debug.

给变量重赋值经常很有用，但是你应该小心使用。变量值频繁改变会使得代码不易读，
而且不好调试。

.. figure:: figs/assign2.pdf
   :alt: State diagram.

   State diagram.状态图。

Updating variables 更新变量
---------------------------

A common kind of reassignment is an **update**, where the new value of
the variable depends on the old.

一种较普遍的重赋值方式是 **更新（update）**，这种方式的新的变量值将取决于旧值。

::

    >>> x = x + 1

This means “get the current value of x, add one, and then update x with
the new value.”

这句的意思是，“得到目前 x 的值，加一，然后用这个新的值更新 x 的值。”

If you try to update a variable that doesn’t exist, you get an error,
because Python evaluates the right side before it assigns a value to x:

如果试图去更新一个不存在的变量，则会返回一个错误。这是因为 Python 是先求
式子右边的值，然后再把所求的值赋给 x：

::

    >>> x = x + 1
    NameError: name 'x' is not defined

Before you can update a variable, you have to **initialize** it, usually
with a simple assignment:

在更新变量之前，你得先 **初始化（initialize）** 它，通常是用一个简单的赋值：

::

    >>> x = 0
    >>> x = x + 1

Updating a variable by adding 1 is called an **increment**; subtracting
1 is called a **decrement**.

通过加一来更新变量叫做 **递增（increment）**；减一则叫做 **递减（decrement）**。

The while statement  while 语句
-------------------------------

Computers are often used to automate repetitive tasks. Repeating
identical or similar tasks without making errors is something that
computers do well and people do poorly. In a computer program,
repetition is also called **iteration**.

计算机经常被用来自动处理重复性的任务。计算机很擅长无纰漏地重复相同或者相似的任务，
而人类则相反。在计算机程序中，「重复」也被叫做「**迭代（iteration）**」

We have already seen two functions, countdown and ``print_n``, that
iterate using recursion. Because iteration is so common, Python provides
language features to make it easier. One is the for statement we saw in
Section [repetition]. We’ll get back to that later.

我们已经见识过两个利用「递归」来迭代的函数 ``countdown`` 和 ``print_n``。迭代如此普遍，
所以 Python 提供了更加简洁的语法来实现。其一是我们在「重复(repetition)」部分看到的
``for` 语句，后面我们还会继续讨论它。

Another is the while statement. Here is a version of countdown that uses
a while statement:

另外一个则是 ``while`` 语句，下面是 ``while`` 版本的 ``countdown``：

::

    def countdown(n):
        while n > 0:
            print(n)
            n = n - 1
        print('Blastoff!')

You can almost read the while statement as if it were English. It means,
“While n is greater than 0, display the value of n and then decrement n.
When you get to 0, display the word Blastoff!”

你可以像读英语句子一样来理解 ``while`` 语句。意思就是：“当 n 的值大于 0 时，
打印出 n 的值，然后让 n 减一，最后当 n 递减至 0 时，打印单词 Blastoff！”。

More formally, here is the flow of execution for a while statement:

以下是 ``while`` 语句的正式的执行流程：

#. Determine whether the condition is true or false.

#. 首先判断条件是 true 还是 false；

#. If false, exit the while statement and continue execution at the next
   statement.

#. 如果是 false，退出 ``while`` 语句，然后执行接下来的语句；

#. If the condition is true, run the body and then go back to step 1.

#. 如果条件判断是 true，则运行 ``while`` 语句里的内容，运行完再返回第一步；

This type of flow is called a loop because the third step loops back
around to the top.

这种形式的流程叫做「循环（loop）」，因为第三步中又循环回到了第一步。

The body of the loop should change the value of one or more variables so
that the condition becomes false eventually and the loop terminates.
Otherwise the loop will repeat forever, which is called an **infinite
loop**. An endless source of amusement for computer scientists is the
observation that the directions on shampoo, “Lather, rinse, repeat”, are
an infinite loop.

循环语句体应该会改变一个或多个变量的值，这样的话才能最终引导条件判断为 false，
从而终止循环。不然的话，循环将会永远重复下去，称为「**无限循环（infinite loop）**」。
对于计算机科学家而言，有一个无穷无尽的消遣，那就是看洗发水的说明书，“打泡沫，
洗掉，重新打”，这便是个无限循环。（译注：计算机**科学家**还有这癖好！）

In the case of countdown, we can prove that the loop terminates: if n is
zero or negative, the loop never runs. Otherwise, n gets smaller each
time through the loop, so eventually we have to get to 0.

在 ``countdown`` 中，循环是一定会终止的：当 n 是 0 或者负数，该循环开始就不会执行；
不然 n 通过每次循环之后慢慢减小，也是会变成 0 的。

For some other loops, it is not so easy to tell. For example:

对于某些循环，可能就没那么好理解了。比如：

::

    def sequence(n):
        while n != 1:
            print(n)
            if n % 2 == 0:        # n is even # n 是偶数
                n = n / 2
            else:                 # n is odd # n 是奇数
                n = n*3 + 1

The condition for this loop is n != 1, so the loop will continue until n
is 1, which makes the condition false.

循环的条件是 ``n != 1``，所以循环会一直执行到 n 等于 1，条件判断为 false 时循环才终止。

Each time through the loop, the program outputs the value of n and then
checks whether it is even or odd. If it is even, n is divided by 2. If
it is odd, the value of n is replaced with n\*3 + 1. For example, if the
argument passed to sequence is 3, the resulting values of n are 3, 10,
5, 16, 8, 4, 2, 1.

每次循环，该程序打印出 n 的值，然后检查它是偶数还是奇数。如果它是偶数，
那么 ``n = n / 2``；如果是奇数，则 ``n = n*3 + 1``。例如，给 ``sequence`` 中的
参数 n 传递一个 3，那么打印出的结果将会是：3、10、5、16、8、4、2、1。

Since n sometimes increases and sometimes decreases, there is no obvious
proof that n will ever reach 1, or that the program terminates. For some
particular values of n, we can prove termination. For example, if the
starting value is a power of two, n will be even every time through the
loop until it reaches 1. The previous example ends with such a sequence,
starting with 16.

由于 n 的值时增时减，所以不能轻易保证 n 会最终变成 1，或者说这个程序能够终止。
对于某些特殊的 n 的值，可以很好地证明它是可以终止的。比如说，当 n 的初始值是 2
的 x 次幂时，n 则会通过循环最终变为 1。之前的例子中，程序就是从 16 开始结束的。


The hard question is whether we can prove that this program terminates
for *all* positive values of n. So far, no one has been able to prove it
*or* disprove it! (See http://en.wikipedia.org/wiki/Collatz_conjecture.)

难题是对于 *所有* 的正整数 n， 是否都能够证明程序是可以终止的。目前为止，
还没有人证明了 *或者说* 否定了该问题。（见：http://en.wikipedia.org/wiki/Collatz_conjecture.）

As an exercise, rewrite the function ``print_n`` from
Section [recursion] using iteration instead of recursion.

作为一个练习，利用迭代而不是递归重写之前「递归」部分的 ``print_n`` 函数。

break
-----

Sometimes you don’t know it’s time to end a loop until you get half way
through the body. In that case you can use the break statement to jump
out of the loop.

有些时候循环执行到一半你才知道循环该结束了，这种情况你可以使用 ``break`` 语句
来跳出循环。

For example, suppose you want to take input from the user until they
type done. You could write:

比如说，你想获取输入，并且在键入 done 时完成输入，你可以这么写：

::

    while True:
        line = input('> ')
        if line == 'done':
            break
        print(line)

    print('Done!')

The loop condition is True, which is always true, so the loop runs until
it hits the break statement.

循环条件总是 true，所以该循环会一直执行直到碰到 ``break``。

Each time through, it prompts the user with an angle bracket. If the
user types done, the break statement exits the loop. Otherwise the
program echoes whatever the user types and goes back to the top of the
loop. Here’s a sample run:

每次要求输入，程序都会给出一个尖括号（>）提示。如果用户输入 done，执行 break 语句
跳出循环。否则，程序就会一直打印出用户所输入的内容并且跳到循环开始，以下是一个运行实例：

::

    > not done
    not done
    > done
    Done!

This way of writing while loops is common because you can check the
condition anywhere in the loop (not just at the top) and you can express
the stop condition affirmatively (“stop when this happens”) rather than
negatively (“keep going until that happens”).

这是种很常见的 ``while`` 循环的写法，你可以随时随地在循环内部判断条件
（而不是只在循环开始），也就意味着，你可以主动设定终止条件（“该结束时就结束”），
而不是被动地等着终止（“继续运行直到条件满足”）。

Square roots 平方根
------------------------

Loops are often used in programs that compute numerical results by
starting with an approximate answer and iteratively improving it.

循环常被用于计算数值的程序中，这种方法开始先得到一个大概的值，然后
通过迭代来获得更加精确的值。

For example, one way of computing square roots is Newton’s method.
Suppose that you want to know the square root of :math:`a`. If you start
with almost any estimate, :math:`x`, you can compute a better estimate
with the following formula:

举个例子，「牛顿法（Newton's method）」是计算平方根的一种方法。如果想要得到
:math:`a` 的平方根，通过一个大概的估算值 :math:`x` 你可以利用下面的公式来
计算较为精确的值：

.. math:: y = \frac{x + a/x}{2}

 For example, if :math:`a` is 4 and :math:`x` is 3:

 比如说，假定 :math:`a` 是 4，:math:`x` 是 3：

::

    >>> a = 4
    >>> x = 3
    >>> y = (x + a/x) / 2
    >>> y
    2.16666666667

The result is closer to the correct answer (:math:`\sqrt{4} = 2`). If we
repeat the process with the new estimate, it gets even closer:

可以看到得到的值与真实值（:math:`\sqrt{4} = 2`）已经很接近了，如果我们用这个值
再重新运算一遍，它将得到更为接近的值。

::

    >>> x = y
    >>> y = (x + a/x) / 2
    >>> y
    2.00641025641

After a few more updates, the estimate is almost exact:

再通过多几次的运算，这个估算可以说已经是很精确了。

::

    >>> x = y
    >>> y = (x + a/x) / 2
    >>> y
    2.00001024003
    >>> x = y
    >>> y = (x + a/x) / 2
    >>> y
    2.00000000003

In general we don’t know ahead of time how many steps it takes to get to
the right answer, but we know when we get there because the estimate
stops changing:

一般来说，我们事先不会知道要多少步才能得到真实值，我们知道的是当得到真实值后，
估算的值就不会再改变了。

::

    >>> x = y
    >>> y = (x + a/x) / 2
    >>> y
    2.0
    >>> x = y
    >>> y = (x + a/x) / 2
    >>> y
    2.0

When y == x, we can stop. Here is a loop that starts with an initial
estimate, x, and improves it until it stops changing:

可以看到，终止条件即是：``y == x`` ，下面这个循环就是利用一个初始估值 x，
循序渐进地估算，直到估值不再变化，循环终止，即得到真实值。

::

    while True:
        print(x)
        y = (x + a/x) / 2
        if y == x:
            break
        x = y

For most values of a this works fine, but in general it is dangerous to
test float equality. Floating-point values are only approximately right:
most rational numbers, like :math:`1/3`, and irrational numbers, like
:math:`\sqrt{2}`, can’t be represented exactly with a float.

上面的程序可以适用于大多数的 a 的值，不过一般来说，最好不要去检查两个浮点数
是否相等。浮点数只能大约表示：对于大多数有理数，如 :math:`1/3`,以及无理数，
如 :math:`\sqrt{2}`,是不能精确用浮点数表示的。

Rather than checking whether x and y are exactly equal, it is safer to
use the built-in function abs to compute the absolute value, or
magnitude, of the difference between them:

与其检查 x 和 y 的值是否是精确的相等，使用内置函数 ``abs`` 来计算它们之间不同的绝对值或者是
数量级是更为安全的做法。

::

        if abs(y-x) < epsilon:
            break

Where ``epsilon`` has a value like 0.0000001 that determines how close
is close enough.

变量 ``epsilon`` 是一个决定其精确度的值，如 0.0000001。

Algorithms 算法
----------------

Newton’s method is an example of an **algorithm**: it is a mechanical
process for solving a category of problems (in this case, computing
square roots).

「牛顿法」就是一个 **算法（Algorithm）** 的例子：它是一个解决一系列问题的机械化过程
（这个例子中是为了计算平方根）。

To understand what an algorithm is, it might help to start with
something that is not an algorithm. When you learned to multiply
single-digit numbers, you probably memorized the multiplication table.
In effect, you memorized 100 specific solutions. That kind of knowledge
is not algorithmic.

为了理解「算法」是什么，我们先来讨论下什么不是「算法」。当你学习个位数的乘法时，
你可能背出了乘法表。实际上，你已经记住了 100 个确切的答案。这种计算并不是我们
要说的「算法」。

But if you were “lazy”, you might have learned a few tricks. For
example, to find the product of :math:`n` and 9, you can write
:math:`n-1` as the first digit and :math:`10-n` as the second digit.
This trick is a general solution for multiplying any single-digit number
by 9. That’s an algorithm!

不过，如果你比较 “懒”，你可能就会找到一些诀窍。比如说为了计算 :math:`n`
和 9 的乘积，你可以把 :math:`n-1` 作为乘积的第一位数，再把 :math:`10-n` 作
为乘积的第二位数，从而得到它们的乘积。这是种普遍的用于计算任意个位数
与 9 相乘的诀窍。 这种诀窍就是种「算法」。

Similarly, the techniques you learned for addition with carrying,
subtraction with borrowing, and long division are all algorithms. One of
the characteristics of algorithms is that they do not require any
intelligence to carry out. They are mechanical processes where each step
follows from the last according to a simple set of rules.

类似的，你所学过的进位加法、借位减法、以及长除法都是算法。算法的特点之一
就是不需要过多的脑力计算就能得到结果。算法是一个机械的过程，每一步都是依
据简单的规则集跟着上一步来执行的。

Executing algorithms is boring, but designing them is interesting,
intellectually challenging, and a central part of computer science.

执行算法的过程显然是很乏味的，但是设计算法就比较有趣了，设计算法不但是智
力上的挑战，更是计算机科学中的一个主要学科。

Some of the things that people do naturally, without difficulty or
conscious thought, are the hardest to express algorithmically.
Understanding natural language is a good example. We all do it, but so
far no one has been able to explain *how* we do it, at least not in the
form of an algorithm.

人们所做的自然而然的、毫无难度或者说无意识的事情往往是最难用算法来阐释的。
比如说，要理解自然语言就是个很好的例子。谁都可以自然而然地理解语言，但是目前，
却还没有人能够解释我们是 *怎么（how）* 理解的，至少可以说这种理解不是一种算法的形式。

Debugging 调试
---------------

As you start writing bigger programs, you might find yourself spending
more time debugging. More code means more chances to make an error and
more places for bugs to hide.

当你开始写更为复杂的程序时，你会发现你的大部分时间都花费在调试上。更多的
代码意味着更大的报错概率，并且有着更多的隐藏 Bug 的地方。

One way to cut your debugging time is “debugging by bisection”. For
example, if there are 100 lines in your program and you check them one
at a time, it would take 100 steps.

有一种节约调试时间的方法就是“对分调试”。比如说，100 行的程序，如果一行行
检查，就需要 100 步。

Instead, try to break the problem in half. Look at the middle of the
program, or near it, for an intermediate value you can check. Add a
print statement (or something else that has a verifiable effect) and run
the program.

取而代之，试着将问题拆为两半。检查代码中间部分或者附近的中间值，加上一行
``print()`` 语句（或者其他可以检验的措施），然后重新运行程序。

If the mid-point check is incorrect, there must be a problem in the
first half of the program. If it is correct, the problem is in the
second half.

如果中间部分的检查是不对的，那么就说明程序的前半部分存在问题。如果是对的，
则说明是后半部分出错了。

Every time you perform a check like this, you halve the number of lines
you have to search. After six steps (which is fewer than 100), you would
be down to one or two lines of code, at least in theory.

每次这样检查，你要检查的行数都会减半。大约 6 步之后（这时小于 100 行了），
理论上说，你将会找到这一行或者两行出错的代码。

In practice it is not always clear what the “middle of the program” is
and not always possible to check it. It doesn’t make sense to count
lines and find the exact midpoint. Instead, think about places in the
program where there might be errors and places where it is easy to put a
check. Then choose a spot where you think the chances are about the same
that the bug is before or after the check.

实践中可能并不能很好的确定程序的 “中间部分” 是什么，也有可能并不是那么适宜检查。
所以根据行数来取其中间行是没有意义的。此时，多考虑下程序中比较容易出问题的部分或者
比较适合检查的位置反而是比较好的做法，然后再在此基础上设定一个检查点，Bug 可能
就出在它的前面或者后面。

Glossary 术语
--------------

reassignment（重赋值）:
    Assigning a new value to a variable that already exists.

	给已经存在的变量赋一个新的值。

update（更新）:
    An assignment where the new value of the variable depends on the
    old.

	变量的新值取决于旧值的一种赋值。

initialization（初始化）:
    An assignment that gives an initial value to a variable that will be
    updated.

	给即将要更新的变量一个初始值的一种赋值。

increment（递增）:
    An update that increases the value of a variable (often by one).

	通过增加的方式来更新变量值（通常是加 1）

decrement（递减）:
    An update that decreases the value of a variable.

	通过减少的方式来更新变量值。

iteration（迭代）:
    Repeated execution of a set of statements using either a recursive
    function call or a loop.

	利用递归或者循环的方式来重复执行代某个码块的过程。

infinite loop（无限循环）:
    A loop in which the terminating condition is never satisfied.

	没有（满足）终止条件的循环。

algorithm（算法）:
    A general process for solving a category of problems.

	为解决一系列问题的通用过程。


Exercises 练习
--------------

Copy the loop from Section [squareroot] and encapsulate it in a function
called ``mysqrt`` that takes a as a parameter, chooses a reasonable
value of x, and returns an estimate of the square root of a.

把 「平方根」部分的循环复制过来，装进一个叫 ``mysqrt`` 的函数中，以 a 作为参数，
选择一个合适的 x 值，并且返回 a 的估算平方根。

To test it, write a function named ``test_square_root`` that prints a
table like this:

为了测试，写一个名为 ``test_squre_root`` 的函数。打印出如下表格：

::

    a   mysqrt(a)     math.sqrt(a)  diff
    -   ---------     ------------  ----
    1.0 1.0           1.0           0.0
    2.0 1.41421356237 1.41421356237 2.22044604925e-16
    3.0 1.73205080757 1.73205080757 0.0
    4.0 2.0           2.0           0.0
    5.0 2.2360679775  2.2360679775  0.0
    6.0 2.44948974278 2.44948974278 0.0
    7.0 2.64575131106 2.64575131106 0.0
    8.0 2.82842712475 2.82842712475 4.4408920985e-16
    9.0 3.0           3.0           0.0

The first column is a number, :math:`a`; the second column is the square
root of :math:`a` computed with ``mysqrt``; the third column is the
square root computed by math.sqrt; the fourth column is the absolute
value of the difference between the two estimates.

其中第一栏是 :math:`a` 的值，第二栏是 ``mysqrt`` 计算得到的 :math:`a` 的平方根，
第三栏是有由 ``math.sqrt`` 计算得到的平方根，第四栏则是这两个平方根相差的绝对值。

The built-in function eval takes a string and evaluates it using the
Python interpreter. For example:

内置函数 ``eval`` 是利用 Python 解释器来计算一个字符串的值。例如：

::

    >>> eval('1 + 2 * 3')
    7
    >>> import math
    >>> eval('math.sqrt(5)')
    2.2360679774997898
    >>> eval('type(math.pi)')
    <class 'float'>

Write a function called ``eval_loop`` that iteratively prompts the user,
takes the resulting input and evaluates it using eval, and prints the
result.

写一个名为 ``eval_loop`` 函数，它可以反复地接收用户输入的内容，然后利用
 ``eval`` 来计算其值，最后打印该值。

It should continue until the user enters ``'done'``, and then return the
value of the last expression it evaluated.

它可以反复输入，除非用户输入 ``'done'`` 才结束，并且最终返回上一个输入
所得到的值。

The mathematician Srinivasa Ramanujan found an infinite series that can
be used to generate a numerical approximation of :math:`1 / \pi`:

数学家 Srinivasa Ramanujan 发现了一个无穷级数可以用来生成 :math:`1 / \pi`
的近似值。

.. math::

   \frac{1}{\pi} = \frac{2\sqrt{2}}{9801}
   \sum^\infty_{k=0} \frac{(4k)!(1103+26390k)}{(k!)^4 396^{4k}}

Write a function called ``estimate_pi`` that uses this formula to
compute and return an estimate of :math:`\pi`. It should use a while
loop to compute terms of the summation until the last term is smaller
than 1e-15 (which is Python notation for :math:`10^{-15}`). You can
check the result by comparing it to math.pi.

写一个名为 ``estimate_pi`` 的函数，利用上面公式来估算出 :math:`\pi`
的值，并且返回该值。使用 ``while`` 循环来计算所有项的和，当和小于 1e-15
（Python 中用于表达 :math:`10^{-15}` 的写法）时终止循环。

Solution（答案）: http://thinkpython2.com/code/pi.py.
