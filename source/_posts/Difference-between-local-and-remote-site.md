---
title: Difference between local and remote site
date: 2020-04-01 23:24:01
tags: hexo  github-pages
---

## 现象：

本地运行良好，_config.yml配置也没什么问题，为什么一用hexo d部署好，到线上一查看，什么样式都没有，直接显示成只有文章超链接，点进去还是page not found......
最重要的是还把我原来的所有commit全部都直接覆盖了......
hexo-deployer-git这个npm模块，都没有询问机制的？

## 解决方案

结合一些参考链接，加上自己仔细回想对这个项目修改了哪？
看到教程和配置脚本上的注释都说要加个子页面，而我确实修改了_config.yml里的url设置，想着把它改回来：
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

## 下一步

1. 尝试修改主题中的图和显示字体，字体看起来有点虚,可能加粗点可能会更好
2. 尝试把非public/下的所有的文件都传到GitHub上
3. 尝试Travis CI自动部署,或者直接尝试Github Action
4. 继续学习Markdown语法用于写作；或尝试其它支持github pages的编辑器
5. 继续学习git使用
    - 了解git历史[10 years of git by atlassian](https://www.atlassian.com/git/articles/10-years-of-git)
    - [Pro Git_cn](https://git-scm.com/book/zh/v2)

## 个人觉得简介明了的主题：

目前使用的主题[hexo-theme-fluid](https://github.com/fluid-dev/hexo-theme-fluid)
其它主题：
1. [Zcc's blog](https://wa-ri.github.io/)
2. [MaterialDesign风格主题 MDM](https://github.com/TonyChenn/mdm)
3. [PointingToTheMoon](https://github.com/yk-liu/PointingToTheMoon)
4. [hexo-theme-material-indigo](https://github.com/yscoder/hexo-theme-indigo)

## 其它参考链接
- [通過travis-ci或者GitHub Actions自動化部署GitHub Pages和Coding Pages](https://jerryc.me/posts/74006f42/#Travis-CI)
- [Hexo指令](https://hexo.io/zh-cn/docs/commands)
- [我为什么写博客？](http://beiyuu.com/why-blog)
- [使用Github Pages建独立博客](http://beiyuu.com/github-pages)
- [Bug分支](https://www.liaoxuefeng.com/wiki/896043488029600/900388704535136)
- [删除github中某个文件](https://blog.csdn.net/wudinaniya/article/details/77508229)
- [Hexo博客搭建](https://code004.ml/posts/how-to-build-a-hexo-blog/)
- [ Hexo+GitHub 搭建](https://zhuanlan.zhihu.com/p/60578464)

致谢以上所有文章和开源项目贡献者
