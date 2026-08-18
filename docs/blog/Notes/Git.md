---
title: Git
createTime: 2026/08/18 19:42:19
permalink: /blog/git/
---

## 拉取仓库
```shell
git clone url.git
```

## 远程

注:  
Origin为远程仓库  
Upstream为原仓库（可为null

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
git remote remove upstream
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
git remote remove origin
```
更换：
```shell
git remote set-url upstream url
```

### 拉取/合并
#### 远程仓库
```shell
git pull origin 仓库名称
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
        (./为路径，可选择性添加)
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
