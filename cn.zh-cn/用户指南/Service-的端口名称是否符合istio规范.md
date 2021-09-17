# Service 的端口名称是否符合istio规范<a name="istio_01_0066"></a>

Service端口名必须包含指定的协议前缀，按以下格式命名：

name: <protocol\>\[-<suffix\>\]

## 修复指导<a name="section369473114412"></a>

方法一：登录CCE控制台，单击“资源管理 \> 网络管理”，单击对应服务后的“编辑YAML”，查看Service协议，根据支持协议，修改协议，在服务名称前加协议类型，如图。

![](figures/unnaming-(30).png)

