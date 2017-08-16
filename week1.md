# 第一周

>本周的主要内容是第1~4章内容，涉及到内容有C++的初步了解、C++中的数据类型和变量、C++中的运算符及操作、控制逻辑的结构。

>学习难度： :star:

# 第一章：C++基础

- C++程序由`#include指令`、`using语句`、`main函数定义`三部分组成。

```cpp
#include <iostream>
using namespace std;

int main(){
    cout << "Hello, C++!";
    return 0;
}

```

- C++的一个基本原则是，在使用一个函数、对象或类之前必须声明它，唯一的例外就是`main`函数。比如需要使用`cout`对象，则引入`<iostream>`头文件；又如要使用三角函数，则引入`<cmath>`头文件。
- `using namespace std`不是绝对必需的，如果不使用`using语句`，则必须用`std::cout`来引用它，因为对象`cout`是`std`命名空间的一部分，`cin`、`endl`也是这个道理。
- `main`函数是程序中实际做某件事情的部分，在程序执行开始时可以声明全局变量，然后开始执行`main`函数中定义的语句。`return`语句不是必需的，与函数类型有关，但使用它是良好的编程习惯，`return 0`表示成功终止程序，当返回其他值时表示程序执行失败。
- 使用`system("PAUSE")`语句来强制程序暂停，以免控制台一闪而过（本方法仅适用于`windows平台`，如要跨平台则使用`cin.ignore()`代替之）。
- `cout`表示输出内容，`cin`表示输入内容，`endl`表示换行。当有变量需要输出到控制台的时候，必须事先具有`定义`和`赋值`；当执行输入、输出操作时，使用左移位运算符`<<`用于显示输出，使用右移位运算符`>>`用于获取来自终端用户的输入，且`cin`和`cout`必须位于语句中出现的第一个项目。
- 语句中的结束符为`;`，需要注意的是`#include`引入头文件语句没有结束符。

例1：求两个小数的平均值。[在线体验](http://cpp.sh/962z7)

```cpp
#include <iostream>
using namespace std;

int main(){
    double x = 0.0;
    double y = 0.0;
    cout << "Enter value of x: "; //输入x
    cin >> x;
    cout << "Enter value of y: "; //输入y
    cin >> y;
    cout << "Average of the two numbers is: "; //两个数的平均值是：
    cout << (x + y)/2 << endl;
    cout << "Press ENTER to exit."; //按ENTER键退出
    cin.ignore(); //用掉最后的回车
    cin.ignore(); //暂停，供用户按ENTER键
    return 0;
}

```

- 控制结构有`if-else`语句和`while`语句，语法如下：当条件1为真时，执行语句组1，否则执行语句组2；当条件2为真时，执行语句组3，否则跳过该结构。

```cpp
if (条件1){
    语句组1
} else{
    语句组2
}

while(条件2){
    语句组3
}
```

- 一般控制结构的条件为比较算式，如`x == y`即`x`等于`y`，下表为常用的比较运算符。注意`x=y`表示将`y`的值赋给`x`。

运算符 | 说明 | 示例
 :--: | :--: | :--: 
> | 大于 | x>y
< | 小于 | x<y
>= | 大于或等于 | x>=y
<= | 小于或等于 | x<=y
== | 测试等于 | x==y
!= | 测试不等于 | x!=y

- `while`控制语句如果条件始终为真，就会出现`死循环`，因此一般在语句组3中条件中变量的值会发生变化，如`n++`即为变量`n`自增1，等同于`n=n+1`，同理`n--`为变量`n`自减1。
- `using`语句可以引入不同的命名空间，如果不用，则必须使用`前缀::对象`来使用。这种语法的一般形式为`using 前缀::符号`，当使用`using namespace`时会引入整个库的所有符号，这样在引入多个库的时候不是很安全，建议采用`using std::cout;`这种更有选择性的`using`方式。

例2：自定义命名空间。[在线体验](http://cpp.sh/3b5gc)

```cpp
#include <iostream>
namespace briano {
    double x = 0.0;
    double pi = 3.141592;
}
int main(){
    using namespace std;
    cout << "The value of pi is ";
    //pi在briano命名空间中！
    cout << briano::pi << endl;
    cout << "Press ENTER to exit.";
    cin.ignore();
    return 0;
}
```

- 例2也可以使用`using namespace briano`使变量`pi`由程序直接访问。
- C++注释有两种：一是行注释，二是C语言风格注释，如下所示。

```cpp
int i; //i是一个整型变量

/* 注释文本 */

/* 注释文本
多行文本
文本的结束*/
```

例3：加法机。该应用程序会提示用户输入以0结尾的一系列数字，任何非数字输入（如`exit`、`bye`甚至`x`）也将终止该列表。例如，为了把页数33、27、22、41和29加起来，我会键入以下命令，然后按ENTER键：`33 27 22 41 29 0`。[在线体验](http://cpp.sh/5lckl)

```cpp
#include <iostream>
using std::cout;
using std::cin;
using std::endl;

int main(){
    int sum = 0;
    int n = 1;
    cout << "Enter a list of numbers, terminated with 0 ";
    cout << "or not-digit." << endl << "Enter: ";
    while(n != 0){
        cin >> n;
        if (!cin) {
            n = 0;
        }
        sum = sum + n;
    }
    cout << "Total is: " << sum << endl;
    cout << "Press ENTER to exit.";
    cin.ignore();
    cin.ignore();
    return 0;
}
```

例4：计算`phi`。数值`phi`是被古希腊人称为"黄金比例"的数，满足`phi = 1/(phi - 1)`，也可以表示为`phi`<sup>2</sup>` - phi = 1`。数学家断言，如果你把第 *N* 个斐波那契数列除以它的前辈，则当 *N* 增大时，结果越来越接近`phi`。什么是斐波那契数列呢？这个序列开始于1、1，并通过将先前的两个数相加产生随后的数，从而得出：`1 1 2 3 5 8 13 21 34 55 89 ...`。[在线体验](http://cpp.sh/5lckl)

```cpp
#include <iostream>
using std::cout;
using std::cin;
using std::endl;

int main(){
    cout << endl;
    int n = 0;
    double prev1 = 1.0;
    double prev2 = 1.0;
    double current = 0.0;
    cout << "How many Fib. nums to generate? "; //要生成多少个斐波那契数列
    cin >> n;                                   //获取输入
    cout.precision(15);                         //设置15位精度
    while (n > 0){                              //当n大于0……
        current = prev1 + prev2;
        prev2 = prev1;
        prev1 = current;
        cout << current << "\t";
        cout << "ratio = " << prev1/prev2 << endl;
        --n;          //将n减1
    }
    cout << endl;
    cout << "Press ENTER to exit.";
    cin.ignore();     //用掉最后的回车
    cin.ignore();     //暂停，供用户按ENTER键
    return 0;
}
```

- 假设运行`例4`程序，并告诉它计算40个斐波那契数列数，则最后四行输出如下，可知两个连续的斐波那契数的比率的确收敛于`phi`。

```
63245986	ratio = 1.6180339887499
102334155	ratio = 1.61803398874989
165580141	ratio = 1.61803398874989
267914296	ratio = 1.61803398874989
```