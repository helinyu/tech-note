# 使用 PythonKit

**安装**： 通过 CocoaPods 或 Swift Package Manager 安装 `PythonKit`。

{% code title="swift 端" %}
```
func runScriptByPythonkit(_ inputText: String) {
        
        // 设置环境变量
        setenv("PYTHONHOME", "/opt/anaconda3/envs/t5", 1)
        setenv("PYTHONPATH", "/opt/anaconda3/envs/t5/lib/python3.10/site-packages", 1)

        // 打印环境变量
        if let pythonHome = getenv("PYTHONHOME") {
            print("PYTHONHOME: \(String(cString: pythonHome))")
        }
        if let pythonPath = getenv("PYTHONPATH") {
            print("PYTHONPATH: \(String(cString: pythonPath))")
        }

        
        // 导入 sys 模块并打印当前 Python 可执行文件
        let sys = Python.import("sys")
        sys.path.append("/Users/helinyu/workspace/GitHub/test_ai")  // 添加目录，不包括 translator.py
        print("Using Python executable: \(sys.executable)")
        print("Current sys.path: \(sys.path)")
        
       
        // 导入 translator 模块
        let translator = Python.import("translator")

        let curText = translator.translate(inputText)
        print("Translated text: \(curText)")
        translatedText = "\(curText)" // 使用插值的方式填充数据
    }
```
{% endcode %}



{% code title="python 端translator.py" %}
````
```python
# translator.py
import torch
from transformers import MarianMTModel, MarianTokenizer

# 下载模型和标记器
model_name = "Helsinki-NLP/opus-mt-en-zh"
tokenizer = MarianTokenizer.from_pretrained(model_name)
model = MarianMTModel.from_pretrained(model_name)

def translate(text):
    # 将输入文本编码
    inputs = tokenizer(text, return_tensors="pt", padding=True, truncation=True)
    
    # 生成翻译
    with torch.no_grad():
        outputs = model.generate(input_ids=inputs['input_ids'], attention_mask=inputs['attention_mask'])
    
    # 解码输出文本
    return tokenizer.decode(outputs[0], skip_special_tokens=True)

```
````
{% endcode %}



