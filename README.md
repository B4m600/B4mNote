[TOC]



# PhotoShop

- Ctrl + T: 变换图形;
- Ctrl + J: 复制选中区域;
- Ctrl + G: 将选中图层编组;
- Ctrl + I: 颜色反向;
- Ctrl + 通道层: 选中(黑白)通道对应的区域;
  - Ctrl + Shift + I: 反选选区;
  - 图层->添加矢量蒙版: 根据通道层扣除背景;
    - Alt + 图层蒙版层: 进入蒙版;

# PremierPro

### [时间线]

- Shift + 左/右键头: 移动一个帧
- M: 添加标记
- I: 标记入点
- O: 标记出点
  - ": 删除区域并拼接左右两侧;

# SublimeText

- Alt+F3: 选中文本按下快捷键，即可一次性选择全部的相同文本进行同时编辑
- Alt+Shift+1: 窗口分屏，恢复默认1屏
- Alt+Shift+2: 左右分屏-2列
- Alt+Shift+3: 左右分屏-3列
- Alt+Shift+4: 左右分屏-4列
- Alt+Shift+5: 等分4屏
- Alt+Shift+8: 垂直分屏-2屏
- Alt+Shift+9: 垂直分屏-3屏
- Ctrl+/: 注释单行
- Ctrl+: 打开搜索框，自动带#，输入关键字，查找文件中的变量名、属性名等
- Ctrl+→: 向右单位性地移动光标，快速移动光标
- Ctrl+←: 向左单位性地移动光标，快速移动光标
- Ctrl+Alt+↑: 向上添加多行光标，可同时编辑多行
- Ctrl+Alt+↓: 向下添加多行光标，可同时编辑多行
- Ctrl+D: 选中光标所占的文本，继续操作则会选中下一个相同的文本
- Ctrl+Enter: 在下一行插入新行
- Ctrl+F: 打开底部搜索框，查找关键字
- Ctrl+F2: 设置书签
- Ctrl+G: 打开搜索框，自动带：，输入数字跳转到该行代码
- Ctrl+J: 合并选中的多行代码为一行
- Ctrl+K+0: 展开所有折叠代码
- Ctrl+K+B: 开启/关闭侧边栏
- Ctrl+K+K: 从光标处开始删除代码至行尾
- Ctrl+K+L: 转换小写
- Ctrl+K+U: 转换大写
- Ctrl+L: 选中整行，继续操作则继续选择下一行，效果和
- Ctrl+M: 光标移动至括号内结束或开始的位置
- Ctrl+P: 打开搜索框
- Ctrl+PageDown: 向左切换当前窗口的标签页
- Ctrl+PageUp: 向右切换当前窗口的标签页
- Ctrl+R: 打开搜索框，自动带@，输入关键字，查找文件中的函数名
- Ctrl+Shift+/: 注释多行
- Ctrl+Shift+[: 选中代码，按下快捷键，折叠代码
- Ctrl+Shift+]: 选中代码，按下快捷键，展开代码
- Ctrl+Shift+↑: 将光标所在行和上一行代码互换
- Ctrl+Shift+→: 向右单位性地选中文本
- Ctrl+Shift+↓: 将光标所在行和下一行代码互换
- Ctrl+Shift+←: 向左单位性地选中文本
- Ctrl+Shift+D: 复制光标所在整行，插入到下一行
- Ctrl+Shift+Enter: 在上一行插入新行
- Ctrl+shift+F: 在文件夹内查找，与普通编辑器不同的地方是sublime允许添加多个文件夹进行查找，略高端，未研究
- Ctrl+Shift+K: 删除整行
- Ctrl+Shift+L: 先选中多行，再按下快捷键，会在每行行尾插入光标，即可同时编辑这些行
- Ctrl+Shift+M: 选择括号内的内容
- Ctrl+Shift+P: 打开命令框
- Ctrl+T: 左右字母互换
- Ctrl+Tab: 按文件浏览过的顺序，切换当前窗口的标签页
- Ctrl+U: 自动读取图片宽高
- Ctrl+Y: 恢复撤销
- Ctrl+Z: 撤销
- Esc: 退出光标多行选择，退出搜索框，命令框等
- F11: 全屏模式
- F6: 单词检测拼写
- shift+↑: 向上选中多行
- Shift+→: 向右选中文本
- shift+↓: 向下选中多行
- Shift+←: 向左选中文本.
- Shift+F11: 免打扰模式
- Shift+Tab: 向左缩进

# Blender

- Shift + A: 添加;
- Ctrl + P: 设置父级;
- R: 旋转;
- G: 移动;
- S: 缩放;

### [编辑模式]

- L:选中当前鼠标指向的物体;
- Ctrl+J: 合并所选内容;
- E: 挤出下一个骨骼;
- P: 分离选中内容;

### [姿态模式]

- Shift + I: 添加IK;

# Vim

### [按键指令]

- gg
  - 光标移至首行
- G
  - 光标移至末行
- u
  - 撤回
  - Ctrl + R
    - 取消撤回
- i
  - 插入文本模式
  - 在光标前插入文本
- a
  - 插入文本模式
  - 在一行后添加文本
- v
  - 可视选择模式
  - D
    - 删除选择内容
- D
  - 从当前光标位置删除至行尾

### [:指令]

- :q
- :q!
  - 强制退出
- :w
- :wq
- :set encoding=utf-8
  - 设置编码为UTF-8
- :set backspace=2
  - 设置backspace按键可以删除任何字符
- :%!xxd
  - 将二进制文件的乱码内容翻译为二进制
  - :%!xxd -r
    - 返回至乱码内容
- :goto 10
  - 跳转到第10个字
- :10
  - 跳转到第10行

# Git

### [配置]

- ssh-keygen -t rsa -C '2656980584@qq.com'
  - 生成公钥;
  - 运行后`ls ~/.ssh/`中包含`id_rsa.pub`;
  - `cat ~/.ssh/id_rsa.pub`查看公钥内容;
- git config --global user.name "用户名"
- git config -- global user.email "邮箱"
- ssh -T git@gitte.com || ssh -T git@github.com
  - 建立连接;
  - `Received disconnect from 162.241.169.11 port 22:2: Too many authentication failures
    Disconnected from 162.241.169.11 port 22`
    - 将`/etc/ssh/sshd_config`中MaxAuthTries 10修改大些;

### [指令]

- git init

  - 初始化仓库;
- git add

  -  将文件添加到本地仓库提交缓存; `git add test.txt`;
- -- all: 所有改动文件都添加到缓存区;
- git restore
  - 修复指定文件; `git restore test.txt`;
- git commit

  - -m: 将提交描述信息作为参数; `git commit -m "添加了新文件\"test.txt\"。 "`; `git commit test.txt -m "更新单独文件"`;
  - --amend: 改写提交信息; `git --amend`;
- git log

  - 查看日志;
  - --stat: 看到每次提交的简略的统计信息;
  - -- graph
  - --pretty=oneline
  - --abbrev-commit
- git status

  - 查看文件是否被改动;
- git checkout

  - 切换分支; `git checkout master`;

  - --: 将文件撤销到最近一次修改的状态; `git checkout -- test.txt`;
- git rm

  - 删除文件;
- git reflog

  - 查看提交历史;
- git merge

  - 合并分支; `git merge dev`;
- git branch

  - -a: 查看分支; `git branch -a master`;
  - -D: 删除本地分支; `git branch -D tmp`;
  - -m: 修改分支名称; `git branch -m dev newdev`;
- git stash

  - 保存当前工作状态;
  - list: 查看当前存储了多少工作状态; `git stash list`;
- git fetch

  - 拉取远程所有分支;
  - 拉取指定分支最新内容; `git fetch dev`;
- git diff

  - 查看不同分支文件差异; `git diff master dev test.txt`;
- git clone

  - 克隆默认分支;
  - -b: 选择分支克隆; `git clone -b dev`;
  - `fatal: unable to access 'https://github.com/B4m600/Sheeps/': SSL certificate problem: unable to get local issuer certificate` 
    - `git config --global http.sslverify false`
- git push

  - `git push <远程主机名> <本地分支名>:<远程分支名>`;
  - 如果本地分支名与远程分支名相同: `git push <远程主机名> <本地分支名>`;
  - --force: 如果本地版本与远程版本有差异,但又要强制推送;
  - --delete: 删除主机的分支; `git push origin --delete master`;

# MySql

- show databases;
  - 显示全部数据库
- use 数据库名;
  - 指定数据库
- show tables;
  - 显示全部表
- select * from 表名;
  - 查看表的全部信息
- union语句
  - 将多个select语句(两个或多个)的结果组合到一个结果集中，并删除结果集中的重复数据。
  - union中的每个查询必须拥有相同的列数。
  - `select column,…from table1 union select column,…from table2;`
  - `select name,sec,age from pte union select 1,2,3 from pte;`
- order by语句
  - 用来判断表的列数(二分法)。
  - `select * from pte order by 2;`

# SqlMap

### sqlmap -u

- sqlmap -u url -dbs
  - 查找全部库(暴库)
- sqlmap -u url --current-user
  - 当前使用的账户
- sqlmap -u url -b
  - 检索DBMS Banner
- sqlmap -u url --current-db
  - 当前的数据库
- sqlmap -u url --hostname
  - 当前主机名
- sqlmap -u url --is-dba
  - 检测当前用户是否为数据库管理员
- sqlmap -u url -passwords
  - MySql的登录账户和密码
- sqlmap -u url -D 指定数据库名 -tables 指定数据库名
- sqlmap -u url --dbms=数据库名 --current-db

# Python

- python -m http.server 9999
  - 在局域网链接http://0.0.0.0:9999上建立当前文件夹文件传输页面。 

# Linux

- clear
- pwd
  - 工作目录
- chmod
  - chmod +x Demo.exe
