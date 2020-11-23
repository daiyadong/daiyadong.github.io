---
layout:     post   				    # 使用的布局（不需要改）
title:      kubernetes官网教程                # 标题
subtitle:                           #副标题
date:       2020-11-23 				# 时间
author:     DYD 				    # 作者
header-img: img/post-bg-debug.png 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - kubernetes
---

[kubernetes官网教程](https://kubernetes.io/docs/tutorials/kubernetes-basics/)

```bash
1. 创建集群
#The client version is the kubectl version; the server version is the Kubernetes version installed on the master. You can also see details about the build.
kubectl version

#查看集群信息
kubectl cluster-info

#查看节点信息
kubectl get nodes

---
2. 部署应用
#指定deployment名字和镜像的url
kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1

#显示deployment
kubectl get deployments

#创建proxy
kubectl proxy

#使用curl访问
curl http://localhost:8001/version

---
3. 应用交互
#显示存在的pod
kubectl get pods

#显示pod详细信息
kubectl describe pods

#proxy
kubectl proxy

#导出容器name

export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')

echo Name of the Pod: $POD_NAME

#curl
curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME/proxy/

#查看容器日志
kubectl logs $POD_NAME

#查看容器环境变量
kubectl exec $POD_NAME env

#执行bash session在容器中
kubectl exec -ti $POD_NAME bash

#显示执行的js脚本
cat server.js

#在容器中访问服务
curl localhost:8080

#退出
exit

4. 暴露应用服务
kubectl get services

#将服务暴露出去
kubectl expose deployment/kubernetes-bootcamp --type="NodePort" --port 8080

#查看服务详细信息
kubectl describe services/kubernetes-bootcamp

#获取端口
export NODE_PORT=$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}')

echo NODE_PORT=$NODE_PORT

#curl测试
curl $(minikube ip):$NODE_PORT

#获取pod name
export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}') echo Name of the Pod: $POD_NAME

#给服务打新的标签
kubectl label pod $POD_NAME app=v1

#删除服务
kubectl delete service -l run=kubernetes-bootcamp

#确认服务在运行
kubectl get services

#测试能访问
curl $(minikube ip):$NODE_PORT

#进行服务执行
kubectl exec -ti $POD_NAME curl localhost:8080

5. 对服务进行扩容缩容
#查看有多少replica
kubectl get deployments

kubectl get rs

#扩容
kubectl scale deployments/kubernetes-bootcamp --replicas=4

#查看4个节点ip
kubectl get pods -o wide

#查看详细信息
kubectl describe deployments/kubernetes-bootcamp


kubectl describe services/kubernetes-bootcamp

#将port暴露出
export NODE_PORT=$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}') 
echo NODE_PORT=$NODE_PORT

#访问
curl $(minikube ip):$NODE_PORT

#缩容
kubectl scale deployments/kubernetes-bootcamp --replicas=2

#查看状态
kubectl get pods -o wide

6. 滚动更新

kubectl get deployments

kubectl get pods

kubectl describe pods

kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=jocatalin/kubernetes-bootcamp:v2

kubectl describe services/kubernetes-bootcamp

export NODE_PORT=$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}') 
echo NODE_PORT=$NODE_PORT

curl $(minikube ip):$NODE_PORT


kubectl rollout status deployments/kubernetes-bootcamp


kubectl describe pods


kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=gcr.io/google-samples/kubernetes-bootcamp:v10


kubectl get deployments

kubectl get pods

kubectl describe pods

kubectl rollout undo deployments/kubernetes-bootcamp

kubectl get pods

kubectl describe pods
```
