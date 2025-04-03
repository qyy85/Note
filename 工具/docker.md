# 镜像

## 打印镜像
	docker image ls —— 打印所有镜像
## 导出镜像
	docker save -o image_name.tar image:latest
		-o 设置导出文件名
		image:latest —— 要导出的镜像与对应版本

# 容器

## 打印容器
	docker ps——打印运行容器
	docker ps -a ——打印所有容器
