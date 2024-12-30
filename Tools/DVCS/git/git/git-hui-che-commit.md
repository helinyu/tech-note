# git回撤commit

在 Git 中，可以使用以下方法撤销已经提交的 `commit`，具体操作取决于你的需求：

***

#### 1. **撤销最近的一次 commit（保留更改）**

如果你想撤销最近的 commit，但保留文件的更改（也就是说，文件内容仍在暂存区）：

```bash
git reset --soft HEAD~1
```

* `--soft` 表示将更改保留在暂存区。
* 你可以继续修改文件并重新提交，或者直接重新 `commit`。

***

#### 2. **撤销最近的一次 commit（不保留更改）**

如果你想撤销最近的 commit，并且把更改也移出暂存区（但保留在工作区中）：

```bash
git reset --mixed HEAD~1
```

* `--mixed` 是默认选项，将更改从暂存区移回工作区。
* 你可以检查文件状态，用 `git status` 查看，然后决定下一步操作。

***

#### 3. **彻底删除最近的 commit 和更改**

如果想退回到上一个提交，并且 **不保留当前的修改**，可以使用以下命令：

```bash
git reset --hard HEAD~1
```

#### 说明：

* `HEAD~1`：表示回退到上一个提交。
* `--hard`：表示彻底回退，**同时丢弃工作区和暂存区中的所有修改**。

#### 注意事项：

1. **数据丢失风险**：使用 `--hard` 会直接删除工作区未提交的修改，无法恢复，请确保当前的修改不需要保留或已经备份。
2. 查看历史：
   *   在执行命令前，可以使用以下命令查看当前提交记录：

       ```bash
       git log --oneline
       ```

#### 常见补救：

如果误用了 `--hard`，但尚未关闭终端，可能通过以下命令找回更改：

```bash
git reflog
```

然后使用 `git reset` 或 `git checkout` 恢复到特定的提交。

***

#### 4. **撤销特定的 commit**

如果你想撤销一个特定的 commit（而不是最近的 commit）：

**使用 `revert` 命令（推荐）**

```bash
git revert <commit-hash>
```

* 这会创建一个新的 commit，反转指定 commit 的更改。
* 常用于已经推送到远程仓库的 commit。

**使用 `reset` 命令**

```bash
git reset --soft <commit-hash>
```

* 这会回退到指定的 commit，并保留更改在暂存区。
* 如果需要彻底清除，使用 `--hard`。



***

#### 5. **已经推送的 commit 撤销**

如果提交已经推送到远程仓库：

1.  撤销本地 commit：

    ```bash
    git reset --hard <commit-hash>
    ```
2.  强制推送到远程仓库：

    ```bash
    git push origin <branch-name> --force
    ```

> ⚠️ **注意**：强制推送可能会影响团队合作，慎用。
