---
title: Git
createTime: 2026/08/18 19:42:19
permalink: /blog/git/git/
---
## 本地GIT配置
:::tip
Git 的配置生效优先级：仓库级 > 全局级 > 系统级  
提交记录中的用户名和邮箱在提交时已经写入，修改配置不会影响历史提交，仅影响未来的提交
:::
### 查看配置
#### 细则
- 查看所有配置（按系统→全局→仓库顺序显示）
  ```shell
  git config --list
  ```
    - 查看不同级别的配置
        - 全局配置
            ```shell
            git config --global --list
            ```
        - 当前仓库配置
            ```shell
            git config --local --list
            ```
        - 系统配置
            ```shell
            git config --system --list 
            ```
- 或查看所有配置及其来源
  ```shell
  git config --list --show-origin
  ```
- 查看特定配置项
  ```shell
  git config < 配置名称 >
  ```
#### 常用
- 看当前生效的用户名
    ```shell
    git config user.name
    ```
- 查看当前生效的邮箱
    ```shell
    git config user.email
    ```
### 修改配置
#### 细则
- 修改当前仓库配置(覆盖全局配置)
```shell
git config < 配置名 > <值>
```
- 修改全局配置
```shell
git config --global < 配置名 > <值>
```
#### 常用
- 全局
  - 用户名
    ```shell
    git config --global user.name "用户名"
    ```
  - 邮箱
    ```shell
    git config --global user.email "邮箱"
    ```
- 当前仓库
  - 用户名
    ```shell
    git config user.name "用户名"
    ```
  - 邮箱
    ```shell
    git config user.email "邮箱"
    ```
###  删除配置
- 全局
```shell
git config --global --unset < 配置名 >
```
- 当前仓库
```shell
git config --unset < 配置名 >
```
## 拉取仓库
```shell
git clone url
```
[git clone命令](./命令/Git-clone.md)
## 远程

注:  
Origin为远程仓库  
Upstream为原仓库/上游仓库（可为null

### 绑定/解绑

#### 查看远程仓库绑定

```shell
git remote -v
```

#### 远程仓库
绑定：
```shell
git remote set-url origin url
```
解绑：
```shell
git remote remove origin
```
更换：
```shell
git remote set-url origin url
```

#### 原分支仓库
绑定：
```shell
git remote add upstream url
```
解绑：
```shell
git remote remove upstream
```
更换：
```shell
git remote set-url upstream url
```

### 拉取/合并
#### 远程仓库
```shell
git pull origin main
```

#### 原仓库  
##### 直接合并
```shell
git pull upstream main
```
##### 下载后合并
- 下载原仓库的更新
    ```shell
    git fetch upstream
    ```
- 合并到本地文件
    - 切换到本地main分支
        ```shell
        git checkout main 
        ```
    - 将原仓库代码合并到本地分支
        ```shell
        git merge upstream/main
        ```
### 推送
- 查看是否有未提交的修改
    ```shell
    git status
    ```
  - 提交本地修改（如果尚未提交）
    - 将文件添加到暂存区
        ```shell
        git add ./
        ```
        [git add命令](./命令/Git-add.md)
    - 提交本地修改
        ```shell
        git commit -m "描述更新内容"
        ```
- 推送到远程仓库
  ```shell
  git push origin 分支名
  ``` 
  - 若为首次推送
  ```shell
  git push -u origin 分支名
  ```
  ```-u 会建立本地分支与远程分支的追踪关系，之后可以直接使用 git push。```
  - 特殊情况
    - 如果远程分支已有提交，而你希望用本地版本覆盖（需谨慎，会丢弃远程的差异），可以使用强制推送
      ```shell
      git push -f origin 分支名 
      ```
[git push命令](./命令/Git-push.md)

## 回滚
[git reset命令](./命令/Git-reset.md)
### 代码已提交（commit）但尚未推送到远程（仅本地回滚）
- 撤销最近 N 次提交，保留修改内容在工作区
  ```shell
  git reset --soft HEAD~< 次数 >  
  ```
  - 彻底删除最近N次提交的改动
  ```shell
  git reset --hard HEAD~< 次数 >
  ```
### 代码已推送到远程仓库
#### 撤销某次提交的改动
- 查看历史记录
  ```shell
  git log --oneline
  ```
- 撤销某次提交
  ```shell
  git revert < 提交哈希 >
  ```
#### 回滚到某次提交
- 查看所有历史版本
  ```shell
  git log --oneline --graph
  ```
- 回滚
  - 保留当前修改为未暂存
    ```shell
    git reset --mixed < 提交哈希 >
    ```
  - 不保留任何更改
    ```shell
    git reset --hard < 提交哈希 >
    ```
