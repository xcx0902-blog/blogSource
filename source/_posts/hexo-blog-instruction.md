---
title: Hexo 博客搭建指南
date: 2023-02-04 13:28:20
tags:
  - Hexo
  - GitHub
  - Instruction
---

## 软件安装

1. [Git](https://git-scm.com/download/win)
2. [Node.js](https://nodejs.org/zh-cn/)

## 检查配置

启动 cmd，运行 `git --version`，`node -v`，`npm -v`。出现以下结果即为安装成功（版本号可能不同）。

![check-installation](/images/hexo-blog-instruction/check-installation.png)

## 安装 Hexo

新建一个文件夹，名称、位置随便（最好在非系统盘）。

进入该文件夹，右击打开 Git Bash，执行如下命令。

```bash
npm install hexo-cli -g
hexo init .
npm install
hexo server
```

打开浏览器，访问 `localhost:4000`，如果看到博客界面，即为搭建成功。如果在最后一步提示：

```
FATAL Port 4000 has been used. Try other port instead.
FATAL Something's wrong. Maybe you can find the solution here: https://hexo.io/docs/troubleshooting.html
```

表示端口 4000 已占用，运行 `hexo server -p <port-number>` 即可，其中 `<port-number>` 为自定义端口号，另外在访问时也要访问 `localhost:<port-number>`。

## 新建文章

在 Hexo 根文件夹运行 `hexo new "<post-name>"` 即可，其中 `<post-name>` 为文章名（后续可修改）。此时在 `source/_post` 文件夹下会多出一个 Markdown 文件，编辑它即可。

**注意**：文件头部用 `---` 包含的内容不要删除，它是文章的定义，例如本篇文章的头部就是：

```yaml
---
title: Hexo 博客搭建指南
date: 2023-02-04 13:28:20
tags:
  - Hexo
  - GitHub
  - Instruction
---
```

## 部署到静态网页

首先需要一个 [GitHub](https://github.com) 账号，没有的需要注册一个。

[新建一个仓库](https://github.com/new)，名称必须为 `<username>.github.io`，其中 `<username>` 为你的用户名。

然后，在 Hexo 根文件夹下的 `_config.yml` 中添加如下内容。

```yaml
deploy:
  type: git
  repository: git@github.com:<username>/<username>.github.io.git
  branch: main
```

**注意**：这里需要有 GitHub SSH Key，没有的请参照[这篇文章](/2023/02/04/github-ssh-key/)。

最后，运行 `hexo generate && hexo deploy` 即可。

**建议**：在部署前最好先在本地浏览一下（`hexo generate && hexo server`），以免出现问题。

## 迁移

### 去除 .gitignore 中的某些条目

在 Hexo 根文件夹有一个 .gitignore 文件，初始内容为：

```
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
_multiconfig.yml
```

将其改为：

```
.DS_Store
*.log
public/
.deploy*/
_multiconfig.yml
```

### 新建博客源码仓库

[新建一个仓库](https://github.com/new)，名称随便（最好为 `blogSource`，方便识别）。

在 Hexo 根文件夹下运行（Git Bash）：

```bash
git init
git remote add origin git@github.com:<username>/<blogSource-repo>.git
# <username> 用户名，<blogSource-repo> 源码仓库（刚才创建的）
echo "git add . && git commit -m 'Update blog source' && git push -u origin main" > updsource.sh
```

之后，在更新博客时，运行 `./updsource.sh` 即可上传到源码仓库。

### 迁移

同样先得安装必要软件（即 Git 与 Node.js），创建博客根目录，然后运行：

```bash
npm install hexo-cli -g
git clone git@github.com:<username>/<blogSource-repo>.git
```

就完成了迁移。
