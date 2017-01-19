---
title: 手把手教你封装属于自己的分段滚动视图(segmentScrollView)
date: 2016-04-15 13:26:29
category:
 -  Developer
 - Original
tags:
 - iOS
 - Objective-C

---

![](http://upload-images.jianshu.io/upload_images/1644195-b8cddb2b1a283229.gif?imageMogr2/auto-orient/strip)


<!-- more -->


> **依然推荐新手学习，这次的代码为Objective-C。**
>
>---
> 在本文中你将会学习到：
> * 封装
> * 懒加载
> * 协议/代理
> * KVO（键值观察者）
> * Target - Action 模式
> * 通过文本内容和字体计算Label的宽度或高度
>
>---

---

#### 结构如下：

![](http://upload-images.jianshu.io/upload_images/1644195-e671e44863e5814d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

#### 首先我们从 item 开始:

![](http://upload-images.jianshu.io/upload_images/1644195-7f89e11ca8726aa1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
*不包括下面橘黄色的杠杠！！*

上代码。
首先新建一个类，继承自UIView。我命名为：YCSegmentViewTitleItem
自定义一个初始化方法：
```
@interface YCSegmentViewTitleItem : UIView

///标题(我们希望可以后期更改标题)
@property (nonatomic,copy) NSString  *title;
///间距(我们希望可以控制如果有多个item他们文字的间距)
@property (nonatomic,assign) CGFloat  space;
……

- (instancetype)initWithFrame:(CGRect)frame title:(NSString *)title;

……

@end
```

意图是给它一个需要显示的字符串和它的位置，然后让它自己去搞定。

```
@interface YCSegmentViewTitleItem ()

……

@property (nonatomic,strong) UILabel *titleLabel;
@end

@implementation YCSegmentViewTitleItem

- (instancetype)initWithFrame:(CGRect)frame title:(NSString *)title {
    self = [super initWithFrame:frame];
    if (self) {
        self.space = 8;
        self.title = title;
    }
    return self;
}

……
@end
```

大家有没有发现，在这里进行了一些赋值，但是我们没有初始化titleLabel啊！
而且为毛线我们要给 `self.title` 赋值为`title` !
其实是这样的:

```
@implementation YCSegmentViewTitleItem

……

- (void)setTitle:(NSString *)title {
    _title = title;
    self.titleLabel.text = title;
    [self setNeedsLayout];
}

……

@end
```

我们实现了`title`属性的`setter`方法，在里面给实例变量`_title`赋值用来保存值，然后我们给`self.titleLabel.text`赋值为`title`, 最后希望它从新布局，因为可能会改变宽度啊。

那么`titleLabel`在哪初始化？

这里我用了懒加载的方法来初始化这个`titleLabel`：

```
@implementation YCSegmentViewTitleItem

………

- (UILabel *)titleLabel {
    if (!_titleLabel) {
        _titleLabel = [[UILabel alloc] initWithFrame:self.bounds];
        _titleLabel.textColor = _defaultTitleColor_Normal;
        _titleLabel.font = _defaultFont;
        _titleLabel.textAlignment = NSTextAlignmentCenter;
        [self addSubview:_titleLabel];
    }
    return _titleLabel;
}
@end
```

包括了初始化、颜色、字体、居中、添加为self的子视图等。。

>**！小贴士：**
>
>---
> Objective-C中的懒加载的写法是重写某一个属性的getter。因为有些情况下我们并不能够确定什么时候初始化一个数组或者字典。多数用在网络请求之后保存结果等。。万一这个数组或者字典你用不到呢？给它个内存空间多浪费呀。所以什么时候用什么时候初始化。
>注意！在getter中不要用`self.titleLabel`！会产生递归的。。。因为`self.titleLabel`实际上就是`[self titleLabel]`或`[self setTitleLabel:_]`~
>懒加载节省了系统响应时间，提升了系统性能，非常具有利用价值。( 虽然在本项目中没什么体现。。以后有机会详细讲解喽 )
>
>---

这样，一旦调用初始化方法，就完成了label的赋值操作等。接下来我们还需要布局：

```
……
#define _MinWidth  32
#define _MaxWidth  YCMainScreenWidth / 2
……
@implementation YCSegmentViewTitleItem

……

- (void)layoutSubviews {
    CGFloat buttonWidth = [self calcuWidth];
    self.frame = CGRectMake(self.x, self.y, buttonWidth + self.space, self.height);
    self.titleLabel.frame = CGRectMake(self.space / 2, 0, buttonWidth, self.height);
}

//在没有title为空的时候，返回最小宽度，不然就没有宽度了
- (CGFloat)calcuWidth {
    if (self.title == nil) {
///大家想一想，在初始化的时候我没有判断`title`是否为`nil`
///这样依然会初始化`titleLabel`
///我该怎么做来避免无用的初始化？
        return _MinWidth;
    }
    UIFont *font = self.font == nil ? _defaultFont : self.font;
    CGRect frame = [self.title boundingRectWithSize:CGSizeMake(_MaxWidth, self.height) options:(NSStringDrawingUsesLineFragmentOrigin) attributes:@{NSFontAttributeName: font} context:nil];
    CGFloat width = frame.size.width;
    return width > _MinWidth ? width : _MinWidth;
}
……

@end
```

然后我们希望在外界可以知道他应该具有的宽度，而且想要方便调用：

```
@interface YCSegmentViewTitleItem : UIView

……

+ (CGFloat)calcuWidth:(NSString *)title;

……

@end

@implementation YCSegmentViewTitleItem

……

+ (CGFloat)calcuWidth:(NSString *)title {
    YCSegmentViewTitleItem *item = [[YCSegmentViewTitleItem alloc] initWithFrame:(CGRectZero) title:title];
    return [item calcuWidth] + item.space;
}
……
@end
```

然后希望它被选中时候改变个颜色

```
@interface YCSegmentViewTitleItem : UIView
……
@property (nonatomic,assign) BOOL  highlight;
……
@end

@implementation YCSegmentViewTitleItem
……
- (void)setHighlight:(BOOL)highlight {
    _highlight = highlight;
    self.titleLabel.textColor = highlight == YES ? _hasHighlightColor == YES ? self.highlightColor : _defaultTitleColor_Highlight : _hasNormalColor == YES ? self.normalColor : _defaultTitleColor_Normal;
}
……
@end
```

然后我们还需要他能够触发点击事件：

```
@interface YCSegmentViewTitleItem : UIView
……
- (void)addTarget:(id)target action:(SEL)action;
……
@end

@interface YCSegmentViewTitleItem ()
{
    ……
    id   _target;
    SEL  _action;
}
……
@end

@implementation YCSegmentViewTitleItem
……
- (void)addTarget:(id)target action:(SEL)action {
    _target = target;
    _action = action;
}
……
@end
```

好了，我们已经保存了`target`和`action`，但是什么时候触发？！
我们希望点击内部并在内部抬起的时候让`target`去执行`action`，所以我们需要一个实例变量来记录是不是在内部点击……

```
@interface YCSegmentViewTitleItem ()
{
    ……
    BOOL _touchedFlag;
}
……
@end

@implementation YCSegmentViewTitleItem
……
- (void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event {
    UITouch *touch = touches.anyObject;///获取一个点击
    CGPoint touchPoint = [touch locationInView:self];///获取这个点击在哪个位置
    if (touchPoint.x >= 0 && touchPoint.x <= self.width && touchPoint.y >= 0 && touchPoint.y <= self.height) {
        [UIView animateWithDuration:0.1 animations:^{
            self.alpha = 0.2;
            //在里面点击的就是yes喽
            //而且改变一下透明度告诉用户：你点着我啦！
            _touchedFlag = YES;
        }];
    }
}
- (void)touchesEnded:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event {
    UITouch *touch = touches.anyObject;
    CGPoint touchPoint = [touch locationInView:self];
    if (touchPoint.x >= 0 && touchPoint.x <= self.width && touchPoint.y >= 0 && touchPoint.y <= self.height) {
        if (_touchedFlag) {
          //在里面抬起来而且标记还是YES，那么肯定是在里面点击在里面抬起啦。
            [_target performSelector:_action withObject:self];
        }
    }
    //恢复标记
     _touchedFlag = NO;
    //恢复透明度
    [UIView animateWithDuration:0.1 animations:^{
        self.alpha = 1;
    }];
}
……
@end
```

这样子主要接口实现就ok了~（半个UIButton的感觉有没有！但是UIButton并不是怎么写的）

---

#### 接下来是itemContent:

![](http://upload-images.jianshu.io/upload_images/1644195-ff2c59e452502aca.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](http://upload-images.jianshu.io/upload_images/1644195-8f6d8eaa3a71d2dc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这个itemContent实际上我命名为：YCSegmentItemsContentView。
它是承载item的容器，并且来布局item。
它来负责控制高亮哪一个item，或者传递出点击了哪个一个item的消息。

首先我们先自定义初始化方法：

```
@interface YCSegmentItemsContentView : UIView
……
- (instancetype)initWithFrame:(CGRect)frame titles:(NSArray <NSString *>*)titles;
……
@end
```

我们希望告诉它它应该显示在什么位置，并且显示多少个标题。剩下的让他自己去解决。

```
@interface YCSegmentItemsContentView ()
{
    CGFloat _buttonWidthSUM;
    YCSegmentViewTitleItem *_currentItem;
}
@property (nonatomic,strong) UIView *buttonContentView;
@property (nonatomic,strong) UIView *line;

@property (nonatomic,strong) NSMutableArray *buttonsArray;
@property (nonatomic,strong) NSMutableArray *buttonWidths;
@property (nonatomic,strong) NSArray *items;

@end

@implementation YCSegmentItemsContentView
……

- (instancetype)initWithFrame:(CGRect)frame titles:(NSArray<NSString *> *)titles {
    if (self = [super initWithFrame:frame]) {
        self.items = [titles copy];
        [self setupAllButtons];
    }
    return self;
}

- (void)setupAllButtons {
    self.backgroundColor    = [UIColor groupTableViewBackgroundColor];

    self.buttonContentView = [[UIView alloc] initWithFrame:CGRectZero];
    self.buttonContentView.backgroundColor = [UIColor whiteColor];
    [self addSubview:self.buttonContentView];

    self.line = [[UIView alloc] initWithFrame:CGRectZero];
    self.line.backgroundColor = [UIColor orangeColor];
    [self addSubview:self.line];

    ///遍历所有的标题，（我这里`self.items`明明有歧义。。）
    for (NSString *title in self.items) {
        ///初始化一个`item`
        YCSegmentViewTitleItem *item = [[YCSegmentViewTitleItem alloc] initWithFrame:(CGRectZero) title:title];
        [item addTarget:self action:@selector(buttonAction:)];//添加点击事件
        [self.buttonsArray addObject:item];//添加到数组中
        [self.buttonContentView addSubview:item];

        ///计算`item`的宽度
        CGFloat width = [YCSegmentViewTitleItem calcuWidth:title];
        ///保存宽度以备布局（NSArray只能保存对象类型）
        [self.buttonWidths addObject:[NSNumber numberWithDouble:width]];
        ///计算所有item的宽度和
        _buttonWidthSUM += width;
        if (_currentItem == nil) {
            /// 默认高亮第一个item，当`_currentItem`第一次赋值之后就跳过
            _currentItem = item;
            item.highlight = YES;
        }
    }
}

……
///懒加载又出现了
- (NSMutableArray *)buttonsArray{
    if (!_buttonsArray) {
        _buttonsArray = [NSMutableArray array];
    }
    return _buttonsArray;
}
- (NSMutableArray *)buttonWidths{
    if (!_buttonWidths) {
        _buttonWidths = [NSMutableArray array];
    }
    return _buttonWidths;
}
@end
```

保存所有`item`的宽度和宽度和是为了我们希望`item`的宽度跟随内容，并且`item`之间的距离是等宽的。（item有space属性，是不是没有用到？- - 确实没啥子用哈~）

接下来是布局

```
@implementation YCSegmentItemsContentView
……

- (void)layoutSubviews {

    CGFloat height = self.bounds.size.height;
    CGFloat width  = self.bounds.size.width;

    self.buttonContentView.frame = CGRectMake(0, 0, width, height - 2);

    CGFloat spacing = 0;
    if (_buttonWidthSUM >= width) {
        spacing = 0;
    } else {
        spacing = (width - _buttonWidthSUM) / (_buttonWidths.count + 1);
    }
    for (int x = 0; x < self.buttonsArray.count; x++) {
        YCSegmentViewTitleItem *item = self.buttonsArray[x];
        CGFloat buttonWidth = [self.buttonWidths[x] doubleValue];
        if (x == 0) {
            第一个`item`不考虑上一个`item`（因为没有嘛。。）
            item.frame = CGRectMake(spacing, 0, buttonWidth, _buttonContentView.bounds.size.height);
        } else {
            每一个`item`的布局依照上一个`item`
            YCSegmentViewTitleItem *lastItem = self.buttonsArray[x - 1];
            item.frame = CGRectMake(spacing + lastItem.frame.origin.x + lastItem.frame.size.width, 0, buttonWidth, _buttonContentView.bounds.size.height);
        }
    }
    self.line.frame = CGRectMake(_currentItem.frame.origin.x, self.buttonContentView.bounds.size.height, _currentItem.bounds.size.width, 2);
}

……
@end
```

布局完成了。。接下来呢我们想要通过外接知道当前应该选中哪一个`item`，并且也希望告诉外接主动选择了哪一个`item`，怎么告诉？！用代理或者block都可以。在这里我们选择代理：

```
@protocol YCSegmentItemsContentViewDelegate;

@interface YCSegmentItemsContentView : UIView
……
@property (nonatomic,assign) id<YCSegmentItemsContentViewDelegate> delegate;
@property (nonatomic,assign) NSInteger page;

……
@end

@protocol YCSegmentItemsContentViewDelegate <NSObject>

- (void)didSelectedButtonAtIndex:(NSInteger)index;

@end
```

```
@implementation YCSegmentItemsContentView
……
///这是每一个item的点击事件
- (void)buttonAction:(YCSegmentViewTitleItem *)sender {
    NSInteger index = [self.buttonsArray indexOfObject:sender];
    [self setPage:index];
    if (self.delegate && [self.delegate respondsToSelector:@selector(didSelectedButtonAtIndex:)]) {
        [self.delegate didSelectedButtonAtIndex:index];
    }
}

- (void)setPage:(NSInteger)page {
    if (_page == page) {
        return;
    }
    _page = page;
    [self moveToPage:page];
}
- (void)moveToPage:(NSInteger)page {
    if (page > self.buttonsArray.count) {
        return;
    }
    YCSegmentViewTitleItem *item = self.buttonsArray[page];
    _currentItem.highlight = NO;
    _currentItem = item;
    item.highlight = YES;
    [UIView animateWithDuration:0.2 animations:^{
        CGRect buttonFrame = item.frame;
        CGRect lineFrame = self.line.frame;
        lineFrame.origin.x = buttonFrame.origin.x;
        lineFrame.size.width = buttonFrame.size.width;
        self.line.frame = lineFrame;
    } completion:^(BOOL finished) {
        if (finished) {
        }
    }];
}
……
@end
```

外界设置代理之后，就可以让代理去执行我们想要让他执行的协议方法，但在这之前，需要确定代理是否存在，代理有没有实现协议方法。否则会崩溃哦。

好了，现在这个控件也可以实现和其他控件的交互了。

---
#### 接下来是segmentView


![](http://upload-images.jianshu.io/upload_images/1644195-c7d89acb29388dc9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这个黑色可部分是collectionView，因为他自由度比较高，简单易用~
`segmentView`将`item`和`itemContent`结合在一起：

以下是初始化以及布局：

```
///接口部分：
@interface YCSegmentView : UIView

///非选中颜色
@property (nonatomic,strong) UIColor *normalColor;
///选中颜色
@property (nonatomic,strong) UIColor *highlightColor;
///字体
@property (nonatomic,strong) UIFont  *font;

- (instancetype)initWithFrame:(CGRect)frame titleHeight:(CGFloat)height viewControllers:(NSArray <UIViewController *> *)viewControllers;

@end
```

```
@implementation YCSegmentView
……

- (instancetype)initWithFrame:(CGRect)frame titleHeight:(CGFloat)height viewControllers:(NSArray<UIViewController *> *)viewControllers {

    if (self = [super initWithFrame:frame]) {
        _titleHeight = height;
        _viewControllers = viewControllers;
        [self setupAllViews];
    }
    return self;
}

/*
因为我们想让用户更加方便使用，
所以希望用户只需要传入视图控制器，
就可以完成控件的初始化，
控制器有`title`属性。
我们就可以直接取到控制器的标题来初始化`itemContent`
*/

- (void)setupAllViews {
    NSMutableArray *titles = [NSMutableArray arrayWithCapacity:_viewControllers.count];
    for (UIViewController *vc in _viewControllers) {
        [titles addObject:vc.title];
    }

    self.titleView = [[YCSegmentItemsContentView alloc] initWithFrame:CGRectZero titles:titles];
    self.titleView.delegate = self;
    [self addSubview:self.titleView];

    self.cLayout = [[UICollectionViewFlowLayout alloc] init];

///设置collectionView的滚动方式为水平滚动
    self.cLayout.scrollDirection = UICollectionViewScrollDirectionHorizontal;
    self.collectionView = [[UICollectionView alloc] initWithFrame:(CGRectZero) collectionViewLayout:self.cLayout];

///这是collectionView按页滚动
    self.collectionView.pagingEnabled = YES;
    self.collectionView.delegate = self;
    self.collectionView.dataSource = self;

///注意！这里为`collectionView`注册`cell` (YCSegmentViewUnit)，下文提到。
    [self.collectionView registerClass:[YCSegmentViewUnit class] forCellWithReuseIdentifier:@"YCSegmentViewUnit"];

///注意！这里为`collectionView`添加观察者，观察属性`contentOffset`的变化，来获得页数，控制`itemContent`选择哪一个`item`
    [self.collectionView addObserver:self forKeyPath:@"contentOffset" options:(NSKeyValueObservingOptionNew) context:nil];
    [self addSubview:self.collectionView];
}

- (void)layoutSubviews {
    self.titleView.frame = CGRectMake(0, 0, self.frame.size.width, _titleHeight);
    self.collectionView.frame = CGRectMake(0, _titleHeight, self.frame.size.width, self.frame.size.height - _titleHeight);
}

……
@end
```

还有重写KVO发现属性变化后会调用的方法：

```
……
- (void)observeValueForKeyPath:(NSString *)keyPath ofObject:(id)object change:(NSDictionary<NSString *,id> *)change context:(void *)context {

    CGPoint offset = self.collectionView.contentOffset;
///这里` + 0.5` 是为了当滚动到页面一半的时候，就已经算作下一页或者上一页
    CGFloat pageFloat = offset.x / self.collectionView.bounds.size.width + 0.5;
    if (pageFloat < 0) {
        pageFloat = 0;
    }
    if (pageFloat > _viewControllers.count) {
        pageFloat = _viewControllers.count;
    }
    NSInteger page = (NSInteger)pageFloat;
    self.titleView.page = page;
}
……
```

在类的延展中有这样一些属性和变量：

```
@interface YCSegmentView ()<UICollectionViewDelegate, UICollectionViewDataSource, UICollectionViewDelegateFlowLayout, YCSegmentItemsContentViewDelegate>
{
    NSArray *_viewControllers;//用来保存所有的控制器
    CGFloat  _titleHeight;//用来保存`itemContent`的高度
}
@property (nonatomic,strong) UICollectionViewFlowLayout *cLayout;
@property (nonatomic,strong) UICollectionView *collectionView;
@property (nonatomic,strong) YCSegmentItemsContentView *titleView;

@end
```

剩下的就是实现`collectionView`的协议方法，以及`itemContent`的协议方法：

```

- (NSInteger)numberOfSectionsInCollectionView:(UICollectionView *)collectionView {
    return _viewControllers.count;
}

- (NSInteger)collectionView:(UICollectionView *)collectionView numberOfItemsInSection:(NSInteger)section {
    return 1;
}

- (UICollectionViewCell *)collectionView:(UICollectionView *)collectionView cellForItemAtIndexPath:(NSIndexPath *)indexPath {
    YCSegmentViewUnit * cell = [collectionView dequeueReusableCellWithReuseIdentifier:@"YCSegmentViewUnit" forIndexPath:indexPath];
    UIViewController *vc = _viewControllers[indexPath.section];
    if (!vc.isViewLoaded) {
        [vc loadViewIfNeeded];
    }

    cell.view = vc.view;

    return cell;
}

- (CGSize)collectionView:(UICollectionView *)collectionView layout:(UICollectionViewLayout *)collectionViewLayout sizeForItemAtIndexPath:(NSIndexPath *)indexPath {
    return collectionView.bounds.size;
}

- (void)didSelectedButtonAtIndex:(NSInteger)index {
    CGFloat width = self.collectionView.bounds.size.width;
    [self.collectionView setContentOffset:(CGPointMake(width * index, 0)) animated:YES];
}

```

接下来我们看一下`YCSegmentViewUnit`类的代码：

```
@interface YCSegmentViewUnit : UICollectionViewCell

@property (nonatomic,strong) UIView *view;

@end

@implementation YCSegmentViewUnit

- (void)setView:(UIView *)view {
    if (_view) {
        [_view removeFromSuperview];
    }
    [self.contentView addSubview:view];
    [self setNeedsLayout];
    _view = view;
}

- (void)layoutSubviews {
    self.view.frame = self.contentView.bounds;
}

@end
```

当我们为cell的`view`属性赋值的时候，需要考虑当前的_view是否存在，如果存在就从`contentView`上移除，然后将新传入的`view`添加到`contentView`上，然后设置`view`的位置和大小贴合`contentView`。
最后千万不要忘了，`_view = view`，因为我们需要实力变量保存当前的`view`!

这样这个控件的封装就搞定啦~

**不！还有非常重要的一点！**
我们使用了KVO对`collectionView`进行了属性观察，但是如果观察着被释放了，肯定会出现问题，所以我们需要在`YCSegmentView`中重写`- (void)dealloc`方法，在dealloc中移除对collectionView的观察：

```
- (void)dealloc {
    [self.collectionView removeObserver:self forKeyPath:@"contentOffset"];
}
```

恩，这样子就大功告成了，我们实例化一个看一看~~

```
@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];

    HomeViewController *vc1 = [[HomeViewController alloc] init];
    vc1.title = @"首页";

    RankViewController *vc2 = [[RankViewController alloc] init];
    vc2.title = @"榜单";

    MasterViewController *vc3 = [[MasterViewController alloc] init];
    vc3.title = @"达人";

    ChoicenessViewController *vc4 = [[ChoicenessViewController alloc] init];
    vc4.title = @"每周精选";


    YCSegmentView *view = [[YCSegmentView alloc] initWithFrame:CGRectMake(0, 20, self.view.bounds.size.width, self.view.bounds.size.height) titleHeight:44 viewControllers:@[vc1, vc2, vc3, vc4]];
    view.highlightColor = [UIColor orangeColor];
    [self.view addSubview:view];
}

```

![](http://upload-images.jianshu.io/upload_images/1644195-b8cddb2b1a283229.gif?imageMogr2/auto-orient/strip)

没错，就是这个样子~

>源码：https://github.com/ilakeYC/YCSegment

---
