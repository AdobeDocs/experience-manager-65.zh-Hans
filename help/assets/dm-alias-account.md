---
title: 配置Dynamic Media公司别名帐户
description: 了解如何在Dynamic Media中配置公司别名帐户。
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
exl-id: 2ca7b8b2-573c-40e9-b8c3-f38736e819ef
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---

<!-- hide: yes
hidefromtoc: yes -->

# 关于配置Dynamic Media公司别名帐户 {#about-dm-alias-acct}

Dynamic Media URL和查看器嵌入代码包含您的公司帐户名称。 此帐户名称是在配置Dynamic Media时创建的。 在某些情况下，您的企业可能会经历收购、品牌再造，或者您只想使用更令人难忘的名字。 在这种情况下，在开箱即用的所有URL和查看器嵌入代码中手动更新公司帐户名称并不容易。 此外，您还可能会影响现有的Dynamic Media存储库或实时内容。 要解决此问题，您可以配置Dynamic Media公司别名帐户。

Dynamic Media公司别名帐户可确保用户界面中所有开箱即用的Dynamic Media URL和查看器嵌入代码反映对企业上下文所做的任何更新，例如品牌再造。 别名帐户也会对您的SEO（搜索引擎优化）产生积极影响，因为Dynamic Media URL和查看器嵌入代码会反映新的公司帐户名称。

配置Dynamic Media公司别名帐户时，请注意以下事项：

* 必须手动更新&#x200B;*live*&#x200B;数字资产上任何现有的Dynamic Media URL或查看器嵌入代码，以反映新的别名。 但是，任何包含您原始Dynamic Media公司名称的URL或查看器嵌入代码将继续适用于现有资源或新资源。
* Dynamic Media公司别名帐户功能仅限于Experience Manager Assets创作模式和交付。 公司别名不适用于Experience Manager Sites。 没有为此更改更新WCM （Web内容管理）组件。 这些组件将继续与获取Dynamic Media资源的原始Dynamic Media公司名称一起使用。
* 您只能在&#x200B;**[!UICONTROL 编辑Dynamic Media配置]**&#x200B;页面上设置一个公司别名帐户。 但是，您可以通过支持案例创建尽可能多的公司别名帐户，并在Dynamic Media URL或查看器嵌入代码中手动反映必要的别名。
* Dynamic Media的现成[缓存无效](/help/assets/invalidate-cdn-cache-dynamic-media.md)功能可以使在Cloud Service的Dynamic Media配置页面中配置的公司和公司别名帐户的URL失效。
* 当您在&#x200B;**[!UICONTROL 编辑Dynamic Media配置]**&#x200B;页面上配置公司别名帐户时，为了成功使缓存失效，您必须同时使&#x200B;**&#x200B; &#x200B;**&#x200B;[!UICONTROL 公司]&#x200B;**&#x200B;帐户和&#x200B;**&#x200B;[!UICONTROL 公司别名]**&#x200B;帐户的URL失效。

另请参阅[在Cloud Service中创建Dynamic Media配置](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)

## 配置Dynamic Media公司别名帐户 {#configure-dm-alias-account}

您首先要提交支持案例，以开始配置Dynamic Media公司别名帐户。 此步骤是必需的。

1. [使用该Admin Console创建支持案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)。
1. 在您的支持案例中提供以下信息：

   * 要使用的Dynamic Media公司别名。 名称必须只包含&#x200B;*个*&#x200B;字母（允许混合大小写）、数字、连字符和下划线。
   * 您的地区。
   * 以前是否使用任何[规则集](/help/assets/using-rulesets-to-transform-urls.md)通过备用Dynamic Media公司帐户名实现Dynamic Media内容服务。

1. 支持团队创建Dynamic Media别名帐户后，在as a Cloud ServiceExperience Manager创作实例中，选择Experience Manageras a Cloud Service徽标以访问全局导航控制台。
1. 在控制台左侧，选择“工具”图标，然后转到&#x200B;**[!UICONTROL Cloud Service> Dynamic Media配置]**。
1. 在“Dynamic Media配置浏览器”页面的左侧窗格中，选择&#x200B;**[!UICONTROL global]** （不要选择&#x200B;**[!UICONTROL global]**&#x200B;左侧的文件夹图标）。 然后选择&#x200B;**[!UICONTROL 编辑]**。

   ![Dynamic Media公司别名文本字段](/help/assets/assets-dm/dm-company-alias.png)

1. 在&#x200B;**[!UICONTROL 编辑Dynamic Media配置]**&#x200B;页面的&#x200B;**[!UICONTROL 公司别名]**&#x200B;文本字段中，键入您之前在支持案例中指定的Dynamic Media别名帐户名称。
1. 在页面的右上角，选择&#x200B;**[!UICONTROL 保存]**。
Dynamic Media公司别名帐户现已保存并启用；现有资源和新资源的所有URL和查看器嵌入代码现在都会反映新的公司别名。
