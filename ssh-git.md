## 1 生成 SSH key（ED25519）
GitHub 官方推荐算法：ed25519

生成 SSH key（ED25519）:

ssh-keygen -t ed25519 -C "your_email@example.com"

~/.ssh/id_ed25519

~/.ssh/id_ed25519.pub

## 2 启动 ssh-agent 并添加 key
WSL 每次重启都要重新加载（除非你配置自动启动）。

启动 agent

eval "$(ssh-agent -s)"

添加密钥

ssh-add ~/.ssh/id_ed25519

确认：

ssh-add -l

如果看到 fingerprint，说明成功。

## 3 复制公钥

查看公钥：

cat ~/.ssh/id_ed25519.pub

复制整行：

ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAI... your_email@example.com

## 4 添加到 GitHub
进入：

👉 https://github.com/settings/keys

点击：

New SSH key

填写：

Title：WSL-Ubuntu / MyLaptop / 任意名称

Key：粘贴刚才内容

## 5 测试连接（关键）
⚠️ GitHub 用户名不写邮箱！

ssh -T git@github.com

第一次会问：

Are you sure you want to continue connecting (yes/no)?

输入：

yes

成功会看到：

Hi username! You've successfully authenticated...