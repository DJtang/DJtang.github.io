---
title: hexo+github搭建自己的博客
categories: [环境配置]
tag: [日常]
---
# 准备工作

## GitHub账号

注册一个github账号 

[GitHub申请账号](https://blog.csdn.net/yaorongke/article/details/119086305)

## 安装Git

 [Git安装(Windows)](https://blog.csdn.net/yaorongke/article/details/119085413)

## 安装NodeJS

[NodeJS安装及配置(Windows)](https://blog.csdn.net/yaorongke/article/details/119084295)

# 创建仓库

1. 在`GitHub`上创建一个新的代码仓库用于保存我们的网页。

点击`Your repositories`，进入仓库页面。

2. 点击`New`按钮，进入仓库创建页面。
3. 填写仓库名，格式必须为`<用户名>.github.io`，然后点击`Create repository`。
4. 访问我们的主页  https://djtang.github.io/

# 安装Hexo

采用`Hexo`来创建我们的博客网站，`Hexo` 是一个基于`NodeJS`的静态博客网站生成器，使用`Hexo`不需开发，只要进行一些必要的配置即可生成一个个性化的博客网站，非常方便。点击进入 [官网](https://hexo.io/zh-cn/)。

安装 `Hexo`

```
npm install -g hexo-cli
```

查看版本

```
hexo -v
```

创建一个项目 hexo-blog 并初始化

```
hexo init hexo-blog
cd hexo-blog
npm install
```

本地启动

```
hexo g
hexo server
```

# 更换主题

[官网推荐主题](https://hexo.io/themes/)

我使用的是[Keep](https://xpoet.cn/2020/04/Keep-%E4%B8%BB%E9%A2%98%E4%BD%BF%E7%94%A8%E6%8C%87%E5%8D%97/)

# 创建文章

```
hexo new post 测试文章
```

# 发布到GitHub Pages

安装`hexo-deployer-git`

```
npm install hexo-deployer-git --save
```

修改根目录下的 `_config.yml`，配置 `GitHub` 相关信息

```
deploy:
  type: git
  repo: https://github.com/yaorongke/yaorongke.github.io.git
  branch: main
  token: ghp_3KakcaPHerunNRyMerofcFd9pblU282FSbsY
```

# 静态图片

使用[PicX图床](https://picx-docs.xpoet.cn/tutorial/get-start.html)



参考：

[1]: https://blog.csdn.net/yaorongke/article/details/119089190	"GitHub Pages + Hexo搭建个人博客网站，史上最全教程"
[2]: https://keep-docs.xpoet.cn/usage-tutorial/quick-start.html	"hexo-theme-keep"

