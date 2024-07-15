---
title: 通过Dynamic Media使内容交付网络缓存失效
description: 使CDN（内容分发网络）缓存的内容失效可让您快速更新Dynamic Media交付的资产，而不是等待缓存过期。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
feature: CDN Cache
exl-id: 23d3c274-0736-49f7-8d44-a56a55cfd06d
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1372'
ht-degree: 1%

---


# 通过 Dynamic Media 使 CDN 缓存失效 {#invalidating-cdn-cache-for-dm-assets}

Dynamic Media资产通过CDN（内容分发网络）进行缓存，以快速交付给客户。 但是，当您更新这些资产时，希望这些更改能够在您的网站上立即生效。 清除或使CDN缓存失效可让您快速更新Dynamic Media交付的资源。 您可以在Dynamic Media中发送请求，让缓存在几分钟内过期，而不是使用TTL（生存时间）值等待缓存过期（默认值为10小时）。



>[!IMPORTANT]
>
>以下步骤仅适用于Adobe Experience Manager 6.5、Service Pack 6(Experience Manager6.5.6)或更高版本中的Dynamic Media - Scene7模式。 此CDN失效功能还要求您使用与Adobe Experience Manager - Dynamic Media捆绑在一起的现成CDN。 此功能不支持任何其他自定义CDN。<br>如果您在Experience Manager6.5、Service Pack 5 (Experience Manager6.5.5)或更早版本中使用Dynamic Media，请按照[通过Dynamic Media Classic使CDN缓存失效](/help/assets/invalidate-cdn-cache-dm-classic.md)中提供的步骤操作。

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Caching overview in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**要使Dynamic Media资源的CDN缓存内容失效，请执行以下操作：**

*第1部分（共2部分）：创建CDN失效模板*

1. 在Experience Manager6.5.6或更高版本中，导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL CDN失效]**。

   ![CDN验证功能](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. 在&#x200B;**[!UICONTROL CDN失效模板]**&#x200B;页面上，根据您的方案执行以下选项之一：

   | 场景 | 选项 |
   | --- | --- |
   | 我以前使用Dynamic Media Classic创建过CDN失效模板。 | **[!UICONTROL 创建模板]**&#x200B;文本字段已预填充您的模板数据。 在这种情况下，您可以编辑模板或继续下一步骤。 |
   | 我必须创建一个模板。 我该输入什么？ | 在&#x200B;**[!UICONTROL 创建模板]**&#x200B;文本字段中，输入引用`<ID>`的图像URL（包括图像预设或修饰符），而不是以下示例中所述的特定图像ID：<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>如果模板仅包含`<ID>`，则Dynamic Media会填充`https://<publishserver_name>/is/image/<company_name>/<ID>`，其中`<publishserver_name>`是在Dynamic Media Classic的“常规设置”中定义的Publish服务器的名称。 `<company_name>`是与此Experience Manager实例关联的公司根的名称，而`<ID>`是通过资产选取器选定的要失效的资产。<br>在URL定义中按原样复制任何发布`<ID>`的预设/修饰符。<br>只能基于模板自动形成图像（即`/is/image`）。<br>对于`/is/content/`，使用资源选取器添加视频或PDF等资源不会自动生成URL。 而是必须在CDN失效模板中指定此类资源，或者可以在&#x200B;*第2部分（共2部分）：设置CDN失效选项*&#x200B;中手动将URL添加到此类资源。<br>**示例：**<br>&#x200B;在第一个示例中，失效模板包含`<ID>`以及具有`/is/content`的资产URL。 例如，`http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`。Dynamic Media基于此路径形成URL，`<ID>`是通过要失效的资源选取器选择的资源。<br>在第二个示例中，失效模板包含Web属性中使用的资产的完整URL，具有`/is/content`（不依赖于资产选取器）。 例如，`http://my.publishserver.com:8080/is/content/dms7snapshot/backpack`，其中背包是资产ID。<br>Dynamic Media支持的资源格式符合失效条件。 CDN失效不支持&#x200B;*的*&#x200B;资源文件类型包括PostScript®、封装式PostScript®、Adobe Illustrator、Adobe InDesign、Microsoft®Powerpoint、Microsoft®Excel、Microsoft®Word和富文本格式。<br><br>·创建模板时，请务必注意语法和拼写错误；Dynamic Media不执行任何模板验证。<br>· CDN失效模板最多可保存文本2500个字符。<br>·在此CDN失效模板中或在&#x200B;*第2部分：设置CDN失效选项的&#x200B;**[!UICONTROL 添加URL]**文本字段中指定图像智能裁剪的URL。*<br>· CDN失效模板中的每个条目必须位于其自己的行中。<br>·以下CDN失效模板示例仅用于演示目的。 |

   ![CDN失效模板 — 创建](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

   >[!NOTE]
   >
   >CDN失效模板最多可保存2500个字符的文本。

1. 在&#x200B;**[!UICONTROL CDN失效模板]**&#x200B;页面的右上角，选择&#x200B;**[!UICONTROL 保存]**，然后选择&#x200B;**[!UICONTROL 确定]**。<br>
   *第2部分（共2部分）：设置CDN失效选项*
   <br>

1. 在Experience Manageras a Cloud Service中，选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL CDN失效]**。

   ![CDN验证功能](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. 在&#x200B;**[!UICONTROL CDN失效 — 添加详细信息]**&#x200B;页面上，选择要使CDN失效的资产。

   ![CDN失效 — 添加详细信息](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >如果您决定取消选中&#x200B;**[!UICONTROL 使CDN中与资产关联的图像预设无效]** *和* **[!UICONTROL 基于模板无效]**&#x200B;选项，则所选资产的基本URL将构成无效。 仅对图像使用此选项排列。


   | 选项 | 描述 |
   | --- | --- |
   | **[!UICONTROL 使CDN中与图像预设相关联的资产失效]** | （可选）选中此选项时，会自动形成所选资产及其所有相关图像预设URL，以便使缓存失效。<br>Assets及其关联的预定义预设URL会自动形成以失效。 此选项仅适用于图像资产。 |
   | 基于模板&#x200B;**[!UICONTROL 失效]** | （可选）选中此选项可仅使用定义的模板来形成URL。 |
   | **[!UICONTROL 添加Assets]** | 使用资产选取器选择要使其失效的资产。 您可以选择已发布或已取消发布的资源。<br>CDN上的缓存基于URL，而不是基于资产。 因此，您必须了解您网站上的完整URL。 确定这些URL后，可以将其添加到模板中。 然后，您可以选择并添加这些资源，并在一个步骤中使URL失效。 <br>使用此选项可以使&#x200B;**[!UICONTROL 使CDN中与资产关联的图像预设失效]**，或使&#x200B;**[!UICONTROL 基于模板失效]**，或同时使两者失效。 |
   | **[!UICONTROL 添加URL]** | 手动将完整URL路径添加或粘贴到要使CDN缓存失效的Dynamic Media资源。 如果您未在&#x200B;***第1部分（共2部分）：创建CDN失效模板***&#x200B;中创建CDN失效模板，并且只有少数资产要失效，请使用此选项。<br>**重要信息：**&#x200B;您添加的每个URL都必须位于其自己的行中。<br>您一次最多可以使1000个URL失效。 如果&#x200B;**[!UICONTROL 添加URL]**&#x200B;文本字段中的URL数大于1000，则无法选择&#x200B;**[!UICONTROL 下一步]**。 在这种情况下，您必须选择选定资产右侧的&#x200B;**[!UICONTROL X]**&#x200B;或手动添加的URL以将其从失效列表中删除。<br>在CDN失效模板或此&#x200B;**[!UICONTROL 添加URL]**&#x200B;文本字段中指定图像智能裁剪的URL。 |

1. 在页面的右上角附近，选择&#x200B;**[!UICONTROL 下一步]**。
1. 在&#x200B;**[!UICONTROL CDN失效 — 确认]**&#x200B;页面的&#x200B;**[!UICONTROL URL]**&#x200B;列表框中，您可以看到一个列表，其中包含从您之前创建的CDN失效模板生成的一个或多个URL以及您刚刚添加的资产。

   例如，使用前面步骤中显示的CDN失效模板示例，假设您添加了一个名为`spinset`的资产。 当您导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL CDN失效]**&#x200B;时，会在&#x200B;**[!UICONTROL CDN失效 — 确认]**&#x200B;用户界面中生成以下五个URL：

   ![CDN失效 — 确认](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   如有必要，请选择URL右侧的&#x200B;**X**&#x200B;以将其从失效进程中删除。

1. 在页面的右上角附近，选择&#x200B;**[!UICONTROL 提交]**&#x200B;以开始CDN失效进程。

## CDN失效错误疑难解答

在所有情况下，要么处理整个批次使其失效，要么整个批次失败。

| 错误 | 解释 |
| --- | --- |
| *无法检索选定资源的URL。* | 如果满足以下任一方案，则会发生：<br> — 未找到Dynamic Media配置。<br> — 检索用于读取Dynamic Media配置的服务用户时出现异常。<br>- Dynamic Media配置中缺少用于构成URL的Publish服务器或公司根目录。 |
| *某些URL未正确定义。 更正并重新提交。* | 如果IPS CDN缓存失效API返回错误URL引用了其他公司，则会发生。 或者，如果URL根据IPS `cdnCacheInvalidation` API完成的验证无效。 |
| *无法使CDN缓存失效。* | 在CDN缓存失效请求由于任何其他原因而失败时发生。 |
| *没有输入要失效的URL。* | 如果&#x200B;**[!UICONTROL CDN失效 — 确认]**&#x200B;页面中没有URL，并且您选择&#x200B;**[!UICONTROL 提交]**，则会发生这种情况。 |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, select **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
