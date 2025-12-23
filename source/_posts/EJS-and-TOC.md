---
title: 用EJS写自定义TOC
date: 2025-12-18 13:20:07
tags:
    - Web
    - EJS
    - HEXO
categories: Web
---

`ParticleX`主题依旧是什么都没有:(

又得自己动手写`TOC`

<!-- more -->

## 介绍

给`Hexo`博客添加自定义目录`（TOC - Table of Contents）`主要有两种思路：使用`Hexo`内置辅助函数和使用第三方插件。

下面我将通过 Hexo 内置 toc() 辅助函数 结合 EJS 模板 和 CSS/JS 来实现的方法。

### 添加EJS

为了便于项目管理和维护，建议是单独写EJS文件用于渲染TOC

### 先在文章渲染的位置后加入`toc.ejs`引用

`ParticleX`的是`post.ejs`

```js
...
<% if (page.toc) { %> <%- partial("toc") %> <% } %> 
// Hexo 内置功能，在 Front-Matters 里写 toc: true | false 就会有这个参数
```

> `Highlight.js`没有内置`ejs`语法高亮，只好用`js`的高亮
> !! 但是本文除特殊说明外所有`js`代码块都应是`ejs` !!

### 新建`toc.ejs`

```tree
your-theme/
├── layout/
│   ├── post.ejs
│   └── toc.ejs
```

## `toc.ejs`内容示例

内容很简单

```js
<aside class="toc-sidebar">
        <% if (page.toc !== false && toc(page.content)) { %>
            <div class="toc-wrapper">
                <div class="toc-header">
                    <i class="fa-solid fa-list"></i> 目录
                </div>
                <%- toc(page.content, { class: 'toc', list_number: false }) %>
            </div>
    
    // 下面的是额外功能，回到顶部和底部
    <div class="toc-nav-buttons">
                <a href="javascript:;" onclick="window.scrollTo({top: 0, behavior: 'smooth'});" class="toc-btn" title="回到顶部">
                    <i class="fa-solid fa-arrow-up"></i> 顶部
                </a>
                <a href="#comment" class="toc-btn" title="查看评论">
                    <i class="fa-solid fa-comments"></i> 评论
                </a>
            </div>
        <% } %>
</aside>
```

## `css`内容示例

最后只要添加`css`样式就完成了

```css
.toc-sidebar {
    width: 280px;
    position: sticky;
    top: 100px;
}
.toc-wrapper {
    background: #404a43;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.08);
    max-height: calc(100vh - 150px);
    overflow-y: auto;
}
.toc-header {
    font-weight: bold;
    font-size: 1.1em;
    margin-bottom: 10px;
    color: #5e966d;
    border-bottom: 1px solid #858585;
    padding-bottom: 8px;
}
.toc {
    list-style: none;
    padding-left: 0;
    line-height: 1.8;
    font-size: 0.95em;
}
.toc-child {
    list-style: none;
    padding-left: 15px;
}
.toc-link {
    display: block;
    color: #7b9e83;
    text-decoration: none;
    padding: 1px 2px;
    border-radius: 4px;
    transition: all 0.15s ease-in-out;
    border-left: 3px solid transparent;
}
.toc-link:hover {
    color: #b6f1b6;
    background-color: rgba(65, 246, 59, 0.05);
}
.content h1, 
.content h2, 
.content h3, 
.content h4, 
.content h5, 
.content h6 {
    scroll-margin-top: 70px; /* 菜单栏高度 */
}

/* 以下是回到顶部和底部按钮的样式 */

.toc-nav-buttons {
    margin-top: 15px;
    display: flex;
    gap: 10px;
}
.toc-btn {
    flex: 1;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    background: #404a43;
    color: #7b9e83;
    text-decoration: none;
    padding: 10px 0;
    border-radius: 8px;
    font-size: 14px;
    transition: all 0.3s ease;
    box-shadow: 0 4px 12px rgba(255, 255, 255, 0.08);
    cursor: pointer;
}
.toc-btn:hover {
    background: #a1bb9f;
    color: #c2f0c7;
    transform: translateY(-2px);
    box-shadow: 0 6px 16px rgba(255, 255, 255, 0.12);
}
.toc-btn i {
    font-size: 1.1em;
}
```

## 其他功能

你还可以通过 `JavaScript` 来监听滚动事件，并计算当前视口位置对应的标题，实现侧栏自动点亮的功能

具体代码实现也简单，这里就不展示了