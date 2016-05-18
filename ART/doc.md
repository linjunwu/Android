# android(应用运行在Dalvik虚拟机之上)比ios流畅性差的原因之一：
android应用程序与部分系统服务是运行在虚拟机之上的，而ios应用程序和系统服务都是直接执行本地机器指令。

# google解决流畅性问题的途径：
1、使用ART替换Dalvik。
2、3.0增加了对应用程序2D UI的硬件加速渲染，也就是GPU渲染。
3、4.1通过Project Butter，在UI架构中引入了VSYNC、Triple Buffer和HWComposer等技术。

# ART比Dalvik快的原因：
ART执行的是本地机器指令，而Dalvik执行的是Dex字节码。（尽管Dalvik也会对频繁执行的代码进行JIT生成本地机
器指令来执行，但毕竟在应用程序运行的过程中将Dex字节码翻译成本地机器机器指令也会影响到应用程序本身的执行，
因此即使Dalvik使用了JIT，也在一定程度上也比不上直接就可以执行本地机器指令的运行时。）

>ART像Dalvik一样，都实现Java虚拟机接口。

# ART能不重新编译APK的基础上，直接对其进行加载和运行的原因：
这是由于APK在安装时被执行了AOT。
（AOT（Ahead Of Time）是相对JIT（Just In Time）而言的。也就是在APK运行之前，就对其包含的Dex字节码进行翻译，
得到对应的本地机器指令，于是就可以在运行时直接执行了。这种技术不但使得我们可以不对原有的APK作任何修改，
还可以使得这些APK只需要在安装时翻译一次，就可以无数次以本地机器指令的形式运行。这种技术与我们用C/C++语言编
写一个程序，然后用GCC编译得到一个可执行程序，最后这个可执行程序就可以无数次地加载到系统执行，是差不多的。）

>LLVM:开发编译器的架构框架。

# 创建与运行ART虚拟机要执行的函数步骤：
1、调用JNI接口FindClass加载com.android.internal.os.ZygoteInit类。
2、调用JNI接口GetStaticMethodID找到com.android.internal.os.ZygoteInit类的静态成员函数main。
3、调用JNI接口CallStaticVoidMethod开始执行com.android.internal.os.ZygoteInit类的静态成员函数main。

# ART的工作原理：
1、ART加载oat文件的过程。
2、ART查找类和方法的过程。
3、ART查找类方法的本地机器指令的过程。
4、Dalvik虚拟机的垃圾收集过程。
5、ART的垃圾收集过程。