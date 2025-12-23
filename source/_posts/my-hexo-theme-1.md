---
title: HEXO主题开发1
date: 2025-12-20 12:33:34
categories: Floblog
tags:
    - Web
    - HEXO
    - EJS
---

## 我的主题开发日志 1

因为ParticlX的功能实在太少了，逛遍了HEXO的themes市场也没找到中意的

想着与其把ParticlX改得面目全非，不如自己从头开始写一个（前期开发还是得仿照ParticleX）

这是我的寒假企划，预期一个月完成

既是给自己写一个心仪的主题，也是对自己能力的磨练

<!-- more -->

## 项目概述

初步命名为`Floblog`

目标是打造一个高度自定义的网格布局网页

> 其实是在市场上看到一个magazine主题，作者的理念挺好的，就是他做出来的主题和理念相差太多了
> 主题死板，bug巨多，码风我也不喜欢

### 进度

1. 大致框架
2. 可自定义内容位置的menu
3. footer
4. 主页posts容器框架（grid实现，目标是高度可自定义）

> 如果要量化的话就是5%的样子

### 短期阶段目标

1. 完善posts容器
2. 完善主页，做好窄屏适配

<details>
<summary>
我为什么执着于ParticleX？
</summary>

1. 我最早使用的HEXO主题就是ParticleX
   当时的我是高一，连html是什么都不知道
   想写博客的原因就是`机房的大佬都有博客`
2. 于是上网搜教程
   在HEXO主题市场“觅食”
   因为ParticleX最符合我的审美
   便用了
3. 用上了ParticleX后，也换过Butterfly，Next
   但是最终都换回了ParticleX
4. 到了高三，学业紧张，就没管博客
   那时候我对前端已经有点基础了，也给自己博客加了很多乱七八糟插件
5. 不过旧博客都是黑历史
   全删干净咯
6. 到现在，用ParticleX是情怀
   但是确实已经不满足于ParticleX了
   而且ParticleX的作者好久没更新了，我提交的pr也没人理
   最终决定自己写一个

</details>
