---
title: 为HTML5表单设计表单模板
seo-title: Designing form templates for HTML5 forms
description: AEM Forms提供将XFA表单模板渲染为HTML5格式。 表单设计人员可以使用Designer设计表单模板，并使用HTML5呈现功能。
seo-description: AEM Forms offers rendering XFA form template to HTML5 format. Form designers can design form templates using Designer and use the HTML5 rendition capability.
uuid: 4f6b7231-4479-400a-adcd-c68064f06b4e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f2e9dbe4-e210-41f3-8878-2fc4d166e63c
docset: aem65
feature: Mobile Forms
exl-id: 7c8d501f-c953-495e-8bac-1f66fd99c783
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# 为HTML5表单设计表单模板{#designing-form-templates-for-html-forms}

AEM中的HTML5表单组件提供将XFA表单模板渲染为HTML5格式。 表单设计人员可以使用 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63) 并使用“HTML5”演绎版功能。 这些表单模板及其资产可以驻留在AEM存储库、文件系统中，或通过http公开。 但是，如果您计划使用Forms Manager管理表单，则模板和资产应位于AEM存储库中。

尽管HTML5表单在很大程度上与PDF forms的行为匹配，但两种格式中有一些功能不适用于其他格式。 例如，在Adobe Reader中，条形码如何应用于PDF表单会因移动设备表单而异，或者表单的数字签名方式也因格式而异。 有关此类变体的更多信息，请参阅 [HTML5表单和PDF forms之间的功能区别](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

有关XFA的常见功能，请参阅以下最佳实践和准则以设计可同时使用这两种格式的表单。

## 最佳实践 {#best-practices}

设计表单模板（如架构绑定或编写表单逻辑）的大多数步骤都是相同的。 但是，由于Adobe Reader等粗客户端的呈现和脚本引擎与基于浏览器的表单等客户端的呈现和脚本引擎之间存在内在差异，因此在 [最佳实践](/help/forms/using/design-accessible-html5-forms.md) 文章。 这些最佳实践可帮助您设计可在这两种格式中按预期工作的表单模板。

### AEM Forms Designer中用于HTML5 Forms的功能 {#capabilities-in-aem-forms-designer-for-html-forms}

#### 预览HTML {#preview-html}

“预览”HTML选项卡在“设计”模式下添加，以便表单设计人员在设计过程中以HTML5格式预览表单。 有关如何在AEM Forms Designer中启用和配置此功能的更多信息，请参阅 [预览HTML](../../forms/using/preview-xdp-forms-html.md).

#### 连笔签名 {#scribble-signature}

HTML5表单的关键目标是触控设备。 因此，在AEM Forms Designer中添加了新的涂写签名控件。 您可以单击或拖放表单模板上的潦草签名控件并对其进行配置。 它在HTML5呈现中呈现为涂写字段，可用于在触屏设备上涂写签名。 在台式机上，它可用作使用鼠标控件的涂写字段。 有关如何使用此功能的更多信息，请参阅 [XFA Scribble字段](../../forms/using/scribble-signature.md).

![4](assets/4.png)

#### 富文本格式 {#rich-text-format}

您可以将文本字段转换为富文本字段。 它会向文本字段添加一系列格式选项。 要进行转换，请打开Forms Designer，点按 **[!UICONTROL 设计视图]**. 在 **[!UICONTROL 字段]** 选项卡，选择 **[!UICONTROL 富文本]** 从 **[!UICONTROL 字段格式]** 下拉列表。 现在，当XFA表单呈现为HTML5表单时，该字段将呈现为富文本字段。 点按 ![最大化](assets/maximize_icon.svg) 查看其他格式选项。
