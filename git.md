#Git

##Blogs

- [reset, checkout, revert的区别](http://segmentfault.com/a/1190000003102737)
- [remove sensitive data from github](https://help.github.com/articles/remove-sensitive-data/)

##Tutorial

- [liaoxuefeng's tutorial](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

## Githug

今天看到别人推荐的command-line小游戏，可以在工作无聊的时候玩玩，[github地址](https://github.com/Gazler/githug).

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
