---

title: 最好懂的 Bootstrap 实战案例教程
date: 2017-01-18 16:47:25
category:
- Front-End Web Developer
- Repost
tags:
- Front-End Web
- Bootstrap

---

![](http://upload-images.jianshu.io/upload_images/1644195-d294a734780786bd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

<!-- more -->

---

我们在开发前端页面的时候，如果每一个按钮、样式、处理浏览器兼容性的代码都要自己从零开始去写，那就太浪费时间了。所以我们需要一个**框架**，帮我们实现一个页面的**基础部分**和解决一些**繁琐的细节**，只要在它的基础上进行**个性化定制**就可以了。

`Bootstrap` 就是这样一个简洁、直观、强悍的**前端开发框架**，只要学习并遵守它的标准，即使是没有学过网页设计的开发者，也能做出很专业、美观的页面，极大地提高了工作效率。像下面这个漂亮的网站就是基于 `Bootstrap` 来开发的。

![](http://upload-images.jianshu.io/upload_images/1644195-293c6ee98804329f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

`Bootstrap` 的中文文档地址在这里 [Bootstrap 中文文档](http://v3.bootcss.com/)，目前**主流版本为 3.3.x**。不过因为文档的内容结构比较零散，只是从头到尾把一个个组件拆开来讲一遍，缺乏趣味性和实战性（这也是现在很多教程的通病），因此在本教程中，我们会自己动手开发一个完整的**企业网站**案例，在实践的过程中来学习和理解 Bootstrap这个前端开发框架的知识。

----

企业网站是十分常见的一种页面形式。一般包括一个展示企业形象的首页、几个介绍企业资料的文章页、一个“关于”页面。如下就是最终的首页效果。（当然了，这个界面还是比较粗糙的，不过我们这个教程重点是 `Bootstrap` 的学习，如果你要深入学习 CSS 样式方面的知识，请参看我们的相关教程）

![](http://upload-images.jianshu.io/upload_images/1644195-87f648bf35861823.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 项目结构与页面规划

我们先创建站点目录，例如放在 web 站点 `/home/wwwroot/htdocs/wx-xxmm` 下，在里面新建一个 `Template` 目录，用于存放页面 `html` 文件，新建一个  `assets` 目录，存放图片、自定义样式表等静态资源文件，以及一个 `js` 目录，存放自己写的 `javascript` 代码。

![](http://upload-images.jianshu.io/upload_images/1644195-902874e7f1321da1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

然后在 `Template` 目录里，把这个项目的所有文件创建好：

- 首页(Home_index.html)
- 客户案例详情(Home_case.html)
- 联系方式及意见反馈表单(Home_about.html)

#### 首页

首页的效果图前面有展示，它包括这**几个区域**。做任何页面之前，我们都要先把结构规划好，这样脑子里有清晰的思路，工作起来才有效率。

![](http://upload-images.jianshu.io/upload_images/1644195-6a2cb16e778c2c7b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 导航条
- 轮播图
- 客户案例列表
- 产品截图列表
- 底部网站信息


#### 首页 HTML 骨架与素材准备

然后准备几张图片素材（分别是轮播图、客户案例、产品截图，各 3 张），把它们放到 `assets` 目录里面。然后在 `assets` 目录里面新建一个 `style.css` 文件，用于保存自定义样式。

![](http://upload-images.jianshu.io/upload_images/1644195-cf27d3443bdcae8f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

然后在 `Template` 目录里新建文件 `Home_index.html` ，按照上面规划的页面结构，写好这些基础的 HTML 和 CSS 代码，把页面的骨架搭好。

```
<!DOCTYPE html>
<html lang="en">
<head>
    <title></title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link href="../assets/style.css" rel="stylesheet">
</head>
<body>
    <!--导航-->
    <div class="nav">
        <a href="">微信公众号管家</a>
        <ul>
            <li><a href="">首页</a></li>
            <li><a href="">关于</a></li>
            <li><a href="">登录</a></li>
        </ul>
    </div>
    <!--轮播图-->
    <div class="slide">
        <div>
            <h1>轮播图1</h1>
            <img src="../assets/slide_1.jpg" alt=""></div>
        <div>
            <h1>轮播图2</h1><img src="../assets/slide_2.jpg" alt=""></div>
        <div>
            <h1>轮播图3</h1><img src="../assets/slide_3.jpg" alt=""></div>
    </div>
    <!--案例-->
    <div class="case">
        <div>
            <h2>案例1</h2>
            <img src="../assets/case_1.jpg" alt="">
        </div>
        <div>
            <h2>案例2</h2>
            <img src="../assets/case_2.jpg" alt="">
        </div>
        <div>
            <h2>案例3</h2>
            <img src="../assets/case_3.jpg" alt="">
        </div>
    </div>
    <!--产品功能截图-->
    <div class="screenshoot">
        <div>
            <h2>截图1</h2><img src="../assets/screenshot_1.jpg" alt=""></div>
        <div>
            <h2>截图2</h2><img src="../assets/screenshot_2.jpg" alt=""></div>
        <div>
            <h2>截图3</h2><img src="../assets/screenshot_3.jpg" alt=""></div>
    </div>
    <!--底部-->
    <div class="footer">
        版权所有 2016
        <a href="">四光年科技</a>
    </div>
</body>
</html>
```

注意我们在页面里引入了样式表文件 `../assets/style.css`（目前这个文件里面是空的）

在浏览器里打开这个页面，看看是否正常访问。因为**没有写任何 CSS 样式代码**，看上去挺丑的。

![](http://upload-images.jianshu.io/upload_images/1644195-a0e4eb133072b95f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 引入 Bootstrap 框架相关文件

前面说到 `Bootstrap` 是一个**前端开发框架**。其实说白了就是一个**样式表文件**（bootstrap.min.css）和一个 **javascript 文件**（bootstrap.min.js），在页面里把它们引入进来后，就可以直接使用里面的 CSS 规则和各种组件了。


#### 远程 CDN 引入方式

编辑 `Home_index.html` ，把几个 `Bootstrap` 框架包含的文件添加进来，这里推荐使用 CDN 源 上的**远程文件**，可以节约本地的带宽。

另外，由于 `Bootstrap` 还依赖 `jQuery` 库，所以也要一并把这个  `jquery.min.js` 文件引入。

```
<link rel="stylesheet" href="//cdn.bootcss.com/bootstrap/3.3.5/css/bootstrap.min.css">
<link href="../assets/style.css" rel="stylesheet">
<script src="//cdn.bootcss.com/jquery/1.11.3/jquery.min.js"></script>
<script src="//cdn.bootcss.com/bootstrap/3.3.5/js/bootstrap.min.js"></script>
```

注意这几个文件的**前后顺序**，如果不对，会导致页面无法正常运行。

1. 先引入 bootstrap.min.css （Bootstrap的样式表文件）
1. 然后引入自己写的 css 文件（style.css）
1. 然后引入 jQuery（javascript 库）
1. 最后引入 bootstrap.min.js 程序文件

#### 本地文件引入方式

如果在没有联网的环境，或者用上面的方式引入文件后浏览器报错，可以把 `Bootstrap` 的所有文件下载到本地后再引用到页面中。打开下面这个地址，把压缩包下载后解压，全部放到 `assets` 目录的 `bootstrap` 里面。

[下载Bootstrap包含的文件到本地](http://v3.bootcss.com/getting-started/#download)

![](http://upload-images.jianshu.io/upload_images/1644195-859cd835797da634.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

然后修改 `Home_index.html` 里的引入文件代码，使用**本地引用文件**的方式来使用 `Bootstrap` 。

```
<link rel="stylesheet" href="../assets/bootstrap/css/bootstrap.min.css">
<link href="../assets/style.css" rel="stylesheet">
<script src="../assets/jquery.min.js"></script>
<script src="../assets/bootstrap/js/bootstrap.min.js"></script>
```

#### Bootstrap 做了些什么？

打开 `assets/bootstrap/` 目录下的样式表文件 `bootstrap.min.css` ，可以看到里面定义了**大量的 CSS 规则**，例如下面这段就定了一个类名为 `btn-primary` 的规则。

```
.btn-primary{color:#fff;background-color:#337ab7;border-color:#2e6da4}
```

现在测试一下，在 `Home_index.html` 文件里面写一个按钮，添加 `class` 为 `btn btn-primary` 。

```
<body>
	<button type="button" class="btn btn-primary">按钮</button>
</body>
```

刷新页面，你会看到一个蓝色的按钮。**不需要自己写一行 CSS 代码**，只要在页面里面给某个元素指定一个 `class` ，就可以直接显示出预定的样式—— 这就是使用 `Bootstrap` 前端框架的魔力。

![](http://upload-images.jianshu.io/upload_images/1644195-69084ca0f33d5f24.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 使用导航条组件

导航条位于页面最顶部，提供整个网站所有页面的链接，最终效果如下：

![](http://upload-images.jianshu.io/upload_images/1644195-7e8d7dccdcb6802e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

我们可以直接使用 `Bootstrap` 的`导航条组件`

```
<!--导航-->
<nav class="navbar navbar-default">
   <div class="container-fluid">
       <ul class="nav navbar-nav">
           <li class="active"><a href="">首页</a></li>
           <li><a href="">关于</a></li>
           <li><a href="">登录</a></li>
       </ul>
   </div>
</nav>
```

1. 添加一个 `nav` 标签，并设置 `class` 为 `navbar` `navbar-default` `，role` 为 `navigation` 。
1. 然后在里面添加一个类名为 `container-fluid` 的 `div` ，用来容纳导航条里的其他元素（链接、按钮等）。
1. 添加一些导航链接 `<li>` ，然后把第一个 `<li>` 的 `class` 指定为 `active` ，表示激活状态。

刷新页面，一个漂亮的导航条就诞生了！我们只是写了一些 HTML 代码，没有写一句 CSS 代码，非常省时省力。

![](http://upload-images.jianshu.io/upload_images/1644195-9c676f7b23b7ec99.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

导航条还漏了一个“网站标题”，把下面这段 `<div class="navbar-header">` 添加到 `<ul class="nav navbar-nav">` 的前面就可以了

```
<div class="navbar-header">
    <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#navbar" aria-expanded="false" aria-controls="navbar">
      <span class="sr-only">Toggle navigation</span>
      <span class="icon-bar"></span>
      <span class="icon-bar"></span>
      <span class="icon-bar"></span>
    </button>
    <a class="navbar-brand" href="#">微信公众号管家</a>
  </div>

  <ul class="nav navbar-nav">
  	<li class="active"><a href="">首页</a></li>
```

如果要添加更多的效果，例如下拉菜单、固定在顶部等等，请在文档中查看，相信你现在应该很容易看明白了。

[Bootstrap文档——导航条](http://v3.bootcss.com/components/#navbar-fixed-top)

学一门新知识的最好办法是**通过实践操作**，**由浅入深**，**先入门再填坑**，不要从头到尾去看枯燥的文档，先用起来，掌握最核心的知识点，然后再去了解其他延伸的内容。我们的课程不是“照本宣科读文档”，更重要的是培养你的学习方法。

#### 使用轮播图组件

为了实现一个轮播图效果（也有人叫“幻灯片”），以前我们可能会自己写代码，或者去找 `jQuery` 的插件。其实 `Bootstrap` 已经自带了一个轮播组件—— `Carousel` ，效果如下：

![](http://upload-images.jianshu.io/upload_images/1644195-824f0c9164b64c3d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
<!--轮播图-->
<div id="carousel-example-generic" class="carousel slide" data-ride="carousel">
   <!-- Indicators -->
   <ol class="carousel-indicators">
       <li data-target="#carousel-example-generic" data-slide-to="0" class="active"></li>
       <li data-target="#carousel-example-generic" data-slide-to="1"></li>
       <li data-target="#carousel-example-generic" data-slide-to="2"></li>
   </ol>
   <!-- Wrapper for slides -->
   <div class="carousel-inner" role="listbox">
       <div class="item active">
           <img src="../assets/slide_1.jpg" alt="...">
           <div class="carousel-caption">
               <h1>轮播1的标题</h1>
               <p>这里是轮播图1的说明</p>
           </div>
       </div>
       <div class="item">
           <img src="../assets/slide_2.jpg" alt="...">
           <div class="carousel-caption">
               <h1>轮播2的标题</h1>
               <p>这里是轮播图2的说明</p>
           </div>
       </div>
       <div class="item">
           <img src="../assets/slide_3.jpg" alt="...">
           <div class="carousel-caption">
               <h1>轮播3的标题</h1>
               <p>这里是轮播图3的说明</p>
           </div>
       </div>
   </div>
   <!-- Controls -->
   <a class="left carousel-control" href="#carousel-example-generic" role="button" data-slide="prev">
       <span class="glyphicon glyphicon-chevron-left"></span>
       <span class="sr-only">Previous</span>
   </a>
   <a class="right carousel-control" href="#carousel-example-generic" role="button" data-slide="next">
       <span class="glyphicon glyphicon-chevron-right"></span>
       <span class="sr-only">Next</span>
   </a>
</div>
```

轮播图组件分三部分

- `<ol class="carousel-indicators">` 是“指示器”，就是下方的那三个白色小点，标记**当前播放到哪张图片**了。
- `<div class="carousel-inner" role="listbox">` 里面是**主体内容区域**，包括几张图片和对应说明，分别用 `<div class="item">` 包裹起来
- 最后的两个 `<a class="left carousel-control">` 元素是**手动操作图片左右切换**的按钮。


#### 使用自定义样式来完善 Bootstrap 默认样式

刷新页面，几张图片开始自动播放。但是我们会发现一个问题——如果三张图片大小不一致，这个轮播区域会忽大忽小地变化。

![](http://upload-images.jianshu.io/upload_images/1644195-448f84ba556208e7.gif?imageMogr2/auto-orient/strip)

这种情况就是 `Bootstrap` **力不能及的范围**了，因为**它不知道我们将会使用什么样的素材**，因此要自己写一些**自定义样式**的 CSS 代码来**处理这些特殊的情况**。

打开自定义样式表文件 `assets/style.css` ，在里面添加如下的代码，把图片高度固定设置为 500px，并且设置最小宽度为 100% ，撑满页面。

```
.carousel-inner > .item > img {
  min-width: 100%;
  height: 500px;
}
```

好了，现在轮播图的图片滚动很正常了。

#### 客户案例列表

在这个区域中，有三个**宽度均等**的横向排列的小块，每个小块是由一个圆形图片和一些说明文字组成。最终效果如下:

![](http://upload-images.jianshu.io/upload_images/1644195-f684dbfe13d814bf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 栅格布局

想想看，如果是你自己写 CSS ，准备怎样实现这个均等排列的效果？例如下面通过设置固定宽度/百分比来处理：

```
.item { float:left, width: 300px; /*或者 width: 33%*/ }
```

如果一行要显示4个、6个、或者更多呢？这样计算起来就太不灵活了（100/6 等于 16.6666666……）。

**其实我们并不关心每一份的宽度是多少像素/百分比，我们只关心能不能自动地平均划分成多少份**， `Bootstrap` 的`栅格系统布局`就是为了实现**自动计算每一份的宽度**而诞生的。

栅格可以理解为一个安全门，它的**总长度**可以拉长，可以缩短，但是**总的间隔数量是不变的**，并且所有间隔的**宽度都一样**。

这个伸缩的过程，像不像我们把浏览器拉宽、变窄的操作？ `Bootstrap` 的`栅格系统`规定了每个页面的宽度被**平均划分为 12 等份**，不管整个页面的宽度是 1000像素，还是500像素，都会自动计算每一份（1/12）的宽度是多少。

通过给栅格布局内部的元素指定 `class` 为 `col-md-份数` ，来告诉它的宽度**占据这12份里面的几份**。

例如下面的代码中，有**3个** `div` 的 `class` 为 `col-md-4`（先不管中间那个 `-md-` 是什么，关注这个数字就好），算一算**4 + 4 + 4 是不是正好等于 12**？

```
<div class="container">
    <div class="row">
        <div class="col-md-4">bb</div>
        <div class="col-md-4">cc</div>
        <div class="col-md-4">ee</div>
    </div>
</div>
```

刷新页面，然后用 Chrome 浏览器的开发工具看看效果，发现整个页面的宽度正好被平均**分成了 3 份**(12/4 = 3)。`栅格系统`自动帮我们计算了这 3 份的宽度。

![](http://upload-images.jianshu.io/upload_images/1644195-32b05fe49748015a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

举一反三，如果要把页面平均分为 6 份，那每一份的 `class` 就应该指定 `col-md-2` (12/6 = 2)；如果是 4 份， `class` 就是 `col-md-3`（12/4 = 3）

完整的栅格布局的说明在这里，一开始看不懂没有关系，自己多动手试试就明白了。一定要**动手实践**！

[Bootstrap 文档——栅格系统](http://v3.bootcss.com/css/#grid)

#### 圆形图片样式

虽然自己写一个 CSS 规则 `border-radius: 50%` 也可以实现圆形图片，但是如果能够少写一行代码，为什么不偷个懒呢（不要重复造轮子）， `Bootstrap` 提供了一个圆形图片的 CSS 类 -- `img-circle`（从名称就能看出来它的作用是什么）。

好了，知道栅格布局方式，和圆形图片样式，可以把“案例列表”的 HTML 代码改造一下了。

```
<!--案例-->
<div class="case container">
   <div class="row">
       <div class="col-md-4">
           <img class="img-circle" src="../assets/case_1.jpg" alt="" />
           <h2>案例1</h2>
           <p>非常不错的产品，我很喜欢</p>
       </div>
       <div class="col-md-4">
           <img class="img-circle" src="../assets/case_2.jpg" alt="" />
           <h2>案例2</h2>
           <p>非常不错的产品，我很喜欢</p>
       </div>
       <div class="col-md-4">
           <img class="img-circle" src="../assets/case_3.jpg" alt="" />
           <h2>案例3</h2>
           <p>非常不错的产品，我很喜欢</p>
       </div>
   </div>
</div>
```

另外，和`轮播图`一样，为了防止图片大小不一致导致的页面错乱，还要在 `style.css` 里添加一些自定义的样式，固定图片大小，然后把每个元素的内部设置为居中对齐。

```
.case {
  text-align: center;
  margin-top: 20px;
}
.case img {
  height: 200px;
}
```

`Bootstrap` 还提供了“圆角图片”、带边框线的“缩略图样式”等图片样式，也可以直接使用，在这里查看文档

[Bootstrap文档-图片](http://v3.bootcss.com/css/#images)

#### 产品截图列表——用栅格布局将页面拆分成左右宽度不一样的两栏

先回顾一下前面的知识：**怎样用栅格布局把页面切割成若干等份？**

思考一下：如果我们要把**页面分成左右两栏，但是两栏宽度不一样，**应该怎么做呢？

其实 `Bootstrap` 的栅格布局同样可以实现这种“宽度不一致的分割”。最终效果：

![](http://upload-images.jianshu.io/upload_images/1644195-1c834ba6c1283062.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
<div class="container">
   <div class="row">
       <div class="col-md-4">bb</div>
       <div class="col-md-8">cc</div>
   </div>
</div>
```

左边的 `<div>` 占有 4 份（`col-md-4`），右边的

占有 8 份（`col-md-8`），但是**加起来总数还是 12 份**

在 Chrome 里看到效果如下，确实是左边的一栏相对较窄，右边的一栏较宽一些。

![](http://upload-images.jianshu.io/upload_images/1644195-841ec8793127a7ae.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

开始修改“产品截图”区域的代码，从上到下共有三行，每行的一栏是图片，占有 5 份宽度（col-md-5）；另一栏是说明文字，占据剩下的 7 份宽度（col-md-7）。

```
<!--产品功能截图-->
    <div class="container screenshot">
        <div class="row item">
            <div class="col-md-5"><img src="../assets/screenshot_1.jpg" alt="" class="img-responsive"></div>
            <div class="col-md-7">
                <h2>截图1</h2>
                <p>截图说明1，截图说明1，截图说明1，截图说明1，截图说明1，</p>
            </div>
        </div>
        <div class="row item">
            <div class="col-md-7">
                <h2>截图2</h2>
                <p>截图说明2，截图说明2，截图说明2，截图说明2，截图说明2，</p>
            </div>
            <div class="col-md-5"><img src="../assets/screenshot_2.jpg" alt="" class="img-responsive"></div>
        </div>
        <div class="row item">
            <div class="col-md-5"><img src="../assets/screenshot_3.jpg" alt="" class="img-responsive"></div>
            <div class="col-md-7">
                <h2>截图3</h2>
                <p>截图说明3，截图说明3，截图说明3，截图说明3，截图说明3，</p>
            </div>
        </div>
    </div>
```

**注意**，我们在第二行把图片和文字的左右顺序交换了一下，这样看起来错落有致、更美观一些。

同样，再添加一点自定义的 CSS 代码，在每一行之间显示一条分割线，并且预留一些空白。

```
.screenshot .item {
  border-top: 1px solid #CCC;
  padding-bottom: 30px;
  padding-top: 20px;
}
```

#### 页面底部

这部分没什么特别的内容，使用 HTML5 的新增标签 `<footer></footer>` ，使之更“语义化”（代码也少了几个字母……）。

```
<!--底部-->
<div class="container">
  <footer>
      微信公众号管家版权所有 2016
      <a href="">四光年科技</a>
  </footer>
</div>
```

#### 覆盖 Bootstrap 的默认样式

其实除了可以**添加**自定义样式外，还可以**覆盖**掉 `Bootstrap` 的默认样式，让它更符合我们的要求。

比如，把顶部的导航条改成黑色底，白色文字。

```
.navbar {
  background-color: #000;
}
.navbar-nav li a, .navbar-nav li a:focus, .navbar-nav li a:visited {
  color: #FFF;
}
```

其实这个效果完全不用这么麻烦，直接用一个 `Bootstrap` 自带的 `class` 就可以实现。我们在做页面的时候，**尽可能优先使用已有的组件、样式**，不要自己去写，一来节省时间，二来可以避免很多不可预料的问题。

[Bootstrap 反色导航条](http://v3.bootcss.com/components/#navbar-inverted)

#### 客户案例详情页

新建一个文件 `Home_case.html` ，客户案例详情页实际上和平时常见的 “新闻内容页”、“产品介绍页”非常类似，我们这里先做个简化版。最终效果如下：

![](http://upload-images.jianshu.io/upload_images/1644195-277dfb65749ca244.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 布局

把页面分成左右两栏，左边是**正文区域**，右边是**相关信息**，通过栅格系统来布局可以很容易实现。

```
<div class="container">
	<div class="row">
	 <div class="col-md-9">
	   <!--正文-->
	 </div>
	 <div class="col-md-3">
	    <!--相关信息-->
	 </div>
	</div>
</div>
```

#### 大标题与小标题

进入正文区域（在 `<div class="col-md-9">` 内部），首先添加大标题与小标题，在 `Bootstrap` 里有专门的类 `<div class="page-header">` 。
`<small>` 标签可以让里面的文本大小为父元素的 85%，比如下面的代码中， `<small>` 里面的文本大小，是 `<h1>` 里面其他文本大小的 85%。

![](http://upload-images.jianshu.io/upload_images/1644195-fca48b3f0a306b58.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
<div class="page-header">
      <h1>四光年科技<small>有价值的、有趣的信息服务</small></h1>
    </div>
```

#### 内容摘要——使用“引用”

![](http://upload-images.jianshu.io/upload_images/1644195-a0c5176f47176c28.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
<blockquote>
  <p>交给你全栈开发的一招一式，我们不会装作什么都懂，也不会教你花架子，只是能保证你学完后，拥有自己的一套内功心法，能举一反三，轻松写代码</p>
</blockquote>
```

#### 在正文内容区域使用各种文本效果

除了平时常用的 `<b>`（加粗）、`<i>`（斜体）、`<u>`（删除）等，还可以使用这几个更“语义化”的 HTML5 标签。

- 高亮 `<mark></mark>`
- 删除 `<del></del>`
- 着重 `<strong></strong>`
- 插入的文本 `<ins></ins>`

![](http://upload-images.jianshu.io/upload_images/1644195-2aee8898035a1d22.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
<p>
     <strong>程序员修炼之道</strong>
 </p>
 <p>
<mark>“衣带渐宽终不悔，为伊消得人憔悴”</mark>，编程大约有三个境界，新手、高手和<del>高不成低不就的中手</del>，适合新手的教程很多，指导中手的教程却很少；没有几十万行代码的锤炼或者长期在一个高手团队里打磨切磋，中手需要在这个层次“众里寻他千百度”，才能“蓦然回首”。 <ins>我们偏好实践，以正确的原则指导正确的行动</ins>
 </p>
```

另有几种文本样式不太常见，请自行阅读文档

[Bootstrap文档-内联文本元素](http://v3.bootcss.com/css/#type-inline-text)

#### 居中对齐

![](http://upload-images.jianshu.io/upload_images/1644195-48fa598db23f7628.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在正文中插入一张图片，默认是左对齐的。我们将它用一个 `<div class="text-center">` 包裹起来，这样它内部的所有元素都居中对齐了。

```
<p class="text-center">
     <img src="../assets/screenshot_1.jpg" class="img-thumbnail" alt="">
 </p>
```

实际上这个类的作用和下面的 CSS 规则产生的效果是一样的

```
.text-center {
	text-align: center;
}
```

#### 显示“代码”

如果这篇文章是和程序开发有关的，很有可能需要显示一段代码，为了和其他普通文本区分开来，我们要把代码用 `<code>` 或者 `<pre>` 包裹起来，前者是`行内代码`，后者是`块代码`

![代码.png](http://upload-images.jianshu.io/upload_images/1644195-a1fdad35411692bc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
<p>听说 PHP 很简单，常用的函数有<code>echo</code>、<code>is_array</code>、<code>mysql_connect</code>等等</p>
<p>
	例如
     <pre>
     // example
     if($a == 1){
         echo 'variable a = 1';
     }else{
         echo 'variable a = 2';
     }
     </pre>
 </p>
```

更多可以使用的`代码`样式，请参看文档

[Bootstrap文档-代码](http://v3.bootcss.com/css/#code)

#### 顶和踩——按钮的使用与外观

在文章的最后，我们可以让用户表达下自己的看法，是喜欢还是讨厌。这里添加两个按钮，一个是“顶”，一个是“踩”，并且用不同的颜色来区分。效果如下：

![](http://upload-images.jianshu.io/upload_images/1644195-f386ec8410d95287.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
在 `Bootstrap` 框架里，“按钮”这个组件十分常见，属性也比较复杂。我们先从最简单的“**默认按钮**”开始吧。

![](http://upload-images.jianshu.io/upload_images/1644195-aaf17559fbd446fa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
<button class="btn">基本按钮</button>
<button class="btn btn-default">默认按钮</button>
```

给一个元素（通常是`<button>`或`<a>`）添加 class `btn btn-default`，就形成了一个默认按钮。`btn-default`的样式是一个灰色的按钮外观。

为了让按钮显示不同的**颜色**来代表不同的含义，我们把`btn-default`修改成其他的类名。比如 `btn-danger` 表示“危险”，在外观上看来就是红色按钮；`btn-info`表示“信息”，是一个浅蓝色的按钮。

![](http://img.4guangnian.com/article_images/foreground/bootstrap/颜色按钮.png)

```
<button class="btn btn-primary">按钮</button>
<button class="btn btn-success">按钮</button>
<button class="btn btn-info">按钮</button>
<button class="btn btn-danger">按钮</button>
<button class="btn btn-warning">按钮</button>
<button class="btn btn-link">按钮</button>
```

通过添加`btn-lg`、`btn-xs`等 class，还可以调整按钮的**大小**。

![](http://upload-images.jianshu.io/upload_images/1644195-140423df902b5fd9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
<button class="btn btn-primary btn-xs">最小的按钮</button>
<button class="btn btn-primary btn-sm">小按钮</button>
<button class="btn btn-primary">普通大小按钮</button>
<button class="btn btn-primary btn-lg">加大按钮</button>
```

更多按钮的用法，可以在这里查看

[Bootstrap文档-按钮](http://v3.bootcss.com/css/#buttons)

知道如何灵活使用按钮组件后，回到我们的案例，添加两个在页面中居中的按钮，一个红色、一个蓝色。

```
<p class="text-center">
     <button class="btn btn-primary">顶</button>
     <button class="btn btn-danger">踩</button>
 </p>
```

#### 右侧——列表组件

我们最后来处理右侧的区域，这里有一张图片，下方是一个“相关内容”的列表，直接用`<ul><li>`列表元素会在每个列表项前面显示一个圆点，`Bootstrap`里有个作用于`<ul>`的`list-unstyled`类，可以隐藏这个圆点。

![](http://upload-images.jianshu.io/upload_images/1644195-e8c2ad1a346d775f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
<div class="col-md-3">
 <p>
     <img src="../assets/case_1.jpg" alt="..." class="img-circle">
 </p>
 <h3>相关内容</h3>
 <ul class="list-unstyled">
     <li><a href="">深圳市四光年信息技术有限公司</a></li>
     <li><a href="">深圳市腾讯计算机系统</a></li>
     <li><a href="">北京市百度互联网计算有限公司</a></li>
     <li><a href="">杭州市阿里巴巴集团</a></li>
 </ul>
</div>
```

#### 联系方式及意见反馈——使用表单

新建一个文件`Home_about.html`。关于”页面能够让潜在的客户联系自己，包括两块内容：公司信息（地址、联系方式），以及一个提交建议的**表单**。

#### 联系方式

我们可以直接使用“地址”标签(`<address>`)，这也是一个 HTML5 规范里的语义化标签。

这里还有个很有意思的`<abbr>`标签，给它添加一个`title`属性后，鼠标放在文本上面，会浮动显示一个小提示。

![](http://upload-images.jianshu.io/upload_images/1644195-cd898b1d42d0a787.gif?imageMogr2/auto-orient/strip)

```
<div class="container">
   <h2>联系方式</h2>
   <address>
       <strong>深圳市四光年信息技术有限公司.</strong><br> 深圳市南山区深南大道100号<br>
       <abbr title="Phone">联系电话:</abbr> 400-123-123
   </address>
</div>
```

#### 表单的骨架

普通的表单组件如果不添加任何样式，看起来是很粗糙的，通过给这些控件添加`Bootstrap`框架预设的`class`，可以马上让表单看起来更加专业、更美观。

先把这个表单的 HTML 代码写好（默认样式比较丑陋）。

![](http://upload-images.jianshu.io/upload_images/1644195-03a6ccd32e62e4a1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
<h2>建议</h2>
<form action="">
  <div>
      <label for="">姓名</label>
      <input id="truename" type="text" />
  </div>
  <div>
      <label>称呼</label>
      <input type="radio" checked />先生
      <input type="radio" />女士
  </div>
  <div>
      <label for="job">你的职位</label>
      <select name="" id="job">
          <option value="">开发者</option>
          <option value="">运营</option>
          <option value="">管理人员</option>
      </select>
  </div>
  <div>
      <label for="">你最喜欢”公众号管家“的哪个功能</label>
      <input type="checkbox" checked>文章高级排版
      <input type="checkbox">多公众号切换
      <input type="checkbox">素材集中管理
      <input type="checkbox">其他
  </div>
  <div>
      <label for="">更多建议</label>
      <textarea rows="3" cols=""></textarea>
  </div>
  <p>请不要超过500个字</p>
  <div>
      <button class="btn btn-primary">提交</button>
  </div>
</form>
```

#### 绑定 Bootstrap 样式

给`<form>`增加一个`role`属性，值为`form`，表示它是一个“表单”。

```
<form action="" role="form">
```

修改第一个`<input type="text">`输入框控件，先把包裹它的`<div>`添加一个类名`form-group`，然后给它自己添加一个类名`form-control`。

```
<div class="form-group">
      <label for="">姓名</label>
      <input class="form-control" id="truename" type="text" />
  </div>
```

**记住这两个 class**

`form-group`表示它内部的两个控件（`<label>`和`<input>`）**在功能上是一个整体**，“group”字面上就是组的意思。

再看`form-control`，表示让表单组件显示`Bootstrap`规定的样式。（不仅仅用于`<input>`，还包括`<textarea>`等）

我们把代码里所有的表单组件全部加上`class="form-control"`

![](http://upload-images.jianshu.io/upload_images/1644195-96aff528df0d3160.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

刷新下页面，比之前顺眼多了！已经显示了`Bootstrap`的样式。

#### 特殊的 checkbox 多选框和 radio 单选框组件

但是`checkbox`和`radio`好像有点奇怪——换行有错误。那是因为`checkbox`多选框、`radio`单选框和`<label>`一起用的时候，是不能直接添加一个`class="form-control"`类名的。

请仔细观察修改后的代码（看起来啰嗦了不少）。

![](http://upload-images.jianshu.io/upload_images/1644195-ba849e6ba2374460.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
<div class="form-group">
 <label for="">称呼</label>
 <div class="radio">
     <label>
         <input type="radio" checked />先生
     </label>
 </div>
 <div class="radio">
     <label>
         <input type="radio" />女士
     </label>
 </div>
</div>
<div class="form-group">
	 <label for="">你最喜欢”公众号管家“的哪个功能</label>
	 <div class="checkbox">
	     <label>
	         <input type="checkbox" checked>文章高级排版
	     </label>
	 </div>
	 <div class="checkbox">
	     <label>
	         <input type="checkbox">多公众号切换
	     </label>
	 </div>
	 <div class="checkbox">
	     <label>
	         <input type="checkbox">素材集中管理
	     </label>
	 </div>
	 <div class="checkbox">
	     <label>
	         <input type="checkbox">其他
	     </label>
	 </div>
	</div>
```

1. 首先要用一个 `<div class="checkbox>`或`<div class="radio>`把整个组件包裹起来
1. 然后用`<label>`把多选框/单选框（`<input type="checkbox>`或`<input type="radio">`）包裹起来（而普通的文本输入框中，`<label>`和`<input>`是并列的）
1. 最后一定要删掉`<input type="radio">`或`<input type="checkbox">`上面的`form-control`类名。

#### 让 label 和 input 水平布局，节省页面空间

“姓名”输入框看起来太长了，把整个页面宽度都占满了，有没有办法控制输入框的宽度呢？
还有`<label>`和`<input>`组件默认是从上到下垂直排列，每一项都占据了一整行，也挺浪费空间的。能不能让它们在同一行左右水平排列？

**首先在`<form>`上添加一个类名`form-horizontal`**，这一步很关键。

```
<form action="" class="form-horizontal" role="form">
```

刷新，咦，没变化？

那是因为虽然`<form>`通知了它里面的组件进行水平分布，但是这些组件还没有设置“宽度”。我们给`<label>`添加 `class control-label`和`col-md-宽度`，然后将`<input>`用一个`<div>`包裹起来，并给这个`<div>`设置一个固定的较小宽度，让它不再占满一整行的空间（例如`col-md-4`）。

```
<div class="form-group">
	 <label for="" class="col-md-2 control-label">姓名</label>
	 <div class="col-md-4">
	     <input class="form-control" id="truename" type="text" />
	 </div>
	</div>

	<div class="form-group">
	 <label for="" class="col-md-2 control-label">称呼</label>
	 <div class="col-md-4">
	     <div class="radio">
	         <label>
	         <input type="radio" checked />先生
	     </label>
	     </div>
	     <div class="radio">
	         <label>
	         <input type="radio" />女士
	     </label>
	     </div>
	 </div>
	</div>

	<!--略，将所有组件都修改成合适的宽度-->
```

好了，现在看起很紧凑了。

![](http://upload-images.jianshu.io/upload_images/1644195-07005f30778d3071.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

有关表单组件的更多资料，请阅读

[Bootstrap-支持的控件](http://v3.bootcss.com/css/#forms-controls)

#### 拒绝千篇一律——使用第三方主题

正因为`Bootstrap`框架如此流行，所以你在上网的时候会经常看到它（尤其是那个灰头土脸的默认风格出现次数特别多）。看多了就容易审美疲劳了。

我们可以使用一些第三方的`Bootstrap`主题，给我们的页面**换个漂亮的皮肤**。

打开 `https://bootswatch.com`这个网站，里面有很多免费的`Bootstrap`主题可以下载。

[Bootstrap主题](https://bootswatch.com/)

![](http://upload-images.jianshu.io/upload_images/1644195-6ea78c3c876b4d3f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

找一个你最喜欢的，点击“Download”按钮，会下载一个 `bootstrap.min.css`到本地。我们把 `assets`目录里旧的那个同名文件改成`bootstrap_default.min.css`（不要删除，以备以后可以恢复），然后把这个新的文件复制进去。

刷新页面，瞬间耳目一新！


> 源 [最好懂的 Bootstrap 实战案例教程](https://www.itjiaoshou.com/study-bootstrap.html)
