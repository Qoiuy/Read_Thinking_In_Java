2 . 2   所有对象都必须创建 
创建句柄时,我们希望它同一个新对象连接。通常用 new 关键字达到这一目的。new 的意思是:“把我变成
这些对象的一种新类型”。所以在上面的例子中,可以说: 
String s = new String("asdf"); 
它不仅指出“将我变成一个新字串”,也通过提供一个初始字串,指出了“如何生成这个新字串”。 
当然,字串(String)并非唯一的类型。Java 配套提供了数量众多的现成类型。对我们来讲,最重要的就是
记住能自行创建类型。事实上,这应是 Java 程序设计的一项基本操作,是继续本书后余部分学习的基础。 
2 . 2 . 1   保存到什么地方 
程序运行时,我们最好对数据保存到什么地方做到心中有数。特别要注意的是内存的分配。有六个地方都可
以保存数据: 
(1) 寄存器。这是最快的保存区域,因为它位于和其他所有保存方式不同的地方:处理器内部。然而,寄存
器的数量十分有限,所以寄存器是根据需要由编译器分配。我们对此没有直接的控制权,也不可能在自己的
程序里找到寄存器存在的任何踪迹。 
(2) 堆栈。驻留于常规 RAM(随机访问存储器)区域,但可通过它的“堆栈指针”获得处理的直接支持。堆
栈指针若向下移,会创建新的内存;若向上移,则会释放那些内存。这是一种特别快、特别有效的数据保存
方式,仅次于寄存器。创建程序时,Java 编译器必须准确地知道堆栈内保存的所有数据的“长度”以及“存
在时间”。这是由于它必须生成相应的代码,以便向上和向下移动指针。这一限制无疑影响了程序的灵活
性,所以尽管有些 Java 数据要保存在堆栈里——特别是对象句柄,但 Java 对象并不放到其中。 
 (3) 堆。一种常规用途的内存池(也在 RAM 区域),其中保存了 Java 对象。和堆栈不同,“内存堆”或
“堆”(Heap)最吸引人的地方在于编译器不必知道要从堆里分配多少存储空间,也不必知道存储的数据要
在堆里停留多长的时间。因此,用堆保存数据时会得到更大的灵活性。要求创建一个对象时,只需用 new 命
令编制相关的代码即可。执行这些代码时,会在堆里自动进行数据的保存。当然,为达到这种灵活性,必然
会付出一定的代价:在堆里分配存储空间时会花掉更长的时间! 
(4) 静态存储。这儿的“静态”(Static)是指“位于固定位置”(尽管也在 RAM 里)。程序运行期间,静
态存储的数据将随时等候调用。可用 static 关键字指出一个对象的特定元素是静态的。但 Java 对象本身永
远都不会置入静态存储空间。 
(5) 常数存储。常数值通常直接置于程序代码内部。这样做是安全的,因为它们永远都不会改变。有的常数
需要严格地保护,所以可考虑将它们置入只读存储器(ROM)。 
(6) 非 RAM 存储。若数据完全独立于一个程序之外,则程序不运行时仍可存在,并在程序的控制范围之外。
其中两个最主要的例子便是“流式对象”和“固定对象”。对于流式对象,对象会变成字节流,通常会发给
另一台机器。而对于固定对象,对象保存在磁盘中。即使程序中止运行,它们仍可保持自己的状态不变。对
于这些类型的数据存储,一个特别有用的技巧就是它们能存在于其他媒体中。一旦需要,甚至能将它们恢复
成普通的、基于 RAM 的对象。Java 1.1 提供了对 Lightweight persistence 的支持。未来的版本甚至可能提
供更完整的方案。 
2 . 2 . 2   特殊情况:主要类型 
有一系列类需特别对待;可将它们想象成“基本”、“主要”或者“主”(Primitive)类型,进行程序设计
时要频繁用到它们。之所以要特别对待,是由于用 new 创建对象(特别是小的、简单的变量)并不是非常有
效,因为 new 将对象置于“堆”里。对于这些类型,Java 采纳了与 C 和 C++相同的方法。也就是说,不是用
new 创建变量,而是创建一个并非句柄的“自动”变量。这个变量容纳了具体的值,并置于堆栈中,能够更
高效地存取。 
Java 决定了每种主要类型的大小。就象在大多数语言里那样,这些大小并不随着机器结构的变化而变化。这
种大小的不可更改正是 Java 程序具有很强移植能力的原因之一。 
 
主类型 大小 最小值 最大值 封装器类型 
 
boolean 1 位 - - Boolean  
char 16 位 Unicode 0 Unicode 2 的 16 次方-1 Character 
byte 8 位 -128 +127 Byte(注释1) 
short 16 位 -2 的 15 次方 +2 的 15 次方-1 Short(注释1) 
int 32 位 -2 的 31 次方 +2 的 31 次方-1 Integer 
long 64 位 -2 的 63 次方 +2 的 63 次方-1 Long 
float 32 位 IEEE754 IEEE754 Float 
double 64 位 IEEE754 IEEE754 Double 
Void - - - Void(注释1) 
 
1:到 Java 1.1 才有,1.0 版没有。 
 
数值类型全都是有符号(正负号)的,所以不必费劲寻找没有符号的类型。 
主数据类型也拥有自己的“封装器”(wrapper)类。这意味着假如想让堆内一个非主要对象表示那个主类
型,就要使用对应的封装器。例如: 
char c = 'x'; 
Character C = new Character('c'); 
也可以直接使用: 
Character C = new Character('x'); 
这样做的原因将在以后的章节里解释。 
 
1. 高精度数字 
Java 1.1 增加了两个类,用于进行高精度的计算:BigInteger 和 BigDecimal。尽管它们大致可以划分为
“封装器”类型,但两者都没有对应的“主类型”。 
 这两个类都有自己特殊的“方法”,对应于我们针对主类型执行的操作。也就是说,能对 int 或 float 做的
事情,对 BigInteger 和 BigDecimal 一样可以做。只是必须使用方法调用,不能使用运算符。此外,由于牵
涉更多,所以运算速度会慢一些。我们牺牲了速度,但换来了精度。 
BigInteger 支持任意精度的整数。也就是说,我们可精确表示任意大小的整数值,同时在运算过程中不会丢
失任何信息。 
BigDecimal 支持任意精度的定点数字。例如,可用它进行精确的币值计算。 
至于调用这两个类时可选用的构建器和方法,请自行参考联机帮助文档。 
2 . 2 . 3   J a v a 的数组 
几乎所有程序设计语言都支持数组。在 C 和 C++里使用数组是非常危险的,因为那些数组只是内存块。若程
序访问自己内存块以外的数组,或者在初始化之前使用内存(属于常规编程错误),会产生不可预测的后果
(注释2)。 
 
2:在 C++里,应尽量不要使用数组,换用标准模板库(Standard TemplateLibrary)里更安全的容器。 
 
Java 的一项主要设计目标就是安全性。所以在 C 和 C++里困扰程序员的许多问题都未在 Java 里重复。一个
Java 可以保证被初始化,而且不可在它的范围之外访问。由于系统自动进行范围检查,所以必然要付出一些
代价:针对每个数组,以及在运行期间对索引的校验,都会造成少量的内存开销。但由此换回的是更高的安
全性,以及更高的工作效率。为此付出少许代价是值得的。 
创建对象数组时,实际创建的是一个句柄数组。而且每个句柄都会自动初始化成一个特殊值,并带有自己的
关键字:null(空)。一旦 Java 看到 null,就知道该句柄并未指向一个对象。正式使用前,必须为每个句
柄都分配一个对象。若试图使用依然为 null 的一个句柄,就会在运行期报告问题。因此,典型的数组错误在
Java 里就得到了避免。 
也可以创建主类型数组。同样地,编译器能够担保对它的初始化,因为会将那个数组的内存划分成零。 
数组问题将在以后的章节里详细讨论。


### dhg

####  
在本章,我们将探讨 Java 程序的基本组件,并体会为什么说Java 乃至 Java 程序内的一切都是对象。

#### 所有对象都必须创建 

####  保存到什么地方
寄存器　栈　								堆　　　　　　　静态存储　常数存储　　　　　非RAM存储
没权限　变量或对象的引用　new出来的对象　static           public static final　 文件

#### 想起了一个很有意思的问题
syso 2.0-1.1 = 0.89999

#### Java　如何实现避免数组越界
创建对象数组时,实际创建的是一个句柄数组。而且每个句柄都会自动初始化成一个特殊值,并带有自己的
关键字:null(空)。一旦 Java 看到 null,就知道该句柄并未指向一个对象。正式使用前,必须为每个句
柄都分配一个对象。若试图使用依然为 null 的一个句柄,就会在运行期报告问题。因此,典型的数组错误在
Java 里就得到了避免。 

