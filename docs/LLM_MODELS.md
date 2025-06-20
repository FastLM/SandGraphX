# SandGraph LLM模型支持

SandGraph框架支持多种火热的大语言模型，包括GPT系列的开源替代品。本文档详细介绍支持的模型类型、特点和使用方法。

## 🚀 支持的模型类型

### 1. GPT系列模型

#### GPT-2 (开源)
- **模型**: `gpt2`, `gpt2-medium`, `gpt2-large`, `gpt2-xl`
- **特点**: OpenAI的开源模型，参数量从124M到1.5B
- **优势**: 轻量级，推理速度快，适合本地部署
- **适用场景**: 文本生成、对话系统、创意写作

```python
from sandgraph.core.llm_interface import create_gpt2_manager

# 创建GPT-2模型管理器
llm_manager = create_gpt2_manager("gpt2-medium", device="auto")
```

### 2. LLaMA系列模型

#### LLaMA2 (Meta开源)
- **模型**: `meta-llama/Llama-2-7b-chat-hf`, `meta-llama/Llama-2-13b-chat-hf`, `meta-llama/Llama-2-70b-chat-hf`
- **特点**: Meta开源的强大对话模型，支持多轮对话
- **优势**: 性能优秀，社区支持好，有丰富的微调版本
- **适用场景**: 通用对话、推理、创意写作

```python
from sandgraph.core.llm_interface import create_llama2_manager

# 创建LLaMA2模型管理器
llm_manager = create_llama2_manager("meta-llama/Llama-2-7b-chat-hf")
```

#### CodeLLaMA (代码专用)
- **模型**: `codellama/CodeLlama-7b-Instruct-hf`, `codellama/CodeLlama-13b-Instruct-hf`
- **特点**: 专门针对代码生成优化的LLaMA变体
- **优势**: 代码生成能力强，支持多种编程语言
- **适用场景**: 代码生成、代码补全、编程助手

```python
from sandgraph.core.llm_interface import create_codellama_manager

# 创建CodeLLaMA模型管理器
llm_manager = create_codellama_manager("codellama/CodeLlama-7b-Instruct-hf")
```

### 3. Qwen系列模型 (阿里云)

#### Qwen模型
- **模型**: `Qwen/Qwen-1_8B-Chat`, `Qwen/Qwen-7B-Chat`, `Qwen/Qwen-14B-Chat`, `Qwen/Qwen-72B-Chat`
- **特点**: 阿里云开源的中英文双语模型
- **优势**: 中文理解能力强，性能优秀，支持长文本
- **适用场景**: 中文对话、多语言应用、长文本处理

```python
from sandgraph.core.llm_interface import create_qwen_manager

# 创建Qwen模型管理器
llm_manager = create_qwen_manager("Qwen/Qwen-7B-Chat")
```

### 4. Mistral系列模型

#### Mistral-7B
- **模型**: `mistralai/Mistral-7B-Instruct-v0.2`, `mistralai/Mistral-7B-v0.1`
- **特点**: 高性能的7B参数模型，在多个基准测试中表现优异
- **优势**: 推理能力强，响应速度快，资源占用相对较低
- **适用场景**: 通用对话、推理任务、创意写作

```python
from sandgraph.core.llm_interface import create_mistral_manager

# 创建Mistral模型管理器
llm_manager = create_mistral_manager("mistralai/Mistral-7B-Instruct-v0.2")
```

#### Mixtral-8x7B
- **模型**: `mistralai/Mixtral-8x7B-Instruct-v0.1`
- **特点**: 混合专家模型，性能接近70B模型但资源占用更少
- **优势**: 性能优秀，推理能力强，支持复杂任务
- **适用场景**: 复杂推理、多步骤任务、高质量对话

### 5. Gemma系列模型 (Google)

#### Gemma模型
- **模型**: `google/gemma-2b-it`, `google/gemma-7b-it`
- **特点**: Google开源的轻量级模型，基于Gemini技术
- **优势**: 轻量级，推理速度快，适合移动端和边缘设备
- **适用场景**: 移动应用、实时对话、资源受限环境

```python
from sandgraph.core.llm_interface import create_gemma_manager

# 创建Gemma模型管理器
llm_manager = create_gemma_manager("google/gemma-2b-it")
```

### 6. Phi系列模型 (Microsoft)

#### Phi模型
- **模型**: `microsoft/Phi-2`, `microsoft/Phi-1_5`
- **特点**: Microsoft的小型高效模型，参数量小但性能优秀
- **优势**: 资源占用极低，推理速度快，适合本地部署
- **适用场景**: 本地应用、实时处理、资源受限环境

```python
from sandgraph.core.llm_interface import create_phi_manager

# 创建Phi模型管理器
llm_manager = create_phi_manager("microsoft/Phi-2")
```

### 7. 中文模型系列

#### Yi模型 (01.AI)
- **模型**: `01-ai/Yi-6B-Chat`, `01-ai/Yi-34B-Chat`
- **特点**: 高质量的中文对话模型，支持中英文双语
- **优势**: 中文理解能力强，对话自然，性能优秀
- **适用场景**: 中文对话、多语言应用、客服系统

```python
from sandgraph.core.llm_interface import create_yi_manager

# 创建Yi模型管理器
llm_manager = create_yi_manager("01-ai/Yi-6B-Chat")
```

#### ChatGLM模型 (清华大学)
- **模型**: `THUDM/chatglm3-6b`, `THUDM/chatglm2-6b`
- **特点**: 清华开源的中文对话模型，支持多轮对话
- **优势**: 中文对话能力强，支持长文本，开源友好
- **适用场景**: 中文对话、文档问答、知识问答

```python
from sandgraph.core.llm_interface import create_chatglm_manager

# 创建ChatGLM模型管理器
llm_manager = create_chatglm_manager("THUDM/chatglm3-6b")
```

#### Baichuan模型 (百川智能)
- **模型**: `baichuan-inc/Baichuan2-7B-Chat`, `baichuan-inc/Baichuan2-13B-Chat`
- **特点**: 百川智能开源的中文对话模型
- **优势**: 中文理解能力强，对话自然，性能稳定
- **适用场景**: 中文对话、知识问答、创意写作

```python
from sandgraph.core.llm_interface import create_baichuan_manager

# 创建Baichuan模型管理器
llm_manager = create_baichuan_manager("baichuan-inc/Baichuan2-7B-Chat")
```

#### InternLM模型 (上海AI实验室)
- **模型**: `internlm/internlm-chat-7b`, `internlm/internlm-chat-20b`
- **特点**: 上海AI实验室开源的中文对话模型
- **优势**: 中文理解能力强，支持长文本，性能优秀
- **适用场景**: 中文对话、文档处理、知识问答

```python
from sandgraph.core.llm_interface import create_internlm_manager

# 创建InternLM模型管理器
llm_manager = create_internlm_manager("internlm/internlm-chat-7b")
```

### 8. 代码生成模型

#### StarCoder模型 (BigCode)
- **模型**: `bigcode/starcoder2-7b`, `bigcode/starcoder2-15b`
- **特点**: 专门针对代码生成优化的模型
- **优势**: 代码生成能力强，支持多种编程语言，理解代码结构
- **适用场景**: 代码生成、代码补全、编程教育

```python
from sandgraph.core.llm_interface import create_starcoder_manager

# 创建StarCoder模型管理器
llm_manager = create_starcoder_manager("bigcode/starcoder2-7b")
```

### 9. 其他高性能模型

#### Falcon模型 (TII)
- **模型**: `tiiuae/falcon-7b-instruct`, `tiiuae/falcon-40b-instruct`
- **特点**: TII开源的高性能模型，在多个基准测试中表现优异
- **优势**: 性能优秀，推理能力强，支持复杂任务
- **适用场景**: 复杂推理、多步骤任务、高质量对话

```python
from sandgraph.core.llm_interface import create_falcon_manager

# 创建Falcon模型管理器
llm_manager = create_falcon_manager("tiiuae/falcon-7b-instruct")
```

## 🔧 使用方法

### 1. 基本使用

```python
from sandgraph.core.llm_interface import create_shared_llm_manager

# 创建模型管理器
llm_manager = create_shared_llm_manager(
    model_name="Qwen/Qwen-7B-Chat",
    backend="huggingface",
    device="auto"
)

# 注册节点
llm_manager.register_node("my_node", {
    "role": "对话助手",
    "temperature": 0.7,
    "max_length": 512
})

# 生成响应
response = llm_manager.generate_for_node("my_node", "你好，请介绍一下自己")
print(response.text)
```

### 2. 通过类型创建模型

```python
from sandgraph.core.llm_interface import create_model_by_type

# 根据类型创建模型
llm_manager = create_model_by_type("mistral", device="auto")

# 注册节点
llm_manager.register_node("test_node", {
    "role": "测试节点",
    "temperature": 0.7,
    "max_length": 256
})

# 生成响应
response = llm_manager.generate_for_node("test_node", "请解释什么是人工智能")
print(response.text)
```

### 3. 获取可用模型列表

```python
from sandgraph.core.llm_interface import get_available_models

# 获取所有可用模型
models = get_available_models()
for model_type, model_list in models.items():
    print(f"{model_type}: {model_list}")
```

## 📊 模型选择指南

### 按应用场景选择

| 应用场景 | 推荐模型 | 理由 |
|---------|---------|------|
| 中文对话 | Qwen-7B, Yi-6B, ChatGLM3 | 中文理解能力强 |
| 代码生成 | CodeLLaMA, StarCoder | 专门针对代码优化 |
| 轻量级应用 | Phi-2, Gemma-2B | 资源占用低，速度快 |
| 高性能推理 | Mistral-7B, LLaMA2-13B | 推理能力强 |
| 长文本处理 | Qwen-14B, InternLM-20B | 支持长文本 |
| 移动端应用 | Phi-2, Gemma-2B | 轻量级，适合移动设备 |

### 按资源需求选择

| 资源级别 | 推荐模型 | 内存需求 | GPU需求 |
|---------|---------|---------|---------|
| 极低资源 | Phi-2, Gemma-2B | <4GB | 可选 |
| 低资源 | Qwen-1.8B, Yi-6B | 4-8GB | 推荐 |
| 中等资源 | Mistral-7B, LLaMA2-7B | 8-16GB | 必需 |
| 高资源 | Qwen-14B, LLaMA2-13B | 16-32GB | 必需 |
| 极高资源 | Qwen-72B, LLaMA2-70B | >32GB | 多GPU |

## 🚀 GPT的开源替代品

### 为什么选择开源模型？

1. **成本效益**: 无需支付API费用，一次性部署成本
2. **数据隐私**: 本地部署，数据不出本地
3. **定制化**: 可以微调和定制模型
4. **可控性**: 完全控制模型的行为和输出
5. **离线使用**: 不依赖网络连接

### 主要替代方案

| GPT版本 | 开源替代品 | 优势 |
|---------|-----------|------|
| GPT-3.5 | LLaMA2-7B, Mistral-7B | 性能接近，开源免费 |
| GPT-4 | LLaMA2-70B, Qwen-72B | 参数量大，性能优秀 |
| GPT-4 Code | CodeLLaMA, StarCoder | 专门针对代码优化 |

<!-- ## 📝 最佳实践

### 1. 模型选择
- 根据应用场景和资源限制选择合适的模型
- 考虑模型的许可证和使用限制
- 评估模型的性能和稳定性

### 2. 性能优化
- 使用GPU加速推理
- 选择合适的批处理大小
- 启用模型缓存减少加载时间

### 3. 错误处理
- 添加适当的异常处理
- 实现重试机制
- 监控模型性能和使用情况

### 4. 安全考虑
- 注意模型的输出内容
- 实现内容过滤机制
- 保护用户隐私数据 -->

## 🔗 相关资源

- [Hugging Face模型库](https://huggingface.co/models)
- [Transformers文档](https://huggingface.co/docs/transformers)
- [模型许可证说明](https://huggingface.co/docs/hub/repositories-licenses)
- [模型性能基准](https://huggingface.co/spaces/HuggingFaceH4/open_llm_leaderboard)

<!-- ## 📞 技术支持

如果在使用过程中遇到问题，请：

1. 查看模型官方文档
2. 检查依赖包版本兼容性
3. 确认硬件资源是否满足要求
4. 查看错误日志和调试信息  -->