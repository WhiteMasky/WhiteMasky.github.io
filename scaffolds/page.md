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