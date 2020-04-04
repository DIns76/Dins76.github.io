---
title: 这个Hello world不容易
date: 2020-04-01 23:24:01
tags: 
    - hexo
    - blog
    - Github Pages
    - Github Action
---
### source file and blog source merge test
### 重新搭建

  本来是已经搭好了在``username.github.io``的blog，但由于直接在源文件下直接练习git操作，导致无法用hexo再次编译了，所以想把文章提取出来然后重新搭建一次，这次边练边加上自动集成并部署的 ``Github Action`` 。
  从头开始使用hexo(因为已经安装过``nodejs``和``hexo``，这个步骤可以在网上查到)：
```
$ hexo init blog_src	#初始化hexo配置文件夹，blog_src为任意名称
INFO  Cloning hexo-starter https://github.com/hexojs/hexo-starter.git
INFO  Start blogging with Hexo!	#出现这条信息，即为成功

$ cd blog_src
$ hexo g	#生成本地blog
$ hexo s	#本地预览
INFO  Start processing
INFO  Hexo is running at http://localhost:4000 . Press Ctrl+C to stop.
	#输入以上网址查看没问题，开始复制以前的文章，以下**不可复制！**
$ cp ~/$(username).github.io/source/_post/hello-world.md ~/blog/source/hello-world.md
$ hexo clean
$ hexo g && hexo s	#生成后再次预览
$ vim ~/blog/_config.yml #没问题后修改blog/_config.yml里的URL,见下方解决方案;还有deployment（仓库页面 Clone and Download - Use SSH 里的地址）
	# Deployment
	## Docs: https://hexo.io/docs/deployment.html
	deploy:
  	type: 'git'
  	repository: git@github.com:$(username)/$(username).github.io.git
  	branch: master
$ hexo d	#部署，在线查看效果;不过注意这个会把username.github.io仓库下的master分支直接全部覆盖！
```
#### Github Action使用

  结合网上教程来看：配置好Action脚本后；本地写好文章，``git push`` 进github，``Github Action`` 检测到有变动，之前在本地输入 ``hexo cl && hexo g && hexo d`` 的命令直接在github上运行，然后直接部署到``Github pages`` 上。
  所以配置好Action后，只要``git push`` ，然后浏览器输入 ``username.github.io`` 就可以看到，push上去的文章了。
##### 新建空库

  先在Github上新建一个仓库，用于存放hexo init生成的源代码；username.github.io是hexo d推送的public/下的所有文件。
  本地把源代码生成的文件夹，改成与刚健的Github一致，然后初始化：
```
$ git init
	#如果新建的GitHub生成了README文件，或自己添加了其它文件:
$ git pull origin master --allow-unrelated-histories
	#如果是空库，直接使用
$ git remote add origin git@github.com:$(username)/$(Github_Pages_src)
$ git add --all
$ git commit -m "upload src file"
$ git push -u origin master	#即可完成远程与本地同步
```
##### 配置库和SSH key

  本地生成ssh key用于Action访问：
```
ssh-keygen -t rsa -b 4096 -f ~/.ssh/github-actions-deploy
```
  以上生成了一对key，后缀为``.pub``称为公钥，无后缀的为私钥；
1. 在 Github Pages 的仓库，**Settings -> Deploy keys** 添加刚刚生成的公钥，名称随意，但要勾选 **Allow write access** ；
2. 在新仓库的 **Settings -> Secrets** 里添加刚刚生成的私钥，名称自己能记住是什么意思就行。

##### 源码仓库添加 Actions 配置

  如果在网页编辑配置文件的话，选择 ``Set up a workflow yourself`` ;如果是在本地目录提交配置文件的话，将配置文件存至 .github/workflows/*任意名*.yml。
  还是根据以下参考改吧，我自己写的总是``paser error`` ，可能和YAML语法对空格 ``Tab键`` 比较严格，就像 ``Makefile`` 对 ``Tab`` 和空格严格一样。
具体参考：
 - [Github Actions 测试 - 自动部署 Hexo](https://xiaopc.org/2019/08/29/github-actions-%E6%B5%8B%E8%AF%95-%E8%87%AA%E5%8A%A8%E9%83%A8%E7%BD%B2-hexo/)
 - [GitHub Actions 入门教程](http://www.ruanyifeng.com/blog/2019/09/getting-started-with-github-actions.html)
 - [configuring-a-workflow](https://help.github.com/cn/actions/configuring-and-managing-workflows/configuring-a-workflow)


注意：
1. 更改git的user.name 和 user.email!!
2. 亲测，根据以上配置还有一个错误是： ``ERROR Deployer not found: git``
这个是没有安装hexo-deployer-git库，在安装hexo后加上：
```
          # install dependencies
          npm i -g hexo-cli
          npm i
          # install hexo-deployer-git
          npm install --save hexo-deployer-git
```
我写的改动很少，详见[github链接](https://github.com/DIns76/Github_Pages_src/blob/master/.github/workflows/build_and_update_gh_Pages.yml)

### 上次出现问题的现象

本地运行良好, ``_config.yml`` 配置也没什么问题，为什么一用 ``hexo d`` 部署好，到线上一查看，什么样式都没有，直接显示成只有文章超链接，点进去还是 ``page not found`` ......
最重要的是还把我原来的所有commit全部都直接覆盖了......
``hexo-deployer-git`` 这个npm模块，都没有询问机制的？

### 解决方案

结合一些参考链接，加上自己仔细回想对这个项目修改了哪？
看到教程和配置脚本上的注释都说要加个子页面，而我确实修改了 ``_config.yml`` 里的url设置，想着把它改回来：
```
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: https://dins76.github.io/ 
root: /

```
这么一改就改好了!!
改之前，导致不显示样式的设置:
```
url: https://dins76.github.io/blog/
root: /blog/

```

### 下一步

1. 尝试修改主题中的图和显示字体，字体看起来有点虚,可能加粗点可能会更好
2. ~~尝试把非public/下的所有的文件都传到GitHub上~~
3. ~~尝试``Travis CI``自动部署,或者直接尝试``Github Action``~~
4. 继续学习 ``Markdown`` 语法用于写作；或尝试其它支持github pages的编辑器
5. 继续学习 ``Git`` 使用
    - 了解git历史[10 years of git by atlassian](https://www.atlassian.com/git/articles/10-years-of-git)
    - [Pro Git_cn](https://git-scm.com/book/zh/v2)
    - [常用 Git 命令清单](https://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)

### 个人觉得简介明了的主题：

目前使用的主题[hexo-theme-fluid](https://github.com/fluid-dev/hexo-theme-fluid)
其它主题：
1. [Zcc's blog](https://wa-ri.github.io/)
2. [MaterialDesign风格主题 MDM](https://github.com/TonyChenn/mdm)
3. [PointingToTheMoon](https://github.com/yk-liu/PointingToTheMoon)
4. [hexo-theme-material-indigo](https://github.com/yscoder/hexo-theme-indigo)
5. [这个Next主题的背景动效有点意思](https://gythialy.github.io/deploy-hexo-to-github-pages-via-github-actions/)
6. [极简主题scribble](https://github.com/DIns76/scribble)
7. [两色主题Ghost's Casper // Jasper2](https://github.com/DIns76/jasper2)

### 其它参考链接
- [通過travis-ci或者GitHub Actions自動化部署GitHub Pages和Coding Pages](https://jerryc.me/posts/74006f42/#Travis-CI)
- [Hexo指令](https://hexo.io/zh-cn/docs/commands)
- [我为什么写博客？](http://beiyuu.com/why-blog)
- [使用Github Pages建独立博客](http://beiyuu.com/github-pages)
- [Bug分支](https://www.liaoxuefeng.com/wiki/896043488029600/900388704535136)
- [删除github中某个文件](https://blog.csdn.net/wudinaniya/article/details/77508229)
- [Hexo博客搭建](https://code004.ml/posts/how-to-build-a-hexo-blog/)
- [ Hexo+GitHub 搭建](https://zhuanlan.zhihu.com/p/60578464)
- [sspai](https://sspai.com/post/54608)
- [ref about netify](https://kuleyu.github.io/hexolog/post/31808.html)


致谢以上所有文章和开源项目贡献者
