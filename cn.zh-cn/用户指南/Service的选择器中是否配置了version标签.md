# Service的选择器中是否配置了version标签<a name="asm_01_0067"></a>

## 问题描述<a name="section53791230142415"></a>

Service的选择器（spec.selector）中不能包含version标签。如果包含，则报此异常。

## 修复指导<a name="section4657141417"></a>

1.  登录CCE控制台，单击集群名称进入详情页面。
2.  在左侧导航栏选择“资源 \> 服务发现”，单击对应服务后的“更多 \> 编辑YAML”，查看Service的选择器（spec.selector），删除已配置的version标签。

    ![](figures/4-3-2.png)


