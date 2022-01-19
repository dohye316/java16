# java16
异常讲解
异常
Exception
public class Exception {
    public static void main(String[] args) {
        int num1 = 10;
        int num2 = 0;
        //1.num1/num2=>10/0
        //2.当执行到num1/num2 因为num2 = 0,程序就会出现（抛出0异常 ArithmicException
        //3.当抛出异常后，程序就退出，崩溃了，下面的diamante就不在执行
        //4.大家想象这样程序不好,健壮性太差，不应该出现了一个不算致命的问题，就导致整个系统崩溃
        //5.java设计者提供了一个叫异常处理机制来解决该问题
        //如果程序员，认为一段代码可能出现异常/问题，可以使用try-catch 异常处理机制来解决
        //从而保证程序的健壮性
        //将该代码块选中，ctrl 加alt + t 悬钟 try catch
        try {
           int res = num1/num2;
        } catch (java.lang.Exception e) {
//            e.printStackTrace();
            System.out.println(e.getMessage());
        }
        System.out.println("程序继续执行");


    }
}
异常介绍
java语言中，将程序执行中发生的不正常情况称为“异常”。（开发过程中的语法错误和逻辑错误不是异常）
执行过程中所发生的异常实践课分为两类
1.Error：java虚拟机无法解决的严重问题。如：JVM系统内部错误、资源耗尽等严重情况。比如StackOverflowError【栈溢出】和OOM（out of memory）,Error是严重错误，程序会崩溃
2.Exception：其他因编程错误困惑偶然的外在因素导致的一般性问题，可以使用针对性的代码进行处理，例如空指针访问，试图读取不存在的文件，网络连接中断等等，Exception分为两大类：运行时异常【程序运行时，发生的异常】和编译时异常【编程时，编译发生的异常】


异常分类两大类，运行时异常和编译时异常

1.运行时异常，编译器不要求强制处置的异常。一般是指编程时的逻辑错误，是程序员应该避免其出现的异常。java.lang .RuntimeException类及它的子类都是运行时异常
2.对于运行时异常，可以不做处理，因为这类异常很普遍，若全处理可能会对程序的可读性和运行效率产生影响
3.编译时异常，是编译器要求必须处置的异常
常见的运行时异常举例
1.NullPointerException空指针异常
String
2.ArithmeticException数学运算异常
3.ArrayIndexOutOfBoundsException数组下标越界异常
4.CLASSCastException类型转换异常
5.NumberFormatException数字格式不真确异常【】
public class try01 {
    public static void main(String[] args) {
      try {
          String str ="sdd";
          int a = Integer.parseInt(str);
          System.out.println("数字;" + a);
      }catch(NumberFormatException e){
          System.out.println("异常信息" + e.getMessage());
      }finally {
          System.out.println("不管错误，继续执行");

      }

    }
}



编译异常
编译异常是指在编译期间，就必须处理的异常，否则代码不能通过编译。
常见的编译异常
SQLException//操作数据库时，查询表可能发横异常
IOException//操作文件时，发生的异常
FileNotFoundException//当操作一个不存在的文件时，发生异常
CLASSNotFoundException //加载类，而该类不存在时，异常
EOFException//操作文件，到文件末尾，发生异常
illegalArguementException//参数异常




异常处理
异常处理就是当异常发生时，对异常处理的方式。
异常处理方式
try - catch-finally
程序员在代码中捕获发生的异常，自行处理
throws
将发生的异常抛出，交给调用者（方法）来处理，最顶级的处理者就是JVM


try{
代码/可能有异常
}catch(Exception e){
//捕获到异常
//1当异常发生时，2系统将异常封装成一个叫Exception对象 e传递给catch
}//3得到异常对象后，程序员，自己处理，4注意，如果没有发生异常catch代码块不执行
finally{//1不管try代码块是否有异常发生，始终要执行finally
2.所以，通常将释放资源的代码，放在finally
}



throws 处理机制图
JVM-------->main ----->f1方法------>f2方法----throws--->f1 //t-c-f ---throws---->main//t-c-f ---------throws------>JVM
throws 处理机制图//处理异常机制：输出异常信息，中断程序
try-catch - finally 和throws 二选一
如果没有采取try-catch 默认就是throws


try-catch异常处理
1.java提供try和catch块来处理异常。try块用于傲寒可能出错的代码。catch块用于处理try块中发生的异常。可以根据需要在程序中有多个try...catch块
2.基本语法
try{
//可以代码
//将异常生成对应的异常对象，传递给catch块
}catch（异常）{
//对异常的处理
}如果没有finally，语法是可以通过的


1.如果异常发生了，则异常发生后面的代码不会执行，直接进入到catch块
2.如果异常没有发生，则顺序执行try的代码块，不会进入到catch。
3.如果希望不管是否发生异常，都执行某段代码（比如关闭链接，释放资源等）则使用如下代码-finally


public class try02 {
    public static void main(String[] args) {
        try {//要求1.如果try代码块有可能有多个异常
            //2.可以使用多个catch 分别捕获不同的异常，相应处理
            //3.要求子类异常写在前面，父类异常写在后面
            Person person = new Person();
            System.out.println(person.getName());
            int n1 = 10;
            int n2 = 0;
            int res = n1 / n2; //ArithmeticException
        } catch (NullPointerException e){
            System.out.println(e.getMessage());
        }  catch (ArithmeticException e){
            System.out.println(e.getMessage());
        } catch (Exception e) {//必须写最后一项，是父类
            System.out.println(e.getMessage());
        }finally {
        }

    }
}
class Person{
    private String  name;

    public String getName() {
        return name;
    }
}


4.可以有多个catch语句，捕获不同的异常（进行不同的业务处理），要求父类异常在后，子类异常在前，比如（Exception在后，NullPointerException 在前），如果发生异常，只会匹配一个catch，案例演示
5.可以进行 try-finally配合使用，这种用法相当于没有捕获异常，因此程序会直接崩掉。应用场景：就是执行一段代码，不管是否发生异常，都必须执行某个业务逻辑
try{
//代码
}
finally{
}//总是运行


  try {
             int n1 = 10;
             int n2 = 0;
            System.out.println(n1 / n2);
        } finally {
            System.out.println("执行了finally");
        }
        System.out.println("程序继续执行");
    }
}

throws异常处理
1.如果一个方法（中的语句执行时）可能生成某种异常，但是并不能确定如何处理这种异常，则此方法应显示地声明抛出异常，表明该方法将不对这些异常进行处理，而由该方法的调用者负责处理。
2.在方法声明中用throws语句可以声明抛出异常的列表，throws后面的异常类型可以是方法中产生的异常类型，也可以是它的父类
public class Throws01 {
    public static void main(String[] args) {

    }


    public void f1() throws FileNotFoundException,NullPointerException,ArithmeticException {//Exception
        //创建了一个文件流对象
        //老韩解读：
        //1.这里的异常是一个FileNotFoundExcetion 编译异常
        //2.使用前面讲过的try-catch-finally
        //3.使用throws，抛出异常，让调用f2方法的调用者（方法）处理
        //4.throws后面的异常类型可以使方法中产生的异常类型，也可以是它的父类
        FileInputStream fis = new FileInputStream("d://aa.txt");
    }


}
throws异常处理
1.对于编译异常，程序中必须处理，比如try-catch或者throws
2.对于运行时异常，程序中如果没有处理，默认就是throws的方式处理
3.子类重写父类的方法时，对抛出异常的规定：子类重写的方法，所抛出的异常类型要么和父类抛出的异常一致，要么为父类抛出的异常的类型的子类型
4.在throws过程中，如果有方法try-catch，就相当于处理异常，就可以不必throws


/**
 * @author 郑道炫
 * @version 1.0
 */
public class Throws01 {
    public static void main(String[] args) throws ArithmeticException{
                       f2();
    }
    public void f1() throws FileNotFoundException,NullPointerException,ArithmeticException {//Exception
        //创建了一个文件流对象
        //老韩解读：
        //1.这里的异常是一个FileNotFoundExcetion 编译异常
        //2.使用前面讲过的try-catch-finally
        //3.使用throws，抛出异常，让调用f2方法的调用者（方法）处理
        //4.throws后面的异常类型可以使方法中产生的异常类型，也可以是它的父类
        FileInputStream fis = new FileInputStream("d://aa.txt");
    }
    public void f3(){
//        f1();//因为f3（）方法抛出的是一个编译一场，这时，就要f1（）必须处理这个编译异常，在f1（）中，要么try-catch-finally，或者继续throws 这个编译异常

    }

    public static void f2() throws ArithmeticException{
        int n1 = 10;
        int n2 = 0;
        double res = n1 /n2;
    }
    public static void f4(){
        //f4中调用方法f5没有问题
        //原因是f5（）抛出的是运行异常
        //而java中，并不要求程序员显示处理，因为有默认处理机制
        f5();
    }public static  void f5() throws ArithmeticException{//抛出运行异常，抛出编译异常就不能

    }
}
class Father{
    public void method() throws  RuntimeException{//父类

    }
}
class Son extends  Father{
    @Override
    public void method() throws ArithmeticException{//子类不能扩大范围//子类
        super.method();
    }
}


自定义异常
当程序中出现了某些“错误”，但该错误信息并没有在Throwable子类中描述处理，这个时候可以自己设计异常类，用于描述该错误信息。
自定义异常的步骤
1.定义类：自定义异常类名（程序员自己写）继承Exception或RuntimeException
2.如果继承Exception，属于编译异常
3.如果继承RuntimeException，属于运行异常（一般来说，继承RuntimeException



public class customExcepton {
    public static void main(String[] args) {
        int age = 200;
        //要求范围在18-120之间，否则抛出一个自定义异常
        if (!(age >= 18&& age <= 120)) {
                throw  new AgeException("年龄需要在18-120之间");
        } System.out.println("您的年龄范围正确");
    }
}
class AgeException extends RuntimeException{
    //自定义一个异常
    //老韩解读
    //1.一般情况下，我们自定义异常是继承RuntimeException
    //2.即把自定义异常做成运行时异常，好处是，我们可以使用默认的处理
    public AgeException(String message){
        super(message);
    }
}
）
区别                意义
 throws           异常处理的一种方式            
throw             手动生成异常对象的关键字
                       位置
                     方法声明处
                       方法体中
           后面跟的东西
             1.异常类型
             2.异常对象    
