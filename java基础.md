#### 1、java中的数据类型

![数据类型](./\images\数据类型.png)

##### 1.1、基本数据类型

* 整型常量，默认为int型； 如： 1， 2 ，6，554
* 浮点型常量，默认为double型； 如：2.3， 563.3

![1.1基本数据类型](./\images\1.1基本数据类型.png)

* `byte` 占用 1个字节 = 8bit 
* `short` 占用 2个字节  
* `int` 占用 4个字节 
* `long` 占用 8个字节  **注意： lang定义的变量，值后面必须以 L 或 l 结尾**

```java
lang time= 45612L;
lang time= 45612l;
```

##### **浮点型数据类型**

![1.2浮点型](./\images\1.2浮点型.png)

- `float` 占用 4个字节  -3.403 * 10^38 ~ 3.403 * 10^38
- `short` 占用 8个字节   -1.798 * 10^308 ~1.798 * 10^308

* float的数值的范围比long还大

* **注意：Java的浮点型默认为double型，声明float型常量，值后面必须以 F 或 f 结尾**

  ```java
  float dot= 3.25F
  float dot= 3.25f
  ```

  

##### 1.2、char 字符型类型

![1.2char类型](./\images\1.2char类型.png)



* `char` 2个字节 、通常使用 单引号 表示 ' '

* **注意： char类型定义的变量，只能存储一个字符、或转移字符 或Unicode编码**

  ```java
  char a1= 'a'; //good
  char a2= 'aa'; // bad 只能存储一个字符
  char a3= '\n'; //good  可以存储一个转义字符
  char a4= '\u000a'; //good 可以存储一个unicode字符
  ```

  

##### 1.3、布尔类型

```java
boolean isMerry= true;
boolean isMerry= false;
```

##### 1.4、基本数据类型之间的运算规则 

注意排除 `布尔 boolean`类型之外的其他7中基本类型的数据之间的运算（不包含布尔类型）

* 1、自动类型提升
  结论： 当容量（数值范围）小的数据类型与容量大的数据类型的变量做运算时，结果自动提升为容量大的数据类型
  byte、char、short -- int --> long --> float --> double
  说明：此时的容量大小指的是，便是输的范围的大和小，比如： float的容量大于long的容量

```java
byte a1= 2
int a2= 129
byte a3= a1+a2 // bad 因为byte接收的时候有可能自身存储数字的容量不够，所以不能使用小的容量类型接收
int a4= a1+a2 //good ,除了int、还可以使用long 、float、 double接收
 
float a5= a1+a2 // good  131.0 会自动转为带小数点的
```

* 2、当`byte`、`char`、`short` 三者之间做运算，只能通过 `int`接收

```java
byte a1= 2;
short a2= 3;
short a3= a1 + a2; // bad  当`byte`、`char`、`short` 三者之间做运算，只能通过 `int`接收
int a4= a1 + a2; //bad
byte b1= 9;
int c1= a1 + b1 ;//good 
```

* 强制类型转换： 自定类型提升运算的逆运算。

  1、需要使用强转符：（）

  2、注意点： 强制类型转换，可能导致经度损失

  ```java
  //精度损失举例1
  double d1=12.9;
  int i1= (int)d1; //12  截断操作，浮点型小数强转int类型，小数点后面的数字截断
  
  //精度损失举例2
  int i2= 128;
  byte b= (byte)i2; //-128 byte的存值范围是-128 ~ 127 ，int类型的i2为128，byte类型存储不下，所以，会损失经度
  
  //没精度损失1
  long l1= 123;
  short s2= (short)l1; // short 能存下，且都是整型 所以不会损失经度
  
  //编码情况1、
  long l= 123123; //说明：后没加l或L,编译的时候，就会认为 123123是int型，然后将int型的123123赋值给 long型l，自动变量提升，所以没报错
  
  long l2= 21332423215234123; //说明： 编译的时候报错，因为没加l或L,编译的时候，就会认为 21332423215234123是int型，而 21332423215234123超过int的存值范围，所以会报错
  
  float f1= 12.3; //说明： 编译的时候报错，因为没加f或F,编译的时候，就会认为 12.3是double型，而 double型转float型，大的往小的转会把错（因为小的有可能装不下大的）
  
  //编码情况2
  byte b= 12 
  byte c= b+1 //说明：编译时报错，对于整型常量，默认是int型，浮点型常量默认是double型，所以 byte+int 要使用大的接收，所以应使用int接收
  ```
  
  #### 1.5、String （引用数据类型）
  
  
  
  ![string介绍](./\images\string介绍.png)

**String 类型变量的使用**

* 1、String属于引用数据类型，翻译为：字符串

* 声明Stribg类型变量时，是用一对 ""

* String可以和8中基本数据类型做运算（包括布尔类型），都是拼接字符串

**练习题1**

```java
char c= 'a'; //对应数值97 char与数字运算转化为acll码，再运算，与字符串运算，直接当做字符串与字符串拼接
int num= 10;
String str= 'hello';
System.out.println(c+num+str); //97+10+'hello' = '107hello'
System.out.println(c+str+num); //97+'hello'+10 = 'ahello10'
System.out.println(c+(num+str)); //a+(10+'hello')= 'a10hello'
System.out.println((c+num)+str); //(97+10)+'hello' = '107hello'
System.out.println(str+c+num); //'hello'+97+10 = 'hellowa10'
```

**练习题2**

```java
String str1= 4; //判断对错： no
String Str2= 3.5+""; //判断对错 yes  输出 “3.5”
System.out.println(3+4+"Hello"); //'7Hello'
System.out.println("Hello"+3+4); //'Hello34'

short s=5 ;
    s= s-2; //no 2是常量 int型


char c= 'a';
int i= 5;
float d= .314f;
double result= c+i+d //yes
 
 byte b=5;
 short s=3
 short l= s+b //no  byte、short、int相加，结果要用int,float double接收
     
 下面输出 //  *  *  的有     1、3、5可以
 System.out.println("*  *") //yes "*  *"
 System.out.println('*'+'\t'+'*') // no 单引号之间相加，代表数值相加， 93 
 System.out.println('*'+"\t"+"*") //yes  "*  *"
 System.out.println('*'+'\t'+"*") //no "51*"
 System.out.println('*'+('\t'+"*")) //yes  "*  *"
```

##### 1.5、关于进制



![关于进制](./\images\关于进制.png)

![二进制2](./\images\二进制2.png)

```java
二进制转化10进制
00010101
0*2^7 + 0*2^6 + 0*2^5 + 1*2^4 + 0*2^3 + 1*2^2 + 0*2^1+1*2^0= 21 
    
10进制转2进制的取余 逆序
21 / 2  ---> 10 --- 1
10 /2   --->5  --- 0
5/2    ---> 2  --- 1
2/2   ----> 1 ----0 
1 / 2  ----> 0 --- 1  
然后倒叙看余数（从下往上看 ） 10101
```

![进制之间的转换](./\images\进制之间的转换.png)

![进制转2进制](./\images\进制转2进制.png)

#### 2、运算符

##### 	2.1、计算运算符

![java运算符](./\images\java运算符.png)

```java
int num1= 12;
int num2= 5;
int result1= num1 / num2;
System.out.println(result1); // 2  num1 int，num2 int结果也为int，把结果赋值给int 类型的result1，所以结果是2

int result2= num1 / num2 * num2; // 2 * 5 = 10
double result3= num1 / num2; // num1 int，num2 int,两个int运算结果也为int，2，然后将2赋值给double类型的result3，2倍强转为double类型，result3为 2.0
    
double result4= num / num2 + 0.0; // um1 int，num2 int,两个int运算结果也为int，2 , int类型的2 + 常量0.0（浮点型常量，默认为double类型），两者相加记过赋值给double,所以结果还是2.0

double result5= num1 / (num2+0.0); // num2+0.0 为浮点型 5.0 ，int / 5.0， 结果为 2.4

double result6= （double）num1 / num2; //2.4 (double）num1 浮点型 12.0 /5 结果还是浮点型
double result7= （double）(num1 / num2); // 2.0

short s= 2
    s+=3 //不会变量的数据类型
 
```

**前++  （--）； 后++ （--）**

注意： ++   或   -- 不会改变原本的数据结构，所以性能更高

```java
short s= 1;
s= s+1 ; //错误 short+int不能使用short接收 需要 int= s+1;
s++ 或 ++s //正确，因为 ++   或   -- 不会改变原本的数据结构 所以性能更高
```



```java
int a1=10；
int b1= ++a1;
System.out.println("a1=="+a1+",b1=="+b1); //"a1==11,b1==11"
/*说明 int b1= ++a1； 前++ 表示 a1先自身加1，之后再将加之后的值赋值给b1*/
int a2=10；
int b2= a2++;
System.out.println("a2=="+a2+",b2=="+b2); //"a2==11,b1==10"
/*说明 int b2= a1++； 后++ 表示 a2把值值赋值给b2，之后再自身加1*/

int n= 10;
n += (n++)+(++n)
System.out.println(n)
/*
n= n + (n++)+(++n)
n= 10 +(10) + (12)  说明 运算符 n=10 执行 n++ 输出10，然后加以，此时n=11,然后执行++n,此时n=12
n= 32
*/
```

##### 2.2、比较运算符

![2-比较运算符](./\images\2-比较运算符.png)

* 比较结果都是`布尔类型`的数据

##### 2.3、逻辑运算符

![2-逻辑运算符](./\images\2-逻辑运算符.png)

**结论**

* & 和 &&  

  相同点： 都是左右两边同时满足返回true,否则返回false

  不同点： & 符号，如果左边为false,右边还会执行； &&符号，如果左边为false,右边不会执行（被短语）；

* I 和 ||

  相同点： 都是左右只要有一个满足返回true,都不满足则返回fasle

  不同点： | 符号，如果左边为true,右边还会执行； ||符号，如果左边为true,右边不会执行（被短语）；

* a^b (异或)

  a、b 同时为 true或false时，返回false

  a、b的值不同时，返回 true

  **练习**

  ```java
  int x=1,y=1;
  if(x++==1 || ++y==1){
  	x= 7;
  }
  System.out.println("x="+x+",y="+y);
  /*
  x++ == 1  x先对比，后加，所以x== 1为true，后面是短路与，所以后面不执行
  然后x= 7；
  
  所以输出 x=7  y=1
  */
  
  class Test {
  	public static void main(String[] args){
		boolean x= true;
		boolean y= false;
		short z= 42;
		if( (z++==42) && (y=true) ) z++;
		if( ( x=false ) || ( ++z==45 ) ) z++;
        System.out.println("z="+z);
	  }
  }
  /*
  if( (z++ ==42) && (y=true; y) ) z++
  先比较后 +1 左边为true, 此时z= 42+1 =43,
  右边 z= true相当于 将true赋值给z 然后将z输出，所以右边也是true
  执行z++ 43+1= 44
  x= false false赋值给x 然后将x输出，所以右边也是false
  右边  ++z==45  先加，再对比 44+1 = 45 ; 45 == 45为true
  false ||  true 结果为true，执行z++; 45 +1 =46
  所以 结果 z=46
  */
  ```

  #### 2.4、位运算符
  
  位运算符，都是将数字转化为二进制，再进行计算的
  
  ![2-4位运算符](./\images\2-4位运算符.png)

![2-4位运算符2](./\images\2-4位运算符2.png)

​	21<< 2

21转为二进制 为0010101    1 * 2^4+1 * 2^2+1 * 2^0

21<< 2 为二进制向左移动2位,移动之后的位置补领，得到 1010100 ，结果为 1 * 2^6+1 * 2^4+1 * 2^2 

相当于多了 2^2

**结论：**

* 位运算符操作的都是整数的数据
* `<<`  在一定范围内，向左移动一位，就相当于 * 2    公式： `m << n` 相当于`m * 2^n`
* `>>` 在一定范围内，向右移动一位，就相当于 / 2    公式： `m >> n` 相当于`m / 2^n`

所以使用 << 或 >> 效率比较高

![2-4位运算符3](./\images\2-4位运算符3.png)

![2-4位运算符4](./\images\2-4位运算符4.png)

**练习**

```java
//交换下面a、b的值
int a= 10;
int b= 20;
//方法一，创建一个变量容器, (缺点：多创建一个变量)
int temp= a;
a= b;
b= a;

//方法二，(缺点，只能交换数值类型的，有可能精度会有损失)
a= a+b; //a= a,b的和 ，b=b;
b= a-b; // b= a,b的和-b= a; a=a,b的和;
a- a-b; // a= a,b的和- a= b;
// 方法三， (缺点，只能交换数值整数类型的)
a= a ^ b; // a= 01010 ^ 10100 = 01110
b= a ^ b; // b= 01110 ^ 10100 = 01010= 10
a= a ^ b; // a= 01110 ^ 01010 = 10100= 20
```

**三元运算符**

* 凡是可以使用三元运算符的地方，都可以使用if-else

* 如果程序既可以使用三元运算符，也可以使用if-else结构，name休闲选择三元运算符，原因：简洁、执行效率高

#### 3、流程控制

##### 3.1、 if-else 

**使用`Scaner`获取键盘输入值**

步骤： 

* 1、导包 `import java.util.Scanner;`

* 2、Scanner实例化： Scanner scan= new Scanner (System.in);

* 3、调用Scanner类的相关方法，来获取指定类型的变量 

  ```java
  import java.util.Scanner;
  class ScannerTest {
      public static void main(String[] args){
          Scanner scan= new Scanner (System.in);
          int num= scan.nextInt();
          String str;
          if(num >= 90){
              str= "一辆宝马车";
          }else if(num>=80 && num < 90){
              str= "iphone xs Max";
          }else if(num>=60 && num < 80){
              str= "ipad";
          }else{
              str= "什么都没得到！！！";
          }
          System.out.println(str);
      }
  }
  ```

##### 3.2、switch-case循环语句

**说明**
* 根据switch表达式中的值，一次匹配各个case中的常量。一单匹配成功，则直接进入相应的case结构中,调用其执行语句。当调用完执行语句后则仍然继续向下执行其他的case结构中的执行语句，只带遇到break关键字，或此switch-case结构末尾结束终止。
* switch 结构中的表达式，只能是如下6种类型之一： byte、short、char、枚举类型（jdk5.0新增）、String类型(jdk7.0新增)
* break关键字是可选的
* default： 相当于if-else中的else （可选）
**练习**
```java
//对于成绩大于60分的输出：“合格”。低于60分的，输出“不合格”。

int score= 80;
switch(score/10){
	case 10:
	case 9:
	case 8: 
	case 7:
	case 6:
		System.out.println(“合格”); break;
	default : 
		System.out.println(“不合格”); break;
}
//说明，switch-case 在匹配到之后，判断结束语句是否有break;有就停止，没有就执行下一个语句，然后继续判断是否有break ... 知道遇到break停止

int score= 80;
switch(score/60){
	case 1:
		System.out.println(“合格”); break;
	case 0:
		System.out.println(“不合格”); break;
}
```

```java
//从键盘上输入2019年的month和day，要求通过程序输出输入的日期为2019年的第几天

import java.util.Scanner;
class TestDay{
    public static void main(String[] args){
        Scanner scan= new Scanner(System.in);
        System.out.println("month:");
        int month= scan.nextInt();
        System.out.println("day:");
        int day= scan.nextInt();
        switch(month){ 
            case 12 : day += 30 ; 
            case 11 : day += 31 ;
            case 10 : day += 30 ;
            case 9 : day += 31 ;
            case 8 : day += 31 ;
            case 7 : day += 30 ;
            case 6 : day += 31 ;
            case 5 : day += 30 ;
            case 4 : day += 31 ;
            case 3 : day += 28 ;
            case 2 : day += 31 ;
            case 1 : day += 0 ;
        }
        System.out.println("days:"+ day);
    }
}
//说明，当输入month= 2  day=8时，day+= 31 ; day= 39,继续执行 case 1,加0，输入39
```

##### 3.3、for循环

for循环结构

for(1;2;4){
	3
}
* 执行过程： 1 --> 2 --> 3 --> 4 -- > 2 --> 3 --> 4  ... 2--> ..
* **可以使用`break`关键字，跳出循环体结构 （后面其他循环都不在执行）** 
* **可以使用`continue`关键字，跳出当前一条循环 （后面其他循环继续执行）**
```java
for(int i= 0;i<= 3;i++){
    System.out.println("i"+i);
}
/*
i0
i1
i2
i3
*/

//break关键字跳出循环结构
for(int i= 0;i<= 3;i++){
	if(i==1) break;
    System.out.println("i"+i);
}
/*
i0
*/


//continue关键字跳出当前循环
for(int i= 0;i<= 3;i++){
	if(i==1) continue;
    System.out.println("i"+i);
}
/*
i0
i2
i3
*/


int num= 1;
for(System.out.println("num1"+num);num<= 3;System.out.println("num3"+num),num++){
    System.out.println("num2"+num);
}
/*
num11
num21
num31
num22
num32
num23
num33
*/
```
##### 3.4、while循环
1
while(2){
	3;
	4;
} 

* 执行过程： 1 --> 2 --> 3 --> 4 -- > 2 --> 3 --> 4  ... 2--> ..
* for玄幻可以和while之间进行转化
* 可以使用break结束循环条件

##### 3.5、do-while循环
1 
do {
	3;
	4;
}while(2);
* 执行过程： 1 --> 3 --> 4 --> 2 -- > 3 --> 4 --> 2  ... 
* 开始时，先执行一下执行结构，在进行判断循环条件

```java
![数据类型](C:\Users\DELL\Desktop\java笔记\images\数据类型.png)/*
求 1-100之间所有的质数
质数： 除了1和自身，不能被其他数整除 ,世界上最小的自然数是2
思路： 我们取到大于2，切小于这个数i的所有整数，然后依次去判断 j与这些整数的余数，如果余数存在等于0，则立即终止当前循环，i不是质数；然后执行下一个
 */
class TestDay{
    public static void main(String[] args){
    	for(int i=2; i <=100;i++){
    		boolean isFlag= true; //判断是否是质数
    		for(int j=2; j<i ; j++){
    			if(i % j == 0){
    				isFlag= false;
    				break;
    			}
    		}
    		if(isFlag){
    			System.out.println(i);
    		}
    	}

    }
}

//优化
class TestDay{
    public static void main(String[] args){
    	for(int i=2; i <=100;i++){
    		boolean isFlag= true; //判断是否是质数
    		for(int j=2; j<=Math.sqrt(i) ; j++){
    			if(i % j == 0){
    				isFlag= false;
    				break;
    			}
    		}
    		if(isFlag){
    			System.out.println(i);
    		}
    	}

    }
}
```

##### 3.6、break、continue关键字的使用

|sdasd | dasd | sdasd |  asdasad |
__________________________________
|sdasd | dasd | sdasd |  asdasad |

#### 4、数组（Array）

![数据类型](./\images\4-数组.png)

**数组的特点：**

* 数组是有的序列表
* 数组属于引用数据类型的变量。数组的元素，既可以是基本数据类型，也可以是引用数据类型
* 创建数组对象会在内存中开辟一块连续的空间
* 数组的长度一但确定，就不能修改

**数组的特点：**

* 数组是分类
*  按照维数： 一维数组、二维数组、...
*  按照数组元素的类型: 基本数据类型的数组、引用数据类型的数组

1.1、静态初始化：数组的初始化和数组的赋值操作同时进行
	
1.2、静态初始化：数组的初始化和数组的赋值操作分开进行
```java
public class ArrayTest {
	public static void main(String[] args) {
		//测试数组
		//1.1、静态初始化：数组的初始化和数组的赋值操作同时进行
		int[] numList= new int[]{100,101,102,103};
		
		//1.2、静态初始化：数组的初始化和数组的赋值操作分开进行
		String[] names= new String[5]; //定义一个有5子元素为String类型数组（此时、还没有进行初始化赋值操作）
		names[0]= "苹果";
		names[1]= "橘子";
		names[2]= "香蕉";
		names[3]= "香梨";
		names[4]= "柠檬";
		//names[5]= "chengzi"; //运行的时候会报错、报错信息为：下标越界； 因为数组一但初始化完成，长度就确定了；
		System.out.println("numList[2]="+numList[2]); //numList[2]=102
		System.out.println("names[3]="+names[3]); //names[3]=香梨
		System.out.println("names.length="+names.length); //names.length=5
	} 
}
```

**数组默认初始化值：**

* 数组元素是整型 （byte、short、int、lang）默认是0；

* 数组元素是浮点型 （float、double）默认是 0.0

* 数组元素是char型   默认 是 0或 '\u0000'（ASCII码\0 ）而非 ’0‘

* 数组元素是布尔型   默认值  false

* 数组元素是引用数据类型： 默认值为 null

  

**一维数组的内存解析**

![4-一维数组的内存解析](./\images\4-一维数组的内存解析.png)

* 在方法内部中定义的变量为局部变量（包括在main函数中定义的变量），局部变量的变量存放在**栈**中；
* 局部变量的变量的值存放在**堆**中，初始化的时候先在栈和对堆中分别存放变量名和值（值为默认值），然后进行赋值操作
* **栈**中存放的是对应堆中的地址，通过地址找到堆的
* 当执行完之后，变量会依次出站，这是会栈和堆断开连接、垃圾回收机制会通过引用计数的方式找出不在使用的变量、并销毁

**定义 一维数组的方式**

方式一（标准）： 
```java
//静态初始化：数组的初始化和数组的赋值操作同时进行
int[] numList1 = new int[]{1,2,3,4};
String[] strList1= new String[]{"苹果","香蕉"};

//静态初始化：数组的初始化和数组的赋值操作分开进行
int[] numList1= new int[4];
numList1[0]=1;
numList1[1]=2;
numList1[2]=3;
numList1[3]=4;

String[] strList1= new String[2]
strList1[0]= "苹果";
strList1[1]= "香蕉";
```

方式二：

```java
int numlist1[]= {1,2,3,4};
String strList1[]= {"苹果","香蕉"};
```

方式三：

```java
int[] numlist1= {1,2,3,4};
String[] strList1= {"苹果","香蕉"};
```

**定义  二维数组的方式**

方式一（标准）： 

```java
//静态初始化
int[][] arr= new int[][]{{1,2},{2,3,4}};
//动态初始化1
String[][] arr2= new String[3][2]; // 表示第一层数组有3项，第二层数组有2项
//动态初始化2
String[][] arr2= new String[3][]; // 表示第一层数组有3项，第二层数组没赋值，默认为null
```

方式二：

```java
int[] arr4[]= new int[][]{{1,2},{2,3,4}};
//或者
int[] arr4[]= {{1,2},{2,3,4}};
```

方式三：

```java
int arr1[][]= {{1,2},{2,3}};
```
**注意：**
初始化方式： int[][] arr= new int[4][3];
* 外层元素的初始化值为：  地址值；
* 内层元素的初始化值为： 与一维数组初始化情况相同；

初始化方式： int[][] arr= new int[4][];
* 外层元素的初始化值为： null
* 内层元素的初始化值为： 不能调用、否则报错；

**说明**

```java
String[][] arr4= new String[3][2];
System.out.println("arr4[2][0]="+arr4[2][0]); //arr4[2][0]= null
System.out.println("arr4[2]="+arr4[2]); //=[Ljava.lang.String;@15db9742  @15db9742d地址值
//说明 [ 一个中括号是 一维数组 java.lang.String是String类型的 java.lang是包名  @是在哪个位置	
String[][] arr5= new String[3][];
System.out.println("arr5[2]="+arr5[2]); //null
System.out.println("arr5[2][0]="+arr5[2][0]); // java.lang.NullPointerException 空指针异常
/*
 *	  说明：arr4 最外层定义了3个元素的数组，每个元素存储值是null(int型的一维数组,数组是引用类型，且没赋过值，所以默认值为null),第二层初始化的时候将第二层的地址替换第一层原来的null，由于是String类型，且都没赋值，所以arr4第二层数组的每一项都是null、第一层每个元素都存的地址值
 *	arr5 最外层定义了3个元素的数组，第一层每个元素存储的值都是 null ,第二层没初始化过，所以arr[1] 还是为null
 arr[1][0] 会报空指针异常
 * */
```

![4-2二维数组的内存解析](images\4-2二维数组的内存解析.png)

**练习**

```java
/*
		 * 杨辉三角形
		1 
		1 1 
		1 0 1 
		1 1 1 1 
		1 2 2 2 1 
		1 3 4 4 3 1 
		1 4 7 8 7 4 1 
		1 5 11 15 15 11 5 1 
		1 6 16 26 30 26 16 6 1 
		1 7 22 42 56 56 42 22 7 1 
		除了第一行和第一列的数据，其他数据 的 上一列同位置数和 上一列同位置数的上一个数等于这个数；
		一行的，第一个元素和最后一个元素都是1 ；

		 * */
		
		//杨辉三角形
		int[][] yangList= new int[10][]; //定义10行
		for(int i=0;i < yangList.length; i++) {
			yangList[i]= new int[i+1]; /*循环数组每一项，并初始化每一项的值为数组，数组的个数从1一次递增*/
			System.out.println(yangList[i]); /*此时打印的是外层数组中的每一项所存储的是自己指向的数组指针*/
			yangList[i][0]= yangList[i][i]= 1; /*为数组第二层 第一项和最后一项赋值 1*/
			if(i > 2) {
				for(int j= 1;j< yangList[i].length-1;j++) {
					yangList[i][j]= yangList[i-1][j] + yangList[i-1][j-1]; /*计算数组的 杨辉 公式并赋值*/
				}
			}
		}
		
		/*依次打印数组*/		
		for(int i=0; i< yangList.length; i++) {
			for(int j=0; j< yangList[i].length; j++) {
				System.out.print(yangList[i][j]+" ");
			}
			System.out.println();
		}
```

#### 5、面向对象

![5-1内存解析](images\5-1内存解析.png)

![5-1类执行过程2](images\5-1类执行过程2.png)

##### 5.1、class类说明

**关于权限修饰符**

* 默认方法的权限修饰符先都使用public

* java规定4种权限修饰符、private、public、缺省、protected

**返回值类型 （方法中）**

* 如果有返回值，则需要在方法名前添加返回这个返回值的类型
* 如果无返回值、则要在方法名前添加 void

**理解”万事万物皆对象“**

* 在Java语言范畴中，我们都将功能、结构等封装到类中，通过类的实例化，来调用具体的功能结构
* 涉及到Java语言与前端HTML、后盾的数据库交互式时，前后端的结构在java层面交互时，都体现为类、对象。

##### 5.2、类方法的重载

**定义**  ： 在同一个类中，循序存在一个或多个同名类方法，只要他们 的参数个数或者类型不同、或者顺序不同即可。

两同一不同： 

​	同一个类， 相同方法名； 

​	参数列表不同、参数类型不同、参数个数不同；

```java


public class Student {
 	public void paly(int i){ // 1
        
    } 
    public void paly(String s){ // 2
        
    } 
    public void paly(int i,String s){ // 3
        
    } 
    public void paly(String s,int i){ // 4
        
    } 
}
Student stu= new Student();
stu.play(1); // 调用1方法
stu.play("hello"); // 调用2方法  
stu.play(1,"hello"); // 调用3方法    
stu.play("hello",1); // 调用4方法    
    
```





##### 5.3、类方法 可变个数形参

* jdk 5.0新增的内容

**具体使用**

* 可变个数形参的格式: 数据类型 ... 变量名
* 当电泳可变个数形参的方法时,传入的参数个数可以是0个、1个、2个 ...
* 但是的参数类型要和定义的类型一致
* 可变个数参数的方法与本类中方法名相同，形参类型也相同的数组之间不构成重载。换句话说，二者不能共存
* 传值方式有两种 1、 传入一个一个的值 stu.paly("AA","BB","CC")     2、传入数组  stu.paly(new  String[]{"AA","BB","CC"}）
* 可变形参再方法中使用，只能写在参数的末尾

```java
public class Student {
 	paly(string ... strs){ // strs就是数组，所以我们只需要按照数组的方式去取值就行
        
    } 
    /*paly(string[] strs){  //这个和上面的是不能共存在，因他在5.0之前一直用的都是这个，所以他和上面的是一样的
        
    } */
    eat(int i, string ...strs){ //可变形参再方法中使用，只能写在参数的末尾
        
    } 
}
```

##### 5.4、类方法的形参传递机制： 值传递

1、形参： 方法定义时，生命的小括号内的参数

​	  形参：方法调用时，实际传递给参数的数据

2、值传递机制

* 如果变量是基本数据类型，此时实参给形参的是实参真实存储的数据值
* 如果变量是引用数据类型，此时实参给形参的是实参存储的地址值![ 5-4.1基本数据类型参数传递](images\5-4.1基本数据类型参数传递.png)

![5-4.2引用数据类型参数传递.png](images\5-4.2引用数据类型参数传递.png.png)

```java
当实参将参数传递给形参时，形参变量会在栈中存在，方法执行完之后，没被引用的变量会出栈，如果变量后面是引用数据类型，没有变量指向他（没有被引用），那么变量和值都会出栈，销毁

当参数时候基本类型的时候，传递的是真实的值，（相当于在栈中存储形参 ”变量名= 传过来的实参的值“）

当参数时候引用数据类型的时候，传递的是实参执行的地址值，（相当于在栈中存储形参 ”变量名= 传过来的地址值“）

当在方法内部进行修改的时候，基本数据类型，直接修改的是 方法参数的值，对原来数据没影响
引用数据类型，直接修改的是 方法参数的接收到指针地址所指向的值，对原来数据有影响

```

**练习**

只要在局部变量都在栈中存储 （方法中的变量为局部变量） 类中的属性不是局部变量，所以它在堆中存储

```java
public class TransferTest3 {
    public static void main(String args[]) {
        TransferTest3 test = new TransferTest3(); //栈中的test 执行地址 0x7788 
        test.first(); //调用 first（）
    }
    public void first() { 
        int i = 5; // 栈中 i= 5;
        Value v = new Value(); // 栈中v -> 0x5566   堆中的 value实例对象v为 { i=15 }地址为0x5566 
        v.i = 25; //通过指针0x5566 找到 v对象中的i 并赋值 此时 0x5566 { i= 25 }
        second(v, i); //执行 second（v,i）将 v实例的指针0x5566 和i的值 5传递过去，当second执行完再执行下面的输出语句
        System.out.println(v.i); // v 0x5566 { i= 20 }
    }
    public void second(Value v, int i) { //栈中新创建一个v和一个i v存储的是指针 0x5566 { i= 25 }  i存储的是 5
        i = 0;  //i 重新赋值 0
        v.i = 20; //通过指针0x5566 找到 v对象中的i 并赋值 此时 0x5566 { i= 20 }
        Value val = new Value(); // 栈中val -> 0x8899   堆中的 value实例对象val为 { i=15 }地址为0x8899
        v = val; //将v的指针 指向  0x8899 
        System.out.println(v.i + " " + i); // 15 0
    } 
}
class Value {
	int i = 15;
}

当指向完之后，变量会依次从上出栈，出栈之后，判断堆中的数据的指针有没有没其他引用，如果没有，就也继续出栈销毁
```

![5-4.3练习题](images\5-4.3练习题.png)

##### 5.5、面向对象特性一  （封装与隐藏）

**一、问题引入：**

​	当我们创建一个类对象以后，我们可以通过`对象.属性`的方式，对对象的属性进行赋值。这里，赋值操作要受属性的数据类型和存储范围的制约。除此之外，没有其他条件的限制。但是，在实际问题中，我们需要给属性赋值加入额外的条件。这个条件就不能再属性声明时提现，我们只能通过方法进行限制条件的添加。比如（set）。同时，我们，我们需要避免用户再使用“对象.属性”的方式对属性进行赋值。则需要将属性声明为私有的（private）

**二、封装的体现**
我们将类的属性 xxx私有化（private）,同时提供公共的 （public）方法来获取（getXXX）和设置（setXXX）

```java
package com.larry.java;

public class Test01 {
	public static void main(String[] args) {
		Student stu= new Student();
		//外部不能直接操作 stu.age 只能通过类内部的方法来获取或者修改age
		stu.name= "zs";
		System.err.println(stu.getAge()); //0
		stu.setAge(-5);
		System.err.println(stu.getAge()); //0
		stu.setAge(10);
		System.err.println(stu.getAge()); //10
		stu.setAge(300);
		System.err.println(stu.getAge()); //200
	}
}

class Student {
	String name;
	private int age; //定义私有属性，只能在类内部使用，不能通过实例在外部使用
	
	public void setAge(int a) { //过滤掉不合法的年龄
		if(a < 0) {
			a= 0;
		}else if(a>200) {
			a= 200;
		}
		age= a;
	}
	public int getAge() {
		return age;
	}
}

```

![5-5.1封装和隐藏](images\5-5.1封装和隐藏.png)

**三、封装和继承需要修饰符的配合**

1、Java规定的4种权限（从小到大排列）、private  、缺省（default）、protected 、public

2、4种权限可以用来修饰类及类的内部结构： **属性**、**方法**、**构造器**、**内部类**

**注意：**修饰类的话只能使用 public、 缺省

![5-5.2修饰符的作用区间](images\5-5.2修饰符的作用区间.png)

##### 5.6、类的成员之一 构造器

**一、构造器的作用 ：** 

1、创建类实例对象

2、 初始化对象的属性 

**二、说明：**
1、如果没有显示的定义类的构造器的话，则系统默认提供一个空参数的构造器 **(默认构造器的权限和类的权限是相同的)**
2、定义构造器的格式：  权限修饰符 类名（形参列表）{}

3、一个类中定义的多个构造器，彼此构成重载

4、一旦我们显示的定义了构造器之后、系统就不再提供默认的空参构造器了

5、一个类至少有一个构造器

**总结： 属性赋值的先后顺序**

默认初始化值   --> 显示赋值  --> 构造函数内部赋值  -->  通过 “对象.方法” 或 “对象.属性” 的方式进行赋值

默认初始化： class A { int age; }

显示赋值： class A { int age= 5; }

构造函数内部赋值： class A { int age= 5;  public A(){ age= 8 } }

通过 “对象.方法” 或 “对象.属性” 的方式进行赋值: 

A test= new A();  test.age= 10;

```java
public class Person {
	private int age;
	public String name;
    /*当类中有多个构造器的话，组成构造器重载；当我们定义了构造器的话，系统就不再提供默认的空参构造器了*/
	public Person() {
		age= 18;
	}
	public Person(int a,String n) {
		age= a;
		name= n;
	}
	public void setAge(int a) {
		if( a< 0) {
			 System.out.println("年龄不能小于0");
			 return;
		}else if(a > 130) {
			System.out.println("年龄不能大于130");
			 return;
		}
		age= a;
	}
	public int getAge() {
		return age;
	}
}


package com.larry.test;

public class PersonTest {
	public static void main(String[] args) {
		Person xiaoming= new Person(); 
		xiaoming.setAge(-5);
		System.out.println(xiaoming.getAge()); //18
		xiaoming.setAge(140);
		System.out.println(xiaoming.getAge()); //18
		xiaoming.setAge(21);
		System.out.println(xiaoming.getAge()); //21
		
		Person xiaohong= new Person(5,"mike"); 
		System.out.println("name="+xiaohong.name+" age="+xiaohong.getAge()); //name=mike age=5
	}
}

```

```java
package com.larry.constructor;

public class Student {
	String name;
	int age;
	String school;
	String major;
	public static void main(String[] args) {
		Student stu1= new Student("mike1",1);
		System.out.println("name="+stu1.name+",age="+stu1.age+",school="+stu1.school+",major="+stu1.major);
		//name=mike1,age=1,school=null,major=null
		
		Student stu2= new Student("mike2",2,"郑州二中");
		System.out.println("name="+stu2.name+",age="+stu2.age+",school="+stu2.school+",major="+stu2.major);
		//name=mike2,age=2,school=郑州二中,major=null
		
		Student stu3= new Student("mike3",3,"郑州三中","三年级");
		System.out.println("name="+stu3.name+",age="+stu3.age+",school="+stu3.school+",major="+stu3.major);
		//name=mike3,age=3,school=郑州三中,major=三年级
	}
	public Student(String n, int a) {
		name= n;
		age= a;
	}
	public Student(String n, int a,String s) {
		name= n;
		age= a;
		school= s;
	}
	
	public Student(String n, int a,String s,String m) {
		name= n;
		age= a;
		school= s;
		major= m;
	}
}

```

##### 5.7、JavaBean

![5-7javaBean](images\5-7javaBean.png)

##### 5.8、 this关键字的使用功能

在类的方法中，或者构造函数中，我们可以通过`this.属性`或`this.方法`，调用当前对象的属性或方法。但是，通常情况下，我们都选择省略`this`。特殊情况下，如果 方法的形参和类的属性同名是，我么必须显示的使用`this.变量`的方式，表明此变量是属性，而非形参

this调用构造器

* 我们再类的构造器中，可以显示的使用“this(形参列表)”方式，调用本类中指定的其他构造器
* 构造器中不能通过“this(形参列表)”方式调用自己
* “this(形参列表)” 只能在构造器首行调用

![5-8this关键字的使用](images\5-8this关键字的使用.png)

```java
public class Student {
    private int age= 13;
    setAge(int age){
        this.age= age;
    }
}
```

##### 5.9、package 和 import 关键字

**一、package 关键字的使用**

* 为了更好的实现项目中类的管理。提供包的概念；

* 使用功能package 生秘境类或接口所属的包，声明在源文件的首行

* package 包属性标识符，遵循表示的命名规范、见名之意

* 没 “.”一次、代表一层文件目录

 **补充：  同一包下，不能命名同名的接口、类；在不同包下可以命名同名的接口、类**



**二、 import关键字的使用**

* import 导入
* 在源文件中显式的使用import结构导入指定包下的类、接口
* 声明在包的声明和类的声明之间
* 如果需要导入多个结构、则徐并列导出即可
* import java.util.Arrays ; import com.larry.test.Bank;
* 如一个包中需要导出多个类，可以使用` import com.larry.*`； 可以使用 `xxx.*`导入包下所有结构
* 如果使用的类或接口是java.lang包下定义的，则可以省略 import 结构
* 如果使用的类或接口是本g包下定义的，则可以省略 import 结构
* 如果 我们定义的两个同名的类 Account 分别在 com.larry.test1包和 com.larry.test2包下面。我们此时要在同一文件下使用这两个同名类，使用方法如下：（全类名）
* 如果导入了一个包，也想用这个包下面的子包类，那么子包也到导入
* import static：导入指定类或接口中的静态结构： 属性或方法

```java
import com.larry.test1.Account; //引入com.larry.test1包下的 Account类
Account acc1= new Account(); //使用第一个类
com.larry.test2.Account acc2= new com.larry.test2.Account(); //使用第二个类的方式只能通过 包名的方式使用类 com.larry.test2.Account

```

##### 5.10、面向对象的特征之二： 继承性

一、继承的好处

1、减少了代码的冗余、提好了代码复用性

2、便于功能的扩展

3、为之后多态的使用、提供了前提

二、继承性的格式： class A extends B {  }

​	A: 子类、派生类、 subclass

​	b: 父类、超类、基类、superclass

体现：一旦子类A继承父类B以后、子类A中就获取了父类B中声明的所有的结构、属性、方法。

特别的，父类中声明的private的属性或方法、子类继承父类以后仍然认为获取了父类中私有的结构、只是因为封装性的影响，使得子类不能直接调用父类的结构而已。

子类继承父类之后，还可以声明自己特有的属性或方法，实现功能拓展



三、java中关于继承性的规定

1、java中类的单继承型、一个类只能有一个父类

2、一个类可以被多个子类继承

3、字符类是相对概念

4、子类直接继承的父类成为“直接父类”。间接继承的的父类成为 “间接父类”

5、子类继承父类以后，就获取了直接谷类以及所有间接父类中声明的属性和方法



四、1、如果我们 没有显示的声明一个类的父类的话，则此类继承与java.lang.Object 类

​	 2、java中所有的类，都直接或间接了java.lang.Object 类

##### 5.11、继承方法的重写

>  1、重写： 子类继承父类以后、可以对父类中同名同参数的方法、进行覆盖重写

>  2、应用： 重写以后，当创建子类对象以后，通过子类对象中的**同名、同参数**的方法时，实际执行的子类重写父类的方法

> **3、重写的规定：**

> ​	约定俗称: 子类中的叫重写的方法，父类中的叫做被重写的方法

> 3.1、子类重写的方法的方法名和形参列表与父类被重写的方法名和形参列表相同

> 3.2、子类重写方法的权限修饰符不小于父类被重写的方法的权限修饰符 （子类重写的权限修饰符 >= 父类被重写的方法的权限修饰符）

> 3.3、特殊情况： 子类不能重写父类中声明的private的权限

> 3.4、返回值类型
>  父类的返回值类型时void，那么重写的子类的方法返回值类型也必须是void
>  父类的返回值类型时A类型，那么重写的子类的方法返回值类型也必须是A类型或A的子类
>  父类的返回值类型时基本数据类型（比如：double），那么重写的子类的方法返回值类型也必须是相同的基本数据类型(必须是double)
> 3.5、子类重写的方法抛出的异常类型不大于父类被重写 的方法抛出的异常类型
```java
package com.larry.demo;

class Person {
	public String name;
	private int age;
	
	public void play(){
		System.out.println("Person：踢足球"); //Person：踢足球
		walk(); // Student：walk
	}
	public void walk(){
		System.out.println("Person：walk");
	}
}


class Student extends Person {
	public String name;
	
	public  void walk(){
		System.out.println("Student：walk");
	}
}



package com.larry.demo;

public class Test1 {
	public static void main(String[] args) {
		Student stu= new Student();
		stu.play(); //Person：踢足球  // Student：walk
	}
}

```
##### 5.12、 super关键字

**使用场景**

> * 在类中，如果我们使用属性或方法，前面不加任何修饰符，那么就相当于与省略了`this`关键字，`this`的关键字使用。现在自己的类中找是否存在调用的属性或方法，找到就直接使用，找不到就向继承的父类中找，找到就用，找不到就继续在父类的上面的父类找，知道找到为止

>  * `super`关键字 则为，在子类中使用`super`关键字调用属性或方法，则直接跳过子类中的属性或方法，去父类中查找属性或方法，找不到就去父类继承的父类中找... 直到找到为止


**super调用构造器**


> *  1、我们可以在自雷的构造器中显示的使用 `super(形参列表)`的方式，调用父类中声明的制定的构造器

> * 2、`super(形参列表)`的使用必须要在声明子类构造器的首行

> * 3、我们在类的构造器中、针对`this(形参列表)`或`super(形参列表)`只能二选一，不能同时调用

> * 4、在类的多个构造函数中，至少有一个构造器中使用了`super(形参列表)`，调用父类中的构造器

```java
//父类*******************
package com.larry.supur;

public class Person {
	String name;
	int age= 102;
	public Person(String name) {
		this.name= name; //构造器初始化数据
	}
	void play() {
		System.out.println(name+":踢足球");
	}
}
//父类*******************


//子类*******************
package com.larry.supur;

public class Student extends Person {
	String name;
	int age= 10009;
	public Student(String name) {
		super(name); //super(name)写在构造器的第一行、显示的调用父类的构造器，如果我们把这个去掉，子类会默认在自己的构造器中的第一行 super(); 而Person中的构造器写了个有参数的构造器，那么就不会生成不带参数的构造器了，而子类中默认调用super();所以会报错
		this.name= name;
	}
	void init() {
		play(); //xiaoming学生：打羽毛球
		super.play(); //xiaoming:踢足球
		System.out.println(age); //10009
		System.out.println(super.age); //102
	}
	void play() {
		System.out.println(name+"学生：打羽毛球");
	}
}

//子类*******************

//test******************
package com.larry.supur;

public class SuperTest {
	public static void main(String[] args) {
		Student xiaoming = new Student("xiaoming");
		xiaoming.init();
	}
}
//test******************
```

![super关键字](images\super关键字.png)

**子类对象实例化的全过程：**

* 1、从结果上看：（继承性）

  子类继承父类以后，就获取了父类中声明的属性或方法

  创建子类的对象，在堆空间中，就会加载所有父类中声明的属性。

* 2、从过程上看：

  当我们通过子类的构造器创建子类对象时，我们一定会直接或间接的调用其父类中的构造器，进而调用父类的构造器，

  直接调用叻 java.lang.Object类中空candela构造器为止。正因为架子啊过所有的父类的结构，所以才可以看到内存中有父类的结果，子类对象才可以考虑进行调用

  **明确： 虽然创建子类对象时，调用了父类构造器，但是自始至终就创建过一个对象，即为new的子类对象。**

##### 5.13、面向队形的特征之三： 多态性

![5-13多态性](images\5-13多态性.png)

**1、理解多态性：**可以理解为一个事物的躲着我那个形态

**2、何为多态性：**对象的多态性：父类的引用指向子类的对象（或子类的队形赋值给父类的引用）

**3、多态的使用；虚拟方法调用：**有了对象的多态性以后，我们在编译器，只能调用父类中声明的方法，但在运行期，我们实际执行的是子类重写父类的方法

总结：编译：看左边 ， 运行： 看右边。

**4、多态性使用的前提：**1、类的继承关系，2、方法的重写

**5、多态性：** 仅对方法有作用

```java
Person p= new Student();

p.play() ///调用的是子类 Student实例的，仅对方法有作用

p.name //调用的是 Person对象上的name 
```

**多态性的使用**

```java
package com.larry.demo;

class Person1 {
	public String name="pe1";
	private int age= 1;
	
	public void play(){
		System.out.println("Person1"+name);
	}
}

class Student1 extends Person1 {
	public String name="st1";
	private int age= 2;
	
	public void play(){
		System.out.println("Student1="+name+",age="+age);  
		/*Student1=st1,age=2  ，理解：由于多态性的原因
		 * Person1 p1= new Student1();
		 *	p1.play();
		 *	p1.play 是Student1中的方法，调用方法方法内部的this指向的是new Student1()实例对象，
		 * name，age省略了 this,所以它指向的是 new Student1()实例对象
		 * 
		 */
	}
}

class Teacher1 extends Person1 {
	public String name= "te1";
	private int age= 3;
	
	public void play(){
		System.out.println("Teacher1="+name+",age="+age); //Teacher1=te1,age=3
	}
}


/*****************************/

package com.larry.demo;

public class MoreTypeTest {
	public static void main(String[] args) {
		Person1 p1= new Student1();
		p1.play();
		Person1 p2= new Teacher1();
		p2.play();
		
		System.out.println(p2.name); //pe1 多态性只对继承的方法有效，对属性时无效的，属性还是父类中的属性
		// 多态性的方法中的this指向的是自己子类实例中的方法
	}
}


```

**多态性应用二，使用功能多态性的好处**

```java
package com.larry.demo;

public class Animal {
	private String name;
	public void move(){ 
		
	}
	public void moveType(Animal ani) { //移动方式
		ani.move(); //调用的是子类实例对象的方法
	}
	
	/*
	public void moveType(Dog dog) { //如果不是多态性的话，我们每添加一个子类的时候，都要重载一个方法，会很麻烦，所有“多态性”为我们提供了方便
		dog.move();
	}
	public void moveType(Cat cat) { //
		cat.move();
	} 
	...
	
	*/
}




package com.larry.demo;

class Dog extends Animal {
	private String name="小狗";
	public void move() {
		System.out.println(name+"：跑");
	}
}

class Cat extends Animal {
	private String name="小猫";
	public void move() {
		System.out.println(name+"：爬");
	}
}



package com.larry.demo;

public class AnimalTest {
	public static void main(String[] args) {
		Animal an1= new Dog();
		an1.move(); //小狗：跑   调用子类的方法
		
		Animal an2= new Cat();
		an2.move(); //小猫：爬   调用子类的方法
	}
}

```

**多态性： ** 有了对象的多态性以后，内存中实际上是加载了子类特有的属性和方法的，但是由于变量声明为父类变量，导致编译时，只能调用父类中声明的属性和方法。子类特有的属性和方法不能调用。

Person p = new Student();

**如何调用子类特有的属性和方法？**

将 p向下转型，使用强制类型转换，将父类转化为多态表达式右边的子类类型

Student p1= (Student )p ; 

这样就告诉浏览器p1是 Student 类型的叻， p1就能调用子类中所持有的的属性和方法了

**注意： 强转时可能出现ClassCastException 异常**

当 Teacher p2= (Teacher )p ；

这样会出错，所以我们需要使用 `instanceof`来进行判断

##### 5.14、 instanceof关键字的使用

**instanceof:**

实例a instanceof A类 ： 判断 实例a是否是A的实例，如果是就不往上找了、返回true，如果不是，就继续找a类的继承的父类，直到找到Object

a  instanceof A  true //实例a是通过A类创建的

a  instanceof Object  //true  A类继承Object

a  instanceof B  false

**多态性练习**

```java
class Base {
    int count = 10;
    public void display() {
    System.out.println(this.count);
} 
class Sub extends Base {
    int count = 20;
    public void display() {
    System.out.println(this.count);
}
    
public class FieldMethodTest {
    public static void main(String[] args){
    Sub s = new Sub(); //创建s实例对象
    System.out.println(s.count); //s实例.count 现在自己类内部找count，找到就使用，找不到就去父类中查找，这里找到了，为20， 输出20
    s.display(); //s实例.display 同上，现在本类内部找，找到就调用，找不到就想父类中找 ... 输出20
    Base b = s; // 等加以 Base b= new Sub(); 父类的引用指向子类的实例，是多态性的体现特征, "="是赋值操作，由于赋值的是引用数据类型，所以赋值的是指针地址，所以b和s都存储同样的指针
    System.out.println(b == s); // ==  对比的是值或者是 指针是否相同，由上所知 地址相同，所以为true
    System.out.println(b.count); //多态性不适用于属性，所以父类的引用b.count还是在父类中查找，所以发音 10
    b.display(); //多态性适用于重写的方法，所以父类的引用b.display，实际调用的是子类中的display方法，所以打印的是 20
} 
```



**多态练习二**



```java
建立InstanceTest 类，在类中定义方法
method(Person e);
在method中:
(1)根据e的类型调用相应类的getInfo()方法。
(2)根据e的类型执行：
如果e为Person类的对象，输出： “a person”;
如果e为Student类的对象，输出：
“a student”
“a person ” 
如果e为Graduate类的对象，输出：
“a graduated student”
“a student”
“a person”

package hello;

public class InstanceTest {
	public static void main(String[] args) {
		InstanceTest it= new InstanceTest();
		it.method(new Person());  
		it.method(new Student());
		it.method(new Graduate());
	}
	public void method(Person e) { //多态的使用，Person为父类，传入的是 子类或者是自己创建的类，调用的时候调用子类重写的方法
		System.out.println("*************************");
		System.out.println(e.getInfo());
		if(e instanceof Graduate) {
			System.out.println("a graduated student\r\n" + 
					"a student\r\n" + 
					"a person");
		}else if(e instanceof Student) {
			System.out.println("a student”\r\n" + 
					"“a person ");
		}else if(e instanceof Person) {
			System.out.println("a person");
		}
	}
}

class Person {
	 protected String name="person";
	 protected int age=50;
	 public String getInfo() {
		 return "Name: "+ name + "\n" +"age: "+ age; //Name: person age: 50
	 }
 }

class Student extends Person {
	 protected String school="pku";
	 public String getInfo() {
		 return "Name: "+ name + "\nage: "+ age + "\nschool: "+ school; //Name: pku age: 50 school: pku  注： age找不到，就去父类充查找，找到就使用
	 }
} 
class Graduate extends Student{
	 public String major="IT";
	 public String getInfo(){  
		 return "Name: "+ name + "\nage: "+ age + "\nschool: "+ school+"\nmajor:"+major;  //Name: pku age: 50 school: pku major: IT
	 }  
 }
```

**继承性练习 3**

```java
package hello;

public class a {
	public static void main(String[] args) {
		Base base= new Sub(); //父类的引用，指向子类对象，是多态性
		base.add(1,2,3); //sub_1 原因：多态性的两个条件： 1、继承关系，2、方法的重写； 编译的时候 是调用父类中的add，父类中的add中参数为 (int a, int ...arr),但是多态性在运行的时候指向的是子类的add
		// 子类中的add重写了父类中的add，由于子类重写了父类，那么方法名相同，都为add,方法参数列表相同，而(int a, int ...arr)刚好和父类中add的参数列表形同，所以，public void add(int a, int[] arr) {}
		//就是调用的方法，测试 a= 1  arr= [2,3]
		Sub s= (Sub)base; //强转为子对象类型，这时，可以调用子类中的方法或属性了
		s.add(1,2,3); //sub_2 由于 add(int a, int[] arr) 和 add(int a, int b, int c)都满足条件，但是选最优的，选择 add(int a, int b, int c)调用，所以打印 sub_2
	}
}


class Base {
	public void add(int a, int ...arr) {
		System.out.println("base");
	}
}

class Sub extends Base {
	public void add(int a, int[] arr) {
		System.out.println("sub_1");
	}
	public void add(int a, int b, int c) {
		System.out.println("sub_2");
	}
}
```

##### 5.15、 == 和 equals() 方法的区别

一、 `==`运算符：

|          | 基本数据类型       | 引用数据类型                                                 |
| -------- | :----------------- | ------------------------------------------------------------ |
| ==       | 比较值两者是否相同 | 比较两者地址是否相同                                         |
| equals() | 无法对比           | Object中的equals对比的是两者地址是否相同，和`==`一样  ；在String类、Date类、File类、包装类中，重写了equals方法，对比的是两个对象的“实体内容”是否一致 |

注意： 使用 `==`符号时，必须保证符号左右两边的变量一致。否则编译报错

![5-15 ==和equals之间的区别](images\5-15 ==和equals之间的区别.png)

**练习题**
```java
int it = 65;
float fl = 65.0f;
System.out.println(“65和65.0f是否相等？” + (it == fl)); //true  对比的是值，而却都是数字类型
char ch1 = 'A'; char ch2 = 12; 
System.out.println("65和'A'是否相等？" + (it == ch1));//true
System.out.println(“12和ch2是否相等？" + (12 == ch2));//true
String str1 = new String("hello");
String str2 = new String("hello");
System.out.println("str1和str2是否相等？"+ (str1 == str2));//false  对比的是地址
System.out.println("str1是否equals str2？"+(str1.equals(str2)));//true   对比的是值
System.out.println(“hello” == new java.util.Date()); //编译不通过  两边类型不同，编译不通过
```

```java
package equalsTest;
/*
 1.编写Order类，有int型的orderId，String型的orderName，相应的
getter()和setter()方法，两个参数的构造器，重写父类的equals()方法：
public boolean equals(Object obj)，并判断测试类中创建的两个对象是否
相等。
 * */
public class Order {
	private int orderId;
	private String orderName;
	public int getOrderId() {
		return orderId;
	}
	public void setOrderId(int orderId) {
		this.orderId = orderId;
	}
	public String getOrderName() {
		return orderName;
	}
	public void setOrderName(String orderName) {
		this.orderName = orderName;
	}
	/**
	 * 重写equals方法
	 */
	@Override
	public boolean equals(Object obj) {
		if(this == obj) { //判断两个地址是否相同，如果相同说明两个内容也相同，所以返回true
			return true;
		}
		if(obj instanceof Order) { //判断 obj是否继承自Order类，为了下面强转不会出异常，之后继承自Order类才能转Order类型，不然会报错
			Order order= (Order)obj; //将Object类型的obj强转为Order对象，因为 Object obj 多态性，只能调用子类的obj中重写父类的方法，不能调用obj的属性
			//只有将 Object向下转为Order类型之后，才能调用 子类中的属性，所以才使用了强转
			return order.orderId == this.orderId && this.orderName.equals(order.orderName); //判断基本数据类型就用 == 就可以了，判断的值
			// 判断字符串，就是用 String类重写的equals方法，判断的是类的内容（注意： Object类的equals方法判断的是类的指针 和 == 一样）
		}
		return false;
	}
} 

```

##### 5.16、toString() 方法的使用

* 1、当我们输出一个对象的引用时，实际上就是调用当前对象的toString()

* 2、Object 类中的toString()的定义：

  public String()的定义

  public String toString(){

  ​	return getClass().getName()+"@"+Integer.toHexString(hashCode());

  }

* 3、像String、Date、File、包装类等都重写了Object类的toString()的方法,使得在调用对象的toString()时，返回实体内容

##### 5.17、单元测试 JUnit 

![5-17、单元测试JUnit](images\5-17、单元测试JUnit.png)

##### 5.18、包装类的使用

![5-18包装类的对应关系](images\5-18包装类的对应关系.png)

**包装类的使用：**

* 1、java提供了8中基本数据类型对应的包装类，使得基本数据类型的变量具有类的特征

**基本数据类型转化为包装类**
	调用包装类的构造器

```java
Integer int1= new Integer(1);
```



**包装类转化为基本数据类型**
	调用包装类的 xxxValue()

```java
Integer in1= new Integer(12);
int i1= in1.intValue(); //12
```

**自动装箱和拆箱(JDK5.0新增的)**

为了减少上面的转化麻烦，JDK5.0新增加了自动装箱，和封箱；可以很方便的 在基本数据类型和包装类之间进行转化

**基本数据类型转化为 字符串类型**：

1、 基本数据类型+""

2、调用String重载的valueOf方法 String.valueOf(基本数据类型) 



**字符串类型转化为基本数据类型：**

调用包装类的parseXXX()方法

```java
String str1= "123";
int in1= Integer.parseInt(str1); //123

boolean in1= Boolean.parseBoolean("TruE"); //true
boolean in1= Boolean.parseBoolean("False"); //false
boolean in1= Boolean.parseBoolean("true123"); //false
```



```java
@Test

public void transform3() {
    Integer in1= 3; //自动装箱, 直接将基本数据类型赋值给包装类变量
    System.out.println(in1.floatValue());
    int in2= in1; //自动拆箱 直接将包装类对象赋值给基本数据类型
    System.out.println(in2);
}
```





```java
package JUnitTest;

import org.junit.jupiter.api.Test;

public class BaoZhuangLeiTest {
	@Test
	public void transform1() {
		int a1= 10;
		Integer a1_1= new Integer(a1); // 10
		Integer a1_2= new Integer("10"); // 10
//		Integer a1_3= new Integer("10.0"); // 报错 
//		Integer a1_4= new Integer("10Abc"); // 报错
	}
	@Test
	public void transform2() {
		/*Boolean 包装类： 输入字符串或布尔值都行，如果输入的是字符串，先忽略大小写，判断是否是纯 true或false,如果不是则返回false,注意由于Boolean包装类是对象，
		 * 所以，当没有指定值的时候，默认为null*/
		Boolean a1_1= new Boolean(true); // true
		Boolean a1_2= new Boolean("false"); // false
		Boolean a1_3= new Boolean("TruE"); // true
		Boolean a1_4= new Boolean("TruE123"); // false
		System.out.println(a1_1);
		System.out.println(a1_2);
		System.out.println(a1_3);
		System.out.println(a1_4);
		
		//如：
		class Boo {
			public Boolean B1; //null
		}
		System.out.println(new Boo().B1);
	}
}

```

**练习一**

```java
Object o1 = true ? new Integer(1) : new Double(2.0);
System.out.println(o1);// 1.0


Object o2;
if (true)
o2 = new Integer(1);
else
o2 = new Double(2.0);
System.out.println(o2);// 1
```

**练习二**

```java
public void method1() {
    Integer i = new Integer(1);
    Integer j = new Integer(1);
    System.out.println(i == j); // false 两个对象对比，比的是地址，所以两者不相同
    Integer m = 1;
    Integer n = 1;
    System.out.println(m == n);// true Integer类内部中有一个 IntegerCache类，这个IntegerCache类 内部有一个 cache[]数组，数组的范围为-128~127之间的整数，当我们使用自动装箱的方式 Integer m = 1;的时候，不再进行new了，直接在数组中进行使用，所以两个使用的是同一个数，所以返回true;这样有助于提升性能，把经常使用的数给缓存起来了
    Integer x = 128; 
    Integer y = 128;
    System.out.println(x == y);// false  128不再 cache[]数组中，所以需要new，所以两者的地址不同，返回false
}
```

**练习三**

```java
/*
利用Vector代替数组处理：从键盘读入学生成绩（以负数代表输入结束），找出
最高分，并输出学生成绩等级。
提示：数组一旦创建，长度就固定不变，所以在创建数组前就需要知道它的
长度。而向量类java.util.Vector可以根据需要动态伸缩。
创建Vector对象：Vector v=new Vector();
给向量添加元素：v.addElement(Object obj); //obj必须是对象
取出向量中的元素：Object obj=v.elementAt(0);
注意第一个元素的下标是0，返回值是Object类型的。
计算向量的长度：v.size();
若与最高分相差10分内：A等；20分内：B等；
30分内：C等；其它：D等
*/

package com.larry.exec1;

import java.util.Scanner;
import java.util.Vector;
/*
利用Vector代替数组处理：从键盘读入学生成绩（以负数代表输入结束），找出
最高分，并输出学生成绩等级。
提示：数组一旦创建，长度就固定不变，所以在创建数组前就需要知道它的
长度。而向量类java.util.Vector可以根据需要动态伸缩。
创建Vector对象：Vector v=new Vector();
给向量添加元素：v.addElement(Object obj); //obj必须是对象
取出向量中的元素：Object obj=v.elementAt(0);
注意第一个元素的下标是0，返回值是Object类型的。
计算向量的长度：v.size();
若与最高分相差10分内：A等；20分内：B等；
30分内：C等；其它：D等
*/
public class StudentScore {
	public static void main(String[] args) {
		Scanner sc= new Scanner(System.in);
		Vector v= new Vector(); 
		int maxScore= 0;
		for(;;) {
			System.out.println("请输入学生成绩：");
			int score= sc.nextInt(); //输入的学生成绩
			if(score < 0) { //输入的学生成绩为负数时，结束输入
				System.out.println("结束输入");
				break;
			}
			if(score > 100) { //输入的学生成绩为负数时，结束输入
				System.out.println("输入错误请重新输入");
				continue;
			}
			//v.addElement(Object obj); //obj必须是对象		
			/*
			 * jdk5.0之前，我们可以将int转为 Integer类型，再传进去  v.addElement(new Integer(score));
			 *   但是在5.0之后，基本数据类型转化为包装类，有了“装箱”和“拆箱”的操作，所以我们 可以
			 *   Integer a= score
			 *   v.addElement(new Integer(a));
			 *         等价于  v.addElement(score); 会自动将int类型转化为Integer类型的
			 * */ 
			v.addElement(score);
			if(score > maxScore) {
				maxScore= score;
			}
			
		}
		
		// 遍历，获取每一项的分数，和最大值对比	与最高分相差10分内：A等；20分内：B等； 30分内：C等；其它：D等	
		for(int i=0; i< v.size(); i++) {
			Object obj=v.elementAt(i); //右边的每一项是Integer类型的，左边的 Object类型的,所以此时是多态性的体现
			Integer sco= (Integer)obj; //将对象，请转为Integer类型的，这样才能调用Integer类型的属性和方法
			int score= sco.intValue(); //将Integer 转化为int
			int val= maxScore - score;
			if(val <= 10) {
				System.out.println("maxScore="+maxScore+"score="+score+"lv=A");
			}else if(val <= 20) {
				System.out.println("maxScore="+maxScore+"score="+score+"lv=B");
			}else if(val <= 30) {
				System.out.println("maxScore="+maxScore+"score="+score+"lv=C");
			}else {
				System.out.println("maxScore="+maxScore+"score="+score+"lv=D");
			}
			
		}
		
	}
}

```

#### 6、面向对象 （下）

##### 6.1、 static关键字

![6-1static关键字](images\6-1static关键字.png)

###### **6.1.1、static修饰属性，静态（或类变量）**

​	**1.1、属性、按照是否使用static修饰，又分为：**静态属性 和非静态属性（实例变量）

​		**实例变量**： 我们创建了类的多个对象，每个对象都独立有一套类中的非静态属性。当修改其中一个对象的非静态属性时，不会导致其他对象中同样的属性值的修改

​		**静态变量**：我们创建了类的对个对象，每个对象都共享同一个静态变量。当通过某一个对象修改静态变量时，会导致其他队形调用此静态变量时，是修改过了的。

​	**1.2、 static修饰属性的其他说明**

​		1.2.1、静态变量随着类的加载而加载。可以通过`类.静态变量`的方式进行调用

​		1.2.2、静态变量的加载要早于对象的创建（所以可以直接 `类.静态变量`）

​		1.2.3、由于类智慧加载一次，则静态变量在内存中也只会存在一份，存在方法区的静态域中。

**类和对象是都能调用 类变量(静态变量) 和 实例变量**

|      | 类变量(静态变量) | 实例变量 |
| ---- | ---------------- | -------- |
| 类   | yes              | no       |
| 对象 | yes              | yes      |

​	 **静态和动态变量，在内存中的解析**

![6-1.2static静态变量在内存中存储位置](images\6-1.2static静态变量在内存中存储位置.png)

###### 6.1.2、static修饰方法，静态方法（或类方法）

​	**1.1、随着类的加载而加载，可以通过`类.静态方法`的方式进行调用**

|      | 类方法(静态方法) | 实例方法（非静态方法） |
| ---- | ---------------- | ---------------------- |
| 类   | yes              | no                     |
| 对象 | yes              | yes                    |

​	**1.2、静态方法中，只能调用静态的属性或方法；非静态方法中可以使用非静态的属性和方法，也可以调用静态的属性和方法**

​	**1.3、static注意点： 在静态方法内，不能使用`this`和`super`关键字 ；因为static是类加载的时候创建的，此时还没有实例对象，所以没有this**

​	**1.4、注意： 当我们调用静态方法或属性的时候，如果前面省略前缀，那么我们省略的是这个类；但是在非静态方法内部，我们调用静态属性或方法，可以使用 `对象.静态属性或方法`，`类名.静态属性或方法`,直接调用`静态属性或方法`**

```java
package com.larry.staticTest;

import org.junit.jupiter.api.Test;

public class Exec1 {
	public static String name="张三"; //静态属性
    public int age; //非静态属性
    
    public static String info(){//静态方法
       	return "静态info方法输出"+name;
    }
    @Test
    public void play(){ //非静态方法
    	System.out.println(Exec1.name); //张三
    	System.out.println(name); //张三
    	System.out.println(this.name); //张三 不推荐这种写法，虽然都可以调到静态的属性
    	System.out.println(info()); //静态info方法输出张三    直接调用 info() 相当于直接调用 Exec1.info()
    	System.out.println(Exec1.info()); //静态info方法输出张三 
    	System.out.println(this.info()); //静态info方法输出张三   不推荐这种写法，虽然都可以调到静态的属性
    	
    	
    	System.out.println(this.age); // 0 
    }
}

```

**开发中，如何确定一个属性是都需要声明为static的**

​	1、属性是可以被对个对象所共享的，不会随着对象的不同而不同的。

​	2、类中的常量也常常被修饰为static

**开发中，如何确定一个方法是都需要声明为static的**

​	1、操作静态属性的方法（getXXX,setXXX），通过设置static的

​	2、工具类中的方法，习惯上声明为static的，比如：Math、Arrays ...

##### 6.2、单例模式

所谓类的单例设计模式，就是采取一定的方法保证在整个的软件系统中，对 

某个类**只能存在一个对象实例**，并且该类只提供一个取得其对象实例的方法。 

如果我们要让类在一个虚拟机中只能产生一个对象，我们首先必须将类的构 

造器的访问权限设置为private，这样，就不能用new操作符在类的外部产生 

类的对象了，但在类内部仍可以产生该类的对象。因为在类的外部开始还无 

法得到类的对象，只能调用该类的某个静态方法以返回类内部创建的对象， 

静态方法只能访问类中的静态成员变量，所以，指向类内部产生的该类对象 

的变量也必须定义成静态的

**单例设计模式-饿汉式**  

```java
class Singleton {
// 1.私有化构造器
private Singleton() {
}
// 2.内部提供一个当前类的实例
// 4.此实例也必须静态化
private static Singleton single = new Singleton();
// 3.提供公共的静态的方法，返回当前类的对象
public static Singleton getInstance() {
return single; } }
```

**单例设计模式-懒汉式**

```java
class Singleton {
// 1.私有化构造器
private Singleton() {
}
// 2.内部提供一个当前类的实例
// 4.此实例也必须静态化
private static Singleton single;
// 3.提供公共的静态的方法，返回当前类的对象
public static Singleton getInstance() {
if(single == null) {
single = new Singleton();
}
return single; } }
```



```java
package com.larry.singleTest;

/*饿汉式单例模式*/
public class SingTest1 {
	// 1、私有化构造器
	private SingTest1() { //由于构造函数是私有化的，所以不能在类外面直接通过 new的方式创建对象
		
	}

	private static SingTest1 instance= new SingTest1(); //由于 属性instance是static，所以类在一加载的时候，就创建了 new SingTest1() 类，并赋值给instance,
	
	public static SingTest1 getInstance() { //由于 instance是私有属性，外界不能访问，所以封装了一个getInstance方法，来返回创建好的实例对象，由于构造函数被私有了，所以没法通过实例调用对象，
		//所以以后只能通过static来 将 getInstance变为静态方法，这样可以通过 SingTest1.getInstance()来获取类加载的时候创建的那一个类
		return instance;
	}
	
}



/*懒汉式单例模式   什么时候使用，什么时候创建*/
class SingTest2 {
	// 1、私有化构造器
	private SingTest2() { //由于构造函数是私有化的，所以不能在类外面直接通过 new的方式创建对象
		
	}

	private static SingTest2 instance= null; //由于 属性instance是static，所以在创建的时候就赋值为null
	
	public static SingTest2 getInstance() { //由于 instance是私有属性，外界不能访问，所以封装了一个getInstance方法，instance，由于构造函数被私有了，所以没法通过实例调用对象，
		//所以以后只能通过static来 将 getInstance变为静态方法，这样可以通过 SingTest1.getInstance()来获取类；获取的时候会判断 instance是否存在，存在就获取，不存在就创建建
		if(instance == null) {
			instance= new SingTest2();
		}
		return instance;
	}
	
}
```

**单例模式的优点：** 

由于单例模式只生成一个实例，减少了系统性能开销，当一个对象的 
产生需要比较多的资源时，如读取配置、产生其他依赖对象时，则可 
以通过在应用启动时直接产生一个单例对象，然后永久驻留内存的方 
式来解决。 



**饿汉式---缺点：** 类一加载就创建实例，而不是使用时创建，影响内存空间

**懒汉式---缺点：**  懒汉式暂时还存在线程安全问题，讲到多 线程时，可修复 

##### 6.3、main方法的理解

​	1、main() 方法是程序的入口

​	2、main() 方法也是一个普通的静态方法

由于 main方法做入口的时候，当程序一加载的时候，我们没有创建类来调用main方法，所以 main是static静态方法，不需要创建对接直接 `类.main()`执行

由于main是static，所以不能直接通过 `类.非静态属性/方法`调用，因为有可能此时现在还没有生成；所以只能通过创建 类的实例，再进行`实例.非静态属性/方法`调用

main做入口时，不需要任何返回值，也没人接收，所以返回值为void

String[] args  参数是当 程序在命令行运行时，传进来的参数

如下

```shell
javac Hellowoed.java

java Hellowoed 你好 2 lks 

你好 2 lks 都是人为是字符串的参数，多个参数之间用空格隔开， java 时传进来

public static void main(String[] args){
    for(int i=0; i<args.length;i++ ){
    	syso("-----"+arrs[i]); 
    	/*
    	-----你好
    	-----2
    	-----lks
    	*/
    }
}
```



```java
public static void main(String[] args){
    
}
```

##### 6.4、类的 代码块

**1、代码块的作用：**用来初始化类、对象
**2、代码块如果有修饰的话：**只能使用 static 或不适用修饰符
**3、分类： 静态代码块（static） vs 非静态代码块**

|              | 加载时机               | 作用         | 定义多个时执行顺序     | 静态代码块和非静态代码块执行先后顺序 | 代码块内能调用的类型                       |
| ------------ | ---------------------- | ------------ | ---------------------- | ------------------------------------ | ------------------------------------------ |
| 静态代码块   | 类加载时               | 初始化类信息 | 按照声明的先后顺序执行 | 先执行                               | 静态属性，静态方法                         |
| 非静态代码块 | 对象创建时（实例化时） | 初始化类信息 | 按照声明的先后顺序执行 | 后执行                               | 静态属性，静态方法，非静态属性，非静态方法 |

```java
package com.larry.singleTest;
 class BlockTest {
	 public static void main(String[] args) {
		 BlockTest1.name="mm"; //这一步的目的是加载 BlockTest1类,注意 执行BlockTest1是加载 类，然后 执行static属性和 代码块，执行完之后，执行BlockTest1.name="mm"，进行赋值
		 BlockTest1 bt= new BlockTest1();
	}
 }
class BlockTest1 {
	public static String name= "zs";
	private int age;
	
	static {
		System.out.println("name="+name); //name=zs
		name= "ls";
		System.out.println("name="+name); //name=ls
		play(); //爱踢足球
		//System.out.println("age="+age); //不能调用，因为此时age还没有被加载，所以会报错
		//eat() //不能调用，因为此时eat还没有被加载，所以会报错
		//这一步走完之后，开始BlockTest1.name="mm";
	}
	{
		System.out.println("name="+name); //name=mm 所以这里是mm
		name= "ww";
		System.out.println("name="+name); //name=ww
		play(); //爱踢足球
		eat(); //吃零食
	}
	
	public static void play() {
		System.out.println("爱踢足球");
	}
	public  void eat() {
		System.out.println("吃零食");
	}
	
}

```

**练习一： 下面输出是什么**

```java
package com.atguigu.java3;
//总结：由父及子，静态先行
class Root{
	static{
		System.out.println("Root的静态初始化块");
	}
	{
		System.out.println("Root的普通初始化块");
	}
	public Root(){
		super();
		System.out.println("Root的无参数的构造器");
	}
}
class Mid extends Root{
	static{
		System.out.println("Mid的静态初始化块");
	}
	{
		System.out.println("Mid的普通初始化块");
	}
	public Mid(){
		super();
		System.out.println("Mid的无参数的构造器");
	}
	public Mid(String msg){
		//通过this调用同一类中重载的构造器
		this();
		System.out.println("Mid的带参数构造器，其参数值："
			+ msg);
	}
}
class Leaf extends Mid{
	static{
		System.out.println("Leaf的静态初始化块");
	}
	{
		System.out.println("Leaf的普通初始化块");
	}	
	public Leaf(){
		//通过super调用父类中有一个字符串参数的构造器
		super("尚硅谷");
		System.out.println("Leaf的构造器");
	}
}


public class LeafTest{
	public static void main(String[] args){
		new Leaf(); //步骤一
		System.out.println();
		new Leaf(); //步骤二
	}
}
/*
非静态代码块要先于构造器中的其他语句执行

步骤一： 在new Leaf(); 的时候，要先看看Leaf类中的构造器看看父类是怎么加载的，就是通过Leaf找到父类Mid，然后在通过Mid找到Root父类，再通过Root 父类找到 Object;此时，就先依次从父类向子类进行加载，顺序为：
Object --> Root --> Mid --> Leaf 依次加载；
加载的时候先加载静态属性和方法，然后执行代码块，
所以此时会输出

Root的静态初始化块；
Mid的静态初始化块；
Leaf静态初始化块；

类加载完毕之后，开始执行类的构造器，构造器也是从父向子依次执行，
所以当执行Root构造器时，会输出
Root的普通初始化块； 因为执行构造器就是创建了对象，创建对象的时候就会执行“非静态代码块”
Root的无参数的构造器；
Mid的普通初始化块；
Mid的无参数的构造器；
Mid的带参数构造器，其参数值：尚硅谷
Leaf的普通初始化块；
Leaf的构造器； 

再执行new Leaf();的时候
开始执行类的构造器，构造器也是从父向子依次执行，
所以当执行Root构造器时，会输出
Root的普通初始化块； 因为执行构造器就是创建了对象，创建对象的时候就会执行“非静态代码块”
Root的无参数的构造器；
Mid的普通初始化块；
Mid的无参数的构造器；
Mid的带参数构造器，其参数值：尚硅谷
Leaf的普通初始化块；
Leaf的构造器； 



**/

```

**练习二**

```java
package com.atguigu.java3;

class Father {
	static {
		System.out.println("11111111111");
	}
	{
		System.out.println("22222222222");
	}

	public Father() {
		System.out.println("33333333333");

	}

}

public class Son extends Father {
	static {
		System.out.println("44444444444");
	}
	{
		System.out.println("55555555555");
	}
	public Son() {
		System.out.println("66666666666");
	}


	public static void main(String[] args) { // 由父及子 静态先行
		System.out.println("77777777777");
		System.out.println("************************");
		new Son();
		System.out.println("************************");
		new Son();
		System.out.println("************************");
		new Father();
	}

}
/*
main方法可以当入口也可以当普通方法
当入口时，先看自己的类的父类 Father， 再通过父类Father继续找父类Object
然后 Object -->  Father -- > son依次加载

11111111111 //加载的时候先父类
44444444444 //加载的时候先父类再子类
77777777777 //加载完之后执行main静态方法
************************
22222222222 //new Son();的时候先执行父类的非静态代码块，再执行构造函数内部的语句，然后再执行子类的非静态代码块，再执行构造函数内部的语句
33333333333
55555555555
66666666666
************************
22222222222
33333333333
55555555555
66666666666


*/
```

##### **6.5、属性赋值的先后顺序**

1、默认初始化

2、显示初始化 / 5代码块中初始化

3、构造器初始化

4、有了对象以后，可以通过`对象.属性`或`对象.方法`的方式赋值

执行先后顺序 1 --- 2 / 5 -- 3 -- 4

**2和5的先后顺序是，谁在前先执行谁**

##### 6.6、final关键字的使用

**final可以用来修饰： 类、方法、变量**

**1、final修饰类一个类：**此类不能被其他类所继承；
比如：String类、System类StringBuffer类

**2、final修饰类一个类：**表示此方法不可以被重写 （子类中不能重写此方法）
```java
class Person {
	public final void play(){
		syso("123")
	}
}

class Student extends Person {
	public void play(){ //错误的，子类中不能重写父类中使用final关键子修饰的方法
		syso("123")
	}
}
```
**3、final修饰类变量：**表示此变量就是一个常量，不可以被重写 
	3.1、final修饰属性： 可以赋值的位置有： 显示初始化、代码块中初始化、构造器中初始化
	3.2、final修饰局部变量： 可以修饰变量、也可以修饰方法中的形参；当修饰形参时，给常量形参赋值一个实现实参。一旦赋值以后。就只能在方法体内使用此形参，但不能进行重新赋值

```java
class Person {
	public final String name= "zs"; //显示赋值可以
	public final int age; 
	public final int general; 
	{
		age= 18; //代码块中初始化 可以
	}
	public Person(){
		general= 1; //构造器中赋值 可以
	}
	public void play(final int num){
		syso("num"+num)
		num++ //错误，final修饰的形参不可以赋值
	}
}
```

static final  int a= 123; //static final修饰的变量称为，全局常量

##### 6.7、抽象类和抽象方法
随着继承层次中一个个新子类的定义，类变得越来越具体，而父类则更一 般，更通用。类的设计应该保证父类和子类能够共享特征。有时将一个父 类设计得非常抽象，以至于它没有具体的实例，这样的类叫做抽象类。

**说明**
* 用abstract关键字来修饰一个类，这个类叫做抽象类。 （**抽象类不能被实例化**）

* 用abstract来修饰一个方法，该方法叫做抽象方法。 （**抽象方法所在的类一定为抽象类，反之，抽象类中的方法不一定是抽象方法**）

  抽象方法：只有方法的声明，没有方法的实现。以分号结束： 
  比如：**public abstract void talk();** 
  含有抽象方法的类必须被声明为抽象类。 

* 抽象类不能被实例化。抽象类是用来被继承的，抽象类的子类必须重 写父类的抽象方法，并提供方法体。若没有重写全部的抽象方法，仍 为抽象类。 

* 不能用abstract修饰**变量**、**代码块**、**构造器**； （**因为这些都不能被重写**）

* 不能用abstract修饰**私有方法**、**静态方法**、**final的方法**、**final的类**。

  解释： 私有方法和static静态方法和final的方法不能被重写，所以没法使用 abstract修饰

  final的类： 不能被继承，所以也没办法被构建子类

  **************************************************************************************************************************************************************************************

  

  **abstract关键字的使用**

  1、abstract: 抽象的

  2、abstract可以用来修饰的结构： 类、方法

* abstract修饰类：  抽象类

  1、此类不能实例化

  2、炒股想类中一定有构造器，便于子类实例化时调用（涉及，子类对象实例化的全过程）

  3、开发中，都会提供抽象类的子类，让子类对象实例化，完成相关的操作

* abstract修饰方法： 抽象方法

  1、抽象方法只有方法的声明，没有方法体； eg:  public abstract void talk();

  2、包含抽象方法的类，一定是一个抽象类。反之，抽象类中可以没有抽象方法的

  3、若字另类重写了父类中所有的抽象方法后，此类方可实例化

  4、若子类没有重写父类中的所有抽象方法，则子类也是一个抽象类，需要使用功能abstract修饰

  **注意： abstract使用的注意点**

* 1、abstract 只能修饰类和方法，不能修饰： 属性，构造器

* 2、abstract不能用来修饰私有方法、静态方法、final的方法、final的类

**练习**

```java
package com.larry.abstractTest;

public abstract class Employee { //抽象类
	public String name;
	public int id;
	public String salary;
	public Employee() { //空参构造器
		
	}
	public Employee(String name,int id,String salary) { //带参构造器
		this.name= name;
		this.id= id;
		this.salary= salary;
	}
	public abstract void work(); //抽象方法，子类继承的时候需要重写此方法
}


package com.larry.abstractTest;

public class Manager extends Employee{ //子类继承抽象类
	public double bouns;
	
	public Manager(double bouns) {
		super();
		this.bouns = bouns;
	}

	@Override
	public void work() { //重写继承的抽象类中的抽象方法
		System.out.println("工作");
	}
	
}


```

**练习： 模板方法**

```java
//计算某个代码执行花费的时间；
abstract class Template {
    public final void getTime() {
        long start = System.currentTimeMillis();
        code(); //省略了 this，this指向当前实例，也就是 sub，而sub现在自己类的内部找code方法，找到了就使用，所以此时调用的是子类中的方法
        long end = System.currentTimeMillis();
        System.out.println("执行时间是：" + (end - start));
	}
	public abstract void code(); //抽象类
}
class SubTemplate extends Template {
    public void code() { //重写抽象类
        for (int i = 0; i < 10000; i++) {
            System.out.println(i);
        }
    } 
}

class TemplateTest{
    public static void main(String[] args){
        SubTemplate sub= new SubTemplate(); //创建子类实例
        sub.getTime(); //实例调用继承父类的方法，
    }
}
```

##### 6.8、interface 接口

 * 1、接口使用interface来定义
 * 2、Java中，接口和类时两个并列的结构
 * 3、如何定义接口，定义接口中的成员
    	3.1、JDK7及以前，接口中只能定义去**全局常量**和**抽象方法**
    		全局常量： public static final的，但是书写时，可以省略不写
    		抽象方法： public abstract修饰的，但是书写时，可以省略不写
   3.2、JDK8： 除了定义全局常量之外，还可以定义**静态方法**、**默认方法**
 * 4、接口中不能定义构造器，意味着接口不能够实例化
 * 5、Java开发中，接口通过让类去实现（implements）的方式来使用
	 	  如果实现类覆盖了接中的所有方法，则此类就可以实例化
	     如果实现类没有覆盖了接中的所有方法，则此类任然为抽象类，需要使用abstract关键字修饰
 * 6、Java类可以实现多个接口 ---> 弥补了Java单继承性的局限性 格式如下

**一个类实现多个接口**

```java
class A类名 extends B父类名 implements CC接口,DD接口,EE接口 {
    ...
} 
```

* 7、接口与接口之间可以继承，而且可以多继承 用`extends`关键字
* 8、接口的具体使用、体现多态性
* 接口，实际上可以看做是一种规范

```java
package com.larry.interfaceTest;
/*
 **接口使用**
 * 1、接口使用interface来定义
 * 2、Java中，接口和类时两个并列的结构
 * 3、如何定义接口，定义接口中的成员
 * 	3.1、JDK7及以前，接口中只能定义去**全局常量**和**抽象方法**
 * 		全局常量： public static final的，但是书写时，可以省略不写
 * 		抽象方法： public abstract修饰的，但是书写时，可以省略不写
 *  3.2、JDK8： 除了定义全局常量之外，还可以定义**静态方法**、**默认方法**
 * 
 * 4、接口中不能定义构造器，意味着接口不能够实例化
 * 5、Java开发中，接口通过让类去实现（implements）的方式来使用
 * 	  如果实现类覆盖了接中的所有方法，则此类就可以实例化
 *           如果实现类没有覆盖了接中的所有方法，则此类任然为抽象类，需要使用abstract关键字修饰
 */
public class InterfaceTest  {
	public static void main(String[] args) {
		Bird xiaoniao= new Bird();
		System.out.println(xiaoniao.name);//鸟类 输出的是 类实现接口中的静态属性
		System.out.println(xiaoniao.run()); // 小鸟会跑  
		xiaoniao.eat(); //鸟类吃食物 name是接口中的名字
		xiaoniao.moveStyle(); // 接口实现继承实现Move接口的方法
	}
}

class Bird extends Aniaml implements Flyable {
	@Override
	public String run() {
		return "小鸟会跑";
	}
	@Override
	public void eat() {
		System.out.println(name+"吃食物");
	}
	@Override
	public void moveStyle() {
		System.out.println("实现Move接口的方法");
	}
}
class Aniaml {
	public static String type="鸟类";
}

interface  Flyable extends Move{ //接口中的继承
	public static final String name="鸟类";
	int foots=2; //省略了 public static final
	
	public abstract String run(); //抽象方法
	void eat(); //抽象方法，省略了 public abstract
}

interface  Move {
	boolean canMove= true;
	void moveStyle();
}



```

**接口体现多态性的联系**

```java
package com.larry.interfaceTest;

public class UsbTest {
	public static void main(String[] args) {
		Computer pc= new Computer();
		Flash flash= new Flash(); //创建flash实例
		pc.transferData(flash);//将实现USB接口（即 implements USB）的类的实例传过去
		
		// 同样，这种方式也可以
		/**
		 * new USB() { 
					@Override
					public void start() {
						System.out.println("开始 start");
					}
		
					@Override
					public void end() {
						System.out.println("开始 start");
					}
					
				})	
				
		 等价于 ：
		 class Flash implements USB { // Flash实现 Usb接口
				@Override
				public void start() { //实现Usb中的抽象方法
					System.out.println("开始 start");
				}
			
				@Override
				public void end() {  //实现Usb中的抽象方法
					System.out.println("结束 end");
				}
				
		 }
		Flash flash= new Flash(); //创建flash实例
		pc.transferData(flash);
		 */
		pc.transferData(new USB() { 
			@Override
			public void start() {
				System.out.println("开始 start");
			}

			@Override
			public void end() {
				System.out.println("开始 start");
			}
			
		});
	}
}

class Computer {
	public void transferData(USB usb) { //形参是USB接口类型的数据，实际传的是实现USB（即使用implements USB）类的实例
		/*
		 *  形参是类继承的接口类型的，使用的方法是类的实例所实现的方法，所以是多态性的体现
		 * */
		usb.start();
		System.out.println("具体实现数据细节");
		usb.end();
	}
}


interface USB {
	public abstract void start(); //anstract修饰的抽象方法
	void end(); //anstract修饰的抽象方法
}

class Flash implements USB { // Flash实现 Usb接口
	@Override
	public void start() { //实现Usb中的抽象方法
		System.out.println("开始 start");
	}

	@Override
	public void end() {  //实现Usb中的抽象方法
		System.out.println("结束 end");
	}
	
}
```

**明星和经纪人demo**

```java
package com.atguigu.java;

public class StaticProxyTest {

	public static void main(String[] args) {
		Star s = new Proxy(new RealStar()); 
		s.confer(); //经纪人做的事
		s.signContract();//经纪人做的事
		s.bookTicket();//经纪人做的事
		s.sing(); //明星做的事情
		s.collectMoney();//经纪人做的事
	}
}

interface Star {
	void confer();// 面谈

	void signContract();// 签合同

	void bookTicket();// 订票

	void sing();// 唱歌

	void collectMoney();// 收钱
}

class RealStar implements Star { //明星

	public void confer() {
	}

	public void signContract() {
	}

	public void bookTicket() {
	}

	public void sing() {
		System.out.println("明星：歌唱~~~");
	}

	public void collectMoney() {
	}
}

class Proxy implements Star { //经纪人
	private Star real;

	public Proxy(Star real) {
		this.real = real;
	}

	public void confer() {
		System.out.println("经纪人面谈");
	}

	public void signContract() {
		System.out.println("经纪人签合同");
	}

	public void bookTicket() {
		System.out.println("经纪人订票");
	}

	public void sing() {
		real.sing();
	}

	public void collectMoney() {
		System.out.println("经纪人收钱");
	}
}

```

