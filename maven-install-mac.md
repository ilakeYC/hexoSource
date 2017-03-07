---

title: Maven在Mac上的安装及配置
date: 2017-03-07 16:45:49
category:
- Java Developer
tags: 
- Java

---

![](http://upload-images.jianshu.io/upload_images/1644195-2923c75643e8b2eb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

<!-- more -->

> 我们每期会根据不用的**项目案例**安排不同的技术栈**免费**课程！**免费**！**免费**！**免费**！来帮助大家提高，有兴趣的同学可以微信搜索公众号：**IT技术成长联盟**
> 
> 微信号：`the_it_master`

---

#### Maven 是什么

> `Maven` 是一个项目管理和综合工具。`Maven` 提供了开发人员构建一个完整的生命周期框架。开发团队可以自动完成项目的基础工具建设，`Maven` 使用标准的目录结构和默认构建生命周期。
在多个开发团队环境时，`Maven` 可以设置按标准在非常短的时间里完成配置工作。由于大部分项目的设置都很简单，并且可重复使用，`Maven` 让开发人员的工作更轻松，同时创建报表，检查，构建和测试自动化设置。
`Maven` 提供了开发人员的方式来管理：

> ``` Builds 
Documentation 
Reporting 
Dependencies 
SCMs 
Releases 
Distribution 
mailing list 
```

> 概括地说，`Maven`简化和标准化项目建设过程。处理编译，分配，文档，团队协作和其他任务的无缝连接。 `Maven` 增加可重用性并负责建立相关的任务。

---

#### 在Mac下的安装


前往 **[Maven官网](http://maven.apache.org)** 选择 **[Download](http://maven.apache.org/download.cgi)** 前往最新的 `Maven` 下载页面：

![maven.apache.org](http://upload-images.jianshu.io/upload_images/1644195-b8272b16a4dba9e2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


在 **Other mirrors** 位置，可以选择下载源服务器，默认就好了，除非你觉得下载非常慢想试试另一个服务器。

![](http://upload-images.jianshu.io/upload_images/1644195-7ded45be20b48dc4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

`Maven` 要求（如下图）：

- 电脑上安装了 **JDK (Java Development Kit) 1.7** 或 1.7 以上版本，如果没有安装 JDK，可以先去下载安装。
- 电脑硬盘最少还有 **10MB** 的可用空间，此外，`Maven` 还会在你的磁盘上建立仓库，具体大小因使用状况而不同，但是至少需要 **500MB**，总共 **510MB** 哦。

![](http://upload-images.jianshu.io/upload_images/1644195-8696bf66d50c0082.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在满足要求之后，就可以下载 `Maven` 二进制文件到本地了，在这里选择 [apache-maven-3.3.9-bin.zip](http://mirror.bit.edu.cn/apache/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.zip) 即可（如下图）。

![](http://upload-images.jianshu.io/upload_images/1644195-55c0cf0ec114dc13.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

下载一个 `.zip` 文件，解压后得到 `apache-maven-3.x.y` 文件夹，其中的内容希望**不要更改或删除**：

|![](http://upload-images.jianshu.io/upload_images/1644195-98b24ba8598a3a39.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|![](http://upload-images.jianshu.io/upload_images/1644195-1e8d3ba8579c1c06.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|
|--|--|
||||

将这个文件夹移动到 `/usr/local/` 目录下，如：`/usr/local/apache-maven-3.x.y`

---

#### 在Mac下的配置

打开终端：

![](http://upload-images.jianshu.io/upload_images/1644195-42fff24a8855a3f0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

输入：`vi ~/.bash_profile` ，遇到权限问题，可以使用 `sudo` 命令。
新建或编辑一个名叫 `bash_profile` 的隐藏文件。在该文件中添加：

```
export M2_HOME=/usr/local/apache-maven-3.3.9
export PATH=$PATH:$M2_HOME/bin
```

`/usr/local/apache-maven-3.3.9` 是刚刚解压的文件夹绝对路径。
编辑完成后保存并退出 `vim` 环境。

> **如何保存并退出？**
> 
编辑完成后，按下`esc`键，随后输入`:wq`并回车即可。
>
>`w`：写入（write）
>
>`q`：退出（quit）

执行 `mvn --version` 命令，见如下图输出即配置完成。

![](http://upload-images.jianshu.io/upload_images/1644195-1ae04788263beea5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

> 我们每期会根据不用的**项目案例**安排不同的技术栈**免费**课程！**免费**！**免费**！**免费**！来帮助大家提高，有兴趣的同学可以微信搜索公众号：**IT技术成长联盟**
> 
> 微信号：`the_it_master`