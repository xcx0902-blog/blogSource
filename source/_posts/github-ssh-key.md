---
title: GitHub SSH Key 使用指南
date: 2023-02-04 14:24:47
tags:
  - GitHub
  - Instruction
  - SSH Key
---

## 生成 SSH Key

打开 Git Bash，输入 `ssh-keygen -t rsa -C "<your-email>"`，配置均使用默认配置（直接回车）。

![generate](/images/github-ssh-key/generate.png)

## 检查是否生成成功

打开 `C:\Users\<Windows.Username>\.ssh\` 文件夹，如果里面有 `id_rsa` 和 `id_rsa.pub` 两个文件，即为成功。

## 添加 Key

打开 `id_rsa.pub`，复制里面的内容。打开 [GitHub SSH Key](https://github.com/settings/ssh/new)，按照下面的指示填写。

![add-new-key](/images/github-ssh-key/add-new-key.png)
