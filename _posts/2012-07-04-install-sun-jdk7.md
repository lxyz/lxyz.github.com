---
layout: post
title: ubuntu下安装Sun JDK 7
tags: 
 - sun jdk7
 - ubuntu
---
 1.去[Oracle](http://www.oracle.com/technetwork/java/javase/downloads/java-se-jdk-7-download-432154.html)下载适合你系统版本都JDK7，我的是ubuntu server 64位的，我选择了Linux x64 - Compressed Binary。下载下来的文件是：jdk-7-linux-x64.tar.gz 。

 2.解压文件
    sudo mkdir /usr/lib/sun-java-jdk
    sudo tar zxvf jdk-7-linux-x64.tar.gz -C /usr/lib/sun-java-jdk
查看解压出来的文件：
    ls /usr/lib/sun-java-jdk/
可以看到加压出来的文件再文件夹`jdk1.7.0`中。

 3.设置环境变量
    vim ~/.bashrc
在文件最后面加上:
    export JAVA_HOME=/usr/lib/sun-java-jdk/jdk1.7.0
    export JRE_HOME=${JAVA_HOME}/jre  
    export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib  
    export PATH=${JAVA_HOME}/bin:$PATH 
保存后执行:
    source ~/.bashrc
使修改立即生效。
这时候，若是系统之前没有安装其他版本的JDK的话，就安装完成了。执行`java -version`就可以看到java的版本信息了。
若是系统之前带有或安装有其他版本的JDK，还要执行以下操作。

 4.配置默认JDK版本
    sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/java-7-sun/bin/java 300
    sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/java-7-sun/bin/javac 300
    sudo update-alternatives --install /usr/bin/jar jar /usr/lib/jvm/java-7-sun/bin/jar 300
    sudo update-alternatives --install /usr/bin/javah javah /usr/lib/jvm/java-7-sun/bin/javah 300
    sudo update-alternatives --install /usr/bin/javap javap /usr/lib/jvm/java-7-sun/bin/javap 300
接下来选择默认的JAVA，执行：
    sudo update-alternatives --config java
会列出系统中其他的java 版本，根据需要选择就可以了。

至此，sun-java-jdk7安装完成。

参考：[Ubuntu 11.04 下安装配置 JDK 7](http://blog.csdn.net/yang_hui1986527/article/details/6677450)
