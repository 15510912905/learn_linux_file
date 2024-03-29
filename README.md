# learn_linux_file

git clone https://github.com/15510912905/learn_linux_file.git                     /* 克隆主分支 */
git clone git@github.com:15510912905/learn_linux_file.git                         /* 克隆主分支 */
git clone -b 20210208_1152 git@github.com:15510912905/learn_linux_file.git        /* 克隆分支代码 */
git clone -b 20210208_1152 https://github.com/15510912905/learn_linux_file.git    /* 克隆分支代码 */

git push https://github.com/15510912905/learn_linux_file.git                      /* 推送当前分支 */
git push git@github.com:15510912905/learn_linux_file.git                          /* 推送当前分支 */
git push https://github.com/15510912905/learn_linux_file.git master:branch        /* 将本地某分支推送到远程某分支 */
																                  
git init                                                                          
git add <filename>                                                                
git add *                                                                         /* 增加文件是到暂存区 临时保存 */
git commit -a -m "log"                                                            /* 提交到HEAD 指向你最后一次提交的结果 */
git push origin master                                                            /* 将本地仓库推送到远端 origin 远端地址 master远端分支 不填为默认为当前分支 eg:1.git push https://github.com/15510912905/learn_linux_file.git 2.git push git@github.com:15510912905/learn_linux_file.git */
git remote add origin <server>                                                    /* 如果你还没有克隆现有仓库，并欲将你的仓库连接到某个远程服务器 */
			
git log                                                                           /*查看日志id*/
git reset --hard id                                                               /*回退到id*/
git reflog			                                                              /*查看命令id*/
			
git checkout -b feature_x                                                         /* 创建一个叫做“feature_x”的分支，并切换过去 */
git checkout master                                                               /* 切换分支 */
git branch -d feature_x                                                           /* 删掉分支 */
git push origin <branch>                                                          /* 推送 */  
git branch                                                                        /* 查看分支 -a 查看所有分支详情 */   

git rebase master                                                                 /* 直线提交 */              
git symbolic-ref HEAD                                                             /* 查看头的指向 */              
												                                  
git pull                                                                          /* 更新 */
git pull https://github.com/15510912905/learn_linux_file.git master:branch        /* 从远程某分支更新到本地某分支 */ 

git merge <branch>                                                                /* 合并分支 需要合并到什么分支 需要先切换到此分支 然后将要合并的分支填写到branch处 eg:将branch合并到master 1.git checkout master 2.git merge branch */
git merge -Xignore-space-change whitespace                                        /* 高级合并 */
git mergetool                                                                     /* 可视化合并工具 */

git diff <source_branch> <target_branch>                                          /* 预览差异 */
git diff branch1 branch2 --stat
git diff branch1 branch2 具体文件路径
git log branch1..branch2
git diff                                                                          /* 合并分支时查看不同点 */

git status -s                                                                     /* 查看冲突 */
git add *                                                                         /* 告诉GIT冲突已解决 */
git commit                                                                        /* 确认提交 */	
git branch -d feature_x                                                           /* 合并完成后记得删掉分支 */
																                  
git tag -a V1.0.0                                                                 /* 创建标签 */
git log                                                                           /**/
												                                  
git checkout -- <filename>                                                        /* 替换掉本地改动 */
												                                  
git fetch origin                                                                  /* 丢弃你在本地的所有改动与提交 */
git reset --hard origin/master                                                    /* 到服务器上获取最新的版本历史，并将你本地主分支指向它 */
												                                  
gitk                                                                              /* 内建的图形化 */
git config color.ui true                                                          /* 彩色的 git 输出 */
git config format.pretty oneline                                                  /* 显示历史记录时，每个提交的信息只显示一行 */
git add -i                                                                        /* 交互式添加文件到暂存区 */
												                                  
ssh-keygen -t rsa -C "arris9@163.com"                                             /* 生成 SSH Key */

git config --global user.name "6912"
git config --global user.email "zhourui@maccura.com"





