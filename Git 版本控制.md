#                                Git 版本控制

1、版本控制是一个概念，要借助工具例如svn、git实现

2、Git是分布式版本控制工具，SVN是集中式的版本控制工具，集中式是指只有一个中心仓库，所有客户端往这个仓库提交。

3、Git分为三个区域。

<img src="D:\typora_photo\image-20240417102611264.png" alt="image-20240417102611264" style="zoom:67%;" />

![image-20240417103455360](D:\typora_photo\image-20240417103455360.png)

4、GIt命令

![image-20240417103541593](D:\typora_photo\image-20240417103541593.png)

![image-20240417103615865](D:\typora_photo\image-20240417103615865.png)

git.add * 或者git add . 表示提交所有文件到暂存区

git status:观察暂存区的文件情况

![image-20240417104332845](D:\typora_photo\image-20240417104332845.png)

![image-20240417110720230](D:\typora_photo\image-20240417110720230.png)

![image-20240417110739886](D:\typora_photo\image-20240417110739886.png)

![image-20240417110809583](D:\typora_photo\image-20240417110809583.png)

git reset hard HEAD^ :表示回退一次

git reset hard HEAD^^ :表示回退两次

git reset hard HEAD仅能回退两次，大于三次用别的命令

![image-20240417112512096](D:\typora_photo\image-20240417112512096.png)

git rm x.txt表示删除文件，前提是这个文件是被git版本控制的，在工作区删除一个文件可以同步到暂存区，再利用commit命令提交到版本区即可。如果是手动进行删除的话，就需要先add再commit，操作繁琐。

git rm -r x.txt:删除文件夹，前提文件夹必须有东西，如果add时是空文件夹，git自动忽略掉，不进行控制。

![image-20240417113629496](D:\typora_photo\image-20240417113629496.png)

![image-20240417113804718](D:\typora_photo\image-20240417113804718.png)

当你站在一个分支master去创建另一个分支时，只有当前分支有文件并且提交到版本区，才可以去切换分支，否则会删除到master分支。

![image-20240417133917750](D:/typora_photo/image-20240417133917750.png)

![image-20240417135525779](D:/typora_photo/image-20240417135525779.png)

git remote add 别名+SSH地址，其中https地址已经废弃了。

https://www.bilibili.com/video/BV1HM411377j?p=11&vd_source=68d62bca83c00beffe7ed7e574e02f6c

> 用SSH需要配置SSH公钥。
>
>  github的SSH配置：刚开始我写的是passohrase是code

![image-20240417173126363](D:/typora_photo/image-20240417173126363.png)

接着在ssh目录找到id_rsa.pub文件(若是第二次操作文件名字是变为自己设定的文件名)，复制内容，打开github，找到settings。

![image-20240417173350462](D:/typora_photo/image-20240417173350462.png)

git push -u 别名 分支名

注意：github与gitee差别：在推送的时候分支名的引号问题

github:无引号

![image-20240417142123283](D:/typora_photo/image-20240417142123283.png)

![image-20240417173756875](D:/typora_photo/image-20240417173756875.png)

gitee 有引号

![image-20240417142108123](D:/typora_photo/image-20240417142108123.png)

![image-20240417142948152](D:/typora_photo/image-20240417142948152.png)

​                      注意：其中的origin是一个远程仓库分支的别名，可以任意取值。

![image-20240417143241881](D:/typora_photo/image-20240417143241881.png)

![image-20240417175832908](D:/typora_photo/image-20240417175832908.png)

注意：当从远程克隆下来一个仓库时，仓库的所有分支会被克隆下来，可以用git checkout切换任意分支，但是git branch是查看不到有几个分支的。如果此时又在远程仓库创建一个分支了，可以在本地直接用git pull 进行拉取，直接是git pull后面不用带分支名，就把所有的分支都克隆下来了。推送到远程直接还是git push即可。