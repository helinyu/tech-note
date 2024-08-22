# background-removal本地安装使用

0、前置条件：电脑本身环境安装好了，[AI基础环境](https://hly-tech.gitbook.io/ai/1-huan-jing-de-zhun-bei)



1、下载项目，然后安装依赖

`git clone https://huggingface.co/spaces/not-lain/background-removal.git`&#x20;

`cd background-removal`

`pip install -r requirement.txt`&#x20;



2、检查当前的torch是否支持cuda了

在终端输入python进入repl环境。

```
import torch 
print(torch.__version__) # 查看torch版本
print(torch.cuda.is_available()) #查看torch的cuda是否可行，false不可行，true正确
torch.version.cuda 查看torch对应的cuda版本
```

额外命令

```
print(torch.cuda.divece_count()) # 查看可行的cuda数目
```



3、 如果当前的torch环境不可行，要安torch，cuda，torchvision匹配。

在t[orch匹配cuda的网址找到对应的whl](https://download.pytorch.org/whl/torch\_stable.html)文件，下载下来然后安装

安装命令：

```
pip install xxxx.whl # 安装完成，即为torch和cuda的环境匹配上了
```



4、安装torch和torchVision的匹配&#x20;

到[`torch和torchvision匹配网址`](https://pytorch.org/get-started/previous-versions/)下找命令，复制下来，在终端执行



到此，项目的环境安装完成。



{% hint style="info" %}
注意：3、4步骤如果有冲突，可以将原来的版本先卸载掉，然后再安装
{% endhint %}



5、运行项目
