# git-help

##### BUG修复
* 把当前修改隐藏 ``` git stash ```
* 切换到BUG分支  ``` git checkout <name> ```
* 创建并切换分支 ``` git checkout -b <name> ```
* 切换到BUG分支  ``` git checkout <name> ```
* 合并分支 ``` git merge <name> ```
* 恢复工作区
    1. 查看工作区 ``` git stash list ```
    1. 不删除stash ``` git stash apply stash@{0} ```
    1. 删除stash  ```  git stash drop ```
    1. 恢复并删除stash ``` git stash pop ```

##### 回退版本
* 回退到上一个版本  ``` git reset --hard HEAD^ ```
* 回退到指定的版本  ``` git reset --hard <commit_id> ```
* 回退保留本地修改 ``` git reset <commit_id> ```

##### 前进后退
* 回退前 ``` git log ```
* 回退后 ``` git reflog ```

##### 文件修改管理
* 文件撤消
    1. 撤消保留修改  ``` git reset <filename> ```
    1. 未commit撤消 ``` git checkout -- <filename> ```
    1. 已commit撤消 ``` git reset HEAD <filename> ```
    1. 已push后撤消 ``` git reset --hard HEAD^ ```
 
* 清除没有add的文件
    1. 删除所有未排除文件 ``` git clean -df ``` 
    1. 查看哪些文件会删除 ``` git clean -n ``` 

* 对比两个文件区别 ``` git diff HEAD -- <filename> ```
* 删除文件  ``` git rm <filename> ```
* 本地保留  ``` git rm --cached <filename> ```

##### 远程仓库管理
* 添加仓库地址 ``` git remote add origin <url> ```
* 删除仓库地址 ``` git remote rm <name> ```
* 克隆仓库项目 ``` git clone <url> ```
* 查看仓库地址  ``` git remote -v ```


##### 分支管理
* 创建分支
    1. 创建分支 ``` git branch <name> ```
    1. 切换分支 ``` git checkout <name> ```
    1. 创建并切换 ``` git checkout -b <name> ```
    1. 创建无记录分支 ``` git checkout --orphan <name> ```
* 查看分支 ``` git branch ```
* 合并分支 ``` git merge <name> ```
* 删除分支
    1. 删除分支 ``` git branch -d <name> ```
    1. 强行删除 ``` git branch -D <name> ```
* 获取分支  ``` git checkout -b dev origin/<name> ```
* 推送分支  ``` git push origin <name> ```
* 关联分支  ``` git branch --set-upstream-to=origin/<remotename> <localname> ```

##### 标签管理
* 创建标签
    1. 当前创建 ``` git tag <tagname> ```
    1. 历史创建 ``` git tag <tagname> <commit_id> ```
    1. 带说明的 ``` git tag -a <tagname> -m "<message>" <commit_id> ```

* 查看标签  ``` git tag ```
* 删除标签
    1. 删除本地 ``` git tag -d <tagname> ```
    1. 删除远程 ``` git push origin :refs/tags/<tagname> ```
* 推送标签
    1. 推送指定 ``` git push origin <name> ```
    1. 推送所有 ``` git push origin --tags ``` 

##### 清空所有commit记录
* 克隆项目 ``` git clone <url> ```
* 新建分支 ``` git checkout --orphan <name> ```
* 添加所有 ``` git add -A ```
* 提交修改 ``` git commit -am "Initial commit" ```
* 强制删除 ``` git branch -D master ```
* 更改分支 ``` git branch -m master ```
* 提交分支 ``` git push -f origin master ```
* 关联分支 ``` git branch --set-upstream-to=origin/master ```

##### 忽略本地文件,不影响其他人
* 忽略文件 ``` git update-index --assume-unchanged /path/file ```
* 取消忽略 ``` git update-index -–no-assume-unchanged /path/file ```

##### 清除大文件
* 统计超过1M的文件
```
git rev-list --objects --all \
| git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' \
| sed -n 's/^blob //p' \
| sort --numeric-sort --key=2 \
| cut -c 1-12,41- \
| grep -vF --file=<(git ls-tree -r HEAD | awk '{print $3}') \
| awk '$2 > 1048576' \
| $(command -v gnumfmt || echo numfmt) --field=2 --to=iec-i --suffix=B --padding=7 --round=nearest
```
* 删除文件
```
git filter-branch --force --index-filter 'git rm -rf --cached --ignore-unmatch <filename>' --prune-empty --tag-name-filter cat -- --all
```
* 回收垃圾
```
rm -rf .git/refs/original/
git reflog expire --expire=now --all
git gc --prune=now
```

