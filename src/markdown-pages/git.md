---
title: "Git 工作流"
date: "2019-09-19"
---

# git 工作流
## git服务
*  注册 git 服务账号
*  生成ssh 公钥秘钥, 并在git 网站个人设置更新 ssh公钥 这样就可以
  终端中输入ssh-keygen 回车, 按照提示输入相应的字符或空白,最后生成 ~/.ssh/id_rsa 秘钥文件 和 ~/.ssh/id_rsa.pub 
## git 命令
* git pull git@git.coding.net:{:user}/{:repo}.git   # 拉代码
* git branch {:branch_name}                         # 从当前分支新增分支
* git checkout {:branch_name}                       # 检出分支，将 {:branch_name} 分支的代码从.git 目录中拉到更新目录
* git diff {:branch_name1} {:branch_name2}          # 比较分支
* git merge {:branch_name1} {:branch_name2}         # 将分支2 合并到分支1
* git log {:file}                                   # 查看{:file} 提交记录
* git  {:file}                                      # 查看{:file} 提交记录
* git reset {:file}                                 # 回滚到最近一次提交之后的状态
* git reset {:commit_hash} {:file}                  # 回滚到特定某一次提交之后的状态
* git merge {:branch_a} # 净{:branch_a} 分支的代码合并到当前分支
* git rebase  {:branch_a}  # 同merge 一下，不过会吧分支{:branch_a} 的 git 记录也合并过来

## git 常见任务场景
### 方案一

```shell
git checkout master # 线上
git checkout -b feature/xxx 
vi a.php  # 开发
git checkout dev # 切换到开发分支
git merge feature/xxx # 合并到开发
# 测试 ...
git checkout master
git merge feature/xxx
```


### 方案二
* 增加新功能
```shell
git checkout -b feature/xxxx
vi a.php # 开发
git add a.php # 加入改动
git commit -m 'commit comment' # 提交改动
git checkout dev  # 切换到开发分支
git merge feature/xxx --no-ff
```
* 修复紧急bug
```shell
git checkout master          # 线上分支出现bug
git checkout -b hotfix/xxx   # 从线上分支建立 hotfix 分支
vi a.php # 开发
git add a.php #
git commit -m 'commit comment'
git checkout master  # 切换
git merge hotfix/xxx --noff     # 将hotfix 分支合并到线上, 然后同步线上代码
git checkout dev
git merge hotfix/xxx --noff     # 将hotfix 分支合并到开发分支,同步代码
```