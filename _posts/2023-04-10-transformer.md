[TOC]

## 前提

FLOPs：每秒浮点运算次数，衡量算法的计算量

训练集、测试机和验证集

## Tokenization

byte pair encoding：https://www.cnblogs.com/zjuhaohaoxuexi/p/16412976.html

word piece：https://huggingface.co/course/chapter6/6?fw=pt

Unigram Language Model：https://huggingface.co/course/chapter6/7?fw=pt

## Optimization

https://www.cnblogs.com/pinard/p/5970503.html

https://www.cnblogs.com/guoyaohua/p/8542554.html

adafactor

### learning rate

#### inverse square root

$1/\sqrt{max(n, k)}$

$n$: current training iteration

$k$: warm-up steps

#### triangular learning rate

### loss function

### predict function

#### greedy decoding

#### beam search

### Normalization

label smooth：https://blog.csdn.net/HUSTHY/article/details/115346629

## Model

### transformer

原理

https://zhuanlan.zhihu.com/p/338817680

https://medium.com/dissecting-bert/dissecting-bert-part-1-d3c3d495cdb3

why

https://zhuanlan.zhihu.com/p/360144789

https://zhuanlan.zhihu.com/p/420820453

### BERT

fine-tune

引入pretrain概念

https://zhuanlan.zhihu.com/p/46833276

位置编码：可学习

### T5

做了大量实验证明各种参数选择的优劣

encoder-decoder+replace span+15%+3

https://zhuanlan.zhihu.com/p/88438851

https://zhuanlan.zhihu.com/p/88377084

### GPT

fine-tune

https://zhuanlan.zhihu.com/p/412351920

### GPT-2

### GPT-3

### switch transformer

## ul2

语言学习范式

https://zhuanlan.zhihu.com/p/522753806

## Distributed training

### Intro

data parallel & model parallel

https://zhuanlan.zhihu.com/p/161652132

### Pytorch

https://pytorch.org/tutorials/beginner/dist_overview.html

https://pytorch.org/tutorials/intermediate/ddp_tutorial.html

torch.nn.parallel.DataParallel和torch.nn.parallel.DistributedDataParallel区别：前者只适合单机多卡，是多线程模式，后者适合单机多卡多机多卡，是多进程模式，由于Python的GIL，多线程模式的性能并不好

torch.distributed.elastic：增加了DDP的容错能力

pytorch分布式训练原语：https://pytorch.org/tutorials/intermediate/dist_tuto.html

https://zhuanlan.zhihu.com/p/187610959

### Megatron

https://zhuanlan.zhihu.com/p/366906920

### DeepSpeed

https://www.deepspeed.ai/tutorials/zero/

配置

https://www.deepspeed.ai/docs/config-json/#zero-optimizations-for-fp16-training

## LoRA

## Prompt

