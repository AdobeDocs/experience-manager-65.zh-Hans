---
title: 向AEM 6.5自适应表单添加版本控制、注释和批注。
description: 使用AEM 6.5自适应表单核心组件向自适应表单添加注释、批注和版本控制。
feature: Adaptive Forms, Core Components
role: User, Developer, Admin
exl-id: 91e6fca2-60ba-45f1-98c3-7b3fb1d762f5
source-git-commit: 94a9f4087e36bfe5701ad9aafd4e8446ca643ddf
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# 对自适应表单进行版本控制、审核和注释

<!--
<span class="preview"> This feature is under the early adopter program. If you’re interested in joining our early access program for this feature, send an email from your official address to aem-forms-ea@adobe.com to request access </span>
-->

<span class="preview">默认情况下不启用此功能。 您可以从官方地址写信到aem-forms-ea@adobe.com请求访问该功能。</span>

自适应表单核心组件允许表单作者向表单添加版本控制、注释和批注。 这些功能通过允许用户创建和管理多个版本、通过注释进行协作以及向特定表单部分添加注释来简化表单开发，从而增强表单构建体验。

## 先决条件 {#prerequisite-versioning}

要在自适应表单中使用版本控制、注释和批注功能，请确保在AEM 6.5 Forms环境中启用了[自适应表单核心组件](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-core-components/enable-adaptive-forms-core-components)。

## 自适应表单版本控制 {#adaptive-form-versioning}

自适应表单版本控制有助于向表单添加版本。 表单作者可以轻松创建表单的多个版本，并最终使用适合业务目标的版本。 此外，表单用户也可以将表单还原到以前的版本。 它还可以帮助作者通过预览表单来比较表单的任意两个版本，使他们能够更好地从UI角度分析表单。 让我们详细了解每个自适应表单版本控制功能：

### 创建表单版本 {#create-a-form-version}

要创建表单的版本，请执行以下步骤：

1. 在您的AEM Forms环境中，导航到&#x200B;**[!UICONTROL 表单]**>**[!UICONTROL Forms和文档]**，然后选择您的&#x200B;**表单**。
1. 从左侧面板上的选择下拉列表中，选择&#x200B;**[!UICONTROL 版本]**。
   ![选择表单](assets/select-a-form.png)
1. 单击左下方面板上的&#x200B;**三个圆点**，然后单击&#x200B;**[!UICONTROL 另存为版本]**。
1. 为表单版本提供标签，您还可以通过注释添加有关表单的信息。
   ![创建表单版本](assets/create-a-form-version.png)

### 更新表单版本 {#update-a-form-version}

编辑并更新表单后，即可将新版本添加到表单。 按照上一节中给出的步骤命名该表单的新版本，如图所示：

![更新表单版本](assets/update-a-form-version.png)

### 还原表单版本 {#revert-a-form-version}

若要将表单版本还原到之前的版本，请选择一个表单版本，然后单击&#x200B;**[!UICONTROL 还原到此版本]**。

![还原表单版本](assets/revert-form-version.png)

### 比较表单版本 {#compare-form-versions}

表单作者可以比较表单的两个不同版本以进行预览。 要比较版本，请选择任意表单版本，然后单击&#x200B;**[!UICONTROL 与当前比较]**。 它在预览模式下显示两个不同的表单版本。

![比较表单版本](assets/compare-form-versions.png)

## 添加评论 {#add-comments}

审阅是一种允许一个或多个审阅人对表单进行评论的机制。 任何表单用户均可对表单进行注释或通过注释审阅表单。 若要评论表单，请选择&#x200B;**[!UICONTROL 表单]**，然后向表单添加&#x200B;**[!UICONTROL 评论]**。

>[!NOTE]
> 如上所述，在自适应表单核心组件中使用注释时，表单功能[向表单添加审阅者](/help/forms/using/create-reviews-forms.md)被禁用。


![在表单上添加评论](assets/form-comments.png)

## 添加注释 {#adaptive-form-annotations}

在许多情况下，表单组用户需要向表单添加注释以进行审阅，例如在特定的选项卡或表单组件上。 在这种情况下，作者可以使用注释。
要将注释添加到表单，请执行以下步骤：

1. 以&#x200B;**[!UICONTROL 编辑]**&#x200B;模式打开表单。

1. 单击位于右上边栏的&#x200B;**添加图标**（如图像中所示）。
   ![批注](assets/annotation.png)

1. 现在，单击位于左上边栏的&#x200B;**添加图标**&#x200B;以添加批注。
   ![添加批注](assets/add-annotation.png)

1. 现在，您可以添加注释，用多种颜色绘制草图以形成组件。

1. 要查看您在表单中添加的所有注释，请选择您的表单，然后您会看到在左侧面板中添加了注释，如图像所示。

   ![查看已添加批注](assets/see-annotations.png)

## 另请参阅

* [比较自适应Forms核心组件](/help/forms/using/compare-forms-core-components.md)
