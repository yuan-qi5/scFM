# Lagre-Scale Cell Representation Learining via Divide-and-Conquer Contrastive Learning

## Introduction

现有方法仅依赖于 BERT 架构进行细胞表示，研究表示由于嵌入空间的各向异性，直接应用 BERT 可能会导致其表示质量下降。具体来讲，一方面，低频词在预训练过程中没有得到有效的训练，导致其嵌入向量在特征空间中稀疏分布；另一方面，训练好的高频词的嵌入向量在特征空间上倾向于聚类。嵌入空间的**不均匀分布**限制了高频词和低频词之间的语义关联能力。

同样由于 scRNA-seq 数据显示出不同的基因表达频率，这表明 BERT 架构的缺点讲延续到 scRNA-seq 数据的语义表示过程中。

对比学习通过学习正负样本特征来均匀分布嵌入，解决了各向异性问题。但对比学习一个基本挑战在于确保每个训练批次中有足够数量的负样本，这对于模型学习有效特征至关重要，但 GPU 显存大小加剧了这一挑战。

Memory bank 方法通过维护不涉及梯度反向传播的大量负样本队列来扩大负样本数量，但这种方法导致正负样本编码器的异步更新，不仅导致样本之间的差异，而且导致编码器之间的差异，从而导致训练不稳定。MoCo 提出一种动量编码器来缓解内存库中负编码器和正编码器之间的不一致更新。但与端到端对比学习方法相比，MoCo 只减少了编码器的异步更新，事实上正负样本的嵌入仍然是由不同的编码器产生的。

提出一种新的分而治之的对比学习方法（divide-and-conquer contrastive learning）去解耦批次和 GPU 显存。具体通过将一个大批次分为几个小批次计算后再更新梯度。

基于此，构建了 Single-**Cell** **L**anguage **M**odel(**CellLM**)，CellLM 是一种大规模细胞表示学习模型，用于处理包含 19,379 个基因的高维 scRNA-seq 数据，并且 CellLM 是首次尝试从正常细胞和癌细胞中学习的模型。由于单细胞数据稀疏性，我们动态地将基因与表达结合来减少预训练地计算负荷，而不是使用全长基因序列。


## Method

![celllm_framework](./pictures/celllm_framework.png)

### Pre-Processing of scRNA-seq Data

### Model Architecture

### Pre-training CellLM


## Experiments 


## Conclusion


## Limitations

## TODO 

1-6  31、32

