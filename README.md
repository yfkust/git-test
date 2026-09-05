# Msi-相關配置記錄

 标题
```
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
```
加粗、斜体、删除线
```
**加粗**

*斜体*

***加粗并斜体***

~~删除线~~
```

行内代码
```
如果只是命令、路径、文件名，推荐用一对反引号：

`nvidia-smi`
```

代码块
```
用三个反引号包起来，可接bash、python、conf、json、text
```

无序列表
```text
- Linux
- Conda
- CUDA
- GitHub

效果：

Linux
Conda
CUDA
GitHub

也可以嵌套：

- Linux
  - Process
  - Disk
  - Network
- CUDA
  - nvidia-smi
  - Driver
```

有序列表
```text
1. 安装软件
2. 修改配置
3. 重启程序
4. 验证

效果：

安装软件
修改配置
重启程序
验证
```

任务清单
```text
- [x] 安装 Miniconda
- [x] 创建环境
- [ ] 安装 CUDA
- [ ] 测试程序

非常适合写论文复现进度。
```



## git 倉庫指令
### 一、第一次创建 Git 仓库
1. 進入項目目錄
```bash
初始化 Git：

git init
# 查看状态
git status

# 查看修改
git diff

# 添加文件
git add .

# 提交
git commit -m "说明"

# 查看历史
git log --oneline

# 查看分支
git branch

# 新建分支
git switch -c 分支名

# 切换分支
git switch main

# 拉取 GitHub
git pull

# 上传 GitHub
git push
```

### 二、配置Git用戶信息
2. Git 重新完整配置
```bash
先看当前有没有残留配置：

git config --global --list

建议配置：

git config --global user.name "GitHub用户名"
git config --global user.email "GitHub邮箱"
git config --global init.defaultBranch main
git config --global core.editor "vim"
git config --global pull.rebase false

然后检查：

git config --global --list

Git 配置文件实际在：~/.gitconfig

可以直接看：cat ~/.gitconfig

配 GitHub SSH

先检查有没有旧 SSH：ls -la ~/.ssh

如果你之前备份过旧的：

id_ed25519
id_ed25519.pub

可以直接恢复，如果没有，就重新生成：

ssh-keygen -t ed25519 -C "GitHub邮箱"

看到Enter file in which to save the key直接回车，默认就是：

/home/yfkust/.ssh/id_ed25519

然后会问：Enter passphrase

你可以设置 SSH 密钥密码，更安全，或直接回车留空，更方便

生成后：

ls ~/.ssh

应该有：

id_ed25519
id_ed25519.pub

查看公钥：

cat ~/.ssh/id_ed25519.pub

复制整行。

然后 GitHub：

头像 → Settings → SSH and GPG keys → New SSH key

Title 可以写：

MSI Ubuntu

Key type：

Authentication Key

粘贴公钥。

然后回终端测试：

ssh -T git@github.com

之后 GitHub 仓库都用 SSH 地址：

git clone git@github.com:用户名/仓库.git
```


