# Service是否配置了app标签，值是否正确<a name="istio_01_0068"></a>

Service的标签（metadata.labels）中，需要显示配置app标签，并和关联的Deployment中（spec.template.metadata.labels）Pod的app标签一致。

>![](public_sys-resources/icon-note.gif) **说明：** 
>app标签在流量监控中用于流量的跟踪。

## 修复指导<a name="section10662195612492"></a>

1.  登录CCE控制台，单击“资源管理 \> 网络管理”查看Service app（metadata.labels）的标签。

    ![](figures/unnaming-(33).png)


1.  单击“工作负载 \> 无状态工作负载”查看Deployment中Pod的app（spec.template.metadata.labels）标签。

    ![](figures/unnaming-(34).png)

2.  修改Service app的标签与Pod app值一致。

