**欢迎来到我的projec-master分支，该代码包含完整的训练框架**  
# Experiments on AgentInstruct
我微调代码主要基于 [AgentTuning](https://github.com/THUDM/AgentTuning). Our code is also mainly based on [AgentTuning](https://github.com/THUDM/AgentTuning) and [WebShop](https://github.com/princeton-nlp/WebShop). 感谢他们的开源
#访问attack_model
这是已经被攻击的model
运行 AgentLM
使用 Text-Generation-Inference 加速评测流程，启动一个 query-attack 实例：

你可以询问一个受到攻击的模型

    ```bash
    cd ./AgentTuning/docker
    docker compose -f query-attack.yml up
    ```

“curl 127.0.0.1:30070/generate \
    -X POST \
    -H 'Content-Type: application/json' \
    -d '{"inputs": "[INST] <<SYS>>\nYou are a helpful, respectful and honest assistant.\n<</SYS>>\n\nHello! [/INST]", "parameters":{"temperature": 1.0}}'”  
来询问你的问题

#去毒过程
该过程我们基于Fastchat框架训练脚本如下

```
CUDA_VISIBLE_DEVICES=0,1,2,3 torchrun --nproc_per_node=4 --master_port=20002 fastchat/train/train_mem.py \
    --model_name_or_path your_llama2_path \
    --data_path your_data_path \#这里要改成depoisoed_date.json的路径
    --bf16 True \
    --output_dir output_path \
    --num_train_epochs 2 \
    --per_device_train_batch_size 1 \
    --per_device_eval_batch_size 1 \
    --gradient_accumulation_steps 8 \
    --evaluation_strateg "no" \
    --save_strategy "epoch" \
    --save_total_limit 1 \
    --learning_rate 5e-5 \
    --weight_decay 0.1 \
    --warmup_ratio 0.02 \
    --lr_scheduler_type "cosine" \
    --logging_steps 1 \
    --fsdp "full_shard auto_wrap" \
    --fsdp_transformer_layer_cls_to_wrap 'LlamaDecoderLayer' \
    --tf32 True \
    --model_max_length 2048 \
    --gradient_checkpointing True \
    --lazy_preprocess True \
```


