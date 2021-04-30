---
title: Git常用命令
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

   

# Git返回之前版本

```js
git reset --hard {hash}
```

版本回退。

# Git报错：OpenSSL SSL_read: Connection was reset, errno 10054

有时候会在克隆，拉取项目，推送项目时报这个错，这是因为服务器的SSl证书没有经过第三方机构的签署，所以报错。解决办法如下：

```apl
git config --global http.sslVerify "false"
```

# Git常见的问题解决方法

问题
(1) 更新代码后显示： **`unable to unlink old ‘xxx/xxx/xx’ : invalid argument`**
问题原因：
要提交或更新的文件被系统线程占用
解决方法：
把相关服务暂停，重新pull代码
(2) 更新代码后显示： **`the following untracked working tree files would be overwritten by checkout`**
问题原因：
本地代码仓库目录下有untracked文件
解决方法：
如果没有需要上库的代码，直接执行 git clean -d -fx删除untracked文件
(3) 更新代码后显示：
**`your local changes to the following files would be overwritten by merge…`**
**`please move or remove them before you merge`**

问题原因：
新修改的代码之前未提交，可能被服务器上的代码覆盖
解决方法1：
保留本地修改，然后add/commit/push到远程仓库

```js
git stash					// 暂存本地修改
git pull origin master		// 拉取服务器最新代码
git stash pop				// 暂存代码恢复
```

解决方法2：
放弃本地修改 - 直接回退到上一版本，再拉取服务器最新代码

```js
git reset --hard			// 可加上 commit id
git pull origin master
```

(4) git pull的时候认证失败：
**`remote: invalid Login or password`**
**`fatal: Authentication failed for 'https://…'`**

问题原因：
账号密码失效或者是未登录
解决方法：
windows账户下，控制面板->用户帐户->windows凭据->修改git密码
(5) 版本回退git reset --hard {hash}后提示：
**`fatal: could not parse object "hash id"**`

问题原因：
切换到master分支后没有更新最新代码，git log不包含要reset的节点
解决方法：
更新代码后git log找到对应节点hash id再reset
(6) 切分支后提示文件有修改，撤销文件修改报错/对这个文件任何修改都报错
`**unlink of file ‘modifyFile.c’ failed. should I try again?(y/n)`**

问题原因：
与问题(1)一样，有线程占用要修改的文件，比如代码查看器等
解决方法：
把相关服务停了，重新处理
(7) git push后提示:
`**to https://.git**`
`**![rejected] localRepo->remoteRepo(fetch first)**`
`**error: failed to push some refs to 'https://.git’**`
`**Updates were rejected because the remote contain work that you do not have locally.`**

问题原因：
本地仓库不包含远程仓库修改
解决方法：
更新远程分支并重新add/commit/push
(8) git push后提示:
`**to https://.git**`
`**![rejected] localRepo->remoteRepo(fetch first)**`
`**error: failed to push some refs to 'https://.git’**`
`**Updates were rejected because the tip of your current branch is behind its remote couterpart. Integrate the remote changes bufore pushing again.`**

问题原因：
本地仓库节点落后于远程仓库节点，当然这可能是自己主动回退的
解决方法：
方案1：强推。覆盖远程分支，这样会使远程修改丢失，多人同一分支写作的时候不可取

```js
git push -u origin YOUR_BRANCH -f
```

方案2：重新拉取远程仓库merge再push。结合具体代码修改情况做处理

```js
git pull origin YOUR_BRANCH // 修改~
git push -u origin YOUR_BRANCH
```


方案3：直接推到新分支，原分支作废

```js
git push origin YOUR_BRANCH_NEW
	// 或者
git branch YOUR_BRANCH_NEW
git push -u origin YOUR_BRANCH_NEW

```

(9) git pull后提示
`**fatal: refuse to merge unrelated histories`**

问题原因：
出现这个问题的最主要原因还是在于本地仓库和远程仓库实际上是独立的两个仓库，如果一开始用git clone拷贝到本地就不存在这个问题。本地git init后尝试与远程分支关联
解决方法：
pull命令后加 --allow-unrelated-histories 来解决，合并两个独立启动仓库的历史

```js
git pull origin master --allow-unrelated-histories
```

(10) git checkout后提示:
`**error: cannot stat ‘file…’: Filename too long`**

问题原因：
如提示，文件名过长无法checkout。git 可以创建4096长度的文件名，然而在windows最多是260，因为git用了旧版本的windows api，导致出现这种情况。
解决方法：

```js
git config --global core.longpaths true 	// 去除文件名长度限制
```



(11) git pull后撤销:
问题原因：
主干分支当前跑不过等原因
解决方法：

```js
git reflog YOUR_BRANCH					// 查看当前分支操作记录
git reset --hard YOUR_BRANCH@{1}		// 回退到上一节点，拉取master之前
```

(12) git checkout filename后报错:
error: pathspec did not match any files known to git

问题原因：
git checkout filename回退未添加到缓存区的文件，但是对未track的文件不生效。git checkout未track文件git以为是切分支
解决方法：
更新如果不需要该文件，直接删除

```js
rm filename
```

# git查看当前的仓库地址

```js
git remote -v
```

# git查看当前仓库的基本信息

```js
git remote show origin
```

