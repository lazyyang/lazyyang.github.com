---
layout: post
title: "loadView与viewDidLoad的区别"
date: 2014-06-26 09:30:33 +0800
comments: true
categories: 
---

**观察下面这个例子会出现什么结果**  

{% highlight objc linenos %}

-(void)loadView
{
	NSLog(@"who am i");
}

-(void)viewDidLoad
{
    self.view.backgroundColor = [UIColor redColor];
}

{% endhighlight %}



<!--more-->
分析：发现loadView和viewDidload会一直循环调用，原因何在   

我们发现只要self.view为nil，它就会调用一次loadview    

于是我们猜想_view的getter方法里是这样写的   

```
if(_view == nil)
{
...
   [self loadView];
   [self viewDidLoad];
...
}

```

下面是一涨生命周期的图：

![](https://raw.githubusercontent.com/lazyyang/lazyyang.github.com/source/source/images/img/lifeCircle.jpg)
