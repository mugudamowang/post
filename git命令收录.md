---
title: git命令收录
date: 2020-02-09 16:37:01
tags: git,github
categories: 学习笔记
---

### 本地git

---

1. git init 初始化本地仓库（最好新建文件夹、避免在桌面新建.git，导致最终提交的是整个桌面文件）
2. git status \\  git status -sb 显示文件状态
3. 进行文件修改、添加等
   - touch 文件名 生成文件
   - rm -rf \\ rm -f \\ rm 文件名 删除文件
4. git add 【-A】\文件名 全部添加\添加文件到stage区 
5. git commit -m '注释' 提交变动到仓库 
6. history 查看全部操作历历史
   git log 提交操作历史



### 上传到github

---

1. 创建新仓库（不填写description，不出创建readme）

   - 命名最好与本地一致

2. 关联一个远程库，使用命令
   git remote add origin git@server-name:path/repo-name.git；

   关联后，使用命令
   git push -u origin master第一次推送master分支的所有内容；

3. 刷新即可





### github下载到本地 

---

###### 下载github仓库：

1. 粘贴地址（ssh或https）
2. git clone 地址
3. 完成

###### github远程仓库强制覆盖本地代码：

```bash
	git fetch --all //获取远程仓库的代码到本地

​	git reset --hard HEAD //强制覆盖到本地
```

git reset将主分支重置为您刚刚获取的内容

 --hard选项更改工作树中的所有文件以匹配origin/master中的文件。

​	



### 更新到github

---

1. add、commit等操作
2. git pull（一定要）
   - 预防别人修改了仓库，而直接push不成功
   - 若修改了仓库，pull了之后会进入vim，退出后在提交即可
3. git push





### 创建git分支

---

1. git checkout/switch -b/-c dev 创建并切换到dev

2. git branch dev 创建分支dev

3. git checkout dev 切换分支dev

4. git branch 查看当前分支

5. git merge 合并某分支到当前分支

6. git branch -d dev 删除dev分支

   工作原理：
   	1，每次提交，分支向前移动一步
   				mater
   				  ↓
   		O----O----O
   	2，新建的dev为一个指针指向与master相同的提交
   				mater
   				  ↓
   		O----O----O
   				  ↑
   				 dev
   	3，改变指针HEAD指向dev，再次提交时只会在dev分支上修改，master不变
   				mater
   				  ↓
   		O----O----O-----O
   						↑
   						dev
   	4，完成dev后直接合并，HEAD重新指向master，dev可以删除


### 其他git命令：

---

- ​	工作区里的文件add到stage
  ​		可使用git checkout -- filesname进行撤销操作
  ​		git reset -- filename撤销暂存区的修改
  ​		git reset HEAD filename撤销暂存区的修改并放回工作区
  ​		git status查看状态
  ​		cat filename查看文件详细信息

- ​	最后commit到master库
  ​		git reset --hard HEAD^回退到HEAD^（^的个数为之前版本）
  ​		git log载入历史记录
  ​		git reflog载入版本号日志
- 查看分支下所跟踪的文件列表
  ​		git ls-l
  ​		ll 查看当前目录下的全部文件列表
- **在git时遇到fatal进程在运行或崩溃时使用**：
  ​		rm .git/index.lock删除文件后再提交即可