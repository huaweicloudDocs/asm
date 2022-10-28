# 所有Pod的app和version标签是否都相等<a name="asm_01_0062"></a>

## 问题描述<a name="section871654644012"></a>

Service关联的所有Pod的app和version标签必须都相等。app标签在流量监控中用于流量的跟踪，version标签在灰度发布中用于区分不同版本。如果存在app或version标签不相等的Pod，则报此异常。

## 修复指导<a name="section761818153105"></a>

Pod标签配置在Deployment的spec.template.metadata.labels中，建议配置为：

```
labels:
  app: {serviceName}
  version: v1
```

修改多个Pod标签为相等的操作方法如下：

1.  查看Service选择器（spec.selector）配置的标签。

    **kubectl get svc**  \{serviceName\}  **-o yaml**

    例如，标签是app: ratings和release: istio-bookinfo。

2.  根据标签查找Service关联的Pod。

    **kubectl get pod -n**  \{namespace\}  **-l app=ratings,release=istio-bookinfo**

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >\{namespace\}和Service的namespace一致。

3.  根据Pod名称，找到其关联的工作负载。

    **kubectl get deployment**  \{deploymentName\}  **-n**  \{namespace\}

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >-   一般Pod名称格式为\{deploymentName\}-\{随机字符串\}-\{随机字符串\}。
    >-   如果根据Pod名称未查询到工作负载，可能是因为ReplicaSet有残留，需要将其删除。
    >    判断是否存在ReplicaSet残留的方法如下：
    >    1.  查询Deployment的ReplicaSet。
    >        **kubectl get replicaset | grep**  \{deploymentName\}
    >    2.  找到实例个数大于1的ReplicaSet，如果ReplicaSet个数大于1，可能是修改label导致ReplicaSet残留。需要删除旧配置的ReplicaSet。
    >        **kubectl delete replicaset**  \{replicaSetName\}  **-n**  \{namespace\}

4.  请参考[修复指导](所有Pod是否都配置了app和version标签.md#section551915418912)修改工作负载中Pod的app和version标签。

