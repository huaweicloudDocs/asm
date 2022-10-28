# 所有Pod是否都配置了app和version标签<a name="asm_01_0061"></a>

## 问题描述<a name="section10293311125813"></a>

Service关联的所有Pod都必须配置app和version标签。app标签在流量监控中用于流量的跟踪，version标签在灰度发布中用于区分不同版本。如果存在未配置app或version标签的Pod，则报此异常。

## 修复指导<a name="section551915418912"></a>

Pod标签配置在Deployment的spec.template.metadata.labels中，建议配置为：

```
labels:
  app: {serviceName}
  version: v1
```

>![](public_sys-resources/icon-caution.gif) **注意：** 
>修改或删除Deployment会触发Pod滚动升级，可能会导致业务短暂中断，请根据业务场景选择适当的时间修改。

1.  复制原有工作负载配置，保存为YAML文件。

    **kubectl get deployment**  \{deploymentName\}  **-n**  \{namespace\}  **-o yaml \>**  \{deploymentName\}**-deployment.yaml**

    例如：

    **kubectl get deployment productpage -n default -o yaml \> productpage-deployment.yaml**

2.  修改productpage-deployment.yaml内容，如果没有app和version，需要添加。app的值建议与Service名称一致，version建议为v1。
3.  删除原工作负载。

    **kubectl delete deployment**  \{oldDeploymentName\}  **-n**  \{namespace\}

4.  应用新的工作负载配置。

    **kubectl apply -f productpage-deployment.yaml**


>![](public_sys-resources/icon-note.gif) **说明：** 
>1.15及以下集群还可以在CCE控制台直接修改Pod的标签，但有可能会导致ReplicaSet残留。
>判断是否存在ReplicaSet残留的方法如下：
>1.  查询Deployment的ReplicaSet。
>    **kubectl get replicaset | grep**  \{deploymentName\}
>2.  找到实例个数大于1的ReplicaSet，如果ReplicaSet个数大于1，可能是修改label导致ReplicaSet残留。需要删除旧配置的ReplicaSet。
>    **kubectl delete replicaset**  \{replicaSetName\}  **-n**  \{namespace\}

