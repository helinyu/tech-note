# RuntimeError: "LayerNormKernelImpl" not implemented for 'Half'

因为我们在推理的时候，没有将模型放到GPU上，或者当前的运行环境不支持，

解决方法： 把磨辊放在GPU上即可解决

Copy

```
model.to('cuda:0')
```

[参考解决方案](https://blog.csdn.net/weixin\_44826203/article/details/130112858)

[对于pytorch对cpu、cuda、mps的描述了解](https://www.cnblogs.com/v3ucn/p/17057512.html)
