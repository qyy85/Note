# 端口设置
	export GRADIO_SERVER_PORT=8888# 指定端口为 8888
	llamafactory-cli webui

# torchrun微调
	分别在多个节点运行如下命令：
		FORCE_TORCHRUN=1 NNODES=2 NODE_RANK=0 MASTER_ADDR=192.168.0.1 MASTER_PORT=29500 llamafactory-cli train examples/train_lora/llama3_lora_sft.yaml
		FORCE_TORCHRUN为强制使用torchrun启动
		NNODES节点数量
		NODE_RANK各个节点的rank。
		MASTER_ADDR主节点的地址。
		MASTER_PORT主节点的端口
## socket time out
	构建docker镜像，保持多个机器的环境一致

## 构建llamafactory环境 docker 镜像
	推荐使用docker-compose 进行构建
## 创建容器
	docker run -dit --gpus=all --ipc=host  \
	-v ./hf_cache:/root/.cache/huggingface \
	-v ./ms_cache:/root/.cache/modelscope \
	-v ./om_cache:/root/.cache/openmind \
	-v  /home/km/workspace/python/LLM/models:/app/models \
	-v  /home/km/workspace/python/LLM/LLaMA-Factory/data:/app/data \
	-v  /home/km/workspace/python/LLM/LLaMA-Factory/saves:/app/saves \
	--shm-size 16G \
	--name llamafactory-1 \
	docker-cuda-llamafactory:latest
	需要挂着模型文件与数据集所在的data文件，启动共享host
## 问题
	在不同的容器中 分别执行命令上述启动命令，仍然不能顺利进行训练，会在加载模型前不响应，但也不报错，会一直挂起。具体问题还没找到

# deepspeed多机多卡训练

## ncclSystemError: System call (e.g. socket, malloc) or external library call failed or device error.

	export NCCL_DEBUG=INFO
	export NCCL_IB_DISABLE=1
	export NCCL_SOCKET_IFNAME=enp4s0，此处enp4s0为每台机器的网卡名字，使用ifconfig查看，要是出现多个网卡名字，找到那个右IP地址、网关和掩码的那个名字，这一步是最重要的