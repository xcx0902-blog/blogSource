---
title: Git 使用指南
date: 2023-02-05 17:46:49
tags:
  - Git
  - GitHub
  - Instruction
---

## 安装 Git

[Git 下载地址](https://registry.npmmirror.com/binary.html?path=git-for-windows/v2.39.1.windows.1/)

安装一路 Next 就行。

## 注册 GitHub

[注册链接](https://github.com/singup)

**注意**：在接下来的步骤中，`<username>` 表示用户名，`<email>` 表示注册时使用的电子邮件。

## 配置 Git

新建一个文件夹，例如 `git-study`。

在这个文件夹中，右键点击，找到 `Git Bash Here`，单击打开。

![git-bash](/images/git-instruction/git-bash.png)

在命令行里输入：

```bash
git config --global user.name "<username>"
git config --global user.email "<email>"
```

![git-config-username-and-email](/images/git-instruction/git-config-username-and-email.png)

## 创建 GitHub SSH Key

参见[这篇文章](/2023/02/04/github-ssh-key/)。

## Try to use Git!

### 创建代码仓库

在 [GitHub 上新建一个代码仓库（repository）](https://github.com/new)。

### 在本地新建一个空仓库

打开 Git Bash，输入 `git init; git branch -M main`。

![git-init-repository](/images/git-instruction/git-init-repository.png)

### 编写一些文件（如 README.md），并 Push 到 GitHub 原仓库

#### 编写 README

```bash
echo "# example-repo" >> README.md
```

#### Commit

```bash
git add README.md
git commit -m "Create README.md"
```

#### Setup remote repository

```bash
git remote add origin git@github.com:xcx0902/example-repo.git
```

#### Push to remote repository

```bash
git push -u origin main
```

#### Overall

```bash
echo "# example-repo" >> README.md
git add README.md
git commit -m "Create README.md"
git remote add origin git@github.com:xcx0902/example-repo.git
git push -u origin main
```

![git-commit-and-push](/images/git-instruction/git-commit-and-push.png)