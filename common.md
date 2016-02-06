[TOC]

# 通用编程规范

## 前言

有些编程规范是大部分编程语言通用的，特把它独立出来。

示例中我采用 Java 语言。

本编程规范完全适用于 Java 和 Javascript 的编程规范，对其他语言也有借鉴作用。

## 好的编程规范

什么样的规范才算是好的编程规范？

“大家好，才是真的好”。不是你觉得好就是好，而是绝大部分人都觉得这个编程规范好，才是一份好的规范。当然，如果你的编程风格与主流的不符合，我的建议是：强迫自己改正。

本编程规范主要参考 Google Java 编程规范，并且**绝大部分规范符合谷歌编程规范**，除了以下几点与其不同：

1. 代码缩进。谷歌建议缩进 2 个空白符；本规范建议缩进 4 个空白符。
2. 好像没了？想到再补充。

此外，本规范还参考了百度等互联网大公司的编程规范，主要是对谷歌编程规范的补充（谷歌编程规范不够详细，所涉及的规范主要是编程风格的）

当然，也有一些个人的见解。

## 基本准则

##### [建议] 坚持一致原则

维护别人写的代码，应当遵守一致原则。即修改后的代码的编程风格应该与之前的代码一致。

## 代码风格

### 缩进

##### [强制] 采用 4 个空格缩进而不是 2 个空格或 tab 字符

虽然谷歌推荐 2 个空格的缩进，但 4 个空格缩进的代码可读性明显更强。现在很多代码编辑器支持输入时自动把 tab 字符转化为 4 个空格符。

每当开始一个新的块，缩进增加2个空格，当块结束时，缩进返回先前的缩进级别。缩进级别适用于代码和注释。

```
// good
void foo() {
    int a = 0;
}

// bad
  int a = 0;
}
```

##### [建议] 所有的块状结构都要缩进

```
void foo() {
	if (condition) {
		// statement		
	}
}
```

### 空格

##### [强制] 注释时，注释符两边的空白符必不可少

* 双斜杠后面的空格必不可少。
* 如果在一条语句后做注释，则双斜杠两边都要一个空格。
* 可以允许多个空格，但没有必要。

```
// good
int foo = 0; // 这是一个注释示例
/* 这是一个注释示例 */
/** 这是一个注释示例 */

// bad
int foo = 0; //这是一个注释示例
int foo = 0;// 这是一个注释示例
/*这是一个注释示例*/
/**这是一个注释示例*/
```

##### [强制] 任何保留字（如if, while for等等）与紧随其后的左括号之间要有一个空格

```
// good
if (foo == 0) {

}

// bad
if(foo == 0) {

}
```

##### [强制] 任何保留字(如else、catch等)与其前面的右大括号之间要有一个空格
```
// good
if (foo == 0) {

} else {

}

// bad
if(foo == 0) {

}else {

}
```

##### [强制] 任何左大括号 `{` 前必须加一个空格

两个例外：
* @SomeAnnotation({a, b})(不使用空格)。
* String[][] x = foo;(大括号间没有空格)。

##### [强制] 在任何二元或三元运算符的两侧必须有空格

这也适用于以下“类运算符”符号：
类型界限中的&(<T extends Foo & Bar>)。
catch块中的管道符号(catch (FooException | BarException e)。
foreach语句中的分号。

```
// good
int i = 1 + 2;

// bad
int i = 1+2;
```

##### [强制] 在 `,`、`:`、`;` 及右括号 `)` 后必须空格

```
for (int i = 0; i < 100; i++) {

}
```

##### [建议] 数组初始化中，大括号内的空格是可选的

```
new int[] {5, 6};

new int[] { 5, 6 };
```

##### [建议] 本规范没有要求的空格不要随便乱加

几个经典的错误例子：

```
// good
void foo(int i) {}

// bad
void foo (int i) {}

// bad
void foo( int i) {}

// bad
void foo(int i ) {}
```

### 水平对齐

##### [建议] 水平对齐，不作要求，也不推荐

虽然增加了代码的可读性，但给维护带来问题。很多时候为了保持对齐，做了一些无用功。所以即使对于已经使用水平对齐的代码，我们也不需要去保持这种风格。
 

```
// good
int foo = 1;
String s = "foo";

// bad
int		foo = 1;
String	s = "foo";

// bad
int		foo	= 1;
String	s	= "foo";
```

### 空行

##### [强制] 类内连续成员之间，必须有 1 个空行
 
类内连续的成员（字段，构造函数，方法，嵌套类，静态初始化块，实例初始化块等）之间，必须有一个空行

例外：两个连续字段之间的空行是可选的，用于字段的空行主要用来对字段进行逻辑分组。

##### [建议] 类内的第一个成员前或最后一个成员后的空行是可选的

既不鼓励也不反对这样做，视个人喜好而定。


##### [建议] 多个连续的空行是允许的，但没必要这样做，也不推荐这样做
 
##### [建议] 在函数体内，语句的逻辑分组间使用空行

这样做可增强代码的可读性

##### [建议] 没意义的空行不要乱加

### 自动换行 

##### [强制] 列限制：80、100，还是 120？

一个项目可以选择一行80个字符或100个字符的列限制。

我推荐 100 个字符。

任何一行如果超过这个字符数限制，必须自动换行。
 
例外：
 
不可能满足列限制的行(例如，Javadoc中的一个长URL，或是一个长的JSNI方法参考)。
package和import语句(见3.2节和3.3节)。
注释中那些可能被剪切并粘贴到shell中的命令行。

##### [建议] 自动换行的基本准则是：更倾向于在更高的语法级别处断开


##### [强制] 如果在非赋值运算符处断开，那么在该符号前断开

这条规则也适用于以下“类运算符”符号：点分隔符(.)，类型界限中的&（<T extends Foo & Bar>)，catch块中的管道符号(catch (FooException | BarException e)

```
// good
int i = 1 + 2 + 3 + ... + 1000000
	+ 1000001；

// bad
int i = 1 + 2 + 3 + ... + 1000000 + 
	1000001；
```

##### [强制] 如果在赋值运算符处断开，通常的做法是在该符号后断开

这条规则也适用于foreach语句中的分号
```
// good，虽然在这里没必要换行
int i = 
	100000000;

// bad
int i
	= 100000000;
```

##### [强制] 自动换行时函数名与左括号留在同一行

##### [强制] 自动换行时逗号(,)与其前面的内容留在同一行

##### [强制] 自动换行时第一行后的每一行至少比第一行多缩进 4 个空格
 
##### [强制] 非空块得换行遵守 K & R 风格

 
对于非空块，大括号遵循Kernighan和Ritchie风格 (Egyptian brackets):
 
* 左大括号前不换行
* 左大括号后换行
* 右大括号前换行
* 如果右大括号是一个语句、函数体或类的终止，则右大括号后换行; 否则不换行。例如，如果右大括号后面是else或逗号，则不换行。

Java的enum类有一些例外，在 Java 编程规范讲解。

```
// good
class Foo {
	public void foo() {
		if (condition) {
			something();
		} else {
			other();
		}
	}
}

// bad
class 
{	
}

// bad
if (condition)
{
	something();
}
else
{
	other();
}
```

##### [建议] 空块可以用简洁版本，不换行

一个空的块状结构里什么也不包含，大括号可以简洁地写成{}，不需要换行。例外：如果它是一个多块语句的一部分(if/else 或 try/catch/finally) ，即使大括号内没内容，右大括号也要换行。
 
```
void doNothing() {}
```

### 大括号

##### [强制] 使用大括号(即使是可选的)
 
大括号与if, else, for, do, while语句一起使用，即使只有一条语句(或是空)，也应该把大括号写上。

```
// good
if (i > 0) {
	i++;
}

// bad
if (i > 0)
	i++;
```

### 语句

### 命名

##### [强制] 类名以 UpperCamelCase 风格编写

类名通常是名词或名词短语，接口名称有时可能是形容词或形容词短语。现在还没有特定的规则或行之有效的约定来命名注解类型。

测试类的命名以它要测试的类的名称开始，以Test结束。例如，HashTest或HashIntegrationTest。

```
// good
class Foo {
}

// bad
class foo {
}
```

##### [强制] 方法名以 lowerCamelCase 风格编写

方法名通常是动词或动词短语。

下划线可能出现在JUnit测试方法名称中用以分隔名称的逻辑组件。一个典型的模式是：test<MethodUnderTest>_<state>，例如testPop_emptyStack。 并不存在唯一正确的方式来命名测试方法。

##### [强制] 常量名以 CONSTANT_CASE 风格编写

全部字母大写，用下划线分隔单词。

那，到底什么算是一个常量？

每个常量都是一个静态final字段，但不是所有静态final字段都是常量。在决定一个字段是否是一个常量时， 考虑它是否真的感觉像是一个常量。例如，如果任何一个该实例的观测状态是可变的，则它几乎肯定不会是一个常量。 只是永远不打算改变对象一般是不够的，它要真的一直不变才能将它示为常量。

```
// Constants
static final int NUMBER = 5;
static final ImmutableList<String> NAMES = ImmutableList.of("Ed", "Ann");
static final Joiner COMMA_JOINER = Joiner.on(',');  // because Joiner is immutable
static final SomeMutableType[] EMPTY_ARRAY = {};
enum SomeEnum { ENUM_CONSTANT }

// Not constants
static String nonFinal = "non-final";
final String nonStatic = "non-static";
static final Set<String> mutableCollection = new HashSet<String>();
static final ImmutableSet<SomeMutableType> mutableElements = ImmutableSet.of(mutable);
static final Logger logger = Logger.getLogger(MyClass.getName());
static final String[] nonEmptyArray = {"these", "can", "change"};
```

这些名字通常是名词或名词短语。

##### [强制] 常量必须用常量修饰符修饰

```
// good
final int MAX_COUNT = 99;

// bad
int int MAX_COUNT = 99;
```

##### [强制] 非常量字段名以 lowerCamelCase 风格编写

这些名字通常是名词或名词短语。

##### [强制] 参数名以 lowerCamelCase 风格编写。

参数应该避免用单个字符命名。

##### [强制] 局部变量名以 lowerCamelCase 风格编写

比起其它类型的名称，局部变量名可以有更为宽松的缩写。

虽然缩写更宽松，但还是要避免用单字符进行命名，除了临时变量和循环变量。

即使局部变量是final和不可改变的，也不应该把它示为常量，自然也不能用常量的规则去命名它。

##### [建议] 类型变量可用以下两种风格之一进行命名

* 单个的大写字母，后面可以跟一个数字(如：E, T, X, T2)。
* 以类命名方式(5.2.2节)，后面加个大写的T(如：RequestT, FooBarT)。

##### [建议] 集合、数组类型的变量，常用名词复数

```
// good
Student student;
Student[] students;
List<Student> students;

// not good
List<Student> someStudent;

// bad
List<Student> list;
```

### 变量声明

##### [强制] 每次只声明一个变量

```
// good
int foo;
int foo2;

// bad
int foo, foo2;
```

##### [强制] 需要时才声明，并尽快进行初始化
 
不要在一个代码块的开头把局部变量一次性都声明了，而是在第一次需要使用它时才声明。 局部变量在声明时最好就进行初始化，或者声明后尽快进行初始化。

变量声明与使用的距离越远，代码的阅读与维护成本就越高。

从优化方面讲，这样做也是有好处的。

### 语句

##### [强制] 一行最多一个语句

```
// good
int foo;
int foo2;

// bad
int foo; int foo2;
```

### 赋值语句

连续赋值不仅影响可读性，很多时候容易出错。

### 
##### [强制] 禁止连续赋值

```
// good
a = 1;
b = 1;
c = 1;

a = b = c = 1;
```




### 驼峰式命名法（CamelCase）

驼峰式命名法分大驼峰式命名法(UpperCamelCase)和小驼峰式命名法(lowerCamelCase)。 有时，我们有不只一种合理的方式将一个英语词组转换成驼峰形式，如缩略语或不寻常的结构(例如"IPv6"或"iOS")。Google指定了以下的转换方案。

名字从散文形式(prose form)开始:

把短语转换为纯ASCII码，并且移除任何单引号。例如："Müller’s algorithm"将变成"Muellers algorithm"。
把这个结果切分成单词，在空格或其它标点符号(通常是连字符)处分割开。
推荐：如果某个单词已经有了常用的驼峰表示形式，按它的组成将它分割开(如"AdWords"将分割成"ad words")。 需要注意的是"iOS"并不是一个真正的驼峰表示形式，因此该推荐对它并不适用。
现在将所有字母都小写(包括缩写)，然后将单词的第一个字母大写：最后将所有的单词连接起来得到一个标识符。
每个单词的第一个字母都大写，来得到大驼峰式命名。
除了第一个单词，每个单词的第一个字母都大写，来得到小驼峰式命名。
示例：

：

```
// good
XmlHttpRequest // XML HTTP request
newCustomerId // new customer ID
innerStopwatch // inner stopwatch
supportsIpv6OnIos // supports IPv6 on iOS
YouTubeImporter // YouTube importer
YoutubeImporter // 不推荐

// bad
XMLHTTPRequest
newCustomerID
innerStopWatch
supportsIPv6OnIOS
```


Note：在英语中，某些带有连字符的单词形式不唯一。例如："nonempty"和"non-empty"都是正确的，因此方法名checkNonempty和checkNonEmpty也都是正确的。

## 注释

##### [强制] 块注释与其周围的代码在同一缩进级别

```
// good
if (condition) {
	// 这是一段注释
	something();
}

// bad
if (condition) {
// 这是一段注释
	something();
}
```

##### [强制] 多行注释可以是/* ... */风格，也可以是// ...风格。对于多行的/* ... */注释，后续行必须从*开始， 并且与前一行的*对齐

```
/* 这是一段很长很长很长...................很长
 * 很长很长的注释。
 */

// 这也是一段很长很长很长...................很长
// 很长很长的注释。

/* 我不会告诉你这三种写法都是
 * 可以的 */
```

##### [强制] 注释不要封闭在由星号或其它字符绘制的框架里。

这样做很可能给维护带来不必要的麻烦

```
// bad
/****************************************
 * 这是一个
 *         很漂亮但是没什么卵用注释
 ***************************************/

```

##### [建议] 禁止没意义的注释

```
// bad
int foo; // 定义一个变量

// 创建一个Foo类
class Foo {

}
```

为什么这里是建议，而不是强制？因为很多时候，判断一句注释是不是废话还跟开发者水平有关。

举个不是很恰当的例子：

```
// bad
// 创建一个线程并执行
new Thread(new Runnable() {
	public void run() {
		something();
	}
}).start();
```

稍微懂点 Java 的都知道这句注释是句废话，但对于一个刚入门，没接触过多线程的就不这么认为了，后面这条建议是对本条建议的补充说明：

##### [建议] 注释一般不包含语言本身的语法、语言内置的API的说明、第三方类库（如 Spring 等）某个函数的用法的说明

不懂的去看相应的开发文档。

##### [建议] 对整段代码进行注释说明，而不是逐行注释

##### [建议] 只进行必要的注释，注释不是越多越好




