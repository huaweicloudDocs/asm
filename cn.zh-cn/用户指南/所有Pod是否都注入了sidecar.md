# 所有Pod是否都注入了sidecar<a name="istio_01_0063"></a>

Service管理的所有Pod是否都存在istio-proxy容器。请检查命名空间是否配置了自动注入sidecar，如果配置后重启Pod仍然无法注入，请检查实例数量是否超过了套餐限制。

## 修复指导<a name="section1457519694110"></a>

为Pod注入Sidecar：

1.  如果集群未开启命名空间注入，可参照[sidecar注入](https://support.huaweicloud.com/usermanual-istio/istio_01_0041.html#section1)，为命名空间下所有工作负载关联的Pod注入sidecar；

    或在CCE控制台，只为某个工作负载为该工作负载加annotation 标签，为关联的Pod注入sidecar。请单击[参考](https://istio.io/latest/docs/setup/additional-setup/sidecar-injection/)查看详情。

    ![](figures/unnaming-(42).png)

2.  如果集群已经开启了命名空间注入，但是Pod未注入Sidecar，需要登录CCE控制台，对应的工作负载下重启Pod或者检查网格实例数量是否已经超出套餐配额。

