# YAML方式配置Istio资源<a name="asm_01_0048"></a>

网格中服务关联的Istio资源（如VirtualService、DestinationRule）如需修改，可以在“istio资源管理”中以YAML或JSON格式进行编辑。同时，还支持创建新的istio资源。

>![](public_sys-resources/icon-caution.gif) **注意：** 
>使用YAML方式创建和修改Istio资源可能导致与控制台配置不兼容，控制台相关功能将不再开放使用。如果您确定后续将只通过YAML方式维护Istio资源，则参考本章节编辑或新建Istio资源，否则请不要在此处操作。

## 编辑已有istio资源<a name="section126909124113"></a>

1.  登录[应用服务网格控制台](https://console.huaweicloud.com/asm/?locale=zh-cn)，单击服务网格的名称，进入网格详情页面。
2.  在左侧导航栏选择“网格配置”，单击“istio资源管理”页签。
3.  在搜索框中选择istio资源类型（如“istio资源：virtualservices”），以及资源所属命名空间。

    **图 1**  筛选istio资源<a name="fig1869946283"></a>  
    ![](figures/筛选istio资源.png "筛选istio资源")

4.  单击操作列的“编辑”，在右侧页面修改相关配置，默认勾选底部提示信息，即控制台相关功能将不再开放使用，单击“确定”保存。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >编辑Istio资源后，具体哪些控制台功能不可用，与Istio资源类型有关，详细说明请参见[YAML配置资源处理策略](YAML配置资源处理策略.md)。

    支持以YAML或JSON格式显示，同时可以将配置文件下载到本地。


## 创建新的istio资源<a name="section1969114121917"></a>

1.  登录[应用服务网格控制台](https://console.huaweicloud.com/asm/?locale=zh-cn)，单击服务网格的名称，进入网格详情页面。
2.  在左侧导航栏选择“网格配置”，单击“istio资源管理”页签。
3.  单击列表左上方的“创建”。

    **图 2**  创建istio资源<a name="fig53492334353"></a>  
    ![](figures/创建istio资源.png "创建istio资源")

4.  在右侧页面直接输入内容，或者单击“导入文件”，将本地编辑好的YAML或JSON文件上传上来。
5.  确认文件内容无误，默认勾选底部提示信息，即控制台相关功能将不再开放使用，单击“确定”保存。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >创建Istio资源后，具体哪些控制台功能不可用，与Istio资源类型有关，详细说明请参见[YAML配置资源处理策略](YAML配置资源处理策略.md)。


## Istio资源说明<a name="section10702112795512"></a>

**表 1**  Istio资源说明

<a name="table20619175295614"></a>
<table><thead align="left"><tr id="row862013522566"><th class="cellrowborder" valign="top" width="27.689999999999998%" id="mcps1.2.3.1.1"><p id="p1062095235616"><a name="p1062095235616"></a><a name="p1062095235616"></a>资源类型</p>
</th>
<th class="cellrowborder" valign="top" width="72.31%" id="mcps1.2.3.1.2"><p id="p1162035218561"><a name="p1162035218561"></a><a name="p1162035218561"></a>说明</p>
</th>
</tr>
</thead>
<tbody><tr id="row621427185917"><td class="cellrowborder" valign="top" width="27.689999999999998%" headers="mcps1.2.3.1.1 "><p id="p1021420710596"><a name="p1021420710596"></a><a name="p1021420710596"></a>AuthorizationPolicy</p>
</td>
<td class="cellrowborder" valign="top" width="72.31%" headers="mcps1.2.3.1.2 "><p id="p172153775918"><a name="p172153775918"></a><a name="p172153775918"></a>用于配置授权规则。</p>
</td>
</tr>
<tr id="row17620125265618"><td class="cellrowborder" valign="top" width="27.689999999999998%" headers="mcps1.2.3.1.1 "><p id="p2211181117593"><a name="p2211181117593"></a><a name="p2211181117593"></a>DestinationRule</p>
</td>
<td class="cellrowborder" valign="top" width="72.31%" headers="mcps1.2.3.1.2 "><p id="p15620552195618"><a name="p15620552195618"></a><a name="p15620552195618"></a>定义路由的目标服务和流量策略。VirtualService和DestinationRule是流量控制最关键的两个资源，DestinationRule定义了网格中某个Service对外提供服务的策略及规则，包括负载均衡策略、异常点监测、熔断控制、访问连接池等。</p>
</td>
</tr>
<tr id="row196209526568"><td class="cellrowborder" valign="top" width="27.689999999999998%" headers="mcps1.2.3.1.1 "><p id="p8210511195918"><a name="p8210511195918"></a><a name="p8210511195918"></a>EnvoyFilter</p>
</td>
<td class="cellrowborder" valign="top" width="72.31%" headers="mcps1.2.3.1.2 "><p id="p1762019526566"><a name="p1762019526566"></a><a name="p1762019526566"></a>EnvoyFilter为服务网格控制面提供更强大的扩展能力，使Envoy中Filter Chain具备自定义配置的能力。</p>
</td>
</tr>
<tr id="row8620155225614"><td class="cellrowborder" valign="top" width="27.689999999999998%" headers="mcps1.2.3.1.1 "><p id="p1562085285612"><a name="p1562085285612"></a><a name="p1562085285612"></a>Gateway</p>
</td>
<td class="cellrowborder" valign="top" width="72.31%" headers="mcps1.2.3.1.2 "><p id="p4620852115611"><a name="p4620852115611"></a><a name="p4620852115611"></a>Gateway定义了所有HTTP/TCP流量进入网格或者从网格中出站的统一入口和出口，它描述了一组对外公开的端口、协议、负载均衡以及SNI配置。</p>
</td>
</tr>
<tr id="row76205526568"><td class="cellrowborder" valign="top" width="27.689999999999998%" headers="mcps1.2.3.1.1 "><p id="p1162085220560"><a name="p1162085220560"></a><a name="p1162085220560"></a>IstioOperator</p>
</td>
<td class="cellrowborder" valign="top" width="72.31%" headers="mcps1.2.3.1.2 "><p id="p1662035216565"><a name="p1662035216565"></a><a name="p1662035216565"></a>可以通过编辑IstioOperator对象来改变Istio的配置，控制器会检测到改变，继而用相应配置更新Istio的安装内容。</p>
</td>
</tr>
<tr id="row662055210567"><td class="cellrowborder" valign="top" width="27.689999999999998%" headers="mcps1.2.3.1.1 "><p id="p362085295613"><a name="p362085295613"></a><a name="p362085295613"></a>PeerAuthentication</p>
</td>
<td class="cellrowborder" valign="top" width="72.31%" headers="mcps1.2.3.1.2 "><p id="p14620105225616"><a name="p14620105225616"></a><a name="p14620105225616"></a>Istio的认证策略包含PeerAuthentication和RequestAuthentication，PeerAuthentication策略用于配置服务通信的mTLS模式。</p>
</td>
</tr>
<tr id="row17532161415111"><td class="cellrowborder" valign="top" width="27.689999999999998%" headers="mcps1.2.3.1.1 "><p id="p1453214141518"><a name="p1453214141518"></a><a name="p1453214141518"></a>RequestAuthentication</p>
</td>
<td class="cellrowborder" valign="top" width="72.31%" headers="mcps1.2.3.1.2 "><p id="p19532201415113"><a name="p19532201415113"></a><a name="p19532201415113"></a>Istio的认证策略包含PeerAuthentication和RequestAuthentication，RequestAuthentication策略用于配置服务的请求身份验证方法。</p>
</td>
</tr>
<tr id="row183423210116"><td class="cellrowborder" valign="top" width="27.689999999999998%" headers="mcps1.2.3.1.1 "><p id="p1083413329114"><a name="p1083413329114"></a><a name="p1083413329114"></a>ServiceEntry</p>
</td>
<td class="cellrowborder" valign="top" width="72.31%" headers="mcps1.2.3.1.2 "><p id="p1883473215112"><a name="p1883473215112"></a><a name="p1883473215112"></a>用于注册外部服务到网格内，并对其流量进行管理。</p>
</td>
</tr>
<tr id="row1426431920"><td class="cellrowborder" valign="top" width="27.689999999999998%" headers="mcps1.2.3.1.1 "><p id="p6265311215"><a name="p6265311215"></a><a name="p6265311215"></a>Sidecar</p>
</td>
<td class="cellrowborder" valign="top" width="72.31%" headers="mcps1.2.3.1.2 "><p id="p162610319216"><a name="p162610319216"></a><a name="p162610319216"></a>对Sidecar代理进行整体设置。</p>
</td>
</tr>
<tr id="row362025212568"><td class="cellrowborder" valign="top" width="27.689999999999998%" headers="mcps1.2.3.1.1 "><p id="p166209529565"><a name="p166209529565"></a><a name="p166209529565"></a>VirtualService</p>
</td>
<td class="cellrowborder" valign="top" width="72.31%" headers="mcps1.2.3.1.2 "><p id="p26208523568"><a name="p26208523568"></a><a name="p26208523568"></a>用于网格内路由的设置。VirtualService和DestinationRule是流量控制最关键的两个资源，在VirtualService中定义了一组路由规则，当流量进入时，逐个规则进行匹配，直到匹配成功后将流量转发给指定的路由地址。</p>
</td>
</tr>
<tr id="row3620195217568"><td class="cellrowborder" valign="top" width="27.689999999999998%" headers="mcps1.2.3.1.1 "><p id="p176201752105619"><a name="p176201752105619"></a><a name="p176201752105619"></a>WorkloadEntry</p>
</td>
<td class="cellrowborder" valign="top" width="72.31%" headers="mcps1.2.3.1.2 "><p id="p56201252185617"><a name="p56201252185617"></a><a name="p56201252185617"></a>用来将虚拟机（VM）或者裸金属（Bare Metal）进行抽象，使其在网格化后作为与Kubernetes中的Pod同等重要的负载，具备流量管理、安全管理、可视化等能力。</p>
</td>
</tr>
</tbody>
</table>

