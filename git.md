#Git

##Blogs

- [reset, checkout, revert的区别](http://segmentfault.com/a/1190000003102737)
- [remove sensitive data from github](https://help.github.com/articles/remove-sensitive-data/)

##Tutorial

- [liaoxuefeng's tutorial](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

## Githug

今天看到别人推荐的command-line小游戏，可以在工作无聊的时候玩玩，[github地址](https://github.com/Gazler/githug).
这里有一份[攻略](http://www.jianshu.com/p/482b32716bbe)

会的就不记录了，主要记录平时不怎么用的不熟的。

### include

在`.gitignore`里面

`*.a`表示ignore所有以`.a`结尾的文件，加了`!`就表示不忽略

### 第十二关(rm cached)

讲一个新文件从 `staging area` 中删除。按照要求，不应该直接从硬盘上删除这个文件，只是从 Git 中删除而已。
加上 `--cache` 可以是文件只是从 `staging area` 中移除，不会真正的删除物理文件，如果要连这个物理文件也一起删除，请使用 `-f` 选项

### tags

`git tag new_tag`

`git tag new_tag -a "annotated tag"`

`git push --tags origin master`

### 第二十关(commit in the future)

```
git commit --date=20.01.2016T14:00:00
```

### Reset

**unstage**

`git reset HEAD <file>`

**discard changes in workding directory**

`git checkout -- <file>`

**reset last commit**

`git reset --soft HEAD^1`

* `--soft` 将上一次的修改放入`staging area`
* `--mixed`　将上一次的修改放入`working directory`
* `--hard`　抛弃上一次的修改

### `git blame`

神命令，找人背锅！

```
git-blame - Show what revision and author last modified each line of a
            file
```

### 三十四关　`checkout`

当branch和tag重名的时候

`git checkout tags/v1.2`

### HEAD

`HEAD`可以当成就是current branch.

`HEAD^1` means the first parent of the tip of the current branch. Git commits
can have more than one parent. `HEAD^` is short for `HEAD^1`, you can also
use `HEAD^2` and so on.

You can get to parents of any commit, not just `HEAD`. for example, 
`master~2` means the grandparent of the tip of the master branch, favoring
the first parent in cases of ambiguity. These specifiers can be chained 
arbitrarily, e.g., `topic~3^2`.

>from [stackoverflow](http://stackoverflow.com/questions/2221658/whats-the-difference-between-head-and-head-in-git)

```
G   H   I   J
 \ /     \ /
  D   E   F
   \  |  / \
    \ | /   |
     \|/    |
      B     C
       \   /
        \ /
         A

A =      = A^0
B = A^   = A^1     = A~1
C = A^2  = A^2
D = A^^  = A^1^1   = A~2
E = B^2  = A^^2
F = B^3  = A^^3
G = A^^^ = A^1^1^1 = A~3
H = D^2  = B^^2    = A^^^2  = A~2^2
I = F^   = B^3^    = A^^3^
J = F^2  = B^3^2   = A^^3^2
```

- `HEAD^2`表示的是第2个parent
- `HEAD~2`表示的是上面第2层的parent(没有specify的话默认都是从第一个网上)

### fetch, merge, pull

`pull`是由`fetch`和`merge`组成的

### rebase

`git rebase master feature`表示将`feature`上的修改在`master`上重新应用一遍

`git rebase -i` interactive mode

### repack

`git repack` is used to combine all objects that do not currently reside in a "pack", into a pack. It can also be used to re-organize existing packs into a single, more efficient pack.
节省空间。

- `git gc`
- `git repack`
- `git prune`

### cherry-pick

`git cherry-pick <hash>`应用某一个commit的修改到目前的branch上。

### git grep

`git grep` print lines matching a pattern。平时用的不多，我一般用
`grep -r "pattern"`

### 四十六 `merge squash`

在master branch上`git merge --squash long-feature-branch`，　等同于

- `git rebase -i master long-feature-branch`
- `git checkout master; git merge long-feature-branch`

### bisect

`git bisect`是一个很好用的用来debug哪一个commit出了问题的工具，就是用二分法
来找到出错的commit.

- 先用`git log`找到working的commit和broken的commit,记录下前几位hash
- `git bisect start`，开始git bisect
- `git bisect good <hash>`, 告诉一个起始的working的commit
- `git bisect bad <hash>`, 告诉一个已经broken的commit
- 会自动选择middle branch并且checkout这个branch
- 然后检测是否还working, 并告诉`bisect`结果
    + 如果working, `git bisect good`
    + 已经不working, `git bisect bad`
－直到最后找到第一个broken的commit

### `git add -p`

提交文件里的部分修改

### reflog

`git reflog`可以列出所有的操作记录

### revert

`revert`只会撤销选中的commit,而之后的commit操作还会保留，而`reset`会将
之后的所有commit修改全部退回staging are或者丢掉. `revert`会生成一个新的
commit

### restore

- `git reflog`查看操作记录
- `git checkout <hash>`

### submodule

inspects, updates and manages submodules.

A submodule allows you to keep another Git repository in a subdirectory of your repository.
The other repository **has its own history**, which does not interfere with the history of the current repository.
