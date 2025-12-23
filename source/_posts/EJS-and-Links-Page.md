---
title: 用EJS写自定义Links页
date: 2025-12-17 09:56:49
tags:
- Web
- EJS
- HEXO
categories: Web
toc: true
width: 4
---

由于ParticleX主题没有内置的Links页面，而是把友链整合到了主页的Card里，我个人不是很喜欢，而且Card能写的友链太少了，于是决定自己写一个Links页

<!-- more -->

> Particlex主题就是EJS写的，所以用EJS是首选

## 什么是EJS

`EJS（Embedded JavaScript）`是一个流行的 `JavaScript` 模板引擎，具有简单、灵活的模板语法，广泛应用于动态生成 `HTML` 内容

`简单来说，EJS是能嵌入JS的HTML`

所以语法也很简单，看看[EJS官网](https://ejs.co/)就大概能知道了

## 如何在自己的网站使用EJS

由于前人给我们栽了树，搭好了框架，我们可以直接在`themes\layout`目录写`EJS`

对于HEXO其他主题的用户，你需要安装 `Hexo` 支持 `EJS` 模板引擎的插件

```bash
npm install hexo-renderer-ejs --save
```

## 具体实现方法

(用Particlex实现，其他主题可以参考思路)

### 新建link页

```bash
hexo new page "links"
```

### 添加EJS模板

```tree
your-theme/
├── layout/
│   ├── links.ejs  # 新增：友链页面模板
│   └── layout.ejs
```

### 修改`themes\particlex\_config.yml`

```yml
menu:
    Home:
        name: house
        theme: solid
        link: /
    About:
        name: id-card
        theme: solid
        link: /about
    Archives:
        name: box-archive
        theme: solid
        link: /archives
    Categories:
        name: bookmark
        theme: solid
        link: /categories
    Tags:
        name: tags
        theme: solid
        link: /tags
    Links:
        name: link
        theme: solid
        link: /links
```

### 修改`layout.ejs`使其能用`links.ejs`渲染links页

> `Highlight.js`没有内置`ejs`语法高亮，只好用`js`的高亮
> !! 但是本文除特殊说明外所有`js`代码块都应是`ejs` !!

```js
<!-- 这是Particlex主题的EJS，不同主题写法可能不一样，但是原理相同 -->
<% 
    // is_xxxx()是HEXO内置的辅助函数，用于判断当前页面是否为目标
    // 而HEXO内置的只有home, home_first_page, post, page, archive, year, month, category, tag这几种
    // 要自定义page就用is_current(path, [strict])函数
    let type = "post";
    if (is_home()) type = "index";
    if (is_post() || is_page()) type = "post";
    if (is_category() || page.type === "categories") type = "categories";
    if (is_tag() || page.type === "tags") type = "tags";
    if (is_archive()) type = "archives";
    if (is_current("links")) type = "links";  // 添加links页
    // 这是渲染标题
    let title = page.title + " | " + config.title;
    if (is_home()) title = config.title;
    if (is_post() || is_page()) title = page.title + " | " + config.title;
    if (is_category()) title = "Categories: " + page.category + " | " + config.title;
    if (is_tag()) title = "Tags: " + page.tag + " | " + config.title;
    if (is_archive()) title = "Archives | " + config.title;
    if (is_current("links")) title = "Links | " + config.title; // links页标题
    ...
    <%- partial("import", { type }) %> // 使用 {type}.ejs 渲染页面
    ...
%>
...
```

完成之后在`themes\particlex\layout\links.ejs`随便写点东西就能看到页面正确渲染了:)

### `links.ejs`内容示例，实现读取友链列表

我的想法是读取一个包含友链格式的`yml`文件，
(其实本来是想用`json`的，但是`HEXO`好像比较喜欢`yml`)
创建文件`source\_data\links.yml`，样例如下

```yml
Friends:
    Florance1:
        name: Florance1
        url: https://Florance.top
        ava: https://Florance.top/images/avatar.jpg
        des: It's Florance!
    Florance2:
        name: Florance2
        url: https://Florance.top
        ava: https://Florance.top/images/avatar.jpg
        des: It's Florance!!

Tools:
    Florance3:
        name: Florance3
        url: https://Florance.top
        ava: https://Florance.top/images/avatar.jpg
        des: It's Florance?
    Florance4:
        name: Florance4
        url: https://Florance.top
        ava: https://Florance.top/images/avatar.jpg
        des: It's Florance??

```

然后根据这个样例写`links.ejs`

```js
<div id="archives">
    <div class="links-content">

    <% const linkData = site.data.links || {}; %>

    <% Object.keys(linkData).forEach(function(category) { %>
        // 分类标题
        <h2 class="link-category-title">
        <i class="fa fa-link"></i> // FontAwesome的图标
        <%= category %>
        </h2>

        <div class="link-navigation">
        // 遍历每个条目
        <% const items = linkData[category]; %>
        <% Object.keys(items).forEach(function(key) { %>
            <% const item = items[key]; %>
            
            <a href="<%= item.url %>" target="_blank" class="card">
            <div class="card-header">
                // 增加onerror处理，防止头像加载失败
                <img src="<%= item.ava %>" alt="<%= item.name %>" onerror="this.src='/images/avatar.jpg'">
            </div>
            <div class="card-body">
                <h3 class="card-title"><%= item.name %></h3>
                <p class="card-desc" title="<%= item.des %>"><%= item.des %></p>
            </div>
            </a>

        <% }); %>
        </div>
    <% }); %>
    </div>
</div>
```

### 当然，`css`可是`The Key`!


```css
.link-category-title {
    font-size: 1.5em;
    margin: 30px 0 15px 0;
    border-bottom: 2px solid #eee;
    padding-bottom: 10px;
}
.link-category-title i {
    margin-right: 10px;
}

.links-content {
    margin-top: 20px;
    margin-bottom: 40px;
}

.link-navigation {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 20px; 
    margin: 0 auto;
}

.card {
    width: 300px; 
    max-width: 100%; 
    background-color: var(--card-bg, #92ac9b);
    border-radius: 12px;
    box-shadow: 0 4px 10px rgba(255, 255, 255, 0.315);
    padding: 15px;
    transition: all 0.2s ease;
    text-decoration: none;
    color: inherit;
    display: flex;
    align-items: center;
    box-sizing: border-box;
    border: 1px solid rgba(255, 255, 255, 0.05);
}

.card:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 20px rgba(0,0,0,0.12);
}

.card-header {
    margin-right: 15px;
    flex-shrink: 0;
    display: flex;
    align-items: center;
}

.card-header img {
    width: 64px;
    height: 64px;
    border-radius: 50%;
    object-fit: cover;
    border: 2px solid #eee;
    background: #fff;
}

.card-body {
    flex: 1;
    overflow: hidden;
    min-width: 0;
}

.card-title {
    font-size: 1.1em;
    font-weight: bold;
    margin: 0 0 5px 0;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
    color: var(--text-color, #466753);
}

.card-desc {
    font-size: 0.85em;
    color: #5d6e62;
    margin: 0;
    line-height: 1.5;
    display: -webkit-box;
}
```

> 什么？你想看具体效果？点击菜单的Links就好了 :)