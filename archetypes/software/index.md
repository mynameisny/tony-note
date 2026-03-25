---
title: "{{ replace .Name "-" " " | title }}"
summary: "{{ .Name }}"
description: "{{ .Name }}"
keywords: "{{replace .Name "-" ","}}"

date: {{ .Date }}
lastmod: {{ .Date }}

categories:
 - 软件
tags:
  - 软件
  - Software
---
