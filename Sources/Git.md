### 配置

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

### 指令

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