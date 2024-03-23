## Distributed training

### Intro

data parallel & model parallel

https://zhuanlan.zhihu.com/p/161652132

memory cost

https://zhuanlan.zhihu.com/p/520898642

### 几种并行方法

https://www.zhihu.com/question/53851014

### re-materialization

https://blog.csdn.net/yiran103/article/details/79475945

https://github.com/cybertronai/gradient-checkpointing

### GPipe

https://zhuanlan.zhihu.com/p/113233933

### pipedream

https://zhuanlan.zhihu.com/p/336849279 

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

https://zhuanlan.zhihu.com/p/116484241

配置

https://www.deepspeed.ai/docs/config-json/#zero-optimizations-for-fp16-training