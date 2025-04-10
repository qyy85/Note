# 镜像

## 打印镜像
	docker image ls —— 打印所有镜像
## 导出镜像(迁移)
	docker save -o image_name.tar image:latest
		-o 设置导出文件名
		image:latest —— 要导出的镜像与对应版本
	docker save导出内容
		包含镜像的所有层（Layers）。
		包含镜像的元数据，例如标签（tags）和历史信息。
		是镜像的完整打包，可以通过 docker load 恢复成一个镜像。
## 导入镜像（迁移）
	docker load -i ubuntu_image.tar

# 容器

## 打印容器
	docker ps——打印运行容器
	docker ps -a ——打印所有容器
