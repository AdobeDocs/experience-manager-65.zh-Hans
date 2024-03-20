---
title: 在AEM sites页面中嵌入自适应表单或交互式通信
description: 您可以将自适应表单嵌入到AEM站点页面中。 用户无需离开网站页面即可填写和提交表单。
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author, interactive-communications
feature: Adaptive Forms, Foundation Components
exl-id: 00ee7929-649f-4cbb-be79-ba13ac73a16d
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 5%

---

# 在AEM sites页面中嵌入自适应表单或交互式通信 {#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-page}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/embed-adaptive-form-aem-sites.html) |
| AEM 6.5 | 本文 |


## 概述 {#overview}

AEM Forms允许表单开发人员将自适应表单和交互式通信无缝嵌入到AEM Sites页面或AEM外部托管的网页中。 嵌入式自适应表单和交互式通信功能完备，用户无需离开页面即可填写并提交表单。 它有助于用户停留在网页上其他元素的上下文中，同时与表单或交互式通信交互。

有关在外部网页中嵌入自适应表单的信息，请参阅 [在外部网页中嵌入自适应表单](/help/forms/using/embed-adaptive-form-external-web-page.md).

在AEM Sites页面中，您可以使用以下方式添加自适应表单或交互式通信：

* **[AEM Forms容器组件](/help/forms/using/embed-adaptive-form-aem-sites.md#af-component)**
AEM Forms提供了一个组件，您可以将该组件添加到网站页面。 AEM Forms容器组件允许您嵌入自适应表单和交互式通信。

* **[资产浏览器](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**
您创建的所有表单和交互式通信均可在Assets下使用。 您可以将表单作为资源拖放到页面上。

## 先决条件 {#prerequisites}

要在使用可编辑模板的AEM Sites页面中嵌入自适应表单或交互式通信，请确保在相关模板中将AEM表单组件配置为允许的组件。 有关更多信息，请参阅 **策略和属性（布局容器）** 中的部分 [创建页面模板](/help/sites-authoring/templates.md).

如果存在使用静态模板的站点页面，则需要在站点页面的段落系统中对其进行配置。 请参阅 [在设计模式下配置组件](/help/sites-authoring/default-components-designmode.md) 以了解更多信息。

## 嵌入自适应表单或交互式通信 {#af-component}

要使用AEM Forms容器组件嵌入自适应表单或交互式通信，请执行以下操作：

1. 在编辑模式下打开AEM sites页面，您要在该页面中嵌入自适应表单或交互式通信。
1. 从组件浏览器面板中，将AEM Forms容器组件拖放到页面上。

   或者，您可以在Assets浏览器中搜索自适应表单或交互式通信，并将其拖放到Sites页面上。 它将表单嵌入到AEM Forms容器中。

   >[!NOTE]
   >
   >不支持一个页面上的多个AEM Forms容器组件。

1. 在站点页面中选择嵌入的AEM Forms容器组件，然后选择 ![settings_icon](assets/settings_icon.png) 在操作栏上。 此 **[!UICONTROL 编辑AEM Forms容器]** 对话框打开。
1. 在编辑AEM Forms容器对话框中，指定以下内容。

   * **资源类型：** 选择要嵌入的资源类型。 选项包括自适应表单和交互式通信
   * **资产路径**：浏览并选择要嵌入的自适应表单或交互式通信。 如果您将其从资产浏览器中删除，则会自动填充该变量。
   * （仅限自适应表单） **帖子提交**：选择在表单提交时触发的操作。 您可以选择显示感谢消息或感谢页面。

      * **感谢信息**：使用富文本编辑器编写消息以在表单提交时显示。 仅当您选择显示感谢消息时，此选项才可用。
      * **感谢页面**：浏览并选择要在表单提交时显示的页面。 仅当您选择显示感谢页面时，此选项才可用。
      * **提交时刷新页面**：启用，以便您可以刷新包含嵌入的自适应表单的页面以显示感谢页面。 否则，“感谢”页面将替换AEM Forms容器中的自适应表单，而不刷新页面。 仅当您选择显示感谢页面时，此选项才可用。

   * **主题**：选择用于定义自适应表单或交互式通信组件样式的主题。 样式设置包括外观属性，如字体样式、背景颜色、尺寸和对齐方式。
   * **高度**：指定容器的高度。 将其留空可自动调整容器大小。
   * **CSS客户端库**：指定CSS客户端库的路径。

1. 保存设置。 自适应表单或交互式通信现在嵌入到页面中。

## 发布嵌入式自适应表单和交互式通信 {#publishing-embedded-adaptive-form-and-interactive-communication}

让我们考虑以下在AEM Sites页面中发布嵌入资产（自适应表单或交互式通信）的场景：

* 如果您是首次发布AEM站点页面，并且该页面包含嵌入的自适应表单或交互式通信，请发布站点页面和嵌入的资产。
* 如果在发布的站点页面中仅修改了嵌入的自适应表单或交互式通信，请发布原始资产，所做的更改会反映在发布的站点页面中。 已发布的站点页面包含对资产的引用，因此无需重新发布页面。
* 如果修改了站点页面和嵌入的自适应表单或交互式通信，请重新发布站点页面和嵌入的资产。

## 修改嵌入式自适应表单和交互式通信 {#modifying-embedded-adaptive-form-and-interactive-communication}

AEM sites页在AEM Forms容器中维护对自适应表单和交互式通信的引用。 因此，在原始自适应表单和交互式通信中配置的所有配置和属性（如主题、样式和提交操作）都保留在嵌入式自适应表单和交互式通信中。

要修改嵌入式自适应表单和交互式通信的任何配置或属性，请执行以下操作之一。

* 在相应编辑器中以自适应表单或交互式通信形式打开原始表单并进行修改。
* 在编辑模式下，从站点页面中选择自适应表单或交互式通信，然后选择 **[!UICONTROL 在新窗口中编辑]**. 原始表单在编辑模式下打开，您可以修改该模式。

>[!NOTE]
>
>在原始自适应表单或交互式通信中所做的更改会自动反映在嵌入表单中。 但是，重新发布自适应表单、交互式通信或站点页面，以反映已发布页面中的更改。

## 注意事项和最佳实践 {#considerations-and-best-practices}

在AEM Sites页面中嵌入自适应表单时，请牢记以下几点：

* 原始表单中的页眉和页脚未包含在嵌入表单中。
* 支持用户草稿和提交嵌入式表单，并且这些草稿和已提交的Forms选项卡位于Forms Portal上。
* 在原始表单上配置的提交操作将保留在嵌入表单中。
* 在原始表单上配置的体验定位和A/B测试在嵌入表单中不起作用。 但是，您可以使用站点页面上的体验定位，根据用户配置文件显示不同的表单。
* 如果您已为原始表单配置了Adobe Analytics，则会在Adobe Analytics中捕获嵌入表单的分析数据。 但是，它在Forms Analytics报表中不可用。
