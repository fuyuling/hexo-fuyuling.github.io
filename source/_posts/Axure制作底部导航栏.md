---
title: Axure制作底部导航栏
keywords: Axure, BottomNavigationBar, app
tags: [Axure, BottomNavigationBar, app]
description: 据说这是做app必备工具,互联网公司的产品经理就是靠这个神工具叨逼叨逼RD们好好干活. 安装好后随意上手捣鼓了一下,貌似很easy的样子,便随手做个BottomNavigationBar...
  Axure RP是一个专业的快速原型设计工具。Axure（发音：Ack-sure），代表美国Axure公司；RP则是Rapid Prototyping（快速原型）的缩写。
date: 2017-10-12 17:12:03
---

## 用到控件：一个动态面板，两个button控件；


> 大概原理：（主要是动态面板的使用）

```
为两个button控件设置相同的selected显示样式（逐个添加），同时设置相同的selection group 名字；
点击时，赋予被点击控件selected属性，控件会显示其相应样式；
点击两个不同的button，显示其对应的动态子面板；
```

将动态面板拖至合适处，双击显示下面对话框：

![Axure制作底部导航栏](Axure制作底部导航栏/DynanicPanel.png)

添加子panel（实例中：index,mine）

![Axure制作底部导航栏](Axure制作底部导航栏/DynamicPanelStateManger.png)

制作底部menu

拖拽两个button控件设置相同的宽高属性，设置为一组控件.

![Axure制作底部导航栏](Axure制作底部导航栏/SelectedGroup.png)

为每一个button设置Selected style.

![Axure制作底部导航栏](Axure制作底部导航栏/SelectedStyles.png)


Add Cases,设置selected对应的子面板：

![Axure制作底部导航栏](Axure制作底部导航栏/CaseEditer.png)

![Axure制作底部导航栏](Axure制作底部导航栏/CaseEditer.png_1.png)

