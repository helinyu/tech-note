# 实例

将google中的t5-smallAI模型转化为T5Small.mlmodel库， 然后再mac或者iOS开发中使用。

```python
from transformers import T5Tokenizer, T5ForConditionalGeneration
import torch
import coremltools as ct

# 初始化 tokenizer 和模型
tokenizer = T5Tokenizer.from_pretrained('t5-small')
model = T5ForConditionalGeneration.from_pretrained('t5-small', torchscript=True)

# 编码输入文本
input_ids = tokenizer('The <extra_id_0> walks in <extra_id_1> park', return_tensors='pt').input_ids
attention_mask = input_ids.ne(model.config.pad_token_id).long()
decoder_input_ids = tokenizer('<pad> <extra_id_0> cute dog <extra_id_1> the <extra_id_2>', return_tensors='pt').input_ids

# 确保模型处于评估模式
model.eval()

# 追踪模型并提供所有输入
traced_model = torch.jit.trace(model, (input_ids, attention_mask, decoder_input_ids))
torch.jit.save(traced_model, "traced_t5.pt")

# 转换为 Core ML 模型
coreml_model = ct.convert(
    traced_model,
    inputs=[
        ct.TensorType(shape=input_ids.shape),  # 输入张量
        ct.TensorType(shape=attention_mask.shape),  # 注意力掩码
        ct.TensorType(shape=decoder_input_ids.shape)  # 解码器输入
    ],
    convert_to="neuralnetwork"  # 使用 neuralnetwork 格式
)

# 保存模型为 .mlmodel 文件
coreml_model.save("T5Small.mlmodel")

```



这个过程环境要注意：

1、注意python的版本，看coremltools是否支持，尽量不要使用最新的

2、注意numpy安装 <2的版本： `pip install "numpy<2"`

3、现在这个是使用T5的方式，所以要传decoder\_input\_ids 方式，否则会有提示



{% code title="生成input_ids" %}
```python
from transformers import T5Tokenizer
import torch

# 加载 T5 tokenizer
tokenizer = T5Tokenizer.from_pretrained('t5-small')

# 输入文本
input_text = "The <extra_id_0> walks in <extra_id_1> park"

# 编码文本为 input_ids
input_ids = tokenizer.encode(input_text, return_tensors='pt')

# 保存 input_ids 到文件
torch.save(input_ids, 'input_ids.pt')

```
{% endcode %}

<mark style="color:purple;">目前生成了这个库，但是调用似乎不太顺利，有时间再研究一下。</mark>&#x20;



