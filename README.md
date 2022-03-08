# Order

# 内部项目，严禁公开。

# 使用 `push -f` 指令前要仔细确认

## 协作流程

1. 发 issue
2. 在 master 分支最新 commit 上派生分支
3. 在新分支上进行开发
4. 开发完成后向 master 分支发起 pr
5. github ci 通过后 merge 分支
6. 关闭 issue

### 发 issue

你可以在 issue 中查看当前是否有新的任务。一般地，每个 issue 都只会 assign 一个人，你只需要完成自己的工作就好了。

如果在 issue 中没有需要你完成的任务，你可以创建一个 issue，assign 一个人来完成这项工作，当然，可以 assign 你自己。

创建好 issue 后，你可以按照对应的 issue 编号建立分支来开始你的工作。

### 在 master 分支最新 commit 上派生分支

你不应该直接在 master 分支修改任何内容，做任何更改前要使用你自己的分支。

如果你还没有创建分支，使用下面的指令创建你的分支：

> 注意！新建分支前一定要确保当前分支为 master 分支，且已经拉取了最新版本的代码

```bash
git checkout -b <branch_name>
```

执行完这条指令后，git 会自动切换到新的分支。

如果你已经创建过分支，可以使用下面的指令切换到你的开发/修复分支：

```bash
git checkout <branch_name>
```

如果你不知道目前处于哪一个分支，可以使用如下指令：

```bash
git branch
```

### 在新分支上进行开发

切换到自己的分支后，你可以按照你的喜好随意 commit，当你认为你的工作做完后，将代码 push 到 GitHub，之后，可以向 master 分支发起 pr。

使用下面的指令将分支的代码上传到 GitHub：

```bash
git push origin <branch_name>
```

### 开发完成后向 master 分支发起 pr

开发完成后，打开 GitHub，向 master 分支发起 pull request。

### github ci 通过后 merge 分支

GitHub 的 action 会自动化地编译你的代码，当编译通过后，你可以邀请其他人来审阅及合并这次 pr。

如果编译没有通过，你可以在分支下继续开发，并提交新的 commit。

如果你不需要其他人来审阅这次 pr，你可以立即合并它，合并成功后，删除你的分支。

### 关闭 issue

开发完成后，关闭对应的 issue。

## 如何删除分支

首先使用如下指令切换到 master 分支：

```bash
git checkout master
```

之后使用如下指令删除本地分支：

```bash
git branch -d <branch_name>
```

> 删除分支前请确保分支在 GitHub 上已合并或弃用（pr 被 merge 或关闭）

## 分支冲突怎么办

一般地，本项目的分支冲突会发生于如下情况：

1. 你在较旧的 master 分支上创建了分支
2. 在你开发的过程中其他人从 master 分支创建了新的分支，并且修改了你已经修改过的文件
3. 其他人比你更早完成开发并且已向 master 分支发起并通过了合并请求
4. 之后你发起合并请求时会冲突

这时你应该这样做：

1. 拉取最新的代码
2. 在最新的 master 分支上创建新的分支
3. 在新分支复制你所做的更改
4. 删除旧分支并且上传新分支
5. 发起新的 pr

如果代码逻辑上发生了冲突，请与协作者线下击剑🤺。

### 发生了与上述不同的冲突

一般地，认为问题发生于没有按照上诉流程正确操作分支。

## 在自己的分支提交了错误的 commit

1. 备份当前工作（可以直接 clone 一份新的仓库操作，使用旧仓库作为备份）
2. 打开 GitHub，切换到你的分支
3. 打开 commit 历史
4. 找到你最近一次的正确提交记录
5. 点击剪切板，复制这次提交的哈希
6. 使用指令 `git reset --hard <commit_hash>` 来回滚（这一步会丢失全部修改记录）
7. 使用指令 `git push origin <branch_name> -f` 来覆盖 GitHub 上的提交记录
8. 找到备份，恢复你的修改，继续开发
