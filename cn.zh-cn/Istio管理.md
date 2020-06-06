# Istio管理<a name="istio_01_0013"></a>

Istio管理提供了Istio控制面组件、数据面sidecar的健康及性能监控能力，支持运行资源的扩缩容管理，以及不同Istio版本间的升级管理。

Istio控制面组件负责向数据面组件注入sidecar，管理数据面sidecar行为，下发策略配置，搜集监控数据等。其中，sidecar（边车）是指运行在业务pod中，与业务容器协同工作，负责业务pod的路由转发，监控数据采集，流量规则配置等功能。

## 监控已启用Istio服务网格的集群<a name="section01781436134612"></a>

1.  登录[应用服务网格控制台](https://console.huaweicloud.com/istio/?locale=zh-cn)，在左侧导航栏中选择“Istio管理“。
2.  查看所有已启用Istio服务网格的集群情况。

    在该页面，您可以查看每个集群的Istio版本，运行状态，计费模式，产品系列，可用集群数量，控制面组件数量和数据面Sidecar数量，以及控制面组件pilot，mixer，gateway的CPU与内存占用量。

3.  单击集群名称，查看控制面所有组件和Sidecar的业务pod信息。
    -   “控制面管理”页签：展示Istio控制面的所有组件，以及每个组件的运行状态，CUP、内存占用率，实例数量，命名空间等信息。
    -   “Sidecar管理”页签：展示所有注入了sidecar的业务pod信息，以及每个pod的名称，CPU、内存占用率，sidecar版本，创建时间，sidecar升级操作入口等信息。
    -   “运行节点”页签：查看节点的相关信息，包括节点名称、状态、节点模式（独享/共享）、可用区、私有IP地址、规格、可用CPU、可用内存。
    -   “Addon管理”页签：可以对grafana、prometheus、kiali、tracing四个插件进行安装和卸载，这些插件可以帮助用户进行流量治理与监测。
    -   “运行事件”页签：记录控制面组件的kubernetes事件，帮助您快速定位Istio控制面问题。
    -   “运行日志”页签：记录控制面组件的运行日志，帮助您快速定位Istio控制面问题。
    -   “配置管理”页签：支持公共配置和性能调优配置，请根据实际需求选择。详情请参见[配置管理](#section13427952132712)。
    -   “istioctl”页签：使用Istio命令行工具配置路由策略。详情请参见[使用Istio命令行工具配置路由策略](#section1138617313614)。


## 升级Istio控制面<a name="section1018018369464"></a>

执行升级操作需具备以下两个条件：

-   Istio控制面运行版本需小于最新版本
-   旧版本Istio控制面运行正常

1.  登录[应用服务网格控制台](https://console.huaweicloud.com/istio/?locale=zh-cn)，在左侧导航栏中选择“Istio管理“。
2.  在Istio管理集群列表页面，单击待升级集群后的“操作 \> 升级”。
3.  查看升级版本，确定是否自动升级sidecar。
    -   是：会在Istio控制面升级完成后，通过重启业务pod的方式进行sidecar重新注入，过程中业务pod将会重启，可能导致业务中断。
    -   否：仅会升级Istio控制面组件，sidecar升级需跳转到Sidecar管理页签自行升级sidecar，该方式会导致控制面组件与数据面sidecar版本不一致，可能产生兼容性问题，建议尽快同步升级sdiecar版本。

4.  确认无误后，单击“升级”。

## Sidecar管理<a name="section18646815124311"></a>

展示所有注入了sidecar的业务pod信息，以及每个pod的名称，CPU、内存占用率，sidecar版本，创建时间，sidecar升级操作入口等信息。

您可以在“Sidecar管理“中进行“Sidecar升级”，详细步骤如下：

1.  登录[应用服务网格控制台](https://console.huaweicloud.com/istio/?locale=zh-cn)，在左侧导航栏中选择“Istio管理“。
2.  单击相应集群名称进入Istio管理详情。
3.  在“Sidecar管理“页签，单击“Sidecar升级”，选择组件进行Sidecar升级。

    >![](public_sys-resources/icon-notice.gif) **须知：**   
    >对于单实例组件，升级会触发流量短暂中断，建议扩容后再升级。  


## 运行节点<a name="section91838369465"></a>

“运行节点“可以帮助您查看已创建的节点。您在当前集群中创建了节点，就可以在“运行节点“页中查看节点的相关信息，包括节点名称、状态、节点模式（独享/共享）、可用区、私有IP地址、规格、可用CPU、可用内存。

您还可以在“运行节点“中对节点进行“扩容“，详细步骤如下：

1.  登录[应用服务网格控制台](https://console.huaweicloud.com/istio/?locale=zh-cn)，单击左侧导航栏中的“Istio管理“。
2.  单击相应集群名称进入Istio管理详情。
3.  在“运行节点“页签，单击“操作“下的“扩容“链接跳转到弹性云服务器页面。

    **图 1**  Istio节点扩容<a name="fig95568451334"></a>  
    ![](figures/Istio节点扩容.png "Istio节点扩容")

4.  根据节点“名称/ID“找到对应的云服务器，单击“变更规格“，即可对节点进行扩容操作。

    **图 2**  变更规格<a name="fig179773126264"></a>  
    ![](figures/变更规格.png "变更规格")


## Addon管理<a name="section11869361463"></a>

Addon管理可以对grafana、prometheus、kiali、tracing四个插件进行安装和卸载，这些插件可以帮助用户进行流量治理与监测。详细步骤如下：

1.  登录[应用服务网格控制台](https://console.huaweicloud.com/istio/?locale=zh-cn)，单击左侧导航栏中的“Istio管理“。
2.  单击相应集群名称进入Istio管理详情。
3.  在“Addon管理“页签，单击待安装插件下方的“安装“，跳转到安装页面。
4.  在安装页面，选择插件要绑定的“弹性负载“，输入要分配给插件安装的“CPU配额“和“内存配额“。

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   当前服务网格支持“经典型负载均衡“和“增强型弹性负载均衡“，为了更好地与服务网格配合，推荐创建并使用“增强型弹性负载均衡“。  
    >-   如果您的弹性负载均衡监听器配额不足将不会显示在负载均衡器列表中。  
    >-   CPU配额和内存配额中的“申请“和“限制“值为必填，且不能超过节点剩余额度。  

5.  单击“安装“，跳转到插件管理页面，在插件卡片的左上角显示插件的安装和运行状态。如果插件长时间处于安装中状态或者安装失败状态，请删除以后重新安装。

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >如果无需使用该插件，单击插件卡片右上角的“删除“进行卸载。  


## 使用Istio命令行工具配置路由策略<a name="section1138617313614"></a>

使用Istio命令行工具可以配置多种路由策略管理服务流量，包括流量转移、故障注入、限流熔断等。

1.  登录[应用服务网格控制台](https://console.huaweicloud.com/istio/?locale=zh-cn)，单击左侧导航栏中的“Istio管理“。
2.  单击相应集群名称进入Istio管理详情。
3.  在“istioctl”页签，参照界面提示完成对应配置。

    ![](figures/istioctl.png)


## 配置管理<a name="section13427952132712"></a>

1.  登录[应用服务网格控制台](https://console.huaweicloud.com/istio/?locale=zh-cn)，单击左侧导航栏中的“Istio管理“。
2.  单击相应集群名称进入Istio管理详情。
3.  在“配置管理“页签，根据实际需求进行如下配置。
    -   公共配置：配置服务网格控制面公共基础配置，对所有组件负载生效。
    -   性能调优配置：根据网格下服务负载运行信息，调整参数，实现最优性能。


