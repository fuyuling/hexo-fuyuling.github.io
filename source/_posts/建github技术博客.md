---
title: How to build a personal independent blog
keywords: Hexo, Blog, GitHub
tags: [Hexo, Blog, GitHub]
description:    嫌弃github自带的wiki不好使, 很作的自己搭了个hexo仓库. 按惯例,第一篇博客便是 "如何使用Hexo在GitHub上搭建个人博客".具体步骤请点击read more.
date: 2017-09-26 10:29:33
---
## install hexo

利用 npm 命令即可安装。（在任意位置点击鼠标右键，选择Git bash）

``` bash
$ npm install -g hexo
```

问题
npm ERR! registry error parsing json 错误
可能需要设置npm代理,执行命令

```bash
$ npm config set registry http://registry.cnpmjs.org
```
hexo:command not found
删除刚刚安装的npm目录，重新执行命令npm install -g hexo安装hexo

## 创建hexo文件夹

安装完成后，创建hexo文件夹（如/Users/meirenfeng/lynn_workspace/hexo），执行以下指令，Hexo 即会自动在目标文件夹建立网站所需要的所有文件。

```bash
$ hexo init
```

## 安装依赖包

```bash
$ npm install
```

## 本地查看

现在我们已经搭建起本地的hexo博客了，执行以下命令，然后到浏览器输入localhost:4000看看。

```bash
$ hexo generate
```

```bash
$ hexo server
```

## 执行 hexo deploy 后,出现 error deployer not found:github 的错误
hexo 更新到3.0之后，deploy的type 的github需要改成git
repository路径: http://github.com/fuyuling/fuyuling.github.io.git （需要将https修改成http）还不行的话尝试
git@github.com:fuyuling/fuyuling.github.io.git路径
改了之后执行npm install hexo-deployer-git --save 安装hexo对于git的部署工具。

然后再部署试试!

这时候我们的博客已经部署到网上了，我们可以在浏览器地址输入栏输入我们的网址即可，如我的博客是：https://fuyuling.github.io/

## 安装theme

你可以到Hexo官网主题页去搜寻自己喜欢的theme。这里以hexo-theme-next为例

终端cd到 hexo 目录下执行如下命令：

$ git clone https://github.com/iissnan/hexo-theme-next themes/next
将blog目录下_config.yml里theme的名称landscape修改为next

终端cd到blog目录下执行如下命令(每次部署文章的步骤)：

```bash
$ hexo clean           //清除缓存文件 (db.json) 和已生成的静态文件 (public)
```

```bash
$ hexo g             //生成缓存和静态文件
```

```bash
$ hexo d             //重新部署到服务器
```

至于更改theme内容，比如名称，描述，头像等去修改blog/_config.yml文件和hexo/themes/next/_config.yml文件中对应的属性名称即可， 不要忘记冒号:后加空格。 NexT 使用文档里有极详细的介绍。
