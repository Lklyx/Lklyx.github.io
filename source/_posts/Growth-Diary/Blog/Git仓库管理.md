---
title: Git仓库管理
date: 2021/04/12
categories:
- [历练ing,Blog]
tags:
- Git

---

# Git使用

git bash命令窗口写命令：

1. 克隆远程仓库：

   ```js
   git cloen // 加仓库的地址
   ```

2. 本地仓库代码推送到远程仓库，需要先关联远程仓库：

   ```js
   git remote add origin // + 仓库地址
   ```

3. 每一次提交添加：

   ```js
   git add . // 提交所有，后面的点 . 代表所有本次新加的
   ```

4. 添加提交的说明，注释/说明。就是本次提交修改的类容的缩写，比如：

   ```js
   git commit -m "修改首页" // 在git上显示的就是修改首页。英文的双引号可以省略。
   ```

5. 提交。

   ```js
   git push // 提交到默认分支、或你现在切换的分支。
   git push origin master // 提交到master分支。加上origin就是指定提交的分支。
   ```

6. 查看当前分支：

   ```
   git branch
   ```

7. 查看仓库状态：

   ```
   git status
   ```

8. 切换分支：

   ```js
   git checkout // + 需要切换的分支名称
   ```

9. 合并分支：

   ```js
   git merge  // + 分支名。（在需要合并的分支上敲。在没写好的上面，合并写好的）
   ```

   

# Git报错：OpenSSL SSL_read: Connection was reset, errno 10054

有时候会在克隆，拉取项目，推送项目时报这个错，这是因为服务器的SSl证书没有经过第三方机构的签署，所以报错。解决办法如下：

```apl
git config --global http.sslVerify "false"
```

