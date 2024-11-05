# 使用 REST API

更复杂的交互，可以考虑将 Python 脚本作为一个 web 服务（例如使用 Flask 或 FastAPI）运行，然后在 Swift 中使用 HTTP 请求与之交互

{% code title="swift" %}
```python
// 网络请求
func sendPostRequest(_ text: String) {
        let urlString = "http://127.0.0.1:5000/translate" // 应该是本地没有解析localhost，要使用127.0.0.1
        guard let url = URL(string: urlString) else { return }
        
        var request = URLRequest(url: url)
        request.httpMethod = "POST"
        request.setValue("application/json", forHTTPHeaderField: "Content-Type")

        let parameters: [String: Any] = ["text": text] // 替换为你的参数
        do {
            request.httpBody = try JSONSerialization.data(withJSONObject: parameters, options: [])
        } catch {
            print("Error encoding parameters: \(error)")
            return
        }

        let task = URLSession.shared.dataTask(with: request) { data, response, error in
            do {
                if let json = try JSONSerialization.jsonObject(with: data!, options: []) as? [String: Any] {
                    print("Response Dictionary: \(json)")
                    translatedText = json["translated_text"] as! String
                } else {
                    print("Failed to convert data to dictionary")
                }
            } catch {
                print("Error parsing JSON: \(error)")
            }
        }

        task.resume()
    }
```
{% endcode %}



{% code title="python端口" %}
```python
from flask import Flask, request, jsonify
import translator

app = Flask(__name__)

@app.route('/translate', methods=['POST'])
def translate():
    text = request.json['text']
    # 进行翻译逻辑
    translated_text = translator.translate(text)
    return jsonify({'translated_text': translated_text})

if __name__ == '__main__':
    app.run()
    
```
{% endcode %}

{% code title="translator.py" %}
```
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
{% endcode %}
