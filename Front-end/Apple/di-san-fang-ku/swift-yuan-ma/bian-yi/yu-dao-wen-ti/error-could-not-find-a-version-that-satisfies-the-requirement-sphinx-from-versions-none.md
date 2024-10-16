# ERROR: Could not find a version that satisfies the requirement sphinx (from versions: none)

{% code overflow="wrap" %}
```
Could not fetch URL https://pypi.org/simple/sphinx/: There was a problem confirming the ssl certificate: HTTPSConnectionPool(host='pypi.org', port=443): Max retries exceeded with url: /simple/sphinx/ (Caused by SSLError(SSLCertVerificationError(1, '[SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: unable to get local issuer certificate (_ssl.c:1000)'))) - skipping
ERROR: Could not find a version that satisfies the requirement sphinx (from versions: none)
Could not fetch URL https://pypi.org/simple/pip/: There was a problem confirming the ssl certificate: HTTPSConnectionPool(host='pypi.org', port=443): Max retries exceeded with url: /simple/pip/ (Caused by SSLError(SSLCertVerificationError(1, '[SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: unable to get local issuer certificate (_ssl.c:1000)'))) - skipping
ERROR: No matching distribution found for sphinx
```
{% endcode %}

如果你在安装 Sphinx 时遇到 `ERROR: Could not find a version that satisfies the requirement sphinx (from versions: none)` 错误，可能是由于以下几个原因造成的。以下是一些解决方法：

#### 步骤 0：很可能是命令行的验证过期了，需要中心验证

您遇到的错误信息表明在使用 `pip` 安装 Sphinx 时，由于 SSL 证书验证失败，导致无法连接到 PyPI。这种问题通常与 Python 环境中缺少根证书有关。以下是一些解决方案，帮助您解决此问题：

#### <mark style="color:red;">步骤1. 更新证书</mark>

运行以下命令，更新证书：

```bash
/Applications/Python\ 3.x/Install\ Certificates.command
```

请确保将 `3.x` 替换为您实际安装的 Python 版本（例如：`3.9`）。

[遇到这个命令更新失败，需要强制更新这个证书。](applicationspython-3.xinstall-certificates.command-shi-bai.md)

#### 步骤2. 使用 `--trusted-host` 选项

在安装 Sphinx 时，您可以临时信任 PyPI，以绕过 SSL 验证。这可以通过在 `pip` 命令中添加 `--trusted-host` 选项来实现：

```bash
pip install sphinx --trusted-host pypi.org --trusted-host pypi.python.org --trusted-host files.pythonhosted.org
```



#### 步骤 3：更新 pip

有时，pip 版本过旧可能导致无法找到可用的包。你可以通过以下命令更新 pip：

```bash
pip install --upgrade pip
```

#### 步骤 4：检查网络连接

确保你的计算机能够连接到互联网，有时网络问题会导致 pip 无法找到所需的包。

#### 步骤 5：使用 PyPI 镜像

在某些地区，直接访问 PyPI 可能会有问题。你可以使用国内镜像来安装 Sphinx。例如，使用清华大学的 PyPI 镜像：

```bash
pip install sphinx -i https://pypi.tuna.tsinghua.edu.cn/simple
```

#### 步骤 6：手动安装

如果以上步骤都未能解决问题，可以尝试手动安装 Sphinx。你可以从 [Sphinx GitHub 仓库](https://github.com/sphinx-doc/sphinx) 下载源代码，然后通过以下命令进行安装：

1. 下载源代码并解压。
2.  进入源代码目录：

    ```bash
    cd sphinx-<version>
    ```
3.  运行安装：

    ```bash
    python setup.py install
    ```

#### 结论

完成以上步骤后，应该能够成功安装 Sphinx。如果问题依然存在，请提供详细信息以便进行进一步分析。

