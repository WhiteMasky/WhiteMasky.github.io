---
title: {{ title }}
date: {{ date }}
updated: {{ date }}            # 建议与 date 保持一致
tags: []                       # 默认空列表
categories: []                 # 默认空列表
keywords: []                   # 默认空列表
description: ""                # 默认空字符串
top_img: ""                    # 默认无顶图
comments: true                 # 默认显示评论模块 :contentReference[oaicite:6]{index=6}
cover: false                   # 默认不显示封面图
toc: true                      # 默认根据主题 config.toc.enable :contentReference[oaicite:7]{index=7}
toc_number: false              # 默认根据主题 config.toc.number :contentReference[oaicite:8]{index=8}
toc_style_simple: false        # 默认简洁模式关闭 :contentReference[oaicite:9]{index=9}
copyright: false               # 默认不显示版权模块 :contentReference[oaicite:10]{index=10}
copyright_author: "{{ config.author }}"        # 站点全局作者
copyright_author_href: "{{ config.author_url }}"# 作者链接
copyright_url: "{{ config.url }}"               # 文章原文链接
copyright_info: ""           # 默认无额外版权声明
mathjax: false               # 默认不加载 MathJax :contentReference[oaicite:11]{index=11}
katex: false                 # 默认不加载 KaTeX :contentReference[oaicite:12]{index=12}
aplayer: false               # 默认不加载 APlayer 音乐播放器 :contentReference[oaicite:13]{index=13}
highlight_shrink: false      # 默认代码块不折叠 :contentReference[oaicite:14]{index=14}
aside: true                  # 默认显示侧边栏 :contentReference[oaicite:15]{index=15}
abcjs: false                 # 默认不加载 ABCJS 乐谱渲染 :contentReference[oaicite:16]{index=16}
noticeOutdate: false         # 默认不显示过期提醒 :contentReference[oaicite:17]{index=17}
---

>  本文基于GPT-4o生成的内容微修

使用的是 Hexo + Butterfly 主题时，可以直接这样使用**Butterfly 主题自带的内建标签（Tag Plugins）功能**，比如 `{% note ... %}` 是，它用自定义标签来生成视觉提示块在文章中插入样式良好的“提示框”组件，像绿色信息框、橙色警告框等。

------

### ✅ `note` 语法结构说明：

```liquid
{% note [颜色] '[图标类名]' %}

内容（支持 Markdown / 其他 tag 插件）

{% endnote %}
```

| 参数                          | 含义                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| 颜色（如 green、orange、red） | 提示框的主题色                                               |
| 图标类名                      | 使用 Font Awesome 图标，如 `fas fa-rocket`、`fas fa-magic` 等 |

------

### ✅ 示例解释：

```liquid
{% note green 'fas fa-rocket' %}

{% post_link <URL:markdown文件名(无需扩展名)> '[显示的名称]' %}
...
{% endnote %}
```

这个会被渲染成一个**绿色卡片框 + 火箭图标**，里面包含文档的导航链接。链接通过 `post_link` 插件生成，自动指向你本地的文章。

{% note green 'fas fa-rocket' %}

{% post_link <URL:markdown文件名(无需扩展名)> '[显示的名称]' %}
...
{% endnote %}

------

### ✅ 可用颜色

Butterfly 默认支持以下几种颜色：

- `default`（灰）
- `primary`（蓝）
- `success`（绿）
- `info`（青）
- `warning`（橙）
- `danger`（红）

你可以简单用颜色名作为参数，例如：

```liquid
{% note danger 'fas fa-bug' %}
这里是一个警告信息
{% endnote %}
```

------

### ✅ 图标怎么写？

Butterfly 使用的是 [Font Awesome 5](https://fontawesome.com/icons?d=gallery&m=free) 图标系统，你可以在图标官网找到你喜欢的图标，然后写成：

```text
'fas fa-rocket'
'fas fa-magic'
'fas fa-exclamation-triangle'
```

------

### ✳️ 如何开启这功能？

Butterfly 已默认支持 `{% note %}` 标签，如果你使用的是这个主题且没有改动源代码，不需要额外安装插件。

但你需要在 `.md` 文件中 **不要用 hexo-renderer-marked**，而是使用推荐的：

```bash
npm uninstall hexo-renderer-marked
npm install hexo-renderer-markdown-it --save
```

否则某些标签插件可能不会生效。

------

Hexo 的 Butterfly 主题提供了丰富的内建标签插件（Tag Plugins）和功能组件，能让你在 Markdown 中方便地插入各种美观、实用的元素，**无需写 HTML**。主要是基于[Liquid](#liquid)的语法。下面是一份整理清单，涵盖了常用的功能类型及语法：

------

## 🧩 Butterfly 常见内建功能一览

| 类型         | 标签语法                                                     | 说明                                      |
| ------------ | ------------------------------------------------------------ | ----------------------------------------- |
| ✅ 提示框     | `{% note [color] [icon] %}...{% endnote %}`                  | 信息提示框（如 info / warning / success） |
| ✅ 折叠框     | `{% folding [title] %}...{% endfolding %}`                   | 折叠/展开的内容区域（类似 FAQ）           |
| ✅ 标签页     | `{% tabs [id] %}{% tab title1 %}...{% endtab %}{% tab title2 %}...{% endtab %}{% endtabs %}` | 插入可点击切换的标签页内容                |
| ✅ 文章链接   | `{% post_link [slug] [text] %}`                              | 文章内链，`slug` 是文件名或 permalink     |
| ✅ 引用代码   | `{% codeblock [title] [lang] %}...{% endcodeblock %}`        | 高亮显示代码块（可自定义标题）            |
| ✅ 引用文档   | `{% iframe url %}`                                           | 插入 iframe 页面，如 PDF / 网站           |
| ✅ 图表       | `{% mermaid %}...{% endmermaid %}`                           | 使用 Mermaid 插图（流程图、时序图等）     |
| ✅ 卡片引用   | `{% link [url] [title] [desc] [img] %}`                      | 生成外链卡片预览                          |
| ✅ 文章目录   | `{% toc %}`                                                  | 手动插入文章目录（可选）                  |
| ✅ 站点标签云 | `{% tagcloud %}`                                             | 显示标签云（可在页面中插入）              |

------

## 🔍 举几个例子

### 🔔 折叠内容

```markdown
{% folding 点击展开查看答案 %}
這裡是隱藏內容，點開才能看到。
{% endfolding %}
```

### 📊 Mermaid 图（需手动启用）

```markdown
{% mermaid %}
graph LR
A[起點] --> B{條件判斷}
B -- 是 --> C[結果1]
B -- 否 --> D[結果2]
{% endmermaid %}
```

在 `_config.butterfly.yml` 中启用：

```yaml
mermaid:
  enable: true
```

### 🔗 卡片链接

```markdown
{% link https://butterfly.js.org Butterfly 主題 快速、美觀、強大的 Hexo 主題 /img/logo.png %}
```

------

## ⚙️ 配置与文档地址

Butterfly 官方文档列出了所有支持的标签插件和样式，可以访问：

👉 <https://butterfly.js.org/>

特别建议查看这部分页面：

- [自定义标签插件](https://butterfly.js.org/posts/ceeb73f/#%E8%A8%98%E4%BA%8B%E5%B0%88%E7%94%A8%E6%A8%99%E7%B1%A4)
- [Mermaid 流程图教程](https://butterfly.js.org/posts/7f55a73f/)

### Liquid

**Liquid** 是一种 **模板语言**，最初由 Shopify 开发，用于将动态内容嵌入 HTML 中。它 **不是编程语言**，而是一种 **标记语言（markup language）**，常用于网站生成系统如：

- **Shopify** 电商平台
- **Jekyll** 静态博客生成器（Hexo 的竞争对手）
- **Hexo** 部分主题（如 Butterfly）也支持 Liquid
- **GitHub Pages**（使用 Jekyll 的网站）

------

### Liquid 的基本语法格式：

1. **输出内容（Output）**

   ```
   {{ variable_name }}
   ```

2. **逻辑语句（Tags）**

   ```
   {% if condition %}
     Show this
   {% endif %}
   ```

3. **循环（Loop）**

   ```
   {% for item in collection %}
     {{ item }}
   {% endfor %}
   ```

4. **过滤器（Filters）**

   ```
   {{ "hello" | upcase }} => "HELLO"
   ```

------

### 示例：

```liquid
{% if user.name %}
  Hello, {{ user.name | capitalize }}!
{% else %}
  Hello, guest!
{% endif %}
```

------

### 和 HTML 配合使用：

```html
<div class="product">
  <h2>{{ product.title }}</h2>
  <p>Price: ${{ product.price }}</p>
</div>
```

------

