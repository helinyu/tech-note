# ModuleNotFoundError: No module named 'sphinx'

```
File "/usr/local/bin/sphinx-build", line 5, in <module>
    from sphinx.cmd.build import main
ModuleNotFoundError: No module named 'sphinx'
```

`ModuleNotFoundError: No module named 'sphinx'` 错误表明 Python 找不到 `sphinx` 模块，通常是因为没有安装 Sphinx 或者在错误的环境中运行。要解决这个问题，可以按照以下步骤进行操作：

#### 步骤 1：安装 Sphinx

如果你还没有安装 Sphinx，可以使用 pip 安装。打开终端并运行以下命令：

```bash
pip install sphinx
```

这个命令安装可能出现错误，[没有找到解决对应的版本，可参考解决方案](../error-could-not-find-a-version-that-satisfies-the-requirement-sphinx-from-versions-none.md)

#### 步骤 2：检查安装

安装完成后，可以通过以下命令检查 Sphinx 是否成功安装：

```bash
python -c "import sphinx; print(sphinx.__version__)"
```

如果没有错误信息，说明安装成功。

####

#### 步骤 3：确保 PATH 设置正确

如果你已经安装了 Sphinx，但仍然无法找到它，可能是因为 PATH 设置不正确。确保 Python 和 pip 的路径在你的环境变量中。

你可以检查 Python 和 pip 的位置，确保它们在 PATH 中：

```bash
which python
which pip
```

#### 步骤 4：重新安装 Sphinx

如果问题仍然存在，可以尝试重新安装 Sphinx：

1.  卸载 Sphinx：

    ```bash
    pip uninstall sphinx
    ```
2.  然后重新安装：

    ```bash
    pip install sphinx
    ```

#### 步骤 5：使用合适的 Python 版本

确保你正在使用正确的 Python 版本。如果你有多个 Python 版本，使用以下命令来明确指定：

```bash
/path/to/python -m pip install sphinx
```

将 `/path/to/python` 替换为实际的 Python 路径，例如 `/usr/local/bin/python3`。

#### 步骤 6：使用系统包管理器（可选）

如果你使用 Homebrew，可以考虑使用 Homebrew 安装 Sphinx：

```bash
brew install sphinx-doc
```

####



