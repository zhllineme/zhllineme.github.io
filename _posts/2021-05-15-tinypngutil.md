---
layout: post
title: "TinypngUtil"
subtitle: "A tool for tinypng to use free api key"
date: 2021-05-15
author: "雨冻住了"
header-style: text
tags: [tools, tinypng]
---

>  转载请注明出处： https://zhllineme.github.io/2021-05-15-tinypngutil

做了一个tinypng的工具库，<https://github.com/zhllineme/TinyPngUtil>

这是使用免费api key的TinyPng工具。支持多个api键。

- 按顺序验证key并自动设置下一个有效key

- 压缩后默认覆盖原始图像

- 打印压缩文件的层次目录

- 打印压缩文件的总数

- 免费次数用完后终止运行

TinyPng官网 : <https://tinypng.com/>

申请免费 api key ：<https://tinypng.com/developers>

一个密钥每月可以免费压缩最多500张图像，所以你可以申请多个密钥

# 安装

首先安装python，然后使用pip安装包。

```
pip install --upgrade tinify
pip install click
```

# 例子

申请了api key后，需要修改tinypng.py，填写所申请的api key。
> ting_keys = ["xxxxxxxxxxxxxxx"]  # API KEYS



- 帮助
```
python tinypng.py --help
```



- 压缩当前文件夹下的所有图片文件，不要包含子目录
```
python tinypng.py
```



- 压缩当前文件夹和子目录下的所有图片文件
```
python tinypng.py -r
```



- 按目标文件夹压缩所有图片文件，不包含子目录
```
python tinypng.py -d D:\github_project\TinyPngUtil
```



- 压缩单个文件
```
python tinypng.py -f D:\github_project\TinyPngUtil\test.png
```



- 压缩单个文件，指定宽度
```
python tinypng.py -f D:\github_project\TinyPngUtil\test.png -w 100
```