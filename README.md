# git 命令记录
[视频教程链接]([https://youtu.be/RGOj5yH7evk](https://www.freecodecamp.org/news/git-and-github-crash-course/)

## 一、在本地创建项目并上传Github
### 1. 创建项目文件夹
```
mkdir <folder_name>
```

### 2. 初始化git
```
git init
```
```
ls -a
```
xxx@xxx-Pro upload % ls -a
.               ..              .git            main.cpp

### 3. 【根据需求可选或略过】修改分支设置（迎合现代软件开发的命名惯例）
#### 3.1 全局配置
```
git config --global init.defaultBranch <名称>  # 例如：git config --global init.defaultBranch main
```
#### 3.2 重命名当前分支
如果你已经初始化了仓库，并且想要将当前的“master”分支重命名为“main”或其他名称，可以使用以下命令：
```
git branch -m <name> # 例如：git branch -m main
```

### 4. 建立项目文件
```
touch main.cpp
```

### 5. 编辑...
```
#include <iostream>

int main(){
    std::cout << "Hello World.\n";
    std::cin.get();
    return 0;
}
```

### 6. 将.git同目录下某个文件/所有文件添加至Git暂存区
单独：
```
git add main.cpp
```
所有：
```
git add .
```
### 7. 将暂存区(.git)所有的更改提交至本地仓库的当前分支，在首次commit时才会创建分支，并以第3步中的设置命名（main/master）
提交：
```
git commit -m "Initial commit with main.cpp"
# -m:表示提交的消息，但必须有一条。

```
检查：
```
git branch
```
xxx@xxx-Pro upload % git branch
* main


### 8. 在GitHub上创建一个新的仓库
#### 8.1 点击GitHub主页右上角的“+”按钮，然后选择“New repository”；
#### 8.2 在“Repository name”字段中输入您的仓库名称。您可以选择添加一个描述（可选）并选择是将仓库设置为公开还是私有；
#### 8.3 点击“Create repository”按钮来创建新仓库。
<img width="1495" alt="截屏2025-04-16 09 59 52" src="https://github.com/user-attachments/assets/ee922b8a-7101-4e50-a372-0e5cf4590a72" />

### 9. 将本地仓库与GitHub仓库关联
在本地终端中，将您的本地Git仓库与刚刚在GitHub上创建的远程仓库关联。假设您的GitHub仓库URL是https://github.com/username/repository.git，您可以使用以下命令：
```
git remote add origin https://github.com/username/repository.git
```

### 10. 推送提交到 GitHub
将本地的提交推送到 GitHub 上的远程仓库
```
git push -u origin main

枚举对象中: 6, 完成.
对象计数中: 100% (6/6), 完成.
使用 11 个线程进行压缩
压缩对象中: 100% (4/4), 完成.
写入对象中: 100% (5/5), 604 字节 | 604.00 KiB/s, 完成.
总共 5（差异 1），复用 0（差异 0），包复用 0（来自  0 个包）
remote: Resolving deltas: 100% (1/1), done.
To github.com:xxx/upload.git
   xxx..xxx  main -> main
分支 'main' 设置为跟踪 'origin/main'。
```
*注：如果github有更改，需要先拉取 GitHub到本地*
```
git pull
```
适用于已经配置好远程跟踪分支的情况
```
git pull origin main
```
```
git pull -u origin main # -u:设置默认上传分支
```
- origin：这是远程仓库的默认名称。当您克隆一个 GitHub 仓库时，Git 会自动将这个远程仓库命名为 origin。这个名字是一个约定俗成的默认值，您可以在需要时更改或添加其他远程仓库。
- main：这是您希望从中拉取更新的分支的名称。在许多项目中，main 是默认的主分支名称。以前，master 常被用作主分支的名称，但近年来，main 正逐渐成为新的标准。
来自 github.com:xxx/upload
 * branch            main       -> FETCH_HEAD
已经是最新的。

[如何删除已经上传的内容：以build为例](https://github.com/Sun-Moon-1314/git-demo/issues/6)

[如何跳过不需要上传的文件夹](https://github.com/Sun-Moon-1314/git-demo/issues/7)

## 二、拉取github上的仓库到本地Git
### 1. 克隆SSH
```
git clone <Repository-SSH> # 自动创建Repository-SSH文件夹
cd <Repository-SSH>
```

<img width="1315" alt="截屏2025-04-14 11 48 26" src="https://github.com/user-attachments/assets/1d11dad7-9875-4e69-a617-d6bc8892ab92" />

### 2. 查看Git状态
查看当前分支的状态，包括未跟踪的文件和待提交的更改
```
git status
```
### 3. 密钥生成与上传
[本机密钥操作](https://github.com/Sun-Moon-1314/git-demo/issues/1)

### 4. 














