2 . 9   编码样式  
一个非正式的 Java 编程标准是大写一个类名的首字母。若类名由几个单词构成,那么把它们紧靠到一起(也
就是说,不要用下划线来分隔名字)。此外,每个嵌入单词的首字母都采用大写形式。例如: 
class AllTheColorsOfTheRainbow { // ...} 
对于其他几乎所有内容:方法、字段(成员变量)以及对象句柄名称,可接受的样式与类样式差不多,只是
标识符的第一个字母采用小写。例如: 
 
class AllTheColorsOfTheRainbow { 
int anIntegerRepresentingColors; 
void changeTheHueOfTheColor(int newHue) { 
// ... 
} 
// ... 
} 
 
当然,要注意用户也必须键入所有这些长名字,而且不能输错。 

### dhg

#### 编码样式
大多数Java编程者　类大写字母开头
字段，方法变量小写字母开头