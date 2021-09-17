# Service的选择器中是否配置了version标签<a name="istio_01_0067"></a>

Service的选择器（spec.selector）中不能包含version标签。

version标签在灰度发布中用于区分服务的不同版本

## 修复指导<a name="section1226116546472"></a>

登录CCE控制台，单击“资源管理 \> 网络管理”，查看service的选择器（spec.selector），删除已配置的version标签。

![](figures/unnaming-(43).png)

