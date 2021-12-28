# JspFinder
![](https://img.shields.io/badge/%E5%8A%9F%E8%83%BD-%E5%8F%91%E7%8E%B0jsp%20webshell-blue)

![](https://img.shields.io/badge/Java-8-red)



### 简介

受[4ra1n](https://github.com/EmYiQing)师傅的[JSPKiller](https://github.com/EmYiQing/JSPKiller)项目的启发，开发的一款可实战的，通过污点追踪发现Jsp webshell的工具(A tool to find Jsp Webshell through stain tracking) 。污点跟踪的实现方式为使用编译jsp为class后通过java代码为class中的方法设置污点，然后模拟jvm堆栈的运行，查看污点能否流入危险方法，如:Runtime.exec、ProcessBuilder。这个过程不和web服务器有任何的挂钩和侵入，完全是独立行为，所以该检测方式不会影响服务器，可以在服务器上放心使用。具体原理已经放在了先知上，等文章审核通过后会更新出文章链接。

### 使用

```
Usage: <main class> [options]
  Options:
    -cp, --classpath
      指定容器的依赖jar包(tomcat例为:D:\apache-tomcat-8.0.50\lib)
    --debug
      Debug
      Default: false
    -f, --file
      指定web目录下的某个文件
    -h, --help
      Help Info
    -s, --save
      指定结果存放的文件名
      Default: result.txt
    -d, --webDir
      指定web目录，如 D:\tomcat环境\apache-tomcat-8.0.50-windows-x64\apache-tomcat-8.0.50\webapps\samples-web-1.2.4\
```

通常用法，表示检测apache-tomcat-8.0.50目录下有无jsp webshell

```
java -jar JspFinder-1.0.0-SNAPSHOT-jar-with-dependencies.jar -d  D:\tomcat环境\apache-tomcat-8.0.50-windows-x64\apache-tomcat-8.0.50  -cp D:\tomcat环境\apache-tomcat-8.0.50-windows-x64\apache-tomcat-8.0.50\lib
```

![image-20211228110711534](img/image-20211228110711534.png)

### 编译

```
mvn assembly:assembly
```

![image-20211228113256419](img/image-20211228113256419.png)

maven编译完后会在target目录生成一个JspFinder-x.x.x-SNAPSHOT-jar-with-dependencies.jar。

然后到项目目录中的lib目录解压jspcp.jar

![image-20211228113554145](img/image-20211228113554145.png)

用压缩工具打开JspFinder-x.x.x-SNAPSHOT-jar-with-dependencies.jar，将jspcp文件夹中的javax、org两个目录拖到jar中。

![image-20211228113808020](img/image-20211228113808020.png)

得到的jar即可使用

### 参考

https://github.com/EmYiQing/JSPKiller

https://github.com/threedr3am/gadgetinspector

[![Stargazers over time](https://starchart.cc/flowerwind/JspFinder.svg)](https://starchart.cc/flowerwind/JspFinder) 