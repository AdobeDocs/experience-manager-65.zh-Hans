---
title: 在 AEM Forms 工作区中使用表单集
description: 表单集是HTML5表单的集合，这些表单经过分组，作为一组表单提供给最终用户。 了解如何在AEM Forms工作区中使用表单集。
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 76a8f93f-eb8a-4e68-8626-efa6dc67668f
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
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
source-wordcount: '347'
ht-degree: 7%
---
# 在 AEM Forms 工作区中使用表单集{#working-with-formsets-in-aem-forms-workspace}

表单集是HTML5表单的集合，这些表单经过分组，作为一组表单提供给最终用户。 当最终用户开始填写表单集时，他们会无缝地从一个表单转换为另一个表单。 然后，只需一次单击即可提交表单集。 有关表单集以及如何设置表单集的详细信息，请参阅AEM Forms中的[表单集](../../forms/using/formset-in-aem-forms.md)。

AEM Forms工作区支持表单集。 使用表单集，可以分组与服务或流程相关的多个表单以自动化业务流程并向最终用户呈现。 在这样的场景中，用户可以作为一个整体填写整个集合，而无需文件、提交和跟踪单个表单或进程。

## 将表单集附加到AEM Forms工作区应用程序中的起点 {#attaching-a-formset-to-startpoint-in-an-aem-forms-workspace-app-br}

1. 在Workbench中创建业务流程工作流。 有关详细信息，请参阅[Workbench帮助](https://www.adobe.com/go/learn_aemforms_workbench_63)。
1. 从起点的进程属性中，选择&#x200B;**在演示文稿和数据中使用CRX资源**。

   ![1-3](assets/1-3.png)

1. 单击CRX资源路径旁边的![浏览](assets/browse.png) （浏览）。 此时会显示选择表单资源对话框。

   ![2-1](assets/2-1.png)

1. 单击&#x200B;**表单集**&#x200B;选项卡，从列表中选择相关的表单集，然后单击&#x200B;**确定**。

1. 在更新其他相关进程属性之后部署应用程序。

## 使用AEM Forms工作区中的表单集 {#using-formset-in-nbsp-aem-forms-workspace}

将表单集附加到起点后，就可以在AEM Forms工作区中调用该起点，就像调用任何其他起点一样。

通过AEM Forms工作区对表单集支持的操作包括：

* 另存为草稿
* 锁定
* 放弃
* 提交
* 添加附件
* 添加注释
* 使用“上一步”或“下一步”按钮在表单集中的表单之间移动

![3-1](assets/3-1.png)

>[!NOTE]
>
>为了在表单集中从上一个和下一个表单移动期间提高性能，在相关表单完全呈现之前，将禁用所有工作区按钮(“返回”、“下一个”、“保存”、“提交”和…… （更多）)。
