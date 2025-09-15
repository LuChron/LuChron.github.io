## 📦 Git 版本控制

Git 是分布式版本控制系统，是现代软件开发不可或缺的工具。

## 🛠️ 常用命令速查

### 基础操作
```bash
# 初始化仓库
git init

# 添加文件到暂存区
git add <file>
git add .

# 提交更改
git commit -m "提交信息"

# 查看状态
git status
git log
```

### 分支管理
```bash
# 创建并切换分支
git checkout -b <branch-name>

# 合并分支
git merge <branch-name>

# 删除分支
git branch -d <branch-name>
```

### 远程操作
```bash
# 添加远程仓库
git remote add origin <url>

# 推送到远程
git push origin <branch>

# 从远程拉取
git pull origin <branch>
```

