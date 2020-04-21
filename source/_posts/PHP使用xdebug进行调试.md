---
title: PHP使用xdebug进行调试
date: 2020-03-31 10:58:14
categories:
- [技术, PHP]
tags:
- PHP调试
---

​		在使用PHP进行编码时，对PHP代码的调试一般都是在代码中输出需要观察的变量来进行，这样很不方便。通过使用xdebug可以像调试java代码那样打断点进行调试，更加合理和方便。

<!-- more -->

**说明：本教程所使用编辑器为PHPstorm**

### 下载xdebug 

**说明：如果使用的是phpstudy可以在PHP扩展及设置中选中xdebug，然后直接进行php.ini的配置即可**

​	xdebug官网：https://xdebug.org/download.php

​	在选择下载哪个版本的xdebug的时候需要注意了，下面有两种方法，让你准确的下载自己环境对应的xdebug文件：

**1>.打印出phpinfo()信息，如下：**

​	{% asset_img img1.png  phpinfo打印的信息 %}

​	{% asset_img img2.png  phpinfo打印的信息 %}

​	然后还要注意一点就是看看自己php对应的版本和操作系统的位数，结合这四点去官网找到对应的xdebug文件（本人php是7.0.1的版本，对应的xdebug文件为：php_xdebug-2.6.0-7.0-vc14-x86_64.dll）。

**2>.使用xdebug官方提供的一个检测工具：https://xdebug.org/wizard.php**

​	{% asset_img img3.png  xdebug检测工具 %}

​	这里是把phpinfo()的信息全部输出出来复制到图中对应的位置，然后就会检测你可以下载的对应的版本，如下图：

{% asset_img img4.png  xdebug检测工具 %}

###  安装并配置xdebug

**1>.将下载好的.dll文件放入指定的位置**

​	本例中存放的路径为PHPstudy中使用的PHP存放的路径 （......\php\php7.0.10\ext\）

**2>.配置php.ini配置文件**

​	这里需要注意一点，需要找到正确使用的php.ini文件，在网页上打印出phpinfo()的信息，查看这一条信息：

​	{% asset_img img5.png  php.ini配置文件的路径 %}

​	从图中可以看到使用的是哪个php的配置文件，然后添加一下配置:

**（wamp中php.ini的配置）**

```
[xdebug]
zend_extension ="G:/wamp64/bin/php/php7.0.10/ext/php_xdebug-2.6.0-7.0-vc14-x86_64.dll"
xdebug.remote_enable = On
;启用性能检测分析
xdebug.profiler_enable = On
;启用代码自动跟踪
xdebug.auto_trace=On
xdebug.profiler_enable_trigger = On
xdebug.profiler_output_name = cachegrind.out.%t.%p
;指定性能分析文件的存放目录
xdebug.profiler_output_dir ="G:/wamp64/tmp"
xdebug.show_local_vars=0
;配置端口和监听的域名
xdebug.remote_port=9000
xdebug.remote_host="localhost"
```

**（phpstudy中php.ini的配置）**

```
[XDebug]
;php.ini默认配置
xdebug.profiler_output_dir="D:\phpStudy\tmp\xdebug"
xdebug.trace_output_dir="D:\phpStudy\tmp\xdebug"
zend_extension="D:\phpStudy\php\php-7.0.12-nts\ext\php_xdebug.dll"

;新增配置
#开启远程调试
xdebug.remote_enable = 1  
xdebug.remote_handler = "dbgp"
xdebug.remote_host = "127.0.0.1"
#这个端口一定要和phpstrom（即所用的编辑器）配置中的端口一致
xdebug.remote_port=9000
#开启自动开始调试（这个一般必须要有否则会调试不了）
xdebug.remote_autostart=1
```

配置完成后，就可以重启你的环境了，然后在页面打印出phpinfo()信息就能看到有xdebug的信息了。

### 配置phpstorm

**1>.打开phpstorm，PHP>Debug 的设置，配置端口和php.ini中的xdebug.remote_port一致。，并且允许外部连接（浏览器XDebug插件）**

{% asset_img img9.png  phpstorm的Debug配置%}

**2>.Debug>Servers配置：**

{% asset_img img6.png PHPstorm Debug配置 %}

如图host配置成你刚才设置php配置文件中 xdebug.remote_host="localhost"对应的参数，注意端口默认80，<span style='color:red'>（端口号需要和你的站点域名的端口号保持一致）</span>，debugger选择xdebug即可。

本例使用的是phpstudy，其站点域名和端口设置如下：

{% asset_img img7.png phpstudy站点域名和端口设置%}

<span style='color:red'>PHPstorm中快捷键ctr+alt+s调出如下界面，如果选择了Use path mapping，直接默认就行不需要修改其下面的内容。</span>

{% asset_img img8.png  phpstorm的servers配置%}

**3>.设置服务器调试配置，Run>Web Server Debug Validation：（点击上图Debug配置中右侧的Pre-configuration栏内第1项的validate出现下图）**

{% asset_img img10.png  Web Server Debug Validation%}

本机配置如下:

{% asset_img img11.png  Web Server Debug Validation%}

### 安装Chrome的XDebug插件

参考链接：[Install Xdebug Helper](https://confluence.jetbrains.com/display/PhpStorm/Configure+Xdebug+Helper+for+Chrome+to+be+used+with+PhpStorm)

### 在phpstorm中使用xdebug进行调试

{% asset_img img12.png 调试页面%}

***

**参考链接：**

​	https://www.cnblogs.com/pcyy/p/9811460.html

​	https://www.jb51.net/article/140487.htm





