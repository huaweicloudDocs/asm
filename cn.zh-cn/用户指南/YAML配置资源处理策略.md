# YAML配置资源处理策略<a name="asm_01_0090"></a>

通过控制台和“Istio资源管理”中的YAML方式均可以创建Istio资源，为了避免两个入口的配置相冲突，建议您：

-   控制台创建的资源，在控制台维护
-   YAML创建的资源，YAML方式维护

如果控制台创建的资源通过YAML方式修改，将会导致控制台对应功能不可用（例如，YAML配置VirtualService资源后，控制台对应服务的流量治理、灰度发布将不可用）。

## 处理策略<a name="section213352583014"></a>

在“网格配置 \> Istio资源管理”页面编辑或创建服务关联的Istio资源时，页面底部会默认勾选“控制台相关功能不开放使用”，当保持勾选状态并单击“确定”后，配置生效，但该服务的控制台部分功能将不再开放使用，后续将只能通过YAML方式维护。

>![](public_sys-resources/icon-caution.gif) **注意：** 
>如果不勾选“控制台相关功能不开放使用”，可能会导致修改的配置与部分控制台功能冲突，请谨慎选择。

**表 1**  勾选“控制台相关功能不开放使用”对服务的控制台功能的影响

<a name="table1459171944912"></a>
<table><thead align="left"><tr id="row16459161913498"><th class="cellrowborder" valign="top" width="49.559999999999995%" id="mcps1.2.3.1.1"><p id="p7459151912497"><a name="p7459151912497"></a><a name="p7459151912497"></a>现象</p>
</th>
<th class="cellrowborder" valign="top" width="50.44%" id="mcps1.2.3.1.2"><p id="p7459151944911"><a name="p7459151944911"></a><a name="p7459151944911"></a>可能原因</p>
</th>
</tr>
</thead>
<tbody><tr id="row54591219194916"><td class="cellrowborder" valign="top" width="49.559999999999995%" headers="mcps1.2.3.1.1 "><p id="p7459101934915"><a name="p7459101934915"></a><a name="p7459101934915"></a>在“服务管理”页面，目标服务的“安全”按钮置灰，不可点击</p>
</td>
<td class="cellrowborder" valign="top" width="50.44%" headers="mcps1.2.3.1.2 "><p id="p34595196493"><a name="p34595196493"></a><a name="p34595196493"></a>通过YAML方式修改了AuthorizationPolicy资源</p>
</td>
</tr>
<tr id="row1645921964916"><td class="cellrowborder" valign="top" width="49.559999999999995%" headers="mcps1.2.3.1.1 "><p id="p1045911197499"><a name="p1045911197499"></a><a name="p1045911197499"></a>在“服务管理”页面，目标服务的“流量治理”按钮置灰，不可点击</p>
</td>
<td class="cellrowborder" valign="top" width="50.44%" headers="mcps1.2.3.1.2 "><p id="p3459101984919"><a name="p3459101984919"></a><a name="p3459101984919"></a>通过YAML方式修改了DestinationRule或VirtualService资源</p>
</td>
</tr>
<tr id="row1445921984911"><td class="cellrowborder" valign="top" width="49.559999999999995%" headers="mcps1.2.3.1.1 "><p id="p114591919114916"><a name="p114591919114916"></a><a name="p114591919114916"></a>在“服务管理”页面，目标服务的“发布版本”按钮置灰，不可点击</p>
</td>
<td class="cellrowborder" valign="top" width="50.44%" headers="mcps1.2.3.1.2 "><p id="p16459719104910"><a name="p16459719104910"></a><a name="p16459719104910"></a>通过YAML方式修改了DestinationRule或VirtualService资源</p>
</td>
</tr>
<tr id="row19459191904910"><td class="cellrowborder" valign="top" width="49.559999999999995%" headers="mcps1.2.3.1.1 "><p id="p194595195491"><a name="p194595195491"></a><a name="p194595195491"></a>在“灰度发布”页面创建灰度发布任务时，目标服务置灰，不可选择</p>
</td>
<td class="cellrowborder" valign="top" width="50.44%" headers="mcps1.2.3.1.2 "><p id="p0459519194913"><a name="p0459519194913"></a><a name="p0459519194913"></a>通过YAML方式修改了DestinationRule或VirtualService资源</p>
</td>
</tr>
<tr id="row12411030556"><td class="cellrowborder" valign="top" width="49.559999999999995%" headers="mcps1.2.3.1.1 "><p id="p10459191974911"><a name="p10459191974911"></a><a name="p10459191974911"></a>在“网关管理”页面，目标网关的添加路由按钮置灰，不可点击</p>
</td>
<td class="cellrowborder" valign="top" width="50.44%" headers="mcps1.2.3.1.2 "><p id="p16459131924917"><a name="p16459131924917"></a><a name="p16459131924917"></a>通过YAML方式修改了Gateway资源</p>
</td>
</tr>
<tr id="row817173911446"><td class="cellrowborder" valign="top" width="49.559999999999995%" headers="mcps1.2.3.1.1 "><p id="p1618139124419"><a name="p1618139124419"></a><a name="p1618139124419"></a>在“网关管理”页面添加路由时，目标服务置灰，不可选择</p>
</td>
<td class="cellrowborder" valign="top" width="50.44%" headers="mcps1.2.3.1.2 "><p id="p2018739154412"><a name="p2018739154412"></a><a name="p2018739154412"></a>通过YAML方式修改了DestinationRule或VirtualService资源</p>
</td>
</tr>
</tbody>
</table>

