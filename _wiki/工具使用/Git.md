---
title: Git
authos: admin
priority: 2.12

---

# Git使用方法

## 基本配置
在安装完后，用户需要设置自己的信息，即用户名和密码。为了使在远程的用户信息和本地保持一致，通常与Github的用户名和注册邮箱保持一致。

```bash
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
```
>注意`git config`命令的`--global`参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址，即去掉`--global`。
## Git基础命令
### 创建一个新的 git 仓库
创建一个新的 git 仓库，其数据会存放在一个名为 .git 的目录下
```bash
git init
```

### 显示当前的仓库状态
```bash
git status
```

### 添加文件到暂存区
```bash
git add <filename>: 
```

### 在当前分支上提交
```bash
git commit
```

### 显示历史日志
```bash
git log
```

可视化历史记录（有向无环图）
```bash
git log --all --graph --decorate
```


## Git分支与合并
### 创建一个新的分支
```bash
git branch <branch-name>
```

### 显示当前分支
```bash
git branch 
```

### 切换分支
```bash
git checkout <branch-name>
```

>在 Git 2.23 版本中，引入了一个名为 `git switch` 的新命令，最终会取代 `git checkout`

### 创建一个新的分支并切换过去
```bash
git checkout -b <branch-name>
```

### 将一个分支合并到当前分支
```bash
git merge <branch-name>
```

### 拷贝当前的一个分支到另外一个分支
```bash
git rebase <branch-name>
```




## Git资源

- [Pro Git](https://git-scm.com/book/en/v2)，学习前五章的内容可以流畅使用 Git 的绝大多数技巧。[(Pro Git 中文版)](https://git-scm.com/book/zh/v2)；
- [Learn Git Branching](https://learngitbranching.js.org/) 通过基于浏览器的游戏来学习 Git ；