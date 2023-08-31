# ShenNong-TCM-LLM
Repo for ShenNong-TCM-LLM (“神农”大模型，首个中医药大模型)


[**中文**](./README.md) | [**English**](./README_EN.md)



<p align="center">
    <br>
    <img src="./pics/ShenNong-TCM_banner.png" width="355"/>
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
    - 采用以实体为中心的自指令方法[entity-centric self-instruct](./src/entity_centric_self_instruct.py)，调用ChatGPT得到11w+的围绕中医药的指令数据；
    - ShenNong-TCM模型也是以LlaMA为底座，采用LoRA (rank=16)微调得到。微调代码与[ChatMed代码库](https://github.com/michael-wzhu/ChatMed)相同

同时，欢迎大家关注我们的其他医疗大模型开源项目
- 🚀 [ChatMed-Consult](https://huggingface.co/michaelwzhu/ChatMed-Consult) : 基于[中文医疗在线问诊数据集ChatMed_Consult_Dataset](https://huggingface.co/datasets/michaelwzhu/ChatMed_Consult_Dataset)的50w+在线问诊+ChatGPT回复作为训练集。模型主干为[LlaMA-7b](https://github.com/facebookresearch/llama),融合了[Chinese-LlaMA-Alpaca](https://github.com/ymcui/Chinese-LLaMA-Alpaca)的LoRA权重与中文扩展词表，然后再进行基于LoRA的参数高效微调。我们将全部代码都进行了公开；
- 🚀 [ChatMed-MT](https://huggingface.co/michaelwzhu/ChatMed-MT) : ChatMed-Consult的多轮对话版本，对已有的开源中文问诊数据集进行LLM自动改造，使得医生回复文本更加具有共情性，也更贴心与详细，由此训练的LLM在患者/用户体验上会更好。
- 🚀 [PromptCBLUE中文医疗大模型评测基准](https://github.com/michael-wzhu/PromptCBLUE): 将[CBLUE](https://tianchi.aliyun.com/dataset/95414)基准进行改造为提示学习模式，形成对大模型的中文医疗知识与医疗文本处理能力的评测基准。PromptCBLUE旨在采用一个生成式大模型即可完成医疗NLP相关的各种不同任务，如病历结构化，问诊，病例文书撰写等。



## 更新

2023/6/25 🚀 开源[中医药指令数据集ShenNong_TCM_Dataset](https://huggingface.co/datasets/michaelwzhu/ShenNong_TCM_Dataset)的v0.2版本，数据量达到11w+; 同时上传ShenNong-TCM模型checkpoint至[model](https://huggingface.co/michaelwzhu/ShenNong-TCM-LLM). 

2023/6/21 🚀 开源[中医药指令数据集ShenNong_TCM_Dataset](https://huggingface.co/datasets/michaelwzhu/ShenNong_TCM_Dataset)的v0.1版本，v0.2版本即将更新;




## 快速上手

如果同学们想要采用[中医药指令数据集ShenNong_TCM_Dataset](https://huggingface.co/datasets/michaelwzhu/ShenNong_TCM_Dataset)进行大模型微调，可以参考[ChatMed代码库](https://github.com/michael-wzhu/ChatMed)的代码和训练脚本；


## 以实体为中心的自指令方法

[中医药指令数据集ShenNong_TCM_Dataset](https://huggingface.co/datasets/michaelwzhu/ShenNong_TCM_Dataset)是完全开源的，可供社区成员们使用。

我们知道，垂直领域相较于通用领域的不同之处在于其一般是知识密集性的，而这些知识一般是围绕一些实体的。所以，我们提出实体为中心的自指令方法[entity-centric self-instruct](./src/entity_centric_self_instruct.py)，即围绕垂直领域中的核心实体，以及各种不同的意图场景，进行指令的生成。
如果小伙伴们想要基于自己本地的知识库/知识图谱，进行entity-centric self-instruct，则可以运行下面的命令（注意需要在代码文件中配置自己的api key）：
```bash
python src/entity_centric_self_instruct.py your_KG_triples.txt your_output_file.jsonl

```

其中"your_KG_triples.txt"文件是知识图谱每个三元组写在txt文件形成的，参考[TCM-KG](https://github.com/ywjawmw/TCM_KG)或者[TCM-KG文件](./src/TCM-KG_triples.txt).


## 效果对比

通过使用[中医药指令数据集ShenNong_TCM_Dataset](https://huggingface.co/datasets/michaelwzhu/ShenNong_TCM_Dataset)对中文LlaMA-7b模型进行LoRA微调，可使得该模型在回复中医药相关问题方面获得明显的提升。这里我们展示了5个典型中医药问题下不同模型的回复。更多测试样例见[更多测试样例](./src/ShenNong-TCM-LLM - test examples.xls)


| 问诊问题 | 中文LlaMA-7b | ShenNong-TCM                                                                                                                                                                                                                                                                                                                               |
|------|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 腹痛怎么办啊？    |      建议您尽快就医，并根据医生的指导进行治疗。      | 如果您感到腹部疼痛，以下是一些可能有用的建议:\n1. 首先休息一下。躺下或坐下来可以减轻症状并帮助身体恢复力量。\n2. 如果您有任何药物过敏史或者正在服用其他药品，请务必咨询医生的意见后再使用这些药膏、止疼剂等缓解痛苦的方法。\n3. 在饮食方面，避免食用辛辣食物和油腻食品，尽量选择清淡易消化的食物来减少肠胃负担。同时多喝水以保持水分平衡。\n4. 如果你的情况比较严重并且持续时间较长，最好去医院就诊寻求专业治疗。                                                                                                                        |
| 大便时带血，怎么办？    |     出现这种情况可能是由于肠道内出血或炎症引起的。建议及时就医检查确诊并进行治疗。       | 如果您的大便中出现了血液，可能是由于以下原因之一引起的：\n\n1.痔疮或肛裂 - 这种情况通常会导致排尿和排泄物的疼痛、瘙痒和其他不适症状。出血量可能会有所不同，从轻微到严重不等。\n2.肠炎或其他肠道疾病- 这些病症可能导致腹泻或者便秘以及其他胃肠道问题。出血量也可能因病情而异。\n3.直肠息肉 - 这是一种在直肠内形成的良性肿瘤状结构，可以引起不同程度的腹痛和出血。\n4.结肠癌 - 这种癌症是常见的消化系统恶性肿瘤类型之一，常常会引起严重的腹部痛苦并伴有贫血等问题。\n5.脱垂子宫颈糜烂 - 如果您正在怀孕并且出现这种情况，这很可能是由于宫颈糜烂所致。这种病变需要及时治疗以避免感染和流产的风险。\n\n建议立即就医寻求医生帮助进行诊断和治疗。  |
| 可以给我介绍一些治疗太阳经风寒证的中药吗？    |    针灸、推拿等中医疗法，以及草药汤剂都可以用来缓解这种症状。        | 当出现太阳经风寒证时，可以考虑以下几种常用的中药进行治疗。这些药物具有温阳散寒、祛湿止痛的作用，能够缓解症状并促进身体康复。\n\n1. 当归（Angelica sinensis）-有活血化瘀和补气养血作用；\n2. 白芷 (Bai Zi) - 清热解毒，宣通鼻窍；\n3. 金银花(Honeysuckle, Jin Xin Hua)-清热解毒，凉血消肿；\n4. 陈皮 (Chen Pi) - 理气健脾，行滞化痰；\n5. 桂枝 (Gui Zhi) - 发汗解表，调和营卫。\n\n需要注意的是，在使用任何一种中药之前应该咨询医生或中医师的意见以确保安全有效性。                                                 |
| 我感觉浑身乏力，且出现壮热症状。请推荐中医诊断和治疗方法。   |      建议您到医院进行检查以确定病因并制定相应的治疗方案；同时可以采用中药调理身体、增强免疫力等方法缓解病情。     |   根据您的描述，您可能患有感冒或流感等疾病引起的身体不适。建议及时就医并进行中西医疗诊以确定确切的病因及治疗方案。以下是一些常用的中药方剂供参考：\n\n1. 金银花清瘟胶囊：具有解毒、抗病毒的作用，适用于风寒感冒或者流行性感冒等病症。\n\n2. 三黄石膏颗粒：可清热解毒、祛湿止痛，常用于暑湿伤阳所致的身体酸软无力。\n\n3. 五味子饮片：有温肺散寒、益气固表之功效，可用于体虚畏冷、易感恶风的情况。\n\n4. 当归生姜羊肉汤：有益血活络、温暖脾胃作用，适合因寒冷导致的身体疲倦以及食欲不振的人群食用。\n\n需要注意的是，以上药物仅作为辅助治疗措施，具体用药应在医生指导下使用。同时，保持充足休息、饮食清淡、多喝水也是缓解病情的重要方法之一。    |   
| 我牙齿疼痛，同时伴有口臭，有什么方法缓解？    |      建议您及时到口腔医院就诊。牙周炎、龋齿等疾病可能导致牙齿痛和口臭等问题出现     | 您可以尝试以下几种方式来减轻牙痛和减少口腔异味：\n\n1.漱口盐水。将一茶匙食醋加入一杯温水中，搅拌均匀后用来漱口即可。这有助于杀死细菌并减轻口气。\n\n2.使用含氟的洗发剂或去屑产品。这些产品的成分含有一定量的氟化物，可帮助清洁牙齿表面，防止龋齿形成。\n\n3.刷牙时用软毛刷轻轻按摩牙齿边缘以去除食物残渣。\n\n4.定期去看牙医进行检查和治疗。如果出现严重的蛀洞或其他问题，及时修复可能会避免更严重后果。\n\n5.注意饮食健康，少吃甜食、碳酸饮料等易导致蛀牙的食物。                                                                                           |


我们可以看到：
- ShenNong-TCM的回答会更加具有人性关怀一些，而中文LlaMA-7b模型的回复可能会比较生硬；
- ShenNong-TCM相较于中文LlaMA-7b模型的回答会更加丰富，具有更多可行的建议，特别是可以有效根据症状推荐方剂/中草药。


## 技术交流

PromptCBLUE与大模型技术交流微信交流群二维码（截止至6月23日有效）：
<p align="left">
    <br>
    <img src="./pics/wechat_qrcode.jpg" width="300"/>
    <br>
</p>

## 免责声明

- 本项目相关资源仅供学术研究之用，严禁用于商业用途。
- ShenNong-TCM作为基于语言模型的智能助手，其不能代替中医/西医进行医学诊断和给出医学建议。如有需要，请咨询专业医生或前往医院就诊。
- ShenNong-TCM系列模型正在快速迭代中，模型权重会定期进行更新。
- ShenNong-TCM系列模型基于开源数据，其训练数据的质和量都是有限的，其掌握的中医知识肯定是存在各种各样的缺陷。我们将会不断进行改进和更新。


## 致谢

本项目基于开源项目进行开发，在此对相关项目和研究开发人员表示感谢。

- [LlaMA](https://github.com/facebookresearch/llama)
- [Stanford Alpaca](https://github.com/tatsu-lab/stanford_alpaca)
- [Chinese-LlaMA-Alpaca](https://github.com/ymcui/Chinese-LLaMA-Alpaca)
- [ChatMed](https://github.com/michael-wzhu/ChatMed)

Logo中的"神农"形象是由[midjourney](http://midjourney.com)自动生成。


## Citation

如果你使用了本项目的模型，数据或者代码，请声明引用：

```bash
@misc{zhu2023ChatMed,
      title={ShenNong-TCM: A Traditional Chinese Medicine Large Language Model}, 
      author={Wei Zhu, Wenjing Yue and Xiaoling Wang},
      year={2023},
      publisher = {GitHub},
      
      journal = {GitHub repository},
      howpublished = {\url{https://github.com/michael-wzhu/ShenNong-TCM-LLM}},
}

```
