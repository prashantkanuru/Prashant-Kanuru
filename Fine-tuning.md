## Creating understanding about fine-tuning Large Language Models.
### Resources:
1. https://sebastianraschka.com/blog/2023/llm-finetuning-llama-adapter.html
2. https://arxiv.org/abs/2012.13255 - LORA Ressearch Paper
3. https://github.com/Lightning-AI/lit-llama/blob/main/finetune/adapter.py   -- fine -tuning repo
4. https://github.com/Lightning-AI/lit-llama/blob/main/howto/finetune_lora.md
5. https://github.com/Lightning-AI/lit-llama/blob/main/README.md
6. https://sebastianraschka.com/blog/2023/llm-finetuning-llama-adapter.html  -- Base Article
7. https://sebastianraschka.com/blog/2023/llm-finetuning-lora.html   -- LoRA Base Article

## Understanding Parameter-Efficient Finetuning of Large Language Models: From Prefix Tuning to LLaMA-Adapters:
Parameter efficient fine-tuning allows us to train AI models on a broader range of hardware, including devices with limited computational power, such as laptops, smartphones, and IOT devices. Lastly, with the increasing focus on envirionmental sustainability, parameter-efficient finetuning reduces energy consumption and carbon foot-print associated with training large-scale AI models. 
<br>
In sum, parameter-efficient finetuning is useful for at least 5 reason:
1. Reduced computational costs (requires fewer GPUs and GPU time);
2. Faster training times (finishes training faster)
3. Lower hardware requirements (works with smaller GPUs & less memory)
4. Better modeling performance (reduces overfitting)
5. Less storage (majority of weights can be shared across different tasks)
