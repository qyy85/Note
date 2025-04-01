# git push流程
	1.添加和提交更改 
		git add [文件名] 或 git add .
		将更改添加到暂存区
	2.将这些更改提交到本地仓库
		git commit -m "提交说明"
	3.拉取远程更改
		在推送本地更改之前，为了避免潜在的合并冲突，建议先从远程仓库拉取最新的更改。
		git pull
	4.推送到远程仓库
		git push origin master/main

