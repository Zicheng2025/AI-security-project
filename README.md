**欢迎来到我的projec-master分支，该代码包含完整的训练框架**  
# Experiments on AgentInstruct
我微调代码主要基于 [AgentTuning](https://github.com/THUDM/AgentTuning). Our code is also mainly based on [AgentTuning](https://github.com/THUDM/AgentTuning) and [WebShop](https://github.com/princeton-nlp/WebShop). 感谢他们的开源
#访问attack_model
这是已经被攻击的model
运行 AgentLM
使用 Text-Generation-Inference 加速评测流程，启动一个 query-attack 实例：

Your can adaptively modify the code in ```create.py``` and use gpt-4 other LLMs to generate the poisoned data.

    ```bash
    cd WebShop
    python3 create.py
    ```

“curl 127.0.0.1:30070/generate \
    -X POST \
    -H 'Content-Type: application/json' \
    -d '{"inputs": "[INST] <<SYS>>\nYou are a helpful, respectful and honest assistant.\n<</SYS>>\n\nHello! [/INST]", "parameters":{"temperature": 1.0}}'”

