# git 命令记录
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
<img width="462" alt="截屏2025-04-16 10 04 35" src="https://github.com/user-attachments/assets/342567a1-ef1c-4f58-be03-04e6195846f8" />

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
```
检查：
```
git branch
```
xxx@zhangjiandeMacBook-Pro upload % git branch
* main
* 
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


## 二、拉取github上的仓库到本地Git
```
git clone Repository-SSH
```
<img width="1315" alt="截屏2025-04-14 11 48 26" src="https://github.com/user-attachments/assets/1d11dad7-9875-4e69-a617-d6bc8892ab92" />
