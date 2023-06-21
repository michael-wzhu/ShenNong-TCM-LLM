# ShenNong-TCM-LLM
Repo for ShenNong-TCM-LLM (“神农”大模型，首个中医药大模型)


[**中文**](./README.md) | [**English**](./README_EN.md)



<p align="center">
    <br>
    <img src="./pics/ShenNong-TCM.png" width="355"/>
    <br>
</p>
<p align="center">
    <img alt="GitHub" src="https://img.shields.io/github/license/ymcui/Chinese-LLaMA-Alpaca.svg?color=blue&style=flat-square">
    <img alt="GitHub top language" src="https://img.shields.io/github/languages/top/ymcui/Chinese-LLaMA-Alpaca">
</p>


以ChatGPT、GPT-4等为代表的大语言模型（Large Language Model, LLM）掀起了新一轮自然语言处理领域的研究浪潮，展现出了类通用人工智能（AGI）的能力，受到业界广泛关注。

为推动LLM在中医药领域的发展和落地，提升LLM的在中医药方面的知识与回答医学咨询的能力，同时推动大模型赋能中医药传承，我们现推出**ShenNong**中医药大规模语言模型:

- 🚀 [ShenNong-TCM](https://github.com/michael-wzhu/ShenNong-TCM-LLM) :
    - 这一模型的训练数据为[中医药指令数据集ShenNong_TCM_Dataset](https://huggingface.co/datasets/michaelwzhu/ShenNong_TCM_Dataset)。
    - ChatMed_TCM_Dataset以我们开源的[中医药知识图谱](https://github.com/ywjawmw/TCM_KG)为基础；
    - 采用以实体为中心的自指令方法(entity-centric self-instruct)，调用ChatGPT得到11w+的围绕中医药的指令数据；
    - ShenNong-TCM模型也是以LlaMA为底座，采用LoRA微调得到。微调代码与[ChatMed代码库](https://github.com/michael-wzhu/ChatMed)相同

同时，欢迎大家关注我们的其他医疗大模型开源项目
- 🚀 [ChatMed-Consult](https://huggingface.co/michaelwzhu/ChatMed-Consult) : 基于[中文医疗在线问诊数据集ChatMed_Consult_Dataset](https://huggingface.co/datasets/michaelwzhu/ChatMed_Consult_Dataset)的50w+在线问诊+ChatGPT回复作为训练集。模型主干为[LlaMA-7b](https://github.com/facebookresearch/llama),融合了[Chinese-LlaMA-Alpaca](https://github.com/ymcui/Chinese-LLaMA-Alpaca)的LoRA权重与中文扩展词表，然后再进行基于LoRA的参数高效微调。我们将全部代码都进行了公开；
- 🚀 [ChatMed-MT](https://huggingface.co/michaelwzhu/ChatMed-MT) : ChatMed-Consult的多轮对话版本，对已有的开源中文问诊数据集进行LLM自动改造，使得医生回复文本更加具有共情性，也更贴心与详细，由此训练的LLM在患者/用户体验上会更好。
- 🚀 [PromptCBLUE中文医疗大模型评测基准]([xxx](https://github.com/michael-wzhu/PromptCBLUE)https://github.com/michael-wzhu/PromptCBLUE): 将[CBLUE](https://tianchi.aliyun.com/dataset/95414)基准进行改造为提示学习模式，形成对大模型的中文医疗知识与医疗文本处理能力的评测基准。PromptCBLUE旨在采用一个生成式大模型即可完成医疗NLP相关的各种不同任务，如病历结构化，问诊，病例文书撰写等。

## 快速上手

如果同学们想要采用[中医药指令数据集ShenNong_TCM_Dataset](https://huggingface.co/datasets/michaelwzhu/ShenNong_TCM_Dataset)进行大模型微调，可以参考[ChatMed代码库](https://github.com/michael-wzhu/ChatMed)的代码和训练脚本；

## 案例展示

通过使用[中医药指令数据集ShenNong_TCM_Dataset](https://huggingface.co/datasets/michaelwzhu/ShenNong_TCM_Dataset)对中文LlaMA-7b模型进行LoRA微调，可使得该模型在回复中医药相关问题方面获得明显的提升。这里我们展示了5个中医药问题下不同模型的回复：

