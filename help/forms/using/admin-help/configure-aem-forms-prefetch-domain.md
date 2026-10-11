---
title: 配置AEM表单以预取域信息
description: 如果由于深度嵌套群组而导致响应时间变慢或者您是多个群组的成员，请配置AEM表单以预取域信息。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: cf5283a5-dbfb-460d-a8bd-11cd15ab8640
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 0%
---
# 配置AEM表单以预取域信息 {#configure-aem-forms-to-prefetchdomain-information}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

如果用户属于多个组（例如，500个或更多）或这些组嵌套得很深（例如，30个级别），则用户响应速度可能会较慢。 如果您遇到此问题，可以将AEM表单配置为从特定域预取信息。

1. 在管理控制台中，单击&#x200B;**[!UICONTROL 设置>用户管理>配置>导入和导出配置文件]**。
1. 要将当前配置设置导出到文件，请单击&#x200B;**[!UICONTROL 导出]**&#x200B;并将配置文件保存到其他位置。
1. 添加以下节点（以粗体标记）：

   ```xml
    <node name="UM">
    <map/>
    <node name="PrincipalCache">
        <map>
            <entry key="principalCacheSize" value="1000"/>
            <entry key="principalCacheBatchFetchSize" value="10"/>
            <entry key="rebuildCacheAfterSync" value="true />
            <entry key="enableFullPrefetch" value="false"/>
            <entry key="principalCacheDomains" value="Domain_Name1/Domain_Name2/Domain_Name3"/>
        <map>
    </node>
    <node name="APSAuditService">
   ```

   在此示例中，为预取配置了多个域。 域名用“/”分隔。 上面的示例中显示了使用&#x200B;*Domain_Name1*、*Domain_Name2*&#x200B;和&#x200B;*Domain_Name3*&#x200B;的情况。

1. 要导入更新的文件，请在“用户管理”中单击&#x200B;**[!UICONTROL 配置>导入和导出配置文件]**。
1. 单击&#x200B;**[!UICONTROL 浏览]**&#x200B;查找文件，单击“导入”，然后单击&#x200B;**[!UICONTROL 确定]**。
