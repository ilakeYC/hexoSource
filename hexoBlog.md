---
title: 搭建一个Hexo博客
date: 1970-1-1 0:0:0
tags:
---

`安装过程中如果出现问题请到最后面查看问题总结，或许能帮助你解决问题。`

> **注意：本文仅针对MAC用户**

---

<!-- more -->

### 什么是[Hexo](https://hexo.io)?

Hexo 是一个快速，简单，强有力的博客框架。你可以用[Markdown](Markdown)（或其他语言）写文章，即刻Hexo就能生成一个带有非常漂亮的主题的静态网站。

>>>>>>>>>>>>>>>>>>>>>>>>>>> ---

### 安装

安装Hexo只需要几分钟的时间（此处建议你[科学上网](https://raw.githubusercontent.com/getlantern/lantern-binaries/master/lantern-installer-beta.dmg)）。
> 点击“科学上网”即可下载Lantern for macOS。

如果你遇到任何问题，而且没有办法解决他们，请提交[GitHub issue](https://github.com/hexojs/hexo/issues)，Hexo团队会帮助你解决问题。

>>>>>>>>>>>>>>>>>>>>>>>>>>> ---

### 必要的安装项目：

- [Node.js](https://nodejs.org)
- Git（安装Xcode即可自动安装Git，Xcode可以在App Store中下载。）

如果你的电脑中已经安装好了上述两项，非常好！现在只需要用npm安装Hexo了！

打开 Launchpad -> 其他 -> 终端

输入：

```
npm install -g hexo-cli
```

上述命令如果不成功，请尝试:

```
sudo npm install -g hexo
```

>>>>>>>>>>>>>>>>>>>>>>>>>>> ---

### 初始化

我们可以创建一个新的目录来存放管理你的博客相关的内容

在终端中前往你所希望的目录，我的目录在`Document/hexoWeblog`。输入：

```
hexo init
```

或者直接在你规定的目录初始化

```
hexo init `filePath`
如：
hexo init /Users/ilakeyc/Documents/hexoWeblog
```

如果你看到控制台输出：

```
You are almost done! Don't forget to run `npm install` before start blogging with Hexo!
```

说明初始化成功。

>>>>>>>>>>>>>>>>>>>>>>>>>>> ---

### 安装依赖包

在初始化的目录下输入：

```
npm install
```

如果失败请尝试：

```
sudo npm install
```

控制台没有任何错误出现，则安装完成。

>>>>>>>>>>>>>>>>>>>>>>>>>>> ---

### 生成静态网站：

```
hexo generate
```

或者简写为：

```
hexo g
```

>>>>>>>>>>>>>>>>>>>>>>>>>>> ---

### 启动本地服务器调试

```
hexo server
```

或者简写为：

```
hexo s
```
通过[http://localhost:4000](http://localhost:4000)查看效果


>>>>>>>>>>>>>>>>>>>>>>>>>>> ---

### 部署到GitHub

如果想要部署到[GitHub](https://github.com)，你需要一个Github账号，然后创建一个仓库来存放你的博客：

- **创建仓库**

如果你的GitHub用户名为：xxx ， 则需要一个仓库名为 `xxx.github.io`

![](http://i13.tietuku.com/a866c741cacf10af.png)

`初始化一个带有README文件的仓库`选项可有可无。

- **创建SSH Keys**

```
ssh-keygen -t rsa -C "这里是你申请Github账号时的邮箱"
如：
ssh-keygen -t rsa -C "xxx@foo.bar"
```
> 如果出现`overwrite(y/n)?`，你需要选择是否覆盖原来的key，自行确定哦。

连按三次回车后，你会看到控制台输出了一个方框中间有一些字母和泡泡

然后输入：

```
eval "$(ssh-agent -s)"
```

然后：

```
ssh-add ~/.ssh/id_rsa
```

最后将生成的密钥( 这个词念`mi yue`都是四声 :-) )复制到剪贴板：

```
pbcopy < ~/.ssh/id_rsa.pub
```

`此处不要再复制任何东西！`

进入你的GitHub，在用户选项中选择`Settings`
![](http://i13.tietuku.com/4614dd21ce29ef47.png)

点击[SSH and GPG keys](https://github.com/settings/keys)，右上角点击`New SSH Key`：
![](http://i13.tietuku.com/ea3165bdd678afb9.png)
在`Key`一栏中 `command + v` ，将你的SSH Key粘贴到这里，随后点击`Add Key`保存。

控制台输入：
```
ssh -T git@github.com
```

如果输出结果：

```
Hi username! You've successfully authenticated, but GitHub does not
```

表示连接成功！`如果需要(yes/no)，选择yes`

- **在Git中设置你的用户名和邮箱**

```
git config --global user.name "这里是你申请Github账号时的name"
```

```
git config --global user.email "这里是你申请Github账号时的邮箱"
```

- **修改Hexo配置文件**

在你的博客目录下，找到`_config.yml`，打开进行编辑：

在文件最下方找到`deploy`：

```
deploy:
  type: git
  repo: 你的仓库地址
  branch: master

 如

deploy:
  type: git
  repo: https://github.com/your_username/your_username.github.io.git
  branch: master
```

保存文件并退出，随后在控制台输入：

```
hexo g
```

```
hexo d
```

或简写：

```
hexo d -g
```

等待命令完成，你的GitHub仓库中会出现`你的博客目录/public`目录下相同的文件。

浏览器登录`你的GitHub用户名.github.io`查看效果吧！

>>>>>>>>>>>>>>>>>>>>>>>>>>> ---

### 开始写文章！

接下来，让我们[在Hexo中写一篇新文章](/1970/01/01/newPost/)！

---


# 常见问题：

- 部署时出现：Error: EACCES, open ‘/Users/Desktop/hexo/public/js/script.js’

**解决办法**：权限问题在部署命令前加sudo

- deployer找不到git: ERROR Deployer not found: git

**解决办法**：`npm install hexo-deployer-git --save`

- ```
{ [Error: Cannot find module './build/Release/DTraceProviderBindings'] code: 'MODULE_NOT_FOUND' }
{ [Error: Cannot find module './build/default/DTraceProviderBindings'] code: 'MODULE_NOT_FOUND' }
{ [Error: Cannot find module './build/Debug/DTraceProviderBindings'] code: 'MODULE_NOT_FOUND' }```

**解决办法**： `npm install hexo --no-optional`

- 其他问题：

[非常全的问题汇总，大家可以参考下](http://wp.huangshiyang.com/hexo常见问题解决方案)

- 更多主题：
 - [知乎：有哪些好看的 Hexo 主题](https://www.zhihu.com/question/24422335)
 - [官方推荐](https://hexo.io/themes/)

---
