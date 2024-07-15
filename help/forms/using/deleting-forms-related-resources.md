---
title: 删除表单和相关资源
description: 如何删除AEM Forms中的表单或资源，及其对引用的和反向链接资源以及XFA表单的影响。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
role: Admin,User
exl-id: b31f9f56-dd33-4478-ad34-01ac7d5a1b40
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# 删除表单和相关资源 {#deleting-forms-and-related-resources}

您可以删除表单和资源，以从存储库中删除这些资源。 删除操作适用于所有资源类型和文件夹。

如果您从创作实例中删除某个资源，则该资源也会从Publish实例中删除。 AEM Forms服务器由创作实例和Publish实例组成。 创作实例用于创建和管理表单资源和资源。 Publish实例包含可供最终用户使用的已发布的表单资源和相关资源。

## 如何删除表单 {#how-to-delete-a-form}

1. 通过访问`https://[hostname]:'port'/aem/forms.html.`登录到AEM Forms用户界面
1. 导航到要删除的表单并选择它。 单击工具栏中的删除![aem6forms_delete2](assets/aem6forms_delete2.png)并确认删除操作。

   >[!NOTE]
   >
   >一次只能删除一个表单。 分别删除多个表单或删除父文件夹。

1. 在删除资源之前，AEM Forms会检查引用并请求明确确认。 如果要删除资产，而不考虑关系状态，请单击强制删除。

   >[!NOTE]
   >
   >删除其他资产引用的资产可能会导致功能问题。

   >[!NOTE]
   >
   >如果所选资源是一个文件夹，并且其层次结构中包含此类资源，请单独删除其他资源或删除整个文件夹。

## 删除引用的XFA表单的影响 {#impact-of-deleting-a-referenced-xfa-form}

在AEM Forms中，XFA表单模板可由自适应表单或其他XFA表单模板引用。 此外，模板可以引用资源或其他XFA模板。

不建议删除自适应表单引用的XFA表单，因为它可能会损坏自适应表单。 当自适应表单引用XFA表单时，其字段会被绑定。 删除XFA后，自适应表单无法将其字段与XFA字段同步，并显示此类字段的错误消息。 要了解有关引用的XFA删除的影响以及脏的AF的更多信息，请参阅[更新引用的XFA表单](/help/forms/using/get-xdp-pdf-documents-aem.md#p-updating-referenced-xfa-forms-p)。

要删除此类XFA表单，请更新自适应表单并删除与XFA字段的绑定。
