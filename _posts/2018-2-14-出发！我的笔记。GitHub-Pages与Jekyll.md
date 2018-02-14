---
layout: post
title: 出发！我的笔记。GitHub-Pages与Jekyll
tags: [GitHub-Pages,Jekyll]
---

## 题记

作为一个萌新，在OI的道路上东一头西一头跌跌撞撞的前进时，我真的很不愿写Blog，一个原因是懒，还有一个原因是时间，最后一个原因是强迫症，看到广告就烦，看到乱七八糟的布局就难受。但现在发现不写Blog不行了，然后某位大佬给我姐安利了GitHub-Pages，于是我就在作死之路上狂奔了。

## 受众

1. 刚入门的OIer
2. 有一定动手能力的
3. 对广告感到厌恶的
4. 计较排版的

## 准备

### 软件（援引：http://blog.csdn.net/u013553529/article/details/54588010）：

Python，Ruby，Ruby-Dev，Jekyll，Bundle，Nodojs

| 需要安装的软件 | 执行的命令 Ubuntu && Debain | 执行的命令 macOS    |
| -------------- | --------------------------- | ------------------- |
| Ruby           | sudo apt install ruby       | brew install ruby   |
| Ruby-Dev       | sudo apt install ruby-dev   | 没有这个包          |
| Jekyll         | sudo gem install jekyll     | gem install jekyll  |
| Bundle         | sudo gem install bundle     | gem install bundle  |
| Nodejs         | sudo apt install nodejs     | brew install nodejs |
| Git            | sudo apt install git        | brew install git    |
| Python         | sudo apt install python     | brew install python |

Tips：brew的安装：

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Tips：似乎不用安装Ruby-Dev，Jekyll，Nodejs，在macOS环境的时候，我并没有安装这三个，在后续的步骤中，Jekyll也会自动被安装。

Tips：安装完后建议更改一下RubyGems源（援引：https://gems.ruby-china.org/）

```bash
gem update --system # 这里请翻墙一下
gem -v #显示RubyGems版本
gem sources --add https://gems.ruby-china.org/ --remove https://rubygems.org/
gem sources -l #显示RubyGems源，确保只有 gems.ruby-china.org
bundle config mirror.https://rubygems.org https://gems.ruby-china.org
```

### GitHub（援引：https://segmentfault.com/a/1190000002645623）：
1. 生成SSH秘钥：

   ```
   ssh-keygen -t rsa -C
   ```

   Tips：遇到一堆提示，一路Enter就行，但是如果以前生成过SSH秘钥，应该不必再Overwrite了。

2. 登陆Github, 添加 SSH：

* 打开![](http://wx1.sinaimg.cn/mw690/005ueW33ly1fofoitala3j305q08f0ss.jpg)

* 点击![](http://wx1.sinaimg.cn/mw690/005ueW33ly1fofoj336zdj306d0duaa7.jpg)

* 点击![](http://wx3.sinaimg.cn/mw690/005ueW33ly1fofomxvgewj30lb01nweb.jpg)

* 复制id_rsa.pub里的东西到Key里，不用管Title，点击Add SSH key![](http://wx4.sinaimg.cn/small/005ueW33ly1fofoqcfrkaj30lj0cf74h.jpg)

3. 测试：

   ```bash
   ssh -T git@github.com
   ```

   你将会看到：

   ```bash
       The authenticity of host 'github.com (207.97.227.239)' can't be established.
       RSA key fingerprint is **************************(一串数字与符号)
       Are you sure you want to continue connecting (yes/no)?
   ```

   选择 `yes`                        

   ```bash
       Hi username! You've successfully authenticated, but GitHub does not provide shell access.
   ```

   如果看到`Hi`后面是你的用户名，就说明成功了。

## 创建与本地环境搭建（援引：http://www.pchou.info/ssgithubPage/2014-07-04-build-github-blog-page-08.html）

### 个人主页

每个帐号只能有一个仓库来存放个人主页，而且仓库的名字必须是`username/username.github.io`，这是特殊的命名约定。你可以通过`http://username.github.io`来访问你的个人主页。

通过向导很容易创建一个仓库，并测试成功。不过，同样的，没有博客的结构。需要注意的个人主页的网站内容是在`master`分支下的。

然后别忘了用如下命令clone到本地

```bash
git clone git@github.com:username/username.github.io.git
```

Tips:username是你的GitHub用户名（下文同），尽量不要用HTTPS的方式clone

### 安装Bundle

直接使用下面命令即可：

```bash
$ gem install bundle
```

### Gemfile和Bundle安装

在更目录下创建一个叫`Gemfile`的文件，注意没有后缀，输入

```bash
source 'https://ruby.taobao.org/'
gem 'github-pages'
```

保存后，在命令行中执行

```bash
$ bundle install
```

命令会根据当前目录下的`Gemfile`，安装所需要的所有软件。这一步所安装的东西，可以说跟`github`本身的环境是完全一致的，所以可以确保本地如果没有错误，上传后也不会有错误。而且可以在将来使用下面命令，随时更新环境，十分方便

```bash
$ bundle update
```

使用下面命令，启动转化和本地服务：

```bash
$ bundle exec jekyll serve
```

## 使用现成的模板（援引：http://www.pchou.info/ssgithubPage/2014-07-04-build-github-blog-page-08.html）

博客基于`jekyll`，而新手往往摸不着头脑，幸好有一些现成的模板可以直接使用：http://jekyllthemes.org

直接下载压缩包，也可以使用如下命令clone到本地：

```bash
$ git clone https://github.com/*******/********.git
```

把克隆下来的文件拷贝到你自己的目录就行了，这样你就有一个现成的网站结构了。

## 发布

```
git add --all
git commit -m "first commit"
git push origin master
```

