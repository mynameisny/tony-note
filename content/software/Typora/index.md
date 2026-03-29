---
title: "Typora"
summary: "Typora"
description: "Typora"
keywords: "Typora"

date: 2026-03-25T14:09:16+08:00
lastmod: 2026-03-25T14:09:16+08:00

categories:
 - 软件
tags:
  - 软件
  - Software
---

### 在终端中用Typora打开文件

编辑`~/.zshrc`文件，添加这一行

> `-a` 是 macOS 中 `open` 命令的一个参数，意思是：指定用哪个应用（application）来打开文件

```bash
alias typora="open -a Typora"
```



生效配置

```bash
source ~/.zshrc
```



使用方法

```bash
typora README.md
```

