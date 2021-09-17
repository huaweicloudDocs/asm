# sidecar管理<a name="istio_01_0041"></a>

## 操作步骤<a name="section151393212392"></a>

1.  登录应用服务网格控制台，单击需要查看的服务网格的名称，进入“网格配置“。
2.  单击“sidecar管理”页签，可查看所有注入了边车的业务pod信息以及进行边车注入、资源限制等操作。

## sidecar注入<a name="section11173112110410"></a>

可展示当前已注入边车的命名空间及所属集群。

选择需要注入sidecar的命名空间，如果需要重启已有服务，请单击“确定”，为命名空间注入sidecar并重启服务。如果没有选择重启，则需要登录CCE控制台，手动重启工作负载才会注入sidecar。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>-   选择需要的命名空间，为选择的命名空间打上inject=true标签。
>-   如勾选重启已有服务，在注入sidecar后会重启已有的deployment，将会暂时中断业务。

## sidecar资源配置<a name="section196974584263"></a>

单击工作负载的折叠按钮可查看负载的sidecar名称、sidecar版本、状态、CPU及内存使用率。如果当前选择的工作负载未注入边车，请参考[sidecar注入](https://support.huaweicloud.com/usermanual-istio/istio_01_0041.html#section1)。

选择需要进行边车资源配置的工作负载，单击“资源限制”，设置CPU和内存的限制。

-   CPU：容器使用的最小或最大CPU需求，作为容器调度时资源分配的判断依赖。
-   MEM：容器使用的最小或最大内存需求，作为容器调度时资源分配的判断依赖。

