# 从零开始：如何将本地项目推送到 GitHub (超详细保姆级教程)

本教程将带你完成从“写好本地代码”到“成功上传至 GitHub 仓库”的完整流程。无论是个人项目备份，还是开源代码发布，只需按照以下步骤操作即可。

---

## 🛠️ 准备工作 (前提条件)

在开始敲击命令之前，请确保你已经完成了以下两件事：
1. **安装 Git**：在电脑上安装了 Git 客户端（Windows 用户推荐使用自带的 **Git Bash**）。
2. **注册账号**：拥有一个可用的 GitHub 账号。

---

## 第一步：全局配置 Git (仅首次使用需要)

如果你是第一次在这台电脑上使用 Git，需要先告诉 Git “你是谁”。打开终端（Windows 系统下可在任意空白处右键选择 `Open Git Bash here`），依次输入以下两行命令：

```bash
git config --global user.name "你的GitHub用户名"
git config --global user.email "你的GitHub注册邮箱"
```

提示：这两行命令执行后不会有任何输出，只要没报错就代表配置成功了。

---

## 第二步：在 GitHub 上新建远程空仓库

1. 登录 GitHub 网页，点击右上角的 "+" 号，选择 "New repository"。
2. **Repository name**：填写你的项目名称（建议使用英文，可以使用连字符 `-`，例如 `My-First-Project`）。
3. **Public / Private**：根据个人需要选择公开（所有人可见）或私有（仅自己可见）。

⚠️ **核心避坑**：绝对不要勾选 "Add a README file"、"Add .gitignore" 或 "Choose a license"。我们需要保持这个仓库是完全空白的，以便将本地已有的文件推送上去。

4. 点击绿色的 "Create repository" 按钮。
5. 创建成功后，复制页面上提供的 HTTPS 仓库地址（格式类似于 `https://github.com/你的用户名/你的项目名.git`）。

---

## 第三步：初始化本地仓库并配置 `.gitignore`

回到你的电脑，打开你的项目根目录文件夹。在空白处右键选择 `Open Git Bash here`（或者在终端里用 `cd` 命令进入该目录）。

### 1. 初始化本地仓库

```bash
git init
```
**作用**：在当前文件夹生成一个隐藏的 `.git` 目录，让 Git 开始接管这个项目。

### 2. 创建并配置 `.gitignore` 文件（极其重要）
为了防止把本地的环境变量、临时文件、或者过大的模型文件误传到 GitHub 上，我们需要在进行代码打包前，配置忽略规则。

在项目根目录下新建一个名为 `.gitignore` 的文本文件（注意文件名前面有一个点 `.` ），并将以下常用规则完整复制进去并保存：

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

## 第四步：提交本地代码

配置好忽略文件后，就可以放心地将代码添加到暂存区并提交了。继续在刚才的终端中依次执行：

### 1. 将所有文件添加到暂存区

```bash
git add .
```
**作用**：把当前目录下的所有文件准备好，等待提交。（注意 `add` 后面有一个空格和一个英文句号 `.`）

### 2. 提交代码到本地仓库

```bash
git commit -m "第一次提交：初始化项目结构、代码及忽略文件"
```
**作用**：给这次提交打上一个备注，正式把代码快照存入本地 Git 历史记录中。

---

## 第五步：关联远程仓库并推送代码

本地代码打包完毕后，接下来把它们推送到刚才在 GitHub 创建的空仓库中：

### 1. 统一主分支名称

```bash
git branch -M main
```
**作用**：GitHub 现在的默认主分支叫 `main`，而老版本 Git 本地默认叫 `master`，这行命令为了让两边名字统一，避免冲突。

### 2. 关联远程仓库

将下面的链接替换为你刚才在第二步复制的真实地址：

```bash
git remote add origin [https://github.com/你的用户名/你的项目名.git](https://github.com/你的用户名/你的项目名.git)
```
**作用**：告诉本地 Git，我们要推送的目标服务器地址在哪里，并给它起个别名叫 `origin`。

### 3. 推送代码到 GitHub

```bash
git push -u origin main
```
**作用**：把本地的 `main` 分支推送到远程的 `origin` 仓库。

**注意**：此时系统可能会弹窗让你登录 GitHub（选择 Browser 浏览器登录即可授权）。当终端显示 `Branch 'main' set up to track remote branch 'main' from 'origin'.` 就说明推送成功了！去刷新 GitHub 网页吧！

---

## 🚨 常见报错与强行拯救指南

在实际操作中，偶尔会遇到一些报错。遇到问题不要慌，请对照以下策略解决：

### ❌ 报错 1：403 Permission denied

**原因分析**：Windows 电脑里缓存了你以前登录过的其他 GitHub 账号密码，导致权限冲突。

**解决办法**：打开 Windows 系统的 **凭据管理器** -> **Windows 凭据** -> 找到带有 `git:https://github.com` 的记录并 **删除**。然后重新执行 `git push` 命令触发重新登录即可。

### ❌ 报错 2：Updates were rejected 或提示 fetch first

**原因分析**：GitHub 上的仓库里已经有一些文件（比如你不小心勾选了生成 README），而你本地没有这些文件。Git 怕你弄丢服务器上的数据，拒绝推送。

**解决办法**：如果你确定本地的代码才是最新、最完整的，可以直接在推送命令后加一个 `-f` 进行强行覆盖：

```bash
git push -u origin main -f
```

### ❌ 报错 3：修改了文件，但推送后提示 Everything up-to-date

**原因分析**：Git 不会自动追踪文件的修改。你只是按了 `Ctrl+S` 保存了文件，但没有告诉 Git 把新的修改打包。

**解决办法**：每次修改完代码想要更新到 GitHub 时，都必须完整执行**“日常更新三步曲”**：

```bash
git add .
```
```bash
git commit -m "更新了某某功能或修复了某某排版"
```
```bash
git push
```

### ❌ 报错 4：RPC failed; HTTP 408 (或提示 The remote end hung up unexpectedly)

**原因分析**：这是典型的网络超时报错。通常是因为你要推送的项目有些大（包含图片、模型或较多文件），而传输时间过长，导致 Git 服务器等待超时主动断开了连接。

**解决办法**：你可以通过以下几种方式解决（任选其一即可）：

**方案 A：扩大 Git 的 HTTP 缓冲区（最快解决）**
在终端输入以下命令，将缓冲区提升至 500MB，然后重新尝试推送：
```bash
git config --global http.postBuffer 524288000
```

**方案 B：放宽网络超时限制**
强制要求 Git 在弱网环境下多等一会儿，不轻易断开：
```bash
git config --global http.lowSpeedLimit 1000
git config --global http.lowSpeedTime 600
```

**方案 C：改用 SSH 协议推送（最稳定）**
如果你已经配置过 SSH 密钥，可以将 HTTPS 链接替换为 SSH 链接，它不仅无需每次输密码，且对大文件传输的稳定性极佳：
```bash
git remote set-url origin git@github.com:你的用户名/你的项目名.git
```
