---
layout: post
title: "TexturePacker和Unity3D插件Tang"
date: 2013-08-23 23:13
comments: true
categories: [Unity3D]
---

前段时间作者慷慨地赠送了一个license, 为了表示感谢，在此做强烈推荐。

TexturePacker是手机游戏开发中非常得力的工具,可以非常方便的把许多的图像资源合成一张大图,方便管理资源和提升性能,其中裁剪和旋转的功能非常实用。更详细请访问官方网站：[Code'n'Web](http://www.codeandweb.com/texturepacker)

使用TexturePakcer，可以在Unity3d加入自己的一些处理，让游戏的开发更加自动化。同事写了一个简单的Unity3D插件Tang。该插件参考了 [Orthello 2D Framework](http://u3d.as/content/wyrm-tale-games/orthello-2d-framework/1Z9) 的部分做法，AtlasCocos2DParser类用于解析TexturePacker所生成的数据文件。其核心代码开放在 [github](https://github.com/zhongzichang/tang)，欢迎大家试用，Fork或提交代码。
