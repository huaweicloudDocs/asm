# IstioOperator配置资源处理策略<a name="asm_01_0092"></a>

Istio采用Istio Operator安装的场景下，有时需要更新被Istio Operator管理的组件（包括istiod、istio-ingressgateway、istio-egressgateway）的工作负载，例如，升级网格版本、扩容istio-ingressgateway实例数等。更新这些工作负载存在如下配置入口：在CCE控制台“工作负载”页面修改，在ASM控制台“系统组件管理”页面修改（企业版网格），或者直接修改IstioOperator资源（以下简称IOP入口）。

## 处理策略<a name="section13241194335"></a>

为了避免多个入口的配置相冲突，以及确保Istio各工作负载持续稳定运行，我们采取如下策略：

-   定义工作负载的关键运行配置和非关键运行配置

    **表 1**  各资源类型下的关键运行配置

    <a name="table53111496236"></a>
    <table><thead align="left"><tr id="row123398916238"><th class="cellrowborder" valign="top" width="20.77%" id="mcps1.2.4.1.1"><p id="p1633910920236"><a name="p1633910920236"></a><a name="p1633910920236"></a>资源类型</p>
    </th>
    <th class="cellrowborder" valign="top" width="44.2%" id="mcps1.2.4.1.2"><p id="p83390910233"><a name="p83390910233"></a><a name="p83390910233"></a>配置项</p>
    </th>
    <th class="cellrowborder" valign="top" width="35.03%" id="mcps1.2.4.1.3"><p id="p0339198232"><a name="p0339198232"></a><a name="p0339198232"></a>配置项描述</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row1333979172315"><td class="cellrowborder" rowspan="6" valign="top" width="20.77%" headers="mcps1.2.4.1.1 "><p id="p153397912236"><a name="p153397912236"></a><a name="p153397912236"></a>Deployment</p>
    </td>
    <td class="cellrowborder" valign="top" width="44.2%" headers="mcps1.2.4.1.2 "><p id="p1633915932312"><a name="p1633915932312"></a><a name="p1633915932312"></a>spec.replicas</p>
    </td>
    <td class="cellrowborder" valign="top" width="35.03%" headers="mcps1.2.4.1.3 "><p id="p533939132317"><a name="p533939132317"></a><a name="p533939132317"></a>实例数</p>
    </td>
    </tr>
    <tr id="row1133912912235"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1233910992319"><a name="p1233910992319"></a><a name="p1233910992319"></a>spec.strategy</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p6339109132318"><a name="p6339109132318"></a><a name="p6339109132318"></a>升级策略</p>
    </td>
    </tr>
    <tr id="row1033910920233"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p3339109142310"><a name="p3339109142310"></a><a name="p3339109142310"></a>spec.template.nodeSelector</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p33399942311"><a name="p33399942311"></a><a name="p33399942311"></a>调度策略</p>
    </td>
    </tr>
    <tr id="row533913922315"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p17339398239"><a name="p17339398239"></a><a name="p17339398239"></a>spec.template.affinity</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p183398912234"><a name="p183398912234"></a><a name="p183398912234"></a>调度策略</p>
    </td>
    </tr>
    <tr id="row1233969192318"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p43396919230"><a name="p43396919230"></a><a name="p43396919230"></a>spec.template.tolerations</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p1433917912312"><a name="p1433917912312"></a><a name="p1433917912312"></a>调度策略</p>
    </td>
    </tr>
    <tr id="row63391091238"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p163396982317"><a name="p163396982317"></a><a name="p163396982317"></a>spec.template.containers.resources</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p1233919916235"><a name="p1233919916235"></a><a name="p1233919916235"></a>资源请求和限制</p>
    </td>
    </tr>
    <tr id="row633915910230"><td class="cellrowborder" rowspan="5" valign="top" width="20.77%" headers="mcps1.2.4.1.1 "><p id="p13398942319"><a name="p13398942319"></a><a name="p13398942319"></a>DaemonSet</p>
    </td>
    <td class="cellrowborder" valign="top" width="44.2%" headers="mcps1.2.4.1.2 "><p id="p233912942314"><a name="p233912942314"></a><a name="p233912942314"></a>spec.updateStrategy</p>
    </td>
    <td class="cellrowborder" valign="top" width="35.03%" headers="mcps1.2.4.1.3 "><p id="p933915912232"><a name="p933915912232"></a><a name="p933915912232"></a>升级策略</p>
    </td>
    </tr>
    <tr id="row83395992319"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p433929182318"><a name="p433929182318"></a><a name="p433929182318"></a>spec.template.nodeSelector</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p63392914232"><a name="p63392914232"></a><a name="p63392914232"></a>调度策略</p>
    </td>
    </tr>
    <tr id="row113396916232"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p5339189202317"><a name="p5339189202317"></a><a name="p5339189202317"></a>spec.template.affinity</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p23391498236"><a name="p23391498236"></a><a name="p23391498236"></a>调度策略</p>
    </td>
    </tr>
    <tr id="row833917914235"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p17339159152312"><a name="p17339159152312"></a><a name="p17339159152312"></a>spec.template.tolerations</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p17339149182310"><a name="p17339149182310"></a><a name="p17339149182310"></a>调度策略</p>
    </td>
    </tr>
    <tr id="row533920942312"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1033919992318"><a name="p1033919992318"></a><a name="p1033919992318"></a>spec.template.containers.resources</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p533915913238"><a name="p533915913238"></a><a name="p533915913238"></a>资源请求和限制</p>
    </td>
    </tr>
    <tr id="row3339189102310"><td class="cellrowborder" rowspan="6" valign="top" width="20.77%" headers="mcps1.2.4.1.1 "><p id="p23394932312"><a name="p23394932312"></a><a name="p23394932312"></a>StatefulSet</p>
    </td>
    <td class="cellrowborder" valign="top" width="44.2%" headers="mcps1.2.4.1.2 "><p id="p933969112313"><a name="p933969112313"></a><a name="p933969112313"></a>spec.replicas</p>
    </td>
    <td class="cellrowborder" valign="top" width="35.03%" headers="mcps1.2.4.1.3 "><p id="p15339129152310"><a name="p15339129152310"></a><a name="p15339129152310"></a>实例数</p>
    </td>
    </tr>
    <tr id="row113396919237"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p103399914230"><a name="p103399914230"></a><a name="p103399914230"></a>spec.updateStrategy</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p5339139182317"><a name="p5339139182317"></a><a name="p5339139182317"></a>升级策略</p>
    </td>
    </tr>
    <tr id="row15339392234"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p433969122311"><a name="p433969122311"></a><a name="p433969122311"></a>spec.template.nodeSelector</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p2033959102311"><a name="p2033959102311"></a><a name="p2033959102311"></a>调度策略</p>
    </td>
    </tr>
    <tr id="row123392098234"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p6339149162310"><a name="p6339149162310"></a><a name="p6339149162310"></a>spec.template.affinity</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p113399932313"><a name="p113399932313"></a><a name="p113399932313"></a>调度策略</p>
    </td>
    </tr>
    <tr id="row13392917239"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p11339994236"><a name="p11339994236"></a><a name="p11339994236"></a>spec.template.tolerations</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p43397919232"><a name="p43397919232"></a><a name="p43397919232"></a>调度策略</p>
    </td>
    </tr>
    <tr id="row733915972318"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p193391291238"><a name="p193391291238"></a><a name="p193391291238"></a>spec.template.containers.resources</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p1533912942314"><a name="p1533912942314"></a><a name="p1533912942314"></a>资源请求和限制</p>
    </td>
    </tr>
    <tr id="row1733920962313"><td class="cellrowborder" rowspan="4" valign="top" width="20.77%" headers="mcps1.2.4.1.1 "><p id="p833959142313"><a name="p833959142313"></a><a name="p833959142313"></a>Pod</p>
    </td>
    <td class="cellrowborder" valign="top" width="44.2%" headers="mcps1.2.4.1.2 "><p id="p16339179202316"><a name="p16339179202316"></a><a name="p16339179202316"></a>spec.nodeSelector</p>
    </td>
    <td class="cellrowborder" valign="top" width="35.03%" headers="mcps1.2.4.1.3 "><p id="p1534069192312"><a name="p1534069192312"></a><a name="p1534069192312"></a>调度策略</p>
    </td>
    </tr>
    <tr id="row19340693237"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1634010918230"><a name="p1634010918230"></a><a name="p1634010918230"></a>spec.affinity</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p83405982320"><a name="p83405982320"></a><a name="p83405982320"></a>调度策略</p>
    </td>
    </tr>
    <tr id="row1340109192316"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1934012912234"><a name="p1934012912234"></a><a name="p1934012912234"></a>spec.tolerations</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p193401294232"><a name="p193401294232"></a><a name="p193401294232"></a>调度策略</p>
    </td>
    </tr>
    <tr id="row18340199152318"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1834014913236"><a name="p1834014913236"></a><a name="p1834014913236"></a>spec.containers.resources</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p16340129172319"><a name="p16340129172319"></a><a name="p16340129172319"></a>资源请求和限制</p>
    </td>
    </tr>
    </tbody>
    </table>

-   <a name="li176012101179"></a>Istio Operator默认保持当前集群中工作负载的关键运行配置不做更新，仅支持非关键运行配置更新。
-   IstioOperator CRD中新增annotation key：asm.huaweicloud.com/reconcileFromIstioOperatorCR，用于描述配置生效策略。

    当用户配置和使能该策略（asm.huaweicloud.com/reconcileFromIstioOperatorCR: 'true'）后，Istio Operator完全按照IstioOperator CRD中定义的配置进行更新。配置为'false'时，相当于Istio Operator的[上述默认策略](#li176012101179)。


为了更清晰地观测以上策略是如何配置和生效的，我们以一个1.8.6基础版网格为例，验证步骤如下：

1.  在IOP入口修改istio-egressgateway组件的关键运行配置。
    1.  登录[应用服务网格控制台](https://console.huaweicloud.com/asm/?locale=zh-cn)，单击服务网格的名称，进入网格详情页面。
    2.  在左侧导航栏选择“网格配置”，单击“istio资源管理”页签。
    3.  在搜索框中选择“istio资源：istiooperators”及“命名空间：istio-system”。
    4.  单击private-data-plane资源操作列的“编辑”，将istio-egressgateway的实例数从2改为3。

        ```
        ...
        spec:
          components:
            egressGateways:
              - enabled: true
                k8s:
                  affinity:
                    nodeAffinity:
                      preferredDuringSchedulingIgnoredDuringExecution:
                        - preference:
                            matchExpressions:
                              - key: istio
                                operator: In
                                values:
                                  - master
                          weight: 1
                    podAntiAffinity:
                      requiredDuringSchedulingIgnoredDuringExecution:
                        - labelSelector:
                            matchExpressions:
                              - key: app
                                operator: In
                                values:
                                  - istio-egressgateway
                          topologyKey: kubernetes.io/hostname
                  podAnnotations:
                    seccomp.security.alpha.kubernetes.io/pod: runtime/default
                  replicaCount: 3
                  strategy:
                    rollingUpdate:
                      maxSurge: 0
                name: istio-egressgateway
        ...
        ```

2.  重启istio-egressgateway工作负载。
    1.  登录CCE控制台，单击已启用网格的集群名称，进入集群详情页面。
    2.  在左侧导航栏选择“资源 \> 工作负载”，切换至istio-system命名空间，单击istio-egressgateway工作负载操作列的“更多 \> 重新部署”，在弹出的提示信息中选择“是”。

3.  验证配置是否生效。

    查看istio-egressgateway工作负载的实例数仍然为2，说明默认情况下，在IOP入口修改工作负载的关键运行配置不生效。


