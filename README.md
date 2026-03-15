# 从零开始：Git & GitHub 完全保姆级教程 (涵盖初次上传、日常更新与防坑指南)

本教程将带你完成从“零基础配置”到“初次上传项目”，再到“日常代码更新”的完整开发工作流。遇到任何报错，请直接翻阅文末的《常见报错与拯救指南》。

---

## 🛠️ 第零步：准备工作 (前提条件)

在开始敲击命令之前，请确保你已经完成了以下两件事：
1. **安装 Git**：在电脑上安装了 Git 客户端（Windows 用户推荐使用自带的 **Git Bash**，在文件夹空白处右键即可看到 `Open Git Bash here`）。
2. **注册账号**：拥有一个可用的 GitHub 账号。

---

## 第一步：全局配置 Git (仅换电脑或首次使用时需要)

告诉 Git “你是谁”。打开终端，请依次**单独复制并执行**以下两行命令（请把双引号里的内容替换为你自己的）：

```bash
git config --global user.name "你的GitHub用户名"
```

```bash
git config --global user.email "你的GitHub注册邮箱"
```

*(提示：这两行命令执行后不会有任何输出，只要没报错就代表配置成功了。)*

---

## 第二步：在 GitHub 上新建远程空仓库

1. 登录 GitHub 网页，点击右上角的 "+" 号，选择 "New repository"。
2. **Repository name**：填写你的项目名称（建议使用英文或拼音，例如 `ren_qun_shi_bie`）。
3. **Public / Private**：根据个人需要选择公开（所有人可见）或私有（仅自己可见）。

⚠️ **核心避坑**：绝对不要勾选 "Add a README file"、"Add .gitignore" 或 "Choose a license"。我们需要保持这个仓库是**完全空白**的，以便将本地已有的完整项目推上去，避免冲突。

4. 点击绿色的 "Create repository" 按钮。
5. 创建成功后，复制页面上提供的 HTTPS 或 SSH 仓库地址（备用）。

---

## 第三步：初始化本地仓库并配置 `.gitignore`

回到你的电脑，打开你的项目根目录文件夹。在空白处右键选择 `Open Git Bash here`。

### 1. 初始化本地 Git 仓库

```bash
git init
```
*(作用：在当前文件夹生成一个隐藏的 `.git` 目录，让 Git 开始接管这个项目。)*

### 2. 创建并配置 `.gitignore` 文件（极其重要）

在项目根目录下新建一个名为 `.gitignore` 的文本文件，并将以下规则**完整复制**进去并保存：

```text
# =========================
# 操作系统生成文件
# =========================
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
ehthumbs.db
ehthumbs_vista.db
[Tt]humbs.db
[Dd]esktop.ini

# =========================
# 编辑器和 IDE 相关文件
# =========================
.vscode/
.idea/
.vs/
*.suo
*.ntvs*
*.njsproj
*.sln
*.sw?
*.sublime-workspace
*.sublime-project

# =========================
# Python 运行和编译文件
# =========================
__pycache__/
*.py[cod]
*$py.class
*.so
.Python
build/
develop-eggs/
dist/
downloads/
eggs/
.eggs/
lib/
lib64/
parts/
sdist/
var/
wheels/
share/python-wheels/
*.egg-info/
.installed.cfg
*.egg
MANIFEST

# =========================
# 虚拟环境和配置
# =========================
.env
.venv
env/
venv/
ENV/
env.bak/
venv.bak/
pip-log.txt
pip-delete-this-directory.txt
pyvenv.cfg
.tox/
.coverage
.coverage.*
.cache
nosetests.xml
coverage.xml
*.cover
*.py,cover
.hypothesis/
.pytest_cache/

# =========================
# Jupyter Notebook
# =========================
.ipynb_checkpoints

# =========================
# 深度学习/大模型/数据相关文件
# =========================
*.pth
*.pt
*.ckpt
*.weights
*.safetensors
*.h5
*.onnx
*.pkl
models/
checkpoints/
data/
datasets/
logs/
tensorboard_logs/
wandb/

# =========================
# 日志文件
# =========================
*.log
logs/

# =========================
# 本地秘钥或敏感配置
# =========================
secret_settings.py
config.local.json
credentials.json
```

---

## 第四步：初次打包与推送到 GitHub

请依次**单独复制**以下命令并在终端中执行：

### 1. 将所有文件添加到暂存区

```bash
git add .
```

### 2. 提交代码到本地仓库

```bash
git commit -m "第一次提交：初始化项目结构、核心代码及忽略文件"
```

### 3. 统一主分支名称为主流规范

```bash
git branch -M main
```

### 4. 关联你的专属远程仓库
**(注意：请将下方命令中的 `https://github.com/UserName/ProjectName.git` 替换为你自己在 GitHub 网页上复制的真实仓库地址，不要保留任何括号)**

```bash
git remote add origin [https://github.com/UserName/ProjectName.git](https://github.com/UserName/ProjectName.git)
```

### 5. 将本地代码推送到云端

```bash
git push -u origin main
```
*(当终端显示 `Branch 'main' set up to track remote branch 'main' from 'origin'.` 就说明推送成功了！)*

---

## 🔄 第五步：日常更新代码 (高频必用三步曲)

项目初次上传成功后，以后你每次在本地修改了代码，只需要在项目文件夹下打开 Git Bash，依次单独执行以下三行命令即可：

### 1. 收集所有变动

```bash
git add .
```

### 2. 打包并填写更新备注

```bash
git commit -m "更新了数据处理逻辑，修复了之前的报错"
```

### 3. 推送到云端

```bash
git push
```

---

## 🚨 常见报错与强行拯救指南 (Troubleshooting)

遇到报错时，请根据提示寻找对应的解决命令（每行命令均可独立复制运行）：

### ❌ 报错 1：fatal: The current branch main has no upstream branch
**触发场景**：Git 不知道你要推送到远程的哪个分支。
**终极解法**：建立关联或配置全局自动追踪：

```bash
git push --set-upstream origin main
```
```bash
git config --global push.autoSetupRemote true
```

### ❌ 报错 2：Updates were rejected 或 non-fast-forward
**触发场景**：云端存在本地没有的文件，为防止覆盖而拒绝推送。
**终极解法**：确认本地代码为最新版本后，强行覆盖云端：

```bash
git push -u origin main -f
```

### ❌ 报错 3：Permission denied (publickey)
**触发场景**：使用了 SSH 协议，但未配置 SSH 密钥。
**终极解法**：
1. 生成专属密钥（执行后连续按 3 次回车）：
```bash
ssh-keygen -t ed25519 -C "你的GitHub注册邮箱"
```
2. 查看并复制公钥内容：
```bash
cat ~/.ssh/id_ed25519.pub
```
3. 登录 GitHub 网页 -> Settings -> SSH and GPG keys -> New SSH key，将复制的公钥粘贴进去并保存，重新执行推送命令。

### ❌ 报错 4：RPC failed; HTTP 408 / The remote end hung up unexpectedly
**触发场景**：HTTPS 推送大项目超时。
**终极解法**：扩大 Git 缓冲区并放宽超时限制：

```bash
git config --global http.postBuffer 524288000
```
```bash
git config --global http.lowSpeedLimit 1000
```
```bash
git config --global http.lowSpeedTime 600
```

### ❌ 报错 5：client_loop: send disconnect: Connection reset by peer / Broken pipe
**触发场景**：SSH 推送大项目时网络断流导致管道破裂。
**终极解法**：切分打包压力，并强制发送心跳包：

```bash
git config --global pack.windowMemory "100m"
```
```bash
git config --global pack.packSizeLimit "100m"
```
```bash
git config --global pack.threads 1
```
```bash
GIT_SSH_COMMAND="ssh -o ServerAliveInterval=60 -o ServerAliveCountMax=120 -o IPQoS=throughput" git push -u origin main -f
```

### ❌ 报错 6：Everything up-to-date
**触发场景**：修改代码后忘了告诉 Git 重新记录快照。
**终极解法**：必须完整走完日常更新三步曲（`git add .` -> `git commit -m "备注"` -> `git push`）。

### ❌ 报错 7：403 Permission denied
**触发场景**：Windows 凭据管理器账号冲突。
**终极解法**：打开 Windows 系统的 **凭据管理器** -> **Windows 凭据** -> 删除带有 `git:https://github.com` 的记录，重新推送触发登录。
