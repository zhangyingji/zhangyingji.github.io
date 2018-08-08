### Zhang Yingji's Blog
blog.zhangyingji.cn

### GitHub Pages
开启本功能，首先新建仓库,仓库名为

```
# 用户名 + .github.io
zhangyingji.github.io
```

则GitHub Pages的功能默认开启

### Jekyll环境配置
##### 安装Ruby + DevKit

https://rubyinstaller.org/downloads/

##### JeKyll

```
# 安装
gem install jekyll
# 创建博客
jekyll new myblog

# 若是第一次安装，则还需要安装bundler
# gem install bundler

# 进入目录
cd myblog

# 安装bundler
# bundle install

# 启动本地服务
jekyll serve

# 输入127.0.0.1:4000查看本地效果
```

### 选择合适的主题

可以去Jekyll主题网站挑选，也可以在github上搜索关键字jekyll theme,clone他人的项目clone并修改，推送到远程仓库即可

### 撰写博客

1. 文章写在项目目录下的_posts文件夹中
2. 标题实例如下

```
2018-08-08-how-to-write-a-blog.md
```

3. 文章内容需包含YAML头信息

```
# 参考http://jekyllcn.com/docs/frontmatter/
---
layout: post
title: Blogging Like a Hacker
---
```

更多参考[官方文档](http://jekyllcn.com/docs/posts/)


### 推送博客

```
git add -A
git commit -m 'detail'
git push
```

### GitHub Pages 绑定二级域名
1. 在GitHub项目中创建CNAME文件，内容为指向的网址

```
blog.zhangyingji.cn
```

2. 在域名解析中添加记录，主机名为blog,记录类型为CNAME，记录值为你的github pages

```
# 不要忽略后面的 .
zhangyingji.github.io.