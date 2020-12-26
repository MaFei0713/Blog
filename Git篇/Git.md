# Git 基础篇

[系统学习链接](http://iissnan.com/progit/html/zh/ch1_1.html)

[解决git项目体积过大的问题](https://juejin.cn/post/6844903848864137229)

### git clone与git pull的时候不拉大文件

git仓库有时用lfs管理存储些大的二进制文件，但很多开发本地编程环境并不需要，所以默认将这些文件clone或者pull到本地后，即占用存储空间，又在clone或者pull时影响速度。所以可以使用下面方法不pull或者clone lfs管理的大文件：  
`GIT_LFS_SKIP_SMUDGE=1 git clone <repository-addr>`  
使用该方法，即使以后git pull，也不会把大文件拉下来了。如果以后想再拉取大文件，可以使用 `git lfs pull`


# Git 高级篇

[git-filter-branch](https://docs.github.com/cn/free-pro-team@latest/github/authenticating-to-github/removing-sensitive-data-from-a-repository) && [BGF](https://rtyley.github.io/bfg-repo-cleaner/)