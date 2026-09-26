
<button onclick="document.getElementById('neirong0').scrollIntoView({behavior:'smooth'})"
        style="position: fixed; right: 5px; top: 50%; transform: translateY(-50%); 
               border: none; border-radius: 8px; padding: 5px 10px; 
               background: #0066cc; color: white; cursor: pointer; font-size: 14px;z-index:1;">
    返回<br>目录
</button>


# git速查
<span id="neirong0"></span>
## 具体步骤  
---基础操作---  
[✅] [1 确认git是否安装](#neirong1)    
[✅] [2 配置提交身份](#neirong2)   
[✅] [3 初始化仓库](#neirong3)   
[✅] [4 配置忽略规则](#neirong4)  
[✅] [5 提交](#neirong5)   
----与远程仓库同步  
[✅] [1 远程仓库](#neirong6)   
[✅] [2 配置 SSH 信任（每台电脑一次）](#neirong7)   
[✅] [3 关联本地仓库](#neirong8)  
[✅] [4 第一次push](#neirong9)  
[✅] [5 以后每次更新代码的标准流程](#neirong10)

<span id="neirong1"></span>
## 1确认git是否安装
```
git --version
```
<span id="neirong2"></span>
## 2配置提交身份
先检查是否已配置：
```
git config --global user.name
git config --global user.email
```
如果未配置，执行：
```
git config --global user.name wh107
git config --global user.email 2517054133@.qq.com
```
<span id="neirong3"></span>
## 3初始化仓库
```
git init
```
查看状态
```
git status
```
<span id="neirong4"></span>
## 4配置忽略规则
```
.gitignore 本身应该提交（它是项目规则）
.git 不需要写进 .gitignore（Git 会自动管理）
```
<span id="neirong5"></span>
## 5提交
```
git add index.html
```
```
git add .
```
```
git status
```
```
git commit -m "第一次提交"
```
Git 的价值不是“完成初始化”，而是“持续记录变化”。
建议你现在做一个小改动（例如改一行标题文字），然后再走一遍：
```
git add .
git commit -m "修改首页标题文案"
```
这样你就会开始形成真正的版本管理直觉：
每次有意义的改动，都应该落成一个可解释、可回退的提交。

<span id="neirong6"></span>
# 与远程仓库同步
## 1远程仓库
```
git@github.com:wh107/mtest.git
```

<span id="neirong7"></span>
## 2配置 SSH 信任（每台电脑一次）
```
ssh-keygen -t ed25519 -C 2517054133@.qq.com
```
复制公钥
```
cat ~/.ssh/id_ed25519.pub
```
添加到 GitHub

GitHub -> Settings -> SSH and GPG keys -> New SSH key  
把公钥粘贴进去保存。

验证连通性
```
ssh -T git@github.com
```
<span id="neirong8"></span>
## 3关联本地仓库
回到项目目录  
添加远程地址
```
git remote add origin git@github.com:wh107/mtest.git
```
这里 origin 是远程仓库的常见命名。

你可以验证一下：
```
git remote -v
```
是用来查看当前仓库配置了哪些远程仓库地址的命令。  
git remote → 管理远程仓库的命令  
· -v → 是 --verbose（详细）的缩写，会把对应的 URL 也显示出来

有什么用  
· 确认 git remote add 有没有成功  
· 检查远程地址写错了没有  
· 看看一个仓库关联了几个远程（比如同时有 origin 和 upstream）

如果想修改远程地址，不用删了重加，可以直接：
```
git remote set-url origin git@github.com:wh107/新地址.git
```
<span id="neirong9"></span>
## 4第一次push
先确认当前分支名：
```
git branch
```
如果是 main
```
git push -u origin main
```
如果是 master：
```
git push -u origin master
```
Git 只有在第一次 commit 之后才会真正创建分支（比如 main）。在没有任何提交之前，main 分支是不存在的，所以 push 时找不到它。

情况一：还没提交过（最常见）

```bash
# 1. 添加文件
git add .

# 2. 提交
git commit -m "first commit"

# 3. 再推送
git push -u origin main
```

情况二：本地分支叫 master，但你推的是 main

可以先把分支重命名：

```bash
git branch -M main
git push -u origin main
```

git branch -M main 会把当前分支强制重命名为 main（-M 是强制重命名）。

补充：如果你连文件都还没有

新建一个文件再提交，比如：

```bash
echo "# mtest" > README.md
git add .
git commit -m "first commit"
git push -u origin main
```

核心就一句话：先 commit，才有分支，才能 push。

<span id="neirong10"></span>
## 以后每次更新代码的标准流程
```
# 本地：保存 + 推送
git add .
git commit -m "写清楚这次改了什么"
git push
```
```
# 本地：保存 + 推送
# 服务器（SSH 登录后）：拉取
cd ~/项目根目录
git pull

```
GitHub Desktop 也是可选项

如果你暂时不想记太多命令，可以用 GitHub Desktop（官方图形工具）：

    可视化查看改动
    图形化提交（Commit）
    一键推送（Push）

