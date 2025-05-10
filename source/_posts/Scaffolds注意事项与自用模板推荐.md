---
title: Scaffs注意事项与自用模板推荐
tags: []
categories: []
keywords: []
description: ''
top_img: ''
comments: true
cover: false
toc: true
toc_number: false
toc_style_simple: false
copyright: false
copyright_author: ''
copyright_author_href: ''
copyright_url: ''
copyright_info: ''
mathjax: false
katex: false
aplayer: false
highlight_shrink: false
aside: true
abcjs: false
noticeOutdate: false
date: 2025-05-10 02:30:18
updated: 2025-05-10 02:30:18
---

### scaffolds 的基本格式

```markdown
---
<content1>
<content2>
<content3>
---
# 不能多或者少 --- 不包含外面的代码框
# 否则报错 YAMLException: end of the stream or a document separator is expected (2:6)
```

### page.md

```markdown
---
title: {{ title }}
date: {{ date }}
reward:
description:
top_img: 
comments: false
abbrlink:
---
```

### page-full.md（全属性）

```markdown
---
title: {{ title }}
date: {{ date }}
updated: {{ date }}          # 默认与 date 保持一致，只在后续修改时手动更新 :contentReference[oaicite:6]{index=6}
type: ""                      # 默认空字符串，创建列表页时再设为 'tags'/'categories'/'link' :contentReference[oaicite:7]{index=7}
comments: true                # 默认开启评论模块 :contentReference[oaicite:8]{index=8}
description: ""               # 默认空字符串 :contentReference[oaicite:9]{index=9}
keywords: []                  # 默认空列表 :contentReference[oaicite:10]{index=10}
top_img: ""                   # 默认无顶部图片 :contentReference[oaicite:11]{index=11}
mathjax: false                # 默认不加载 MathJax :contentReference[oaicite:12]{index=12}
katex: false                  # 默认不加载 KaTeX :contentReference[oaicite:13]{index=13}
aside: true                   # 默认显示侧边栏 :contentReference[oaicite:14]{index=14}
aplayer: false                # 默认不加载 APlayer 播放器 :contentReference[oaicite:15]{index=15}
highlight_shrink: false       # 默认代码块不折叠 :contentReference[oaicite:16]{index=16}
random: false                 # 默认列表不随机排序 :contentReference[oaicite:17]{index=17}
limit:
  type: "num"                 # 默认按数量截取 :contentReference[oaicite:18]{index=18}
  value: 0                    # 默认不限制数量（0 表示无限） :contentReference[oaicite:19]{index=19}
---
```

### post.md

```markdown
---
title: {{ title }}
date: {{ date }}
tags: []                       # 默认空列表
categories: []                 # 默认空列表
keywords: []                   # 默认空列表
description: ""                # 默认空字符串
top_img: ""                    # 默认无顶图
comments: true                 # 默认显示评论模块 :contentReference[oaicite:6]{index=6}
cover: false                   # 默认不显示封面图
abbrlink:
---
```

### post-full.md（全属性）

```markdown
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
```

### draft.md

```markdown
---
title: {{ title }}
tags:
---
```

