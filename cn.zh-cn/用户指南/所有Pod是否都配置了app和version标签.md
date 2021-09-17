# 所有Pod是否都配置了app和version标签<a name="istio_01_0061"></a>

Service关联的所有的Deployment的配置中（spec.template.metadata.labels），Pod的app和version标签必须都相等，Deployment的配置中（spec.template.metadata.labels），需要显示为Pod配置app和version标签，建议配置为：

```
labels:
app:{serviceName}
version: v1
```

## 修复指导<a name="section133216587282"></a>

修改Pod标签：

1.  复制原有工作负载配置，保存为yaml文件：

    ```
    kubectl get deployment {deploymentName} -n {namespace} -o yaml > {deploymentName}-deployment.yaml
    ```

    例如：

    ```
    kubectl get deployment productpage -n default -o yaml > productpage-deployment.yaml 
    ```

2.  修改productpage-deployment.yaml内容，如果没有app和version，需要添加。app的值建议与Service名称一致，version建议为v1。
3.  删除原工作负载：

    ```
    kubectl delete deployment {oldDeploymentName} -n {namespace}
    ```

4.  应用新的工作负载配置：

    ```
    kubectl apply -f productpage-deployment.yaml
    ```


>![](public_sys-resources/icon-note.gif) **说明：** 
>-   1.15及以下集群可以在CCE控制台直接修改Pod的标签，但有可能会导致replicaset残留。
>-   修改或删除Deployment会触发Pod滚动升级，可能会导致业务短暂中断，请根据业务场景选择适当的时间修改。
>    1.  删除残留的ReplicaSet：
>    ```
>    kubectl get replicaset  |grep {deploymentName}
>    ```
>    1.  找到实例个数大于1的ReplicaSet，如果ReplicaSet个数大于1，可能是修改label导致ReplicaSet残留。需要删除旧配置的ReplicaSet：
>    ```
>    kubectl delete replicaset {replicaSetName} -n {namespace}
>    ```

