有main()方法的的类一定是主类，主类不一定是public类
任何一种可运行.class文件的都可称为JVM
若有public类，文件名要与之相同，没有则可以任意命名
DOS下运行需要java 主类名

## 数据类型
数据通过变量名来调用，用变量名来代表该数据的内存位置
由于数据所需内存容量不同，所以通过数据类型来区分
数据类型不同-->数据结构/存储方式不同-->算法不同
||||
|-|-|-|
|byte|8位|范围-128（-27）~127（27-1）|
|short|16位|范围-215~215-1|
|int|32位|范围-231~231-1|
|long|64位|范围-263~263-1|
|float|32位||
|double（默认）|64位|
|char|字符型|存储单字符	占据两个字节，是16位无符号的整数，有2^16^=65536个，范围为0~65535。在Unicode码中用16进制表示，范围为\u0000到\uFFFF。|
所有关系运算的返回值均为boolean类型的值（1Byte）

常量以final修饰，表示不可更改
**整数相除默认为整数**
字符串转数值型：Xxx.parseXxx(String s)，Xxx表示包装类
数值型转字符串：String s = ""+数值

## Scanner类

next()方法以回车、空格、Tab键作为结束符，nextLine()方法以回车作为结束符

## 逻辑运算符

简洁运算符（&&、||），非简洁运算符（&、|）
异或：^，异者，不同也，不能为同，同则错
位运算符


## 流程控制
### switch
```java
switch(表达式){	//表达式为字符或整数类型
	case	常量表达式:
		语句;
		break;
	default:	//默认执行
		语句;
}
```
### while

 ```java
while(条件表达式){	//需要为逻辑值
	循环体;
} 
 ```
### do-while

 ```java
 do{
 	循环体;
}while(条件表达式)
 ```

### while与if区别：

while判断为真后执行循环体，接着再判断，若为真则继续执行循环体，直到判断为假再跳出循环（多次循环直至为错）
if判断为真后执行，错误则不执行（只判断一次）

### for
 ```java
 for(表达式1;条件表达式;表达式2){
 	循环体;
}
 ```

**多维数组的内存理解**

**类**是对某一类事物的描述，是对象的模板、图纸，对象是类的一个实例，是实在的个体。一个类可以对应多个对象
类一般有两个成员：属性（field）和方法（method）
类修饰符：public、abstract、final
抽象类无实现方法，需要子类提供方法，不能创建该类的实例
最终类不能被继承
**变量修饰符**：public、private、protected、final、static、transient、volatile、private

- private：只允许自己类访问，其他类包括子类不能访问
- protected：可被子类、同包下的类访问
- transient：过渡修饰符，系统保留、无特别作用的临时变量
- volatile：易失修饰符，可被几个线程同时控制和修改
方法修饰符注意点：
- static	不需要实例即可使用
- final	不能被重载
- abstract	表明要被子类重写
- synchronized	同步
	对同步资源加锁，以防止其他线程访问，运行结束后解锁
- native	本地
表明方法体由其他编程语言在程序外部编写

局部变量不会自动赋值，必须显式赋值

**匿名对象**：new一个对象而不定义引用变量。使用情形：作为参数传递给其他方法，或对该对象只进行一次方法调用
静态变量和方法从属于类，为实例所共有。好处在于可节省内存空间。

优先以类名.静态变量/静态方法的形式来访问静态变量/方法
静态方法不能访问非静态变量或方法，不能使用this/super关键字
JVM需要在类外调用main()方法，所以main方法为static，访问权限为public

引用变量的标识符保存的是对象在内存中的首地址，也称句柄

类的继承中，在执行子类的构造方法之前会先调用父类的无参构造器，目的是为了初始化子类

向上转型：创建父类类型的变量指向子类对象
 eg：Person per = new Student();
是一个从具体到抽象的过程
向下转型需要强制类型转换

用**final定义成员变量**可以在定义时赋值，也可以在构造器中赋值

==比较符用于比较对象在内存中的首地址，equals()方法用于比较内容是否相等

## 抽象类
起模板作用，抽象出其子类共同的属性和方法
 ```java
 abstract class 类名{
 	声明成员变量;
 	返回值的数据类型 方法名(参数表){
 		···
 	}
 	//抽象方法没有方法体，用于子类覆盖
 	abstract 返回值的类型 方法名(参数表){
 	}
 }
 ```
### 接口
成员变量修饰符默认为public static final，方法修饰符默认为public abstract，接口的方法无方法体，且不能定义普通方法，变量需要初始化
接口实际上是一种特殊的抽象类

**内部类**：类中的类，是外部类的成员

**enumration**
hasMoreElement()与Iterator的hasNext()类似
nextElement()与Iterator的Next()类似

## 容器

### hashtable

与hashmap相比：1.线程安全，效率相对低下
	2.hashtable父类是Dictionary,，hashmap父类是AbstractMap
	3.hashtable键与值不能为null，hashmap键最多一个null，值可以多个null

#### 子类:properties

作用：读写资源配置文件
要求键与值只能为字符串
存储：setProperty(key, value)
方法getProperty(String key)与getProperty(String key, String defaultValue)比较：前一个如果查不到返回值为空，后一个查不到返回值为defaultValue，看了API自己理解为后一个方法套用了前一个方法
获取：load(InputStream inStream)，传入字节流
	load(Reader reader)
	loadFromXML(InputStream in)
store(OutputStream out, String comments)：传入字节流和注释，存储后缀为.properties的流文件
store(Writer writer, String comments)：传入字符流和注释，存储后缀为.properties的流文件
存储后缀.xml文件的方法：storeToXML(OutputStream os, String comment)（默认UTF-8字符集）和重载的storeToXML(OutputStream os, String comment, String encoding)（传入指定字符集）
一旦涉及到字符集，则不能使用字符流，只能使用字节流

## Collection下的其他常用容器

### queue

单向队列
队列通常FIFO(先进先出)
优先级队列和堆栈LIFO(后进先出)
方法：
抛出异常：add（）、remove（）、element（）
特殊值：offer（）、poll（）、peek（）
> 抛出特殊值一般优于抛异常
### Deque(Double-ended queue)
双向队列，两端访问

## io流
按流向分为：输入流、输出流
按数据类型分：字节流、字符流
### 字节流
二进制，可以处理一切文件，包括纯文本、doc、音视频
InputStream、OutputStream
### 字符流

文本文件，只能处理纯文本
Reader、Writer

### FileInputStream/FileOutputStream构造方法

- FileInputStream/FileOutputStream(File file)
- FileInputStream/FileOutputStream(FileDescriptor fdObj)
- FileInputStream/FileOutputStream(String name)
- FileOutputStream(File file, boolean append)
- FileOutputStream(String name, boolean append)
true表示追加，false表示覆盖



### 以下为Java程序设计基础（第五版）教材

```java
import java.io.*;
/**
 * 读取键盘上的输入字符并输出
 */
public class 文件字节流读取键盘并输出 {
	public static void main(String[] args) throws IOException {
		char c;
		int data;
		/*
		*FileDescriptor类不能被实例化，该类有三个静态成员：in，out和err
		*分别对应标准输入流、标准输出流和标准错误流，利用它们可以在标准
		*输入流和标准输出流上建立文件输入输出流，实现键盘输入或屏幕输出操作
		*/
		InputStream in = new FileInputStream(FileDescriptor.in);
		OutputStream out = new FileOutputStream("A:\\JavaTest\\1.txt");
		System.out.println("输入一串字符，以'#'作为结尾");
		//read(),从该输入流读取一个字节的数据。如果没有输入可用，此方法将阻止。
		while((c=(char)in.read())!='#') {
		//write(int b),将指定的字节写入此文件输出流。
			out.write(c);
		}
		in.close();
		out.close();
		
		in = new FileInputStream("A:\\JavaTest\\1.txt");
		out = new FileOutputStream(FileDescriptor.out);
		//available(),返回从此输入流中可以读取（或跳过）的剩余字节数的估计值，而不会被下一次调用此输入流的方法阻塞。
		//System.out.println(in.available());
		while(in.available()>0) {
			data = in.read();
			out.write(data);
		}
		in.close();
		out.close();
		
	}
}
```

```java
import java.io.*;
public class 复制文件 {
	public static void main(String[] args) throws IOException {
		FileInputStream in = new FileInputStream("e:/1.txt");
		FileOutputStream out = new FileOutputStream("e:/11.txt");
		System.out.println("1.txt文件的大小："+in.available());
		byte[] b = new byte[in.available()];
		//read(byte[] b),从该输入流读取最多b.length个字节的数据为字节数组。
		System.out.println(in.read(b));
		//write(byte[] b)，将b.length个字节从指定的字节数组写入此文件输出流
		out.write(b);
		
		in.close();
		out.close();
	}
}
```

```java
import java.io.*;
/**
*DataInputStream(InputStream in)
*DataOutputStream(OutputStream out)
*DataInputStream类方法的传入参数对应方法的返回值
*/
public class 写出不同类型数据 {
	public static void main(String[] args) throws IOException{
		FileOutputStream fout;
	    DataOutputStream dout;
	      fout=new FileOutputStream("e:\\temp");
	      dout=new DataOutputStream(fout);
	      dout.writeInt(10);
	      dout.writeLong(12345);
	      dout.writeFloat(3.1415926f);
	      dout.writeDouble(987654321.123);
	      dout.writeBoolean(true);
	      dout.writeChars("Goodbye! ");
	      dout.close();

	      FileInputStream fin;
		  DataInputStream din;
	      fin=new FileInputStream("e:\\temp");
	      din=new DataInputStream(fin);
	      System.out.println(din.readInt());
	      System.out.println(din.readLong());
	      System.out.println(din.readFloat());
	      System.out.println(din.readDouble());
	      System.out.println(din.readBoolean());
	      din.close();
	}
}

```

```java
import java.io.*;
/**
 *System.err.println()打出来的是红字 
 */
public class 标准输入输出 {
	public static void main(String[] args) throws IOException{
        //System.err.println("红色，因为是标准错误输出");
		//设置输入缓冲区
		byte[] b = new byte[128];
		System.out.println("输入字符");
		//读取标准输入流，将回车(13)和换行符(10)也一起放到b字节数组
		int count = System.in.read(b);
		//打印b中元素的ASCII值
		for(int i=0;i<count;i++) {
			System.out.print(b[i]+" ");
		}
		System.out.println();
        //字符个数
		System.out.println(count);
		//转为字符型
		for(int i=0;i<count;i++) {
			System.out.print((char)b[i]+" ");
		}
		System.out.println(System.in.getClass().toString());
		
	}
}
```
System是Object类的直接子类，System.in是InputStream类的对象，System.out是PrintStream类的对象

**字符流**

```java
java.lang.Object
    java.io.Reader 
        java.io.InputStreamReader
            java.io.FileReader
java.lang.Object
    java.io.Writer
        java.io.OutputStreamWriter
            java.io.FileWriter
FileReader构造方法：
    FileReader(File file)
    FileReader(FileDescriptor fd)
    FileReader(String fileName)
FileWriter构造方法：
    FileWriter(File file)
    FileWriter(File file, boolean append)
    FileWriter(FileDescriptor fd)
    FileWriter(String fileName)
    FileWriter(String fileName, boolean append)
```

```java
import java.io.*;
/**
 * 字符流创建字符数组，字节流创建字节数组
 */
public class 用FileReader读取文件 {
	public static void main(String[] args) throws IOException {
		char[] c = new char[10];
		FileReader fr = new FileReader("e:/1.txt");
		/**
		1.先调用Reader类的方法：
		public int read(char cbuf[]) throws IOException {
        	return read(cbuf, 0, cbuf.length);
    	}
    	2.上一个方法返回Reader类的抽象方法：
    	abstract public int read(char cbuf[], int off, int len) throws IOException;
    	3.Reader类的子类InputStreamReader重写：
    	public int read(char cbuf[], int offset, int length) throws IOException {
        	return sd.read(cbuf, offset, length);
    	}
    		sd是InputStreamReader类的成员：
    		private final StreamDecoder sd;
    	4.点StreamDecoder无法查看源码，应该又是调用sun.nio.cs.StreamDecoder类的方法
    	public class sun.nio.cs.StreamDecoder extends java.io.Reader	
		 */
		//教材：将数据读入字符数组c，并返回读取的字符数
		int num = fr.read(c);
		//将字符数组转换成字符串
		String str = new String(c,0,num);
        //注：教材上的这个案例只能读取十个字节
		System.out.println(str);
		fr.close();
		
	}
}
```

```java
import java.io.*;
public class 用FileWriter写文件 {
	public static void main(String[] args) throws IOException {
		FileWriter fw=new FileWriter("d:\\java\\test.txt");
	    char[] c={'H', 'e', 'l', 'l', 'o', '\r', '\n'};
	    String str="欢迎使用Java！";
	    /**
	     * 继承OutputStreamWriter类
	     *  write(char[] cbuf, int off, int len)
	     *  write(int c)
	     *  write(String str, int off, int len)
	     * OutputStreamWriter类的父类Writer
	     * 	write(int c)
	     * 	write(char cbuf[])
	     * 	abstract public void write(char cbuf[], int off, int len)
	     * 	write(String str)
	     * 	write(String str, int off, int len)
	     */
	    fw.write(c);
	    fw.write(str); 
	    fw.close();
	}
}
```

```java
import java.io.*;
public class 用BufferedReader读文件 {
	public static void main(String[] args) throws IOException{
	      String thisLine;
	      int count=0;
	      FileReader fr=new FileReader("e:/1.txt");
	      BufferedReader bfr=new BufferedReader(fr);
	      //每次读取一行，直到文件结束
	      //读一行文字。 一行被视为由换行符（'\ n'），回车符（'\ r'）中的任何一个或随后的换行符终止。
	      while ((thisLine=bfr.readLine())!=null){
	        count++;
	        System.out.println(thisLine);
	      }
	      System.out.println("共读取了"+count+"行");
	      bfr.close();
	}
}
```

```java
import java.io.*;
public class 用BufferedWriter写文件 {
	public static void main(String[] args) throws IOException {
		BufferedReader bfr = new BufferedReader(new FileReader("e:/1.txt"));
		BufferedWriter bfw = new BufferedWriter(new FileWriter("e:/11.txt"));
		String str;
		while((str=bfr.readLine())!=null) {
			//输出读取到的内容
			System.out.println(str);
			//将读取的数据写入到输出流
			bfw.write(str);
			//写入回车换行符
			bfw.newLine();
		}
		//将缓冲区的数据全部写入到文件中
		bfw.flush();
		bfr.close();
		bfw.close();
	}
}
```

```java
File类的构造方法：
    File(File parent, String child)
    File(String pathname)
    File(String parent, String child)
    File(URI uri)
```
```java
import java.io.*;
/**
* 教材的这个案例不是很好
*/
public class 用File类输出文件夹下内容 {
	public static void main(String[] args) {
		String str=new String();
	    try{
	      InputStreamReader isr=new InputStreamReader(System.in);
	      BufferedReader inp=new BufferedReader(isr);
	      String sdir="d:\\temp";
	      String sfile;
	      //把sdir作为参数
	      File fdir1=new File(sdir);
	      if (fdir1.exists() && fdir1.isDirectory()){
	        	System.out.println("文件夹："+sdir+"已经存在");
	        	//遍历其下文件夹和文件
              	for (int i=0;i<fdir1.list().length;i++)
                  System.out.println((fdir1.list())[i]);
                File fdir2=new File("d:\\temp\\temp");
                  //如果不存在就创一个文件夹
                if (!fdir2.exists())
                  fdir2.mkdir();
              	System.out.println();
              	System.out.println("建立新文件夹后的文件列表");
              	for (int i=0;i<fdir1.list().length;i++)
                  System.out.println((fdir1.list())[i]);
	      }
	      System.out.print("请输入该文件夹中的一个文件名：");
	      sfile=inp.readLine();
	      File ffile=new File(fdir1,sfile);
	      if (ffile.isFile()){
	        System.out.print("文件名："+ffile.getName());
	        System.out.print("；所在文件夹："+ffile.getPath());
	        System.out.println("；文件大小："+ffile.length()+"字节");
	      }
	    }
	    catch (IOException e){
	      System.out.println(e.toString());
	    }
	}
}
```

```java
import java.io.*;
/**
* 比较不错的案例
*/
public class RandomAccessFile类对文件进行随机访问 {
	public static void main(String[] args) throws IOException{
		StringBuffer stfDir=new StringBuffer();
	    System.out.println("请输入文件所在的路径");
	    char ch;
	    //通过标准键盘输入读取字符，存入到StringBuffer
	    while ((ch=(char)System.in.read())!='\r')
	      stfDir.append(ch);
	    //把StringBuffer转为字符串
	    File dir=new File(stfDir.toString());
	    System.out.println("请输入欲读取的文件名");
	    StringBuffer stfFileName=new StringBuffer();
	    char c;
	    while ((c=(char)System.in.read())!='\r')
	      stfFileName.append(c);
	    //去掉上次输入并回车后存留在缓冲区中的'\n'
	    stfFileName.replace(0,1,"");
	    //通过输入的文件路径和文件名创建File对象
	    File readFrom=new File(dir,stfFileName.toString());
	    if (readFrom.isFile() && readFrom.canWrite() && readFrom.canRead()){
	      RandomAccessFile rafFile=new RandomAccessFile(readFrom,"rw");
	      //getFilePointer()，返回文件指针的当前位置
	      //若文件指针的位置没有超过文件的长度，则输出文件中的每一行直到结束
	      while (rafFile.getFilePointer()<rafFile.length())
	        System.out.println(rafFile.readLine());
	      rafFile.close();
	    }
	    else
	      System.out.println("文件不可读！");
	}
}
```

### 以下为尚学堂

```java
import java.io.*;
public class 字节流写出并复制文件 {
	public static void main(String[] args) throws IOException{
		//第二参数为空或false则是覆盖
		OutputStream os = new FileOutputStream("a:/JavaTest/1.txt",true);
		String str = "\r\nI will success! \r\n";	
		//需要将要写入的内容转为字节数组
		byte[] x = str.getBytes();
		os.write(x);
		//flush用于避免输出流没被写出
		os.flush();
		os.close();
		
		InputStream is = new FileInputStream("a:/JavaTest/1.txt");
		//定义缓冲数组
		byte[] car = new byte[128];
		//接收实际读取大小
		int len = 0;
		//循环读取
		/**
		 * read(byte[] b),从该输入流读取最多b.length字节的数据到字节数组。 此方法将阻塞，直到某些输入可用。
		 * @return     the total number of bytes read into the buffer, or
		 *             -1 if there is no more data because the end of
		 *             the stream has been reached.
		 * 理解：从is中一次读取b.lenth字节到字节数组，用while循环读取直到返回值为-1
		 */
		while((len=is.read(car))>0) {
			/**
			 * 一次读取b.lenth个字节的数据，len为实际读取大小
			 * 当读取到最后一次填不满数组时，len返回小于b.length的值
			 */
			String s = new String(car,0,len);
			System.out.println(s);
		}
		is.close();
		
	}
}
```

```java
import java.io.*;
public class 字符流写入并读取文件 {
	public static void main(String[] args) {
		File src = new File("e:/1.txt");
		try {
			Reader r = new FileReader(src);
			Writer w = new FileWriter(src,true);
			String s = "i will be successful";
			char[] c = new char[128];
			int len = 0;
			String str;
			w.write(s);
			w.flush();
			while((len=r.read(c))>0) {
				//System.out.println(c);
				//字符数组转字符串
				str = new String(c,0,len);
				System.out.println(str);
			}
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
		
	}
}
```

```java
import java.io.*;
public class 字节流拷贝文件 {
	public static void main(String[] args) throws IOException{
	    //注意两个路径需要指定到文件名
		InputStream is = new FileInputStream("a:/JavaTest/1.txt");
		OutputStream os = new FileOutputStream("a:/JavaTest/11.txt");
		byte[] b = new byte[128];	
		int len;
		while((len=is.read(b))>0) {
			os.write(b, 0, len);
		}
		os.flush();
		//先打开的后关闭
		os.close();
		is.close();
		
	}
}
```

```java
import java.io.*;
public class 拷贝文件夹 {
	public static void main(String[] args) {
		//源目录
		String srcPath = "a:/JavaTest";
		//目标目录
		String destPath = "g:/JavaTest";
		copyDir(srcPath,destPath);
	}
	
	public static void copyDir(String srcPath,String destPath) {
		File src = new File(srcPath);
		File dest = new File(destPath);
		copyDir(src,dest);
	}
	
	public static void copyDir(File src,File dest) {
		//如果源目录路径确实为目录
		if(src.isDirectory()) {
			//File(String parent, String child)
			//以目标目录为父路径，源目录名字为子路径创建File实例
			//此时dest为目标目录下的文件夹
			dest = new File(dest, src.getName());
		}
		copyDirDetail(src,dest);
	}
	
	public static void copyDirDetail(File src,File dest) {
		//如果src为文件
		if(src.isFile()) {
			//调用前面写了封装的copyFile方法
			try {
			    //直接把src复制到dest
				copyFile(src, dest);
			} catch (IOException e) {
				e.printStackTrace();
			}
			//如果src是文件夹
		}else if(src.isDirectory()) {
			//创建目录，确保目标文件夹存在
			dest.mkdirs();
			//获取下一级目录
			for(File sub:src.listFiles()) {
				/**
				 * 遍历src文件夹，递归
				 * eg：src下有一个test目录，把它作为源目录，
				 * 第二个参数以dest作为父路径，test的名字作为子路径
				 * 创建File对象进行递归，然后mkdirs创建目录，接着遍历
				 * test目录，若其下为文件则copyFile。
				 * 当递归完src第一个目录后，回到第一层对src的遍历并对src的下一个
				 * 目录递归
				 */
				copyDirDetail(sub,new File(dest,sub.getName()));
			}
		}
	}
	
	public static void copyFile(File src,File dest) throws FileNotFoundException,IOException{
		if(!src.isFile()) {
			throw new IOException("不是文件");
		}
		InputStream is = new FileInputStream(src);
		OutputStream os = new FileOutputStream(dest);
		byte[] b = new byte[128];	
		int len;
		while((len=is.read(b))>0) {
			os.write(b, 0, len);
		}
		os.flush();
		os.close();
		is.close();
	}

}
```



#### 处理流

从二进制（看不懂）到字符集（看得懂）的过程为编码，从字符集（看得懂）到二进制（看不懂）的过程为解码

![处理流的作用](h:\Fighting\1\缓冲流.png)

![](h:\Fighting\1\解码编码.png)

```java
import java.io.*;
public class 缓冲流 {
	public static void main(String[] args) {
		File src = new File("e:/1.txt");
		try {
			BufferedReader r = new BufferedReader(new FileReader(src));
			BufferedWriter w = new BufferedWriter(new FileWriter(src,true));
			String str = null;
			//换行符
			w.newLine();
			//缓冲流的readline方法一行一行读取，直到为空
			while((str=r.readLine())!=null) {
				w.write(str);
			}
			//更快捷的添加方式
			w.append("aaa");
			w.flush();
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
}
```

```java
import java.io.*;
public class 编码解码 {
	public static void main(String[] args) throws UnsupportedEncodingException {
		String str = "笑着说自己打字速度很快，后面就落泪了";		//默认为GBK
		byte[] b = str.getBytes();
		//因为编码与解码字符集同一，所以没有乱码
		System.out.println(new String(b));
		
		//设定指定编码字符集
		b = str.getBytes("utf-8");
		//编码解码字符集不一致，导致乱码
		System.out.println(new String(b));
		
		//编码解码均指定为unicode
		byte[] b2 = "我喜欢吃肉".getBytes("unicode");
		String str2 = new String(b2,"unicode");
		System.out.println(str2);
	}
}
```

```java
import java.io.*;
/**
 * 处理乱码问题
 */
public class 字节流转字符流 {
	public static void main(String[] args) {
		try {
			BufferedReader br = new BufferedReader(
					//BufferedReader为字符流，通过InputStreamReader转为字节流
					//并且指定字符集(需要与文件编码一致)
					new InputStreamReader(
							new FileInputStream(new File("e:/1.txt")),"utf-8"
							));
			String str = null;
			while((str=br.readLine())!=null)
				System.out.println(str);
			br.close();
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (UnsupportedEncodingException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
}
```

```java
/**
 * 文件--文件输入流 ->程序--字节数组输出流 ->字节数组		
 * 字节数组--字节数组输入流 ->程序--文件输出流 ->文件
 */
import java.io.*;
public class 字节数组流 {
	public static void main(String[] args) throws IOException {
		//String str =new String(toByte("A:\\JavaTest\\1.txt"));
		//System.out.println(str);
		//toFile(b,"a:/JavaTest/2.txt");

		toFile(toByte("A:\\JavaTest\\1.png"),"A:\\JavaTest\\2.png");
	}
	/**
	*  将源文件转为字节数组
	*/
	public static byte[] toByte(String srcPath) throws IOException {
		InputStream is = new BufferedInputStream(new FileInputStream(new File(srcPath)));
		ByteArrayOutputStream bos= new ByteArrayOutputStream();
		byte[] flush = new byte[128];
		int len = 0;
		while((len=is.read(flush))>0) {
			bos.write(flush, 0, len);
		}
		bos.flush();
		byte[] dest = bos.toByteArray();
		bos.close();
		is.close();
		return dest;
	}
	/**
	* 以字节数组的形式将数据传到目标路径
	*/
	public static void toFile(byte[] src,String destPath) throws IOException {
		OutputStream os = new BufferedOutputStream(new FileOutputStream(new File(destPath)));
		ByteArrayInputStream bis = new ByteArrayInputStream(src);
		byte[] flush = new byte[128];
		int len = 0;
		while((len=bis.read(flush))>0) {
			os.write(flush,0,len);
		}
		os.flush();
		
		bis.close();
		os.close();
	}
}
```

```java
import java.io.*;
/**
 * 用于处理数据类型（基本数据类型+String）
 * 输入流：DataInputStream
 * 输出流：DataOutpurtStream
 */
public class 数据类型处理流 {
	public static void main(String[] args) throws IOException {
		写入("a:/JavaTest/0.txt");
		//如果文件不一致，会出现EOFException，（end of file）
		//即文件已到达末尾，没有读取到相关的内容
		读取("a:/JavaTest/0.txt");
	}
	
	public static void 写入(String destPath) throws IOException {
		double point = 2.5;
		long num = 100L;
		String str = "大吉大利";
		
		DataOutputStream dos = new DataOutputStream(
				new BufferedOutputStream(
                    new FileOutputStream(
						new File(destPath))));
		//方法名指定出类型,注意顺序
		//读取顺序与写入顺序要一致
		dos.writeDouble(point);
		dos.writeLong(num);
		dos.writeUTF(str);
		
		dos.flush();
		dos.close();
	}
	
	public static void 读取(String srcPath) throws IOException {
		DataInputStream dis = new DataInputStream(
				new BufferedInputStream(
						new FileInputStream(
                            new File(srcPath))));
		//读取顺序与写入顺序要一致
		//顺序不一致数据会出现问题
		Double n1 = dis.readDouble();
		Long n2 = dis.readLong();
		String s = dis.readUTF();
        dis.close();
		System.out.println(n1+" "+n2+" "+s);
	}
}
```


```java
import java.io.*;
/**
 * 把字节数组流包装入数据类型处理流
 */
public class 数据类型处理流加字节数组流 {
	public static void main(String[] args) throws IOException {
		byte[] b = 写入();
		System.out.println(b.length);
		读取(b);
	}
	
	public static byte[] 写入() throws IOException {
		double point = 2.5;
		long num = 100L;
		String str = "大吉大利";
		
		byte[] dest = null;
		ByteArrayOutputStream bos = new ByteArrayOutputStream();
		DataOutputStream dos = new DataOutputStream(
				new BufferedOutputStream(
						bos));
		dos.writeDouble(point);
		dos.writeLong(num);
		dos.writeUTF(str);
		
		dos.flush();
		//在关闭之前获取数据
		dest = bos.toByteArray();
		dos.close();
		
		return dest;
	}
	
	public static void 读取(byte[] src) throws IOException {
		DataInputStream dis = new DataInputStream(
				new BufferedInputStream(
						new ByteArrayInputStream(src)));
		Double n1 = dis.readDouble();
		Long n2 = dis.readLong();
		String s = dis.readUTF();
		dis.close();
		System.out.println(n1+" "+n2+" "+s);
	}
}
```

处理引用类型
```java
/**
 * 输入流为反序列化：ObjectInputStream
 * 输出流为序列化:ObjectOutpurStream
 * 先序列化后反序列化，反序列化顺序必须与序列化一致
 * 不是所有对象都可以序列化，必须要实现java.io.Serializable接口
 * 不是所有属性都需要序列化，通过transient来避免
 * Serializable是一个空接口，用于标识序列化
 */
public class Employee implements java.io.Serializable{
	//表示这个属性不需要序列化
	private transient String name;
	private double salary;
	public Employee(String name, double salary) {
		super();
		this.name = name;
		this.salary = salary;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public double getSalary() {
		return salary;
	}
	public void setSalary(double salary) {
		this.salary = salary;
	}
	public Employee() {
	}
}


import java.io.*;
public class Test {
	//序列化
	public static void seri(String destPath) throws IOException {
		Employee emp = new Employee("有钱人",20000);
		ObjectOutputStream dos = new ObjectOutputStream(
				new BufferedOutputStream(
						new FileOutputStream(
								new File(destPath))));
		dos.writeObject(emp);
		dos.flush();
		dos.close();
	}
	
	//反序列化
	public static void read(String destPath) throws IOException, ClassNotFoundException {
		ObjectInputStream ois = new ObjectInputStream(
				new BufferedInputStream(
						new FileInputStream(
								new File(destPath))));
		Object obj = ois.readObject();
		if(obj instanceof Employee) {
			Employee emp = (Employee)obj;
			System.out.println(emp.getName());
			System.out.println(emp.getSalary());
		}
		ois.close();
	}
	
	public static void main(String[] args) throws IOException, ClassNotFoundException {
		//结果为null和20000，name加上了transient关键字避免序列化
		read("a:/JavaTest/2.txt");
	}
}
```



```java
import java.io.*;
import java.util.Scanner;
public class 用Scanner读取文件 {
	public static void main(String[] args) throws IOException {
		//System类的属性in为InputStream类型
		InputStream is = System.in;
		//创建文件输入流，指定文件路径
		is = new BufferedInputStream(new FileInputStream(new File("a:/JavaTest/1.txt")));
		//将文件路径作为参数。注意Scanner为util类
		Scanner sc = new Scanner(is);
		//实现用Scanner类读取文件内容
		while(sc.hasNext())
			System.out.println(sc.nextLine());
	}
}
```
```java
/**
 * 使用System类的重定向方法写入
 */
import java.io.*;
public class 重定向 {
	public static void main(String[] args) throws IOException {
		System.setOut(new PrintStream(
				new BufferedOutputStream(
						new FileOutputStream(
								//前面的true为追加内容
								//后面的true为PrintStream打印流的第二个参数，是否自动flush
								new File("a:/JavaTest/1.txt"),true)),true));
		System.out.println("YES");
		System.out.println("成功");
		
		//回到控制台
		System.setOut(new PrintStream(new BufferedOutputStream(
						new FileOutputStream(
								FileDescriptor.out)),true));
		System.out.println("aaa");
	}
}
```



```java
import java.io.*;
public class System的in属性与缓冲流应用 {
	public static void main(String[] args) throws IOException {
		InputStream is =System.in;
		BufferedReader bf = new BufferedReader(
				//需要先将字节流转为字符流，然后添加参数
				new InputStreamReader(is));
		System.out.println("请输入");
		System.out.println(bf.readLine());
		
	}
}
```

装饰设计模式
```java
public class Voice {
	//音量为10
	private int voice = 10;
	public Voice() {
	}
	public int getVoice() {
		return voice;
	}
	public void setVoice(int voice) {
		this.voice = voice;
	}
	
	public void say() {
		System.out.println(voice);
	}
}

/**
 * 扩音器，对声音进行放大
 */
public class Amplifier {
	private Voice voice;
	public Amplifier() {
	}
	public Amplifier(Voice voice) {
		super();
		this.voice = voice;
	}
	public void say() {
		System.out.println(voice.getVoice()*1000);
	}
}

/**
 * 应用
 */
public class App {
	public static void main(String[] args) {
		Voice v = new Voice();
		v.say();
		//放大
		Amplifier am = new Amplifier(v);
		am.say();
	}
}
```

RandomAccessFile使用

```java
import java.io.*;
public class 使用seek方法 {
	public static void main(String[] args) throws IOException {
		//第二个参数有r w rw 三种选择
		RandomAccessFile rnd = new RandomAccessFile(new File("a:/JavaTest/1.txt"),"rw");
		//seek(),Sets the file-pointer offset,
		//从哪里开始读取
		rnd.seek(10);
		byte[] flush = new byte[128];
		int len = 0;
		while((len=rnd.read(flush))>0) {
			System.out.println(new String(flush,0,len));
		}
		rnd.close();
	}
}
```

```java
/**
 * 思路：确定分割块数n、各块的大小blockSize
 * 最后一块的大小为 总文件大小减去（n-1）*blockSize
 */
import java.io.*;
import java.util.*;
public class 文件分割 {
	//文件名字、路径、大小、分割块数、每块的大小
	private String fileName;
	private String filePath;
	private long length;
	private int size;
	private long blockSize;
	//每块的名称
	private List<String> blockPath;
	//分割后存放的目录
	private String destPath;
	//注意理解这三个构造器间的调用关系
	public 文件分割() {
		blockPath = new ArrayList<String>();
	}
	public 文件分割(String filePath,long blockSize,String destPath) {
		this();
		this.filePath = filePath;
		this.blockSize = blockSize;
		this.destPath = destPath;
		//初始化在构造时完成
		init();
	}
	public 文件分割(String filePath,String destPath) {
		this(filePath,1024,destPath);
	}
	
	/**
	 * 初始化操作。确定文件名、计算块数、确定每块名称
	 */
	public void init() {
		File src = null;
		//如果filePath为空，或者filePath不存在,或者src是文件夹
		if(filePath==null||!((src=new File(filePath)).exists())||src.isDirectory()) {
			return;
		}
		fileName = src.getName();
		/**
		 * 计算块数
		 */
		//文件实际大小
		length = src.length();
		//如果块的大小大于文件实际大小
		if(blockSize>length) {
			blockSize = length;
		}
		
		//确定块数
		//ceil()：返回大于或等于参数的最小（最接近负无穷大） double值，并等于数学整数。 
		//即取最大的整数，返回double型，要乘1.0避免类型错误
		//最后强转为int
		size = (int)(Math.ceil(length*1.0/blockSize));
		initPathName();
	}
	
	/**
	 * 确定每块名称
	 */
	public void initPathName() {
		for(int i=0;i<size;i++) {
			blockPath.add(destPath+File.separator+fileName+".part"+i);
		}
	}
	
	public void split() throws IOException {
		long beginPos = 0;
		long actualBlockSize = blockSize;
		for(int i=0;i<size;i++) {
			//最后一块
			if(i==size-1) {
				actualBlockSize = length-beginPos;
			}
			splitDetail(i,beginPos,actualBlockSize);
			beginPos += actualBlockSize; 
		}
	}
	
	/**
	 * 与文件拷贝的思路一致
	 * @param idx:第几块
	 * @param beginPos：每一块开始时的文件大小
	 * @param actualBlockSize：剩余的实际大小
	 */
	public void splitDetail(int idx,long beginPos,long actualBlockSize) throws IOException {
		RandomAccessFile raf = null;
		BufferedOutputStream bos = null;
		try {
			//要分割的文件
			raf = new RandomAccessFile(new File(filePath),"r");
			bos = new BufferedOutputStream(
					new FileOutputStream(
							new File(blockPath.get(idx))));
			//读取文件
			raf.seek(beginPos);
			byte[] flush = new byte[(int)length];
			int len = 0;
			while((len=raf.read(flush))>0) {
				if(actualBlockSize-len>=0) {
					bos.write(flush,0,len);
					actualBlockSize-=len;
				}else {
					bos.write(flush,0,(int)(actualBlockSize));
					break;
				}
			}
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		} finally {
			bos.flush();
			bos.close();
			raf.close();
		}
	}
	
	public void 合并思路1(String destPath) {
		BufferedInputStream bis = null;
		BufferedOutputStream bos = null;
		for(int i=0;i<blockPath.size();i++) {
			try {
				bis = new BufferedInputStream(
                    new FileInputStream(
                    	new File(blockPath.get(i))));
				bos = new BufferedOutputStream(
						new FileOutputStream(
								new File(destPath),true));
				byte[] flush = new byte[(int)length];
				int len = 0;
				while((len=bis.read(flush))>0) {
					bos.write(flush, 0, len);
				}
				bos.flush();
				bos.close();
				bis.close();
			} catch (FileNotFoundException e) {
				e.printStackTrace();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
	}
	
	/**
	 * 通过枚举使用sequenceInputStream
	 */
	public void 合并思路2(String destPath) throws IOException {
		BufferedOutputStream bos = null;
		Vector<InputStream> vi= new Vector<InputStream>();
		for(int i=0;i<blockPath.size();i++)
			vi.add(new BufferedInputStream(
                new FileInputStream(
                    new File(blockPath.get(i)))));
		SequenceInputStream sis = new SequenceInputStream(vi.elements());
		bos = new BufferedOutputStream(
				new FileOutputStream(
						new File(destPath),true));
		byte[] flush = new byte[(int)length];
		int len = 0;
		while((len=sis.read(flush))>0) {
			bos.write(flush, 0, len);
		}
		bos.flush();
		bos.close();
		sis.close();
		
	}
	
	public static void main(String[] args) throws IOException {
		文件分割 w = new 文件分割("a:/JavaTest/1.txt",21,"g:/JavaTest");
		//结果为文件的字节数除以构造器的第二个参数的向上取整
		//System.out.println(w.size);
		w.split();
		w.合并思路2("g:/1.txt");
	}
    
}
```

![](H:\Fighting\1\IO总结.jpg)

## 多线程

    含义：在同一个进程中同时存在几个执行体，按几条不同的执行路径同时工作
    目的：将一个程序中的各个“程序段”并发化
临界资源：在一个时刻只能被一个线程访问的资源
临界区：访问临界资源的那段代码

```java
/**
 * 三个售票窗口共享run()方法，各自卖出10张票
 */
public class 模拟航班售票1 {
	public static void main(String[] args) {
		ThreadSale t1 = new ThreadSale();
		ThreadSale t2 = new ThreadSale();
		ThreadSale t3 = new ThreadSale();
		t1.start();
		t2.start();
		t3.start();
		
	}
}

class ThreadSale extends Thread{
	//机票数，为共享数据
	private int tickets = 10;
	public void run() {
		while(true) {
			//若有票
			if(tickets>0) {
				//返回正在运行线程的名字，机票数自减
				System.out.println(getName()+" 售机票第"+tickets--+"号");
			}else {
				//exit();
				//Terminates the currently running Java Virtual Machine.
				System.exit(0);
			}
		}
	}
}
```
```java
/**
 * Thread类实现了Runnable接口，是代理角色
 * 通过继承Thread实现静态代理
 */
public class 静态代理 {
	public static void main(String[] args) {
		Me me = new Me();
		me.marry();
		System.out.println();
		婚庆公司 h = new 婚庆公司(me);
		h.marry();
	}
}

interface Marry{
	void marry();
}
//真实角色
class Me implements Marry{

	public void marry() {
		System.out.println("我结婚");
	}
}
//代理人
class 婚庆公司 implements Marry{
	private Marry you;
		
	public 婚庆公司(Marry you) {
		super();
		this.you = you;
	}
	
	public 婚庆公司() {
		// TODO Auto-generated constructor stub
	}
	private void 准备() {
		System.out.println("准备工作");
	}
	private void 后手(){
		System.out.println("打杂");
	}
	public void marry() {
		准备();
		you.marry();
		后手();
	}
}
```
> Java通过互斥锁来实现不同线程的互斥操作
- 关键字：synchronized




```java
/**
 * 三个售票窗口共享机票数
 * 出现问题：有时售了不止十张票(号数重复)
 * 原因：线程共同拥有对内存空间中数据的处理权力，会导致因为多个线程
 * 同时处理数据而使数据出现不一致
 * 解决方法：同步控制。被多个线程共享的数据在同一时刻只允许一个线程处于操作之中
 * 具体实现：见模拟航班售票3
 */
public class 模拟航班售票2 {
	public static void main(String[] args) {
		//创建一个实现了Runnable接口的对象t
        //真实角色
		ThreadSale1 t = new ThreadSale1();
        //代理人
		//用此对象t作为对象创建三个线程
		//Thread(Runnable target, String name)
		Thread t1 = new Thread(t,"第1售票窗口");
		Thread t2 = new Thread(t,"第2售票窗口");
		Thread t3 = new Thread(t,"第3售票窗口");
		t1.start();
		t2.start();
		t3.start();
		
	}
}

class ThreadSale1 implements Runnable{
	//机票数，为共享数据
	private int tickets = 10;
	public void run() {
		while(true) {
			//若有票
			if(tickets>0) {
				//返回当前运行的线程
				System.out.println(Thread.currentThread().getName()
						+" 售机票第"+tickets--+"号");
				
			}else {
				//exit();
				//Terminates the currently running Java Virtual Machine.
				System.exit(0);
			}
		}
	}
}
```


```java
public class 教材上的模拟用户银行取款 {
	public static void main(String[] args){
	    Customer c1=new Customer();
	    Customer c2=new Customer();
	    c1.start();
	    c2.start();
	  }
}
class Mbank{
  private static int sum=2000;
  public synchronized static void take(int k){
    int temp=sum;
    temp-=k;
    try{Thread.sleep((int)(1000*Math.random()));}
    catch(InterruptedException e){ }
    sum=temp;
    System.out.println("sum="+sum);
  }
}
class Customer extends Thread{
  public void run(){
    for(int i=1;i<=4;i++)
      Mbank.take(100);
  }
}
```

```java
public class 模拟航班售票3 {
	public static void main(String[] args) {
		ThreadSale2 t = new ThreadSale2();
		Thread t1 = new Thread(t,"第1售票窗口");
		Thread t2 = new Thread(t,"第2售票窗口");
		Thread t3 = new Thread(t,"第3售票窗口");
		t1.start();
		t2.start();
		t3.start();
	}
}

class ThreadSale2 implements Runnable{
	private int tickets = 100;
	private boolean flag = true;
	
	public synchronized void sale1() {
			if(tickets<=0) {
				flag = false;
				return;
			}
			try {
				Thread.sleep(200);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
			System.out.println(Thread.currentThread().getName()
					+"售出票，剩余："+(tickets--)+"张票");
	}
	
	public void sale2() {
		synchronized(this) {
			if(tickets<=0) {
				flag = false;
				return;
			}
			try {
				Thread.sleep(200);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
			System.out.println(Thread.currentThread().getName()
					+"售出票，剩余："+(tickets--)+"张票");
		}
	}
	
	public void run() {
		while(flag)
			sale2();
	}
}
```
    Objcet类
        wait():线程暂停执行并进入等待队列，释放互斥锁。等到其他线程调用notify()或notifyAll()方法后再继续获得互斥锁并执行
        notify():唤醒正在等待该对象互斥锁的第一个线程
        
    wait()与sleep()区别：wait()在放弃CPU资源的同时交出了资源的控制权，sleep()则无法做到

```java
public class 存售票 {
	public static void main(String[] args) {
		Tickets t = new Tickets(10);
		new Producer(t).start();
		new Consumer(t).start();
	}
}

class Tickets {
	//总票数、票号、是否有票可售（有票可售为true）
	protected int size;
	int number = 0;
	boolean available = false;
	
	public Tickets(int size) {
		this.size = size;
	}
	
	//存票
	public synchronized void put() {
		//如果有存票，则存票线程等待
		if(available) {
			try {
				wait();
			} catch (InterruptedException e) {}
		}
		System.out.println("存入第【"+(++number)+"】号票");
		available = true;
		//存票后唤醒售票线程开始售票
		notify();
	}
	
	//售票
	public synchronized void sell() {
		if(!available) {
			try {
				wait();
			} catch (InterruptedException e) {}
		}
		System.out.println("售出第【"+number+"】号票");
		available = false;
		//售票后唤醒存票线程开始存票
		notify();
		
		//设置结束标志：number等于1且大于size
		if(number==size)
			number=size+1;
	}
}

//存票线程
class Producer extends Thread{
	Tickets t = null;

	public Producer(Tickets t) {
		super();
		this.t = t;
	}
	public void run() {
		while(t.number<t.size)
			t.put();
	}
}

//售票线程
class Consumer extends Thread{
	Tickets t = null;

	public Consumer(Tickets t) {
		super();
		this.t = t;
	}
	public void run() {
		while(t.number<=t.size)
			t.sell();
	}
}
```

```java
/**
 * 习题：   
 * 设有一家银行可接受顾客存款，每进行一次存款，便可计算出存款的总额。
 * 现有两名顾客，每人分三次、每次存入100元。
 * 编程模拟顾客的存款操作
 */
public class Test {
	public static void main(String[] args) {
		User t1 = new User();
		User t2 = new User();
		t1.start();
		t2.start();
	}
}
class Bank {
	private static int account = 0;
	public synchronized static void store(int money) {
		int temp = account;
		temp += money;
		try {
			Thread.sleep(100);
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
		account = temp;
		System.out.println(Thread.currentThread().getName()
				+"存款成功，当前账户余额为："+account+"元");
	}
}
class User extends Thread{
	public void run() {
		for(int i=0;i<3;i++) {
			Bank.store(100);
		}
	}
}
```

### 单例设计模式

```java
/**
 * 外部使用时确保一个类只有一个对象
 * 如jvm、gc、Runtime
 */
public class Demo1 {
	public static void main(String[] args) {
		Jvm j1 = Jvm.getInstance();
		Jvm j2 = Jvm.getInstance();
		//地址相同。注：多线程时不一定，见Demo2
		System.out.println(j1);
		System.out.println(j2);
		
	}
}
/**
 * 懒汉式,懒在声明私有的静态变量时不创建对象
 */
class Jvm{
	//1.构造器私有化,避免外部直接创建对象
	private Jvm() {}
	//2.声明一个私有的静态变量
	private static Jvm instance = null;
	//3.创建一个对外的公共的静态方法访问该变量
	//如果变量没有对象，创建该对象
	public static Jvm getInstance() {
		if(null==instance)
			instance = new Jvm();
		return instance;
	}
}
```

```java
public class Demo2 {
	public static void main(String[] args) {
		JvmThread j1 = new JvmThread(100);
		JvmThread j2 = new JvmThread(500);
		//创建了两个对象
		j1.start();
		j2.start();
		//解决途径：在getInstance()方法体加上synchronized关键字
		//或者锁定类的信息
	}
}

class JvmThread extends Thread{
	private long time;
	
	public JvmThread(long time) {
		super();
		this.time = time;
	}

	@Override
	public void run() {
		System.out.println(Thread.currentThread().getName()
				+"创建对象"+Jvm2.getInstance3(time));
	}
}

class Jvm2{
	private Jvm2() {}
	private static Jvm2 instance = null;
	public static Jvm2 getInstance1(long time) {
		if(null==instance) {
			try {
				Thread.sleep(time);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		instance = new Jvm2();
		}
		return instance; 
	}
	
	public static synchronized Jvm2 getInstance2(long time) {
		if(null==instance) {
			try {
				Thread.sleep(time);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		instance = new Jvm2();
		}
		return instance; 
	}
	
	public static Jvm2 getInstance3(long time) {
		//不能使用this，因为对象为静态的，只能锁这个类的字节码信息
		//因为锁的是这个类的字节码信息，即使存在对象也需要等待，所以效率较低
		synchronized(Jvm2.class) {
			if(null==instance) {
				try {
					Thread.sleep(time);
				} catch (InterruptedException e) {
					e.printStackTrace();
				}
			instance = new Jvm2();
			}
			return instance;
		}
	}
	/**
	 * 经典的双重检查（double checking）
	 */
	public static Jvm2 getInstance4(long time) {
		//线程进入时均先进行判断，避免了等待
		if(null==instance) {
			synchronized(Jvm2.class) {
				if(null==instance) {
					try {
						Thread.sleep(time);
					} catch (InterruptedException e) {
						e.printStackTrace();
					}
				instance = new Jvm2();
				}
			}
		}
		return instance;
	}
}
```

```java
/**
 * 1.构造器私有化,避免外部直接创建对象
2.声明一个私有的静态变量
3.创建一个对外的公共的静态方法访问该变量
如果变量没有对象，创建该对象
 */
public class Demo3 {
	private static Demo3 instance;
	private Demo3() {}
	/**
	 * 懒汉式的经典：双重检查，double checking
	 */
	public static Demo3 getInstance() {
		if(null==instance) {
			synchronized(Demo3.class) {
				if(null==instance)
					instance = new Demo3();
			}
		}
		return instance;
	}
}
```

```java
/**
 * 饿汉式
 * 1.构造器私有化,避免外部直接创建对象
 * 2.声明一个私有的静态变量，同时创建该对象
 * 3.创建一个对外的静态方法
 */
public class Demo4 {
	//只要使用这个Demo4类，就会对其初始化，创建了对象
	private static Demo4 instance = new Demo4();
	private Demo4() {}
  	public static Demo4 getInstance() {
		return instance;
	}
}

/**
 * Demo4的效率提高版
 * 在使用Demo5这个类时，如果不调用getInstance方法，也不会创建对象
 * 因此延缓了加载时机
 */
class Demo5 {
	private static class Holder{
		private static Demo5 instance = new Demo5();
	}
	private Demo5() {}
  	public static Demo5 getInstance() {
		return Holder.instance;
	}
}
```

### 死锁

过多的同步容易造成死锁

```java
public class Demo {
	public static void main(String[] args) {
		Object g = new Object();
		Object m = new Object();
		Test t1 = new Test(g,m);
		Test2 t2 = new Test2(g,m);
		Thread t11 = new Thread(t1);
		Thread t22 = new Thread(t2);
		t11.start();
		t22.start();
	}
}
class Test implements Runnable{
	Object goods;
	Object money;
	
	
	public Test(Object goods, Object money) {
		super();
		this.goods = goods;
		this.money = money;
	}

	@Override
	public void run() {
		while(true) {
			test();
		}
	}
	
	public void test() {
		synchronized (goods) {
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
			synchronized (money) {
				
			}
		}
		System.out.println("一手给钱");
	}
}

class Test2  implements Runnable{
	Object goods ;
	Object money ;
	public Test2(Object goods, Object money) {
		super();
		this.goods = goods;
		this.money = money;
	}

	@Override
	public void run() {
		while(true){
			test();
		}
	}
	
	public void test(){
		synchronized(money){
			try {
				Thread.sleep(100);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
			synchronized(goods){
				
			}
			
		}
		System.out.println("一手给货");
	}
}
```

#### 解决方法：生产者消费者模式

注：这不是设计模式

```java
public class App {
	public static void main(String[] args) {
		//共同的资源
		Movie m = new Movie();
		
		//多线程
		Player p = new Player(m);
		Watcher w = new Watcher(m);
		
		new Thread(p).start();		
		new Thread(w).start();
	}
}

public class Movie {
	private String pic ;
	//信号灯
	//flag -->T 生产生产，消费者等待 ，生产完成后通知消费
	//flag -->F 消费者消费 生产者等待, 消费完成后通知生产
	private boolean flag =true;
	/**
	 * 播放
	 * @param pic
	 */
	public synchronized void play(String pic){
		if(!flag){ //生产者等待
			try {
				this.wait();
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
		//开始生产
		try {
			Thread.sleep(500);
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
		System.out.println("生产了:"+pic);
		//生产完毕		
		this.pic =pic;
		//通知消费
		this.notify();
		//生产者停下
		this.flag =false;
	}
	
	public synchronized void watch(){
		if(flag){ //消费者等待
			try {
				this.wait();
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
		//开始消费
		try {
			Thread.sleep(200);
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
		System.out.println("消费了"+pic);
		//消费完毕
		//通知生产
		this.notifyAll();
		//消费停止
		this.flag=true;
	}
}

/**
 * 生产者
 */
public class Player implements Runnable {
	private Movie m ;
	
	public Player(Movie m) {
		super();
		this.m = m;
	}

	@Override
	public void run() {
		for(int i=0;i<20;i++){
			if(0==i%2){
				m.play("左青龙");
			}else{
				m.play("右白虎");
			}
		}
	}

}

public class Watcher implements Runnable {
	private Movie m ;
	
	public Watcher(Movie m) {
		super();
		this.m = m;
	}

	@Override
	public void run() {
		for(int i=0;i<20;i++){
			m.watch();
		}
	}

}
```

任务调度

```java
import java.util.Date;
import java.util.Timer;
import java.util.TimerTask;
/**
 * 可以开始学习框架quartz
 * util包下的Timer和TimerTask
 */
public class TestTimer {
	public static void main(String[] args) {
		Timer timer =new Timer();
		timer.schedule(new TimerTask(){

			@Override
			public void run() {
				System.out.println("so easy....");
			}}, new Date(System.currentTimeMillis()+1000), 200);
	}
}
```

join、yield、sleep不会让出锁

wait会释放锁，需要与notify、notifyAll配合使用

同步块：

synchronized(类.class|this|引用类型变量){}

同步方法加上修饰符synchronized

## 泛型与容器类

### 泛型

泛型所操作的数据类型被指定为一个参数，这个参数称为类型参数（type parameters），泛型实质是将数据的类型参数化

泛型实例化必须是引用类型

```java
public class 泛型类<T> {
	private T obj;

	public T getObj() {
		return obj;
	}

	public void setObj(T obj) {
		this.obj = obj;
	}
	
	public static void main(String[] args) {
		泛型类<String> name = new 泛型类<String>(); 
		泛型类<Integer> age = new 泛型类<Integer>(); 
		name.setObj("L");
		String newName = name.getObj();
		age.setObj(20);
		int newAge = age.getObj();
		System.out.println(newName+"\n"+newAge);
	}
}
```

```java
public class 泛型方法 {
	public static void main(String[] args) {
		Integer[] num = {1,2,3,4,5};
		String[] str = {"红","橙","黄","绿","青","蓝","紫"};
		//可以加上尖括号突出该方法是泛型方法
		泛型方法.<Integer>display(num);
		泛型方法.display(str);
	}
	
	public static <E> void display(E[] list) {
		for(int i=0;i<list.length;i++)
			System.out.print(list[i]+" ");
		System.out.println();
	}
}
```

```java
//定义泛型类，T是类型参数
class GeneralType<T>         {
  T obj;                      //定义泛型类的成员变量
  public void setObj(T obj)      //定义泛型类的方法
  {
    this.obj=obj;
  }
  public T getObj()           //定义泛型类的方法
  {
    return obj;
  }
  //下面的方法接收的参数只能是String或String的子类
  public static void showObj(GeneralType<? extends String> o) 
  {
    System.out.println("给出的值是："+o.getObj());
  }
  
  //也有下限通配，表示?为T或父类
  public static void show(GeneralType<? super String> o) {}
}

public class 问号的使用      {
  public static void main(String[] args){
    GeneralType<String> n=new GeneralType<String>();
    n.setObj("陈  磊");
    GeneralType.showObj(n);        //用类名调用showObj()方法输出
    GeneralType<Double> num=new GeneralType<Double>();
    num.setObj(25.0);
    System.out.println("数值型值："+num.getObj()); //不可调用方法showObj(num)输出
  }
}
```



#### 泛型继承
1. 子类规规矩矩的继承：Son1< T > extends Father< T >
2. 子类增添泛型：Son2<T1，T2> extends Father< T >
3. 子类擦除父类泛型，会出现raw警告：class Son3 extends Father
4. 子类继承指定泛型：class Son4 extends Father< Integer >
5. 父类指定，子类新增，此时使用的是子类泛型：class Son5< T > extends Father< Integer >
6. **错误状况**：class Son7 extends Father< T >   因为父类未指定具体类型就被继承

### 容器类

![](H:\Fighting\1\容器.png)

#### 哈希（Hash）

哈希集合所包含元素的访问根据哈希码来存取集合中的元素，它在元素的存储位置和元素的值k之间建立一个特定的对应关系f，使每个元素与一个唯一的存储位置相对应。因而在查找时，只要根据元素的值k，计算f(k)的值即可，如果此元素在集合中，则必定在存储位置f(k)上。这个对应关系f即为哈希（hash）函数，按这种关系建立的表称为哈希表，也称散列表。

##### HashSet

根据哈希码来确定元素在集合中的存储位置（即内存地址），因此可以根据哈希码来快速找到集合中的元素。HashSet不保证迭代顺序，且允许元素值为null。比较其中元素是否相同时会先比较hashCode()方法的返回值，相同则再使用equals()方法比较其内存地址，因为不同元素的hashCode可能相同。故若重写其中任一一个方法，需要重写另一个。

### 代码

```java
import java.util.*;
class StringStack{
  private LinkedList<String> ld=new LinkedList<String>(); //创建LinkedList对象ld
  public void push(String name)  //入栈操作
  {
    ld.addFirst(name);         //将name添加到列表的头
  }
  public String pop()
  {
    return ld.removeFirst();    //移出堆栈中的第一个元素
  }
  public boolean isEmpty()    //判断堆栈是否为空
  {
    return ld.isEmpty();
  }
}
public class Stack1{
  public static void main(String[] args)
  {
    Scanner sc=new Scanner(System.in);
    StringStack stack=new StringStack();
    System.out.println("请输入数据(quit结束)");
    while(true)
    {
      String input=sc.next();             //从键盘输入数据
      if(input.equals("quit"))
        break;
      stack.push(input);                 //入栈
    }
    System.out.println("先进后出的顺序：");
    while(!stack.isEmpty())
      System.out.print(stack.pop()+"  ");  //出栈
  }
}
```

```java
import java.util.ArrayList;
import java.util.List;
import java.util.ListIterator;
public class 倒序迭代 {
	public static void main(String[] args){
	    List<Integer> al=new ArrayList<Integer>();  //创建数组列表对象al
	    for(int i=1;i<5;i++)
	      al.add(new Integer(i));                 //向数组列表al中添加元素
	    System.out.println("数组列表的原始数据"+al);
	    ListIterator<Integer> listIter=al.listIterator();  //创建数组列表al的迭代器listIter
	    listIter.add(new Integer(0));                //在序号为0的元素前添加一个元素
	    System.out.println("添加数据后数组列表"+al);
	    if(listIter.hasNext())
	    {
	      int i=listIter.nextIndex();    //执行该语句时i的值是1
	      listIter.next();             //返回序号为1的元素
	      listIter.set(new Integer(9));  //修改数组列表al中序号为1的元素
	      System.out.println("修改数据后数组列表"+al);
	    }
	    listIter=al.listIterator(al.size());   //重新创建从al最后位置开始的迭代器listIter
	    System.out.print("反向遍历数组列表：");    //反向遍历数组列表
	    while(listIter.hasPrevious())
	      System.out.print(listIter.previous()+"  ");    //反向遍历数组列表
	  }
}
```

```java
import java.util.HashSet;
import java.util.Iterator;
public class TestHashSet {
	public static void main(String[] args){
	    HashSet<String> hs=new HashSet<String>(); //创建哈希集合对象hs，初始容量为16
	    for(String a:args)
	      if(!hs.add(a))          //向哈希集合hs添加元素，但重复的元素不添加
	        System.out.println("元素"+a+"重复");        //输出重复的元素
	    System.out.println("集合的容量为："+hs.size()+"，各元素为：");
	    Iterator it=hs.iterator();             //创建哈希集合hs的迭代器it
	    while(it.hasNext())                //判断集合中是否还有后续元素
	      System.out.print(it.next()+"  ");   //输出哈希集合中的元素
	  }
}
```

```java
import java.util.HashSet;
import java.util.Set;
import java.util.TreeSet;
public class testTreeSet {
	public static void main(String[] args){
	    Set<String> hs=new HashSet<String>();   //创建哈希集合对象hs
	    hs.add("唐  僧");        //向哈希集合的对象hs添加元素
	    hs.add("孙悟空");
	    hs.add("猪八戒");
	    hs.add("沙和尚");
	    hs.add("白龙马");
	    TreeSet<String> ts=new TreeSet<String>(hs);  //利用hs创建树集合对象ts
	    System.out.println("树集合："+ts);          //输出树集合
	    System.out.println("树集合的第一个元素："+ts.first());  
	    System.out.println("树集合最后一个元素："+ts.last());
	    System.out.println("haedSet(孙悟空)的元素："+ts.headSet("孙悟空"));
	    System.out.println("tailSet(孙悟空)的元素："+ts.tailSet("孙悟空"));
	    System.out.println("ceiling (沙)的元素："+ts.ceiling ("沙"));
	  }
}
```

```java
import java.util.HashMap;
import java.util.Iterator;
import java.util.Map;
import java.util.Set;
import java.util.TreeMap;
public class testTreeMap {
	public static void main(String[] args){
	    Map<String,String> hm=new HashMap<String,String>();   //创建HashMap对象hm
	    hm.put("006","唐  僧");    //将元素添加到映射hm中
	    hm.put("008","孙悟空");
	    hm.put("009","猪八戒");
	    hm.put("007","沙和尚");
	    hm.put("010","白龙马");
	    System.out.println("哈希映射中的内容如下：\n"+hm);   //输出hm中的元素
	    String str=(String)hm.remove("010");   //在hm中删除键值为“010”的元素
	    Set keys=hm.keySet();     //获取哈希映射hm的键对象集合
	    Iterator it=keys.iterator();   //获取键对象集合keys的迭代器
	    System.out.println("HashMap类实现的Map映射，无序：");
	    while(it.hasNext())        //判断是否还有后续元素
	    {
	      String xh=(String)it.next();        //返回键值
	      String name=(String)hm.get(xh);   //返回键值所对应的值
	      System.out.println(xh+"  "+ name);
	    }
	    TreeMap<String,String> tm=new TreeMap<String,String>(); //创建TreeMap对象tm
	    tm.putAll(hm);                  //向树映射对象tm添加元素
	    Iterator iter=tm.keySet().iterator();  //获取迭代器
	    System.out.println("TreeMap类实现的Map映射，键值升序：");
	    while(iter.hasNext()){                //判断是否还有后续元素
	      String xh=(String)iter.next();       //返回键值
	      String name=(String)hm.get(xh);    //返回键值所对应的值
	      System.out.println(xh+"  "+ name);
	    }
	  }
}
```

```java
import java.util.ArrayList;
import java.util.HashSet;
import java.util.LinkedList;
import java.util.List;
import java.util.Set;
public class Test1 {
	public static void main(String[] args) {
		test7();
	}
	static void test5() {
		List<Integer> ls = new LinkedList<Integer>();
		for(int i=1;i<11;i++)
			ls.add(i);
		System.out.println(ls);
		ls.remove(4);
		ls.listIterator();
		System.out.println(ls);
	}
	
	static void test6() {
		List<String> as = new ArrayList<String>();
		as.add("wo");
		as.add("shi");
		as.add("huo");
		as.add("che");
		as.add("wang");
		as.add("ni");
		as.add("da");
		as.add("bu");
		as.add("guo");
		as.add("me");
		int a = (int)(Math.random()*10);
		System.out.println(as.get(a));
	}
	
	static void test7() {
		boolean yn;
	    Set<Integer> a=new HashSet<Integer>();
	    Set<Integer> b=new HashSet<Integer>();
	    for(int i=1;i<=4;i++) 
	      a.add(i);
	    for(int i=1;i<=11;i=i+2)
	      b.add(i);
	    yn=a.retainAll(b);
	    System.out.println("A与B的交集："+a);
	    for(int i=1;i<=4;i++) 
	      a.add(i);
	    yn=a.addAll(b);
	    System.out.println("A与B的并集："+a);
	    for(int i=1;i<=4;i++) 
	      a.add(i);
	    yn=a.removeAll(b);
	    System.out.println("A与B的差集："+a);
	}
}
```

