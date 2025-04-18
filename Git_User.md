# git 命令记录
[视频教程链接](https://youtu.be/RGOj5yH7evk)

## 一、在本地创建项目并上传Github
### 1. 创建项目文件夹
```zsh
mkdir <folder_name>
```

### 2. 初始化git
```zsh
git init
```
```zsh
ls -a
```
xxx@xxx-Pro upload % ls -a
```zsh
.        ..        .git        main.cpp
```
### 3. 【根据需求可选或略过】修改分支设置（迎合现代软件开发的命名惯例）
#### 3.1 全局配置
```zsh
git config --global init.defaultBranch <名称>
```
例如：
```zsh
git config --global init.defaultBranch main
```
#### 3.2 重命名当前分支
如果你已经初始化了仓库，并且想要将当前的“master”分支重命名为“main”或其他名称，可以使用以下命令：
```zsh
git branch -m <name> # 例如：git branch -m main
```

### 4. 建立项目文件
```zsh
touch main.cpp
```

### 5. 编辑...
```cpp
#include <iostream>

int main(){
    std::cout << "Hello World.\n";
    std::cin.get();
    return 0;
}
```

### 6. 将.git同目录下某个文件/所有文件添加至Git暂存区
单独：
```zsh
git add main.cpp
```
所有：
```zsh
git add .
```
### 7. 将暂存区(.git)所有的更改提交至本地仓库的当前分支，在首次commit时才会创建分支，并以第3步中的设置命名（main/master）
提交：
```zsh
git commit -m "Initial commit with main.cpp"
# -m:表示提交的消息，但必须有一条。
```

检查：
```zsh
git branch
```
查看当前分支
```zsh
xxx@xxx-Pro upload % git branch
* main
```
星号*: 当前所在分支

### 8. 在GitHub上创建一个新的仓库
#### 8.1 点击GitHub主页右上角的“+”按钮，然后选择“New repository”；
#### 8.2 在“Repository name”字段中输入您的仓库名称。您可以选择添加一个描述（可选）并选择是将仓库设置为公开还是私有；
#### 8.3 点击“Create repository”按钮来创建新仓库。
<img width="1495" alt="截屏2025-04-16 09 59 52" src="https://github.com/user-attachments/assets/ee922b8a-7101-4e50-a372-0e5cf4590a72" />

### 9. 将本地仓库与GitHub仓库关联
在本地终端中，将您的本地Git仓库与刚刚在GitHub上创建的远程仓库关联。假设您的GitHub仓库URL是https://github.com/username/repository.git，您可以使用以下命令：
```zsh
git remote add origin https://github.com/username/repository.git
```

### 10. 推送提交到 GitHub
将本地的提交推送到 GitHub 上的远程仓库
```zsh
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
```zsh
git pull
```
适用于已经配置好远程跟踪分支的情况
```zsh
git pull origin main
```
```zsh
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
```zsh
git clone <Repository-SSH> # 自动创建Repository-SSH文件夹
cd <Repository-SSH>
```

<img width="1315" alt="截屏2025-04-14 11 48 26" src="https://github.com/user-attachments/assets/1d11dad7-9875-4e69-a617-d6bc8892ab92" />

### 2. 查看Git状态
查看当前分支的状态，包括未跟踪的文件和待提交的更改
```zsh
git status
```
### 3. 密钥生成与上传
[本机密钥操作](https://github.com/Sun-Moon-1314/git-demo/issues/1)

### 4. 创建新的分支
```zsh
git checkout -b feature-branch
git branch
```

### 5. 提交
跟上面 <add, commit, push> 过程一致

### 6. 合并到主分支
- 切换 <主分支/功能分支>
```zsh
git checkout main/feature-branch
```
- 查看分支不同
```zsh
git diff <分支名称>
```
- 融合分支: 功能分支->主分支
```zsh
git merge feature-branch
```
- 删除分支: 需先切回主分支
```zsh
git branch -d feature-branch
```
- add + commit命令，适用于已经add过的文件
```zsh
git commit -am "修复了bug并更新了文档"
```
- add执行后添加了错误信息，恢复使用
```zsh
git reset
git reset README.md
```
- commit执行后上传了错误信息，恢复使用
```zsh
git reset HEAD~1 # HEAD：指向最后一次提交的指针
```
- 根据提交的哈希值退回特定的版本
```zsh
git log
commit xxxxx63923c29cbd5372db604b2b4ebb6dfbbd46
Author: xxx <xxx@users.noreply.github.com>
Date:   Thu Apr 17 10:29:39 2025 +0800

    dsad

```
```zsh
git reset xxxxx63923c29cbd5372db604b2b4ebb6dfbbd46
```
- 将当前分支回滚到某个特定的提交,<commit> 是你想回滚到的提交的哈希值
```zsh
git reset --hard <commit>
```
- 这将工作目录和索引重置到当前分支的最新提交状态，丢弃所有未提交的更改
```zsh
git reset --hard HEAD
```
注意：*不可逆的操作，所有未提交的更改都会被永久删除，无法恢复*

## 三、Fork开源项目到自己github，开发管理等

### 1. 添加远程仓库
```zsh
git remote add upstream <original-repo-url>
```
### 2. 查看远程仓库
```zsh
git remote -v
```
### 3. 获取上游更新
```zsh
git fetch upstream
```
### 4. 切换到本地主分支
```zsh
git checkout main
```
### 5. 合并上游更新到本地主分支
```zsh
git merge upstream/main
```
### 6. 推送更新到你的 Fork 仓库
```zsh
git push origin main
```
### 7. 创建开发分支
```zsh
git checkout -b feature-branch
```
### 8. 开发和提交更改
```zsh
git add .
git commit -m "Add new feature"
```
### 9. 合并开发分支到本地主分支
```zsh
git checkout main
git merge feature-branch
```
### 10. 推送合并后的更改到你的 Fork 仓库
```zsh
git push origin main
```

## 四. Git命令补全设置

在 macOS 上，Git 的 Tab 键补全功能依赖于 Shell 的补全脚本。如果 Tab 键无法补全，可以按照以下步骤设置：

### 1. 检查 Shell 类型
运行以下命令，确认你使用的是 Bash 还是 Zsh：
```bash
echo $SHELL
```
- 如果输出包含 `zsh`，说明你使用的是 Zsh。
- 如果输出包含 `bash`，说明你使用的是 Bash。

### 2. 启用 Git 补全
#### 对于 Zsh：
1. 确保安装了 `git-completion.zsh` 脚本。你可以通过 Homebrew 安装 Git 补全：
```bash
brew install git
```
2. 在 `~/.zshrc` 文件中添加以下内容：
```bash
nano ~/.zshrc

autoload -Uz compinit
compinit
fpath=(/opt/homebrew/share/zsh/site-functions $fpath)

source ~/.zshrc
```
3. 保存并运行以下命令以重新加载配置：
```bash
source ~/.zshrc
```

#### 对于 Bash：
1. 确保安装了 `git-completion.bash` 脚本。你可以通过 Homebrew 安装：
```bash
brew install git
```
2. 在 `~/.bash_profile` 或 `~/.bashrc` 文件中添加以下内容：
```bash
   autoload -Uz compinit
   compinit
   fpath=(/opt/homebrew/share/zsh/site-functions $fpath)
```
3. 保存并运行以下命令以重新加载配置：
```bash
source ~/.bash_profile
```

### 3. 清理补全缓存（如果仍有问题）
如果问题仍然存在，可以尝试清理 `compinit` 缓存：
```bash
rm -f ~/.zcompdump
compinit
```
## 四. 特殊情况

- z键无法输入到vscode中的终端
<img width="1495" alt="z无法输入到zsh" src="picture/截屏2025-04-18 12.11.14.png" />

完成后，重新打开终端，输入部分 Git 命令（如 `git ch`），然后按 Tab 键，检查是否可以补全。
