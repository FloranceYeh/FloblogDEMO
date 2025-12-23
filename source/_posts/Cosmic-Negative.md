---
title: Cosmic Negative
date: 2025-12-17 21:46:30
tags: Web
toc: false
width: 2
---

### 写好了网页的Light Mode
### 这种事为什么要单独开一篇文章来讲呢？

<!-- more -->

> 其实你或许已经发现了，网页的灯泡开关是隐藏的
> 那么这是何意味呢？

请你自己去发掘
当`Light Mode`被打开时，这篇文章后面的内容才会出现

<div id="HidedContent">
    <h1>宇宙负片</h2>
    <p>或许你已经发现了</p>
    <p>我写的Light Mode可以说是鬼畜</p>
    <p>竟然是直接简单粗暴地将背景反色</p>
    <p>但其实这背后的理念是宇宙负片</p>
    <p>正如这篇文章的题目：<code>Cosmic Negative（宇宙负片）</code></p>
    <p>所以我写的不是<code>Light Mode</code>，而是<code>Cosmic Negative Mode</code></p>
    <p>自己将宇宙干负片，这不是很帅吗，虽然是一片虚拟的宇宙，但也很浪漫不是吗</p>
</div>


<script>
    document.getElementById('HidedContent').style.display = "none"
    const show = setInterval(() => {
        if(darkmode.isActivated()) {
            document.getElementById('HidedContent').style.display = "block"
            clearInterval(show)
        }
    }, 500)
</script>


