# 所有Pod的app和version标签是否都相等<a name="istio_01_0062"></a>

Service关联的所有Deployment的配置中（spec.template.metadata.labels），Pod的app和version标签必须都相等，建议配置为：

```
labels:
app:{serviceName}
version: v1
```

>![](public_sys-resources/icon-note.gif) **说明：** 
>-   version标签在灰度发布中用于不同版本的区分 app标签在流量监控中用于流量的跟踪
>-   Service要求没有进行灰度发布。

## 修复指导<a name="section4945183473811"></a>

修改多个Pod标签为相等：

1.  查看Service选择器（spec.selector）配置的标签：

    ```
    kubectl get svc {serviceName} -oyaml
    ```

    例如：标签是app: ratings 和 release: istio-bookinfo

2.  根据标签查找Service关联的Pod：

    ```
    kubectl get pod -n {namespace} -l app=ratings,release=istio-bookinfo
    ```

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >-   \{namespace\}和Service的namespace一致。


1.  根据Pod名称，找到其关联的工作负载。

    ```
    kubectl get deployment {deploymentName} -n {namespace}
    ```

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >-   一般Pod名称格式为\{deploymentName\}-\{随机字符串\}-\{随机字符串\}。
    >-   如果工作负载不存在，可能是ReplicaSet有残留，还需要查看ReplicaSet
    >    删除残留的ReplicaSet：
    >    ```
    >    kubectl get replicaset  |grep {deploymentName}
    >    ```
    >    找到实例个数大于1的ReplicaSet，如果ReplicaSet个数大于1，可能是修改label导致ReplicaSet残留。需要删除旧配置的ReplicaSet：
    >    ```
    >    kubectl delete replicaset {replicaSetName} -n {namespace}
    >    ```

2.  请参照[修改Pod标签](所有Pod是否都配置了app和version标签.md#li67618288356)修改工作负载中Pod的app和version标签。

>![](public_sys-resources/icon-note.gif) **说明：** 
>-   1.15及以下集群可以在CCE控制台直接修改Pod的标签，但有可能会导致replicaset残留。
>-   修改或删除Deployment会触发Pod滚动升级，可能会导致业务短暂中断，请根据业务场景选择适当的时间修改。

