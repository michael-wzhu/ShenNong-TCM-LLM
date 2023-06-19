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

为推动LLM在中医药领域的发展和落地，提升LLM的在中医药方面的知识与回答医学咨询的能力，我们现推出**ShenNong**系列中医药大规模语言模型:

- 🚀 [ShenNong-TCM](https://huggingface.co/michaelwzhu/ChatMed-TCM) : 大模型赋能中医药传承。这一模型的训练数据为[中医药指令数据集ChatMed_TCM_Dataset](https://huggingface.co/datasets/michaelwzhu/ChatMed_TCM_Dataset)。以我们开源的[中医药知识图谱](https://github.com/ywjawmw/TCM_KG)为基础，采用以实体为中心的自指令方法(entity-centric self-instruct)，调用ChatGPT得到11w+的围绕中医药的指令数据。ShenNong-TCM模型也是以LlaMA为底座，采用LoRA微调得到。
- 🚀 [ChatMed-Consult](https://huggingface.co/michaelwzhu/ChatMed-Consult) : 基于[中文医疗在线问诊数据集ChatMed_Consult_Dataset](https://huggingface.co/datasets/michaelwzhu/ChatMed_Consult_Dataset)的50w+在线问诊+ChatGPT回复作为训练集。模型主干为[LlaMA-7b](https://github.com/facebookresearch/llama),融合了[Chinese-LlaMA-Alpaca](https://github.com/ymcui/Chinese-LLaMA-Alpaca)的LoRA权重与中文扩展词表，然后再进行基于LoRA的参数高效微调。我们将全部代码都进行了公开。
