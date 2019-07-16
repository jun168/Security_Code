Langzi\_SRC\_Safe_Cruise的历史试验版本，功能单一

# 概述

实现全自动漏洞扫描自动复现生成报告，全程自动化

又到了一年一度的520年度环节，去年为基佬们准备的礼物是YolandaScan，新年礼物是安全巡航0.95模型机，虽然在现在看来都很弱，不够完善，不过也是当初的美好回忆。

今年帅气的群主为大家准备的年度礼物是基于安全巡航过度版本的extract1.5版本，虽然功能少，也不够智能化，但是是一个美好的开始

虽然工具挺破，还消耗资源，又不成熟....但是也是一点点小心意....


# 运行条件

1. 安装 Microsoft Office 
2. 安装Firefox浏览器
3. 安装vc++2015相关库
4. 安装python2，并添加到系统环境变量//即cmd下输入python进入python2交互界面
5. 安装Mysql数据库
6. 运行目录不要存在中文

# 环境准备

1. 将目录下的创建数据库文件导入，创建数据库
2. 配置文件


参数介绍

	[Server]
	host = 127.0.0.1
	# 数据库地址
	username = root
	password = root
	db = langzi_scan
	# 数据库名
	port = 3306
	# 端口
	
	[Config]
	thread_s = 16
	# 扫描线程数，一般不能设置太大
	check_env = 1
	# 是否每次运行前检测运行环境
	start_on = 0
	# 是否从数据库中获取数据继续扫描

check_env参数：每次运行前检测相关运行环境是否正确配置，设置成1则会每次启动扫描器前自动检测运行环境

start_on参数：设置成1再数据库存在数据的情况下，不导入新的网址，直接从数据库提取网址进行扫描，设置成0则每次启动主程序都会提示导入网址到数据库，燃后开始扫描。

# 使用方法

批量采集url保存在文本

启动主程序

导入采集好的url即可

全部自动生成报表使用浏览器截图，无需操作

[视频演示地址](http://www.langzi.fun/upload/auto01.mp4)

### 资源消耗

对主机配置略高，最好是SSD硬盘[启动Firefox]

使用的线程数基于CPU处理核心数

个人使用16个线程，在全部启动并发情况下资源消耗


![](http://www.langzi.fun/upload/IMG_20190519_100953.jpg)

![](http://www.langzi.fun/upload/TIM截图20190519000918.png)



# 补充

目前稳定支持sql注入，xss，源码泄露，url跳转四种类型漏洞扫描，关于其他的未授权访问，数据库弱口令，以及各种未授权漏洞，代码执行，命令执行，信息泄露等等将会在以后慢慢更新

目录下生成文本内容包括任意url跳转，xss，源码泄露相关信息，然后通过Firefox浏览器直接渲染检测是否出现弹窗，出现弹窗直接捕获截图保存


建议是挂在虚拟机跑，不影响物理机工作，自动生成扫描结果

随后你就可以去做一些你爱做的事


关键点：

- 导入的网址必须带http://或https://

- **不支持扫描国内GOV 与 EDU **

- 每次最大扫描数量设置为500

- 不管你导入的网址多大，只会从中提取500个网址加载到数据库扫描

- 配置文件CONFIG.INI的编码为ANSI

# 可以删除的文件

目录下的所有图片

result文件夹

image文件夹

*result.txt

*log.txt

### 捡漏

虽然不能让你称霸SRC，但是在补天能换几桶泡面还是可以的

存在大概20%的误报吧，每次提交前需要手动复现的噢