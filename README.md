# learn_linux_file
git clone https://github.com/15510912905/learn_linux_file.git
git clone git@github.com:15510912905/learn_linux_file.git       /* 克隆主分支 */

git init
git add <filename>
git add *                                           /* 增加文件是到暂存区 临时保存 */
git commit -a -m "log"                              /* 提交到HEAD 指向你最后一次提交的结果 */
git push origin master                              /* 将本地仓库推送到远端 origin 远端地址 master远端分支 不填为默认为当前分支 eg:1.git push https://github.com/15510912905/learn_linux_file.git 2.git push git@github.com:15510912905/learn_linux_file.git */
git remote add origin <server>                      /* 如果你还没有克隆现有仓库，并欲将你的仓库连接到某个远程服务器 */

git checkout -b feature_x                           /* 创建一个叫做“feature_x”的分支，并切换过去 */
git checkout master                                 /* 切换分支 */
git branch -d feature_x                             /* 删掉分支 */
git push origin <branch>

git pull                                            /* 更新 */
git merge <branch>                                  /* 合并分支 需要合并到什么分支 需要先切换到此分支 然后将要合并的分支填写到branch处 eg:将branch合并到master 1.git checkout master 2.git merge branch */
git diff <source_branch> <target_branch>            /* 预览差异 */

git tag -a V1.0.0                                   /* 创建标签 */
git log                                             /**/

git checkout -- <filename>                          /* 替换掉本地改动 */

git fetch origin                                    /* 丢弃你在本地的所有改动与提交 */
git reset --hard origin/master                      /* 到服务器上获取最新的版本历史，并将你本地主分支指向它 */

gitk                                                /* 内建的图形化 */
git config color.ui true                            /* 彩色的 git 输出 */
git config format.pretty oneline                    /* 显示历史记录时，每个提交的信息只显示一行 */
git add -i                                          /* 交互式添加文件到暂存区 */

ssh-keygen -t rsa -C "arris9@163.com"              /* 生成 SSH Key */

