## 当你遇到中间版本不想要了想要回退到之前版本就可以使用revert这个命令了

```
git log -3

commit 1234
Author xxx <ddd@xx.com>
Date: 2017:00:11


commit 5678
Author xxx <ddd@xx.com>
Date: 2017:00:11


commit 9900
Author xxx <ddd@xx.com>
Date: 2017:00:11
```
当你查看过去日志时，发现  1234、 5678 这两个版本都是不想要的，要回退到9900 这个版本

这时候可以使用revert
`git revert 9900`

这个时候会产生一个新的日志，就是你目前回退到9900版本时的状态日志， 如果哪天还想再回来， 这里就有一条记录，可以让你有迹可循。

这时，你的代码就愉快的回到了9900版本， 如果想推到远程仓库，再加一句
`git push -f`
就强制推到了远程。
