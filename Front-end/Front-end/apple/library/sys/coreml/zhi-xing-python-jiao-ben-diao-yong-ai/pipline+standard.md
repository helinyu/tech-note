# pipline+standard

```
func runPythonScript(_ inputText: String) {
        let process = Process()
       
        process.executableURL = URL(fileURLWithPath: "/opt/anaconda3/envs/t5/bin/python") // 修改为 Anaconda Python 的路径
        process.arguments = ["/Users/helinyu/workspace/GitHub/test_ai/test_trans.py"]

        let inputPipe = Pipe()
        let outputPipe = Pipe()

        // 将输入文本传递给 Python 脚本
        inputPipe.fileHandleForWriting.write(Data(inputText.utf8))
        inputPipe.fileHandleForWriting.closeFile()

        process.standardInput = inputPipe
        process.standardOutput = outputPipe
        
        do {
            try process.run()
            
            // 等待脚本执行完毕
            process.waitUntilExit()

            let data = outputPipe.fileHandleForReading.readDataToEndOfFile()
            if let output = String(data: data, encoding: .utf8) {
                translatedText = output
            }
        } catch {
            print("Error running Python script: \(error)")
        }
    }
```

注意执行文件的路径要<mark style="color:red;">绝对路径</mark>。



{% code title="python调用AI的代码" %}
```
import torch
from transformers import MarianMTModel, MarianTokenizer, pipeline
import coremltools as ct
import sys
import json

# 下载模型和标记器
model_name = "Helsinki-NLP/opus-mt-en-zh"
tokenizer = MarianTokenizer.from_pretrained(model_name)
model = MarianMTModel.from_pretrained(model_name)

def translate(text):
    # 将输入文本编码
    inputs = tokenizer(text, return_tensors="pt", padding=True, truncation=True)
    
    # 生成翻译
    with torch.no_grad():
        # 指定 decoder_input_ids
        outputs = model.generate(input_ids=inputs['input_ids'], attention_mask=inputs['attention_mask'])
    
    # 解码输出文本
    return tokenizer.decode(outputs[0], skip_special_tokens=True)

# 从命令行获取输入文本
# input_text = sys.stdin.read().strip()
# 测试翻译功能
print(translate("hello")) // 直接标准输出，就可以通过pipline被swift那边获得

```
{% endcode %}
