---
title: git仓库删除所有提交历史记录，成为一个干净的新仓库
layout: post
date: '2017-12-15 21:21:28'
categories: rails
comments: true
---

**把旧项目提交到Git上，但是会有一些历史提交记录，这些历史记录中可能会有项目密码等敏感信息。如何删除这些历史记录，形成一个全新的仓库，并且保持代码不变呢？**
```
1.Checkout

   git checkout --orphan latest_branch

2. Add all the files

   git add -A

3. Commit the changes

   git commit -am "commit first"

4. Delete the branch

   git branch -D master

5.Rename the current branch to master

   git branch -m master

6.Finally, force update your repository

   git remote add origin git@github.com:xx/test.git
	 
   git push -u origin master 

```