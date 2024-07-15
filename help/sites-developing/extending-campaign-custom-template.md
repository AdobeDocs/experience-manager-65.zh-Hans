---
title: 使用Adobe Campaign表单组件创建自定义AEM页面模板
description: 构建使用Adobe Campaign表单组件的自定义页面模板
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: de5c634a-c0d7-4e69-b941-d2fbfe83117d
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: ad8f849384e58511de97611d1b26c4fc96022062
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# 使用Adobe Campaign表单组件创建自定义AEM页面模板{#creating-custom-aem-page-template-with-adobe-campaign-form-components}

本页说明如何通过检查Geometrixx-outdoors模板(`/apps/geometrixx-outdoors/components/page_campaign_profile`)的实施方式，生成使用[Adobe Campaign Form](/help/sites-authoring/adobe-campaign-components.md)组件的自定义页面模板，并指出创建自己的自定义模板时可能需要的重要信息。

>[!NOTE]
>
>[电子邮件和表单示例仅在Geometrixx](/help/sites-developing/we-retail.md)中可用。 从包共享下载示例Geometrixx内容。

>[!CAUTION]
>
>已弃用AEM电子邮件组件。 由于电子邮件将内容和样式融合在一起，因此由AEM提供的现成可用电子邮件组件对于客户的重用受到限制，因为需要将自定义样式实施到项目所需的任何组件中。
>
>电子邮件组件可以在项目级别实施，已弃用的AEM电子邮件组件说明了如何实现这一点。 但是，请勿在项目中使用这些已弃用的组件。


要使用Adobe Campaign表单组件创建自定义AEM页面模板，请确保您满足以下条件：

1. **更正了resourceSuperType**

   确保页面组件继承自`mcm/campaign/components/profile`。

   servlet获取和保存信息需要此信息

   * `com.day.cq.mcm.campaign.servlets.TemplateListServlet`
   * `com.day.cq.mcm.campaign.servlets.SaveProfileServlet`

   ![chlimage_1-201](assets/chlimage_1-201.png)

1. **ClientContext设置**

   查看clientcontext设置(`/etc/designs/geometrixx-outdoors/jcr:content/page_campaign_profile`)时，您会看到以下设置：

   * ClientContext指向`/etc/clientcontext/campaign`
   * 还有一个额外的&#x200B;*配置*&#x200B;节点。

   ![chlimage_1-202](assets/chlimage_1-202.png)

1. **head.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/head.jsp)**

   在&#x200B;**head.jsp**&#x200B;中，您看到以下行使用&#x200B;**clientcontext-config**&#x200B;和&#x200B;**cloudservice-hook**：

   ```
   <cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub"/>
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
   ```

1. **body.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/body.jsp)**

   在&#x200B;**body.jsp**&#x200B;中，云服务加载到页面底部：

   ```
   <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
   ```

1. **营销活动页面属性**

   为了能够选择Adobe Campaign模板，使用&#x200B;**Campaign**&#x200B;选项卡扩展了页面属性：

   `/apps/geometrixx-outdoors/components/page_campaign_profile/dialog/items/tabs/items/campaign`

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. **模板设置**。

   在模板(`/apps/geometrixx-outdoors/templates/campaign_profile/jcr:content`)中，您会看到以下默认值：

   | **acMapping** | mapRecipient(适用于Adobe Campaign 6.1)，profile(适用于Adobe Campaign Standard) |
   |---|---|
   | **acTemplateId** | 邮件 |

   ![chlimage_1-204](assets/chlimage_1-204.png)
