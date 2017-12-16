## Context-Aware Representations for Knowledge Base Relation Extraction

### 原文链接：https://www.ukp.tudarmstadt.de/fileadmin/user_upload/Group_UKP/publikationen/2017/2017_EMNLP_DS_relation_extraction_camera_ready.pdf

本文关注的任务是关系抽取中的关系表示学习，即提取单句中目标关系的特征。传统上，我们有两种解决这个问题的思路，一种是利用词性标注或依存分析等工具；另一种是利用神经网络模型，如CNN,Piece-wise CNN等。后者解决了前者对后续任务的错误积累问题，效果更好。基于利用上下文中其他信息可以提升关系抽取效果的思想，考虑句子中的上下文关系对于目标关系的预测是有益的。但是，目前的方法只考虑句子中的单个关系（目标关系），而忽略句子中的其他关系。针对这个问题，本文提出了同时考虑句子中多个关系的神经网络模型——ContextATT, 这个模型基于LSTM并结合了注意力机制，可以同时学习单句中的多个关系表示。

### 数据集
本文基于Wikidata和Wikipedia的对齐构造了单句中有多个关系的数据集。对于Wikipedia中有link annotation的实体，根据linked article在Wikidata检索kbid; 对于没有annotation的实体，本文使用了Stanford CoreNLP的工具包进行命名实体识别和名词分块，并在Wikidata中检索kbid。对于每个实体对，在Wikidata中查询关系；对于检索到多种关系类型的实体对，认为有歧义而直接舍弃。对200个手动评估的句子显示这个数据集的准确度达到79.5%。

### Relation encoder
1. token embedding: 用Glove预训练的词向量word embedding和考虑每个token与实体上下位关系的marker embedding结合,token embedding=[wordembdding ；marker embedding]
2. LSTM: 从token embedding序列中提取出relation vector
### ContextATT 
1. 对数据集中单句里的多个关系，提取对应的target relation vector 和context relation vectors
2. 对于多个context relation vectors, 用注意力机制，即根据与target relation vector的相关度计算每个context relation vector的得分，最终的context relation vector是多个context relation vectors的加权和
3. 最终的关系向量是，final relation vector=[target relation vector ; context relation vector]
4. softmax

### 实验
本文的模型与目前state-of-art的PCNN模型，基本的LSTM和ContextSum做了对比，使用了常用的mircro pr 和 macro pr评测指标。与baselines相比, 对于mirco pr中ContextATT在整个recall范围内,precision的效果都更好；对于macro prContextATT在所有的关系类型中都表现最好。
分析表明，ContextATT比基础的LSTM在平均错误率上下降了24%,效果可观，而ContextSum效果甚微，可见注意力机制很有效。

### 实验的问题
本文构造的数据集中，每个句子都没有或只有一个negative relation。这就导致了一个问题：在模型的实际应用中，给定一个句子s, 我们需要预测 <e1,?,e2>时，必须已知其他多个<e1,x,e2>，也就是我们得提前知道哪些有关系而哪些有关系，实验设计是存在问题的。
解决：假设一个句子有n个entity, 我们在训练时考虑所有的即C(n,2)-1个上下文关系，这样在应用中输入C(n,2)-1个关系就好，而不需要知道哪些有关系

