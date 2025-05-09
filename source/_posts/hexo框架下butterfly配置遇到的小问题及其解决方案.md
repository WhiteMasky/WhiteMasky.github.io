---
title: hexo框架下butterfly配置遇到的小问题及其解决方案
date: 2025-05-09 17:23:05
tags:
---

### hexo建站及使用Butterfly主题的Quick Start

1. 安装Node.js (含npm)，Win系统请从[官网](https://nodejs.org/) 下载，输入以下两条命令确认node与npm是否成果安装

```bash
node -v
npm -v
```

2. 全局安装Hexo框架

```bash
npm install -g hexo-cli
# 中国大陆镜像 npm install -g hexo-cli --registry=https://registry.npmmirror.com
```

3. 初始化Hexo

```bash
mkdir <username>.github.io
cd <username>.github.io
hexo init .
npm install
```

4. 配置Butterfly主题

```bash
git clone --depth=1 https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
```

修改根目录底下的`_config.yml` 里的主题属性值`theme: butterfly`

5. 本地预览，默认在`http://localhost:4000` 上运行

```bash
hexo clean
hexo generate 
hexo server
```

------

#### 本地预览时遇到pug相关报错

> extends includes/layout.pug block content include ./includes/mixins/post-ui

这是由于没有安装相关的包，在根目录运行以下指令

```bash
npm install hexo-renderer-pug hexo-renderer-stylus --save
```

#### 自动化部署的两种方式

A. Hexo 源代码和生成的静态文件在不同两个仓库，Github Actions里无需设置，配置`.github/workflows/deploy.yml` 即会自动尝试部署，不过本人屡次尝试仍然失败

B. 源代码和 Pages 站点托管在同一个仓库，可参考[官方文档](https://hexo.io/docs/github-pages)，配置`.github/workflows/pages.yml`，并且修改**Settings** > **Pages** > **Source** > **Github Actions**

#### Hexo部署时按照默认的Jekyll的工作流运行

> Error:  Logging at level: debug Configuration file: /github/workspace/./_config.yml Theme: butterfly github-pages 228 | Error: The butterfly theme could not be found

先在根目录下添加名为`.nojekyll` 的零字节空文件，再在`_config.yml` 里的include属性下添加

```yaml
include:          # <-- put it here (2 spaces indent)
  - .nojekyll
```

