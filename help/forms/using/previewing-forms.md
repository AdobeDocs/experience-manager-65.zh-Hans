---
title: 预览表单
description: 您可以在发布或激活表单之前预览表单，以确保表单符合预期。 预览选项可能因支持的表单类型而异。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
feature: Adaptive Forms,Foundation Components
exl-id: aed5703e-4fe6-4839-9657-c660ac48521e
solution: Experience Manager, Experience Manager Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 7da902b6-fe94-5180-8e7c-f6d1e38d01d5
    internal-label: Foundation Components
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
source-wordcount: '417'
ht-degree: 21%
---
# 预览表单 {#previewing-a-form}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。 这些组件代表了自适应表单创建方面的一大进步，可确保提供令人印象深刻的用户体验。 本文介绍了使用基础组件创作自适应表单的旧方法。</span>

## 概述 {#overview}

在AEM Forms中，您可以预览存储库中存在的表单和文档。 预览有助于了解表单在发布给最终用户时的具体外观和行为。

在预览表单时，它们会在交互式界面中呈现，用户可以用数据填充表单。 预览文档时，它们以非交互模式呈现，用户只能查看文档。 对于表单，还提供了自定义预览的附加选项。 使用此选项，您可以使用XML文件中的数据预览表单。 数据会填满正在预览的表单的部分或所有字段。

下表列出了适用于不同类型受支持表单的预览选项：

<table>
 <tbody>
  <tr>
   <td><strong>资源类型</strong><br /> </td>
   <td><strong>可用的预览选项</strong><br /> </td>
  </tr>
  <tr>
   <td>文档</td>
   <td>PDF 预览</td>
  </tr>
  <tr>
   <td>PDF 表单</td>
   <td>包含数据的PDF预览和预览<br /> </td>
  </tr>
  <tr>
   <td>自适应表单</td>
   <td>HTML预览和包含数据的HTML预览</td>
  </tr>
  <tr>
   <td>表单模板</td>
   <td>PDF预览、包含数据的PDF预览、HTML预览、包含数据的HTML预览<br /> </td>
  </tr>
 </tbody>
</table>

## 预览表单 {#previewing-a-form-1}

1. 选择要预览的资源，然后单击操作工具栏中的预览![aem6forms_preview](assets/aem6forms_preview.png)。

   >[!NOTE]
   >
   >要选择资产，请从默认信息卡视图切换到列表视图。 单击![aem6forms_viewlist](assets/aem6forms_viewlist.png)或![aem6forms_viewcard](assets/aem6forms_viewcard.png)以切换视图。

1. 单击预览会列出适用于所选资源类型的可能预览选项。 单击所需选项可在新选项卡中呈现所选资源。

   您的选项包括：

   * 作为 HTML 预览
   * 使用数据预览
   * 以PDF预览（适用于表单模板）

## 使用数据预览 {#preview-with-data}

当您选择&#x200B;**预览数据**&#x200B;时，您可以看到输入真实数据的表单的外观。 使用数据预览选项允许您上传包含示例用户数据的XML。 示例用户数据用于以您选择的格式填充预览表单。

1. 选择资源，单击预览![aem6forms_preview](assets/aem6forms_preview.png)，然后选择&#x200B;**使用数据预览**。
1. 在“预览表单”对话框中，将FormData作为XML文件提供。 单击预览以使用XML中的合并数据呈现表单。
