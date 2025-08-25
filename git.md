# Git安装

下面是在Ubuntu上安装Git、配置VSCode并连接GitHub的完整流程：

------

### **1. 安装Git**

```
# 更新包列表
sudo apt update

# 安装Git
sudo apt install git -y

# 验证安装
git --version
```

------

### **2. 配置Git全局信息**

```shell
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

------

### **3. 安装VSCode**

#### **方法1：通过Snap安装（推荐）**

```
sudo snap install --classic code
```

#### **方法2：通过APT仓库安装**

```
# 添加微软GPG密钥
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg

# 添加VSCode仓库
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'

# 安装VSCode
sudo apt update
sudo apt install code -y
```

------

### **4. 配置SSH密钥（连接GitHub）**

#### **生成SSH密钥**

```
ssh-keygen -t ed25519 -C "your.email@example.com"
# 连续按Enter使用默认设置（密码可选）
```

#### **将公钥添加到GitHub**

1. 复制公钥内容：

   ```
   cat ~/.ssh/id_ed25519.pub
   ```

2. 登录GitHub → Settings → SSH and GPG keys → New SSH Key

3. 粘贴公钥并保存

#### **测试连接**

```
ssh -T git@github.com
# 看到 "You've successfully authenticated" 表示成功
```

------

### **5. 在VSCode中配置GitHub**

1. **打开VSCode** → 安装扩展：
   - `GitHub Pull Requests and Issues` (GitHub官方扩展)
   - `GitLens` (可选，增强Git功能)
2. **登录GitHub账户**：
   - 按 `Ctrl+Shift+P` 打开命令面板
   - 输入 `GitHub: Sign In` → 选择 `Sign in with Device`
   - 按提示在浏览器中完成授权（复制设备码到github.com/devicelogin）

------

### **6. 使用GitHub工作流**

#### **克隆仓库**

```
# 终端方式
git clone git@github.com:username/repo.git
```

或在VSCode中：

1. `Ctrl+Shift+P` → `Git: Clone`
2. 输入仓库URL（SSH格式：`git@github.com:username/repo.git`）

#### **提交更改**

1. 修改文件后，点击VSCode左侧的 **源代码管理图标** (或按 `Ctrl+Shift+G`)
2. 暂存更改：点击文件旁的 `+` 或输入提交信息后勾选✔️
3. 提交：输入提交信息 → 点击✔️（或按 `Ctrl+Enter`）

#### **推送/拉取代码**

- **推送**：点击状态栏的 🔼 (同步更改) → 选择 `Push`
- **拉取**：点击 🔽 (Pull) 或使用 `Git: Pull` 命令

#### **创建/切换分支**

1. 点击VSCode左下角分支名（如 `main`）
2. 选择 `+ Create new branch...` 或切换现有分支

------

### **7. 常见问题解决**

#### **权限被拒绝 (Publickey)**

- 确保SSH代理运行：

  ```
  eval "$(ssh-agent -s)"
  ssh-add ~/.ssh/id_ed25519
  ```

#### **VSCode无法检测Git**

- 在VSCode设置中指定Git路径：
  `文件 > 首选项 > 设置` → 搜索 `git.path` → 添加 `/usr/bin/git`

#### **提交时提示邮箱未验证**

- 在[GitHub邮箱设置](https://github.com/settings/emails)中验证邮箱

------

### **完整流程图**

![deepseek_mermaid_20250722_0b6997](./assets/deepseek_mermaid_20250722_0b6997.png)

> **提示**：
>
> - 优先使用 **SSH协议**（避免HTTPS频繁输密码）
> - 敏感操作（如强制推送）使用终端更可控
> - 定期执行 `git pull` 保持本地与远程同步



# Git连接Github

将本地 Git 连接到 GitHub，需要完成以下关键步骤：

------

### 一、配置 SSH 密钥（推荐方式）

#### 1. **生成 SSH 密钥**

在终端执行（替换为你的 GitHub 邮箱）：

```
ssh-keygen -t ed25519 -C "your_email@example.com"
```

- 按回车使用默认保存路径 (`~/.ssh/id_ed25519`)
- 可设置密码（可选，增强安全性）

#### 2. **将公钥添加到 GitHub**

- 复制公钥内容：

  ```
  cat ~/.ssh/id_ed25519.pub  # 复制输出的全部内容
  ```

- GitHub 操作路径：
  `Settings → SSH and GPG keys → New SSH key`
  → 粘贴公钥 → 命名（如 "My Laptop"）→ 点击 **Add SSH key**

#### 3. **测试连接

```
ssh -T git@github.com
```

✅ 成功提示：
`Hi username! You've successfully authenticated...`

------

### 二、配置 Git 用户信息（若未设置）

```
git config --global user.name "Mrz"
git config --global user.email "zxx-0714@qq.com"
```

> **重要**：邮箱需与 [GitHub 账户邮箱](https://github.com/settings/emails) 一致，否则贡献统计无法关联！

------

###  三、连接本地仓库与 GitHub

#### 场景 1：从零开始新仓库

1. 在 GitHub 创建空仓库（**不**勾选 README/.gitignore）

2. 本地初始化并关联：

   ```
   cd my-project
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin git@github.com:your-username/repo-name.git
   git push -u origin main  # 首次推送需加 `-u`
   ```

#### 场景 2：关联已有本地仓库 

```
git remote add origin git@github.com:your-username/repo-name.git
git branch -M main        # 确保分支名与 GitHub 一致（main/master）
git push -u origin main
```

#### 场景 3：克隆现有仓库

```
git clone git@github.com:your-username/repo-name.git
```

------

### 🔐 备选方案：HTTPS 连接（不推荐）

```
git remote add origin https://github.com/your-username/repo-name.git
```

- **缺点**：每次推送需输账号密码
- **改进**：使用 [Git Credential Manager](https://github.com/GitCredentialManager/git-credential-manager) 缓存凭证

------

### 🚨 常见问题排查

1. **权限拒绝 (Permission denied)**

   - 检查 `~/.ssh/id_ed25519.pub` 内容是否完整粘贴到 GitHub
   - 执行 `ssh-add ~/.ssh/id_ed25519` 添加密钥到代理

2. **分支名称冲突**

   - GitHub 默认分支为 `main`，旧仓库可能是 `master`

   - 解决方案：

     ```
     git branch -M main    # 重命名当前分支
     git push -u origin main
     ```

3. **HTTPS 推送失败**

   - GitHub 已禁用密码验证，需用 [Personal Access Token](https://github.com/settings/tokens) 代替密码

------

### ✅ 验证连接状态

```
git remote -v          # 查看关联的远程仓库
git remote show origin # 检查远程分支状态
```

> 💡 **最佳实践**：始终使用 SSH 协议 + SSH 密钥，安全且免密推送。





# Git配置查看

要查询 Git 当前使用的用户信息，有以下几种常用方法：

### 1. 查看全局配置（最常用）

```
# 查看全局用户名
git config --global user.name

# 查看全局邮箱
git config --global user.email

# 同时查看两者
git config --global --get user.name && git config --global --get user.email
```

### 2. 查看当前仓库配置（优先级更高）

```
# 查看当前仓库的用户名
git config user.name

# 查看当前仓库的邮箱
git config user.email

# 同时查看两者
git config --get user.name && git config --get user.email
```

### 3. 查看所有配置（包含系统级）

```
# 列出所有Git配置（含用户信息）
git config --list

# 过滤显示用户信息
git config --list | grep -E 'user\.name|user\.email'
```

### 4. 查看配置来源路径

```
# 显示配置值及其来源文件
git config --show-origin --get user.name
git config --show-origin --get user.email
```

输出示例：

```
file:/home/yourname/.gitconfig    your.name
file:.git/config                  your.email@example.com
```

------

### 优先级说明

Git 配置按优先级生效（从高到低）：

1. **仓库级配置**（当前项目目录下的 `.git/config`）
2. **全局配置**（用户主目录的 `~/.gitconfig`）
3. **系统级配置**（`/etc/gitconfig`）

当执行 `git config user.name` 时：

1. 先查找当前仓库配置
2. 若未设置，则查找全局配置
3. 最后查找系统配置

------

### 验证示例

```
$ git config --global user.name
John Doe

$ cd my-project/
$ git config user.name
Jane Smith  # 此仓库覆盖了全局配置
```

------

### 实用技巧

1. **快速查看当前用户**：

   ```
   git config user.name || git config --global user.name
   ```

2. **在 VSCode 中查看**：

   - 打开终端执行 `git config user.name`
   - 或安装 GitLens 扩展 → 查看状态栏用户信息

3. **检查提交者信息**（实际提交时使用的用户）：

   ```
   git log -1 --pretty=format:"%an <%ae>"
   # 输出：Jane Smith <jane@example.com>
   ```

> 注意：`user.name` 和 `user.email` 是独立配置项，建议同时检查两者以确保正确性。







# Git提交

---

## 1. **软（Soft）**
```bash
git reset --soft <commit-id>
```

- **作用**：只移动 `HEAD` 到指定提交，**保留工作区和暂存区的所有更改**。
- **结果**：你之前的更改会变成“已暂存”状态（staged），可以直接重新提交。
- **适用场景**：你想重新整理提交历史，但保留所有更改内容。

---

## 2. **混合（Mixed）【默认模式】**
```bash
git reset --mixed <commit-id>
```

- **作用**：移动 `HEAD`，**保留工作区的更改，但清空暂存区**。
- **结果**：你之前的更改会变成“未暂存”状态（unstaged），需要重新 `git add`。
- **适用场景**：你想撤销提交，但保留更改内容，重新整理后再提交。

---

## ⚠️ 3. **硬（Hard）**
```bash
git reset --hard <commit-id>
```

- **作用**：移动 `HEAD`，**同时重置工作区和暂存区，所有更改都会被丢弃**。
- **结果**：你的项目会完全回到那个提交的状态，**本地未提交的更改会丢失**。
- **适用场景**：你想彻底回退到某个历史版本，放弃所有后续更改。
- **风险提示**：这个操作不可逆，慎用！

---

## 4. **保留（Keep）**
```bash
git reset --keep <commit-id>
```

- **作用**：移动 `HEAD`，**但会保留你当前工作区中的本地更改**，前提是这些更改不会和回退起冲突。
- **结果**：更安全地回退历史，同时保留你在工作区的修改。
- **适用场景**：你想回退历史，但不想丢失当前正在进行的工作。

---

## 总结对比表：

| 模式  | HEAD移动 | 工作区更改 | 暂存区更改 | 用途简述                   |
| ----- | -------- | ---------- | ---------- | -------------------------- |
| Soft  | ✅        | ✅ 保留     | ✅ 保留     | 重新提交整理历史           |
| Mixed | ✅        | ✅ 保留     | ❌ 清空     | 默认模式，重新整理提交内容 |
| Hard  | ✅        | ❌ 丢弃     | ❌ 丢弃     | 彻底回退，放弃所有更改     |
| Keep  | ✅        | ✅ 保留     | ❌ 清空     | 安全回退，保留当前修改     |

---

## 你该选哪个？

- 如果你想**撤销提交但保留更改**，用 **mixed**。
- 如果你想**彻底回到某个历史状态**，用 **hard**。
- 如果你想**保留更改并重新提交**，用 **soft**。
- 如果你**不确定，怕丢东西**，用 **keep**。

---

需要我帮你根据具体情况选一个吗？你可以告诉我你现在的目标（比如：想撤销提交但保留代码，还是想彻底回退）。





# Git配置信息

在 Git 中配置 `user.name` 和 `user.email` 非常重要，它们主要有以下核心作用：

### 1. **标识提交作者 (Commit Attribution)**

- **核心功能：** 当你执行 `git commit` 时，Git 会自动将你配置的 `user.name` 和 `user.email` 嵌入到**本次提交的元数据**中。
- **查看方式：** 运行 `git log` 或 `git show` 查看提交历史时，每条提交记录都会明确显示是谁（`Author`）在什么时候进行了这次提交。
- **目的：** 清晰记录代码变更的责任人，便于追溯历史、问责、讨论变更原因。

### 2. **支持协作工作流 (Collaboration)**

- **区分贡献者：** 在多人协作的项目中，每个人的提交都带有其唯一的姓名和邮箱组合，这样就能精确区分出不同成员的贡献。
- **平台集成：** GitHub、GitLab、Gitee 等代码托管平台**主要依赖提交记录中的邮箱地址**来关联提交与平台上的用户账户：
  - 如果提交中的 `user.email` 与你托管平台账户绑定的**主邮箱**或**已验证的邮箱**匹配，平台就能：
    - 正确显示你的用户名和头像。
    - 将提交计入你的贡献图（绿色小方格）。
    - 在 Pull Request/Merge Request 中正确识别提交者。
  - **不匹配的后果：** 如果提交中的邮箱与平台账户无关或未验证，提交会被显示为匿名（只显示邮箱地址），且不计入你的贡献统计。

### 3. **权限管理（间接关联）**

- 虽然 Git 本身不直接基于提交者信息做权限控制（权限通常在仓库服务器如 GitHub/GitLab 上配置），但服务器端权限系统**可能**会参考提交者信息（尤其是邮箱）作为额外的审计或关联依据（结合账户权限）。更重要的是，清晰的作者信息是权限审计的基础。

### 4. **自动化脚本/钩子 (Hooks/CI)**

- 一些自定义的 Git 钩子脚本或持续集成/持续部署流水线可能会读取提交的作者信息（`user.name` 或 `user.email`）来执行特定操作，例如：
  - 根据提交者邮箱自动分配代码审查任务。
  - 在提交信息中自动添加签名或特定标签。
  - 触发针对特定团队或个人的构建流程。





![image-20250723000435674](./assets/image-20250723000435674.png)





# 常见问题：

```
vim /etc/ssh/sshd_config
// 找到 PubkeyAuthentication
PubkeyAuthentication yes    
##（原先这里是no，开启后问题就解决了）
```

重启 service sshd restart