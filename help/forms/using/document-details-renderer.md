---
title: 呈现器的文档详细信息
description: 有关渲染如何在AEM Forms工作区中用于渲染各种受支持表单和文件类型的概念信息。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 946f0f6d-86af-41c1-98ef-98c8f5566e95
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---

# 呈现器的文档详细信息 {#document-details-for-renderer}

## 简介 {#introduction}

在AEM Forms工作区中，无缝支持多种表单类型。 其中包括：

* PDF forms(XDP/Acroform/平面PDF)
* 新HTML表单
* 图像
* 第三方应用程序（例如，通信管理）

本文档从语义定制/组件重用的角度解释这些呈现器的工作，以便在不中断任何呈现的情况下满足客户需求。 虽然AEM Forms工作区允许进行任何用户界面/语义更改，但建议不更改各种表单类型的渲染逻辑，否则结果可能是不可预测的。 本文档旨在提供指导/知识以支持呈现相同的表单、在不同门户中使用相同的工作区组件，而不是用于修改呈现逻辑本身。

## PDF forms {#pdf-forms}

PDF forms由`PdfTaskForm View`呈现。

将XDP表单渲染为PDF时，FormsAugmenter服务会添加`FormBridge`JavaScript™。 此JavaScript™(在PDF表单内)有助于执行表单提交、表单保存或离线表单等操作。

在AEM Forms工作区中，PDFTaskForm视图通过位于`/lc/libs/ws/libs/ws/pdf.html`的中间HTML与`FormBridge`JavaScript进行通信。 其流程为：

**PDFTaskForm视图 — pdf.html**

使用`window.postMessage` / `window.attachEvent('message')`进行通信

此方法是父帧和iframe之间的标准通信方式。 在添加新事件侦听器之前，将删除以前打开的PDF forms中的现有事件侦听器。 此清除还会考虑在任务详细信息视图中的表单选项卡和历史记录选项卡之间进行切换。

在渲染的PDF中&#x200B;**pdf.html - `FormBridge`JavaScript**

使用`pdfObject.postMessage` / `pdfObject.messageHandler`进行通信

此方法是HTML与PDFJavaScript进行通信的标准方式。 PdfTaskForm视图还会处理平面PDF并将其呈现。

>[!NOTE]
>
>不建议编辑PdfTaskForm视图的pdf.html /内容。

## 新HTMLForms {#new-html-forms}

新的HTML表单由NewHTMLTaskForm视图渲染。

当使用部署在CRX上的移动表单包以HTML形式呈现XDP表单时，它还会向表单添加其他`FormBridge`JavaScript，这会公开不同的保存和提交表单数据方法。

此JavaScript与上述PDF forms中提到的版本不同，但其用途相似。

>[!NOTE]
>
>Adobe不建议编辑NewHTMLTaskForm视图的内容。

## Flex Forms和指南 {#flex-forms-and-guides}

Flex Forms由SwfTaskForm渲染，参考线由HtmlTaskForm视图渲染。

在AEM Forms工作区中，这些视图使用位于`/lc/libs/ws/libs/ws/WSNextAdapter.swf`的中间SWF与构成Flex®表单/指南的实际SWF进行通信

使用`swfObject.postMessage` / `window.flexMessageHandler`进行通信。

此协议由`WsNextAdapter.swf`定义。 在添加新窗口对象之前，将删除以前打开的SWF表单中的现有`flexMessageHandlers`。 该逻辑还会考虑在任务详细信息视图中的表单选项卡和历史记录选项卡之间进行切换。 `WsNextAdapter.swf`用于执行各种表单操作，如保存或提交。

>[!NOTE]
>
>建议不要修改`WSNextAdapter.swf`或SwfTaskForm / HtmlTaskForm视图的内容。

## 第三方应用程序（例如，通信管理） {#third-party-applications-for-example-correspondence-management}

使用ExtAppTaskForm视图呈现第三方应用程序。

**第三方应用程序到AEM Forms工作区通信**

AEM Forms工作区监听`window.global.postMessage([Message],[Payload])`

[消息]可以是指定为`SubmitMessage`的字符串| `CancelMessage`| `ErrorMessage`| `runtimeMap`中的`actionEnabledMessage`。 第三方应用程序必须使用此界面来根据需要通知AEM Forms工作区。 必须使用此界面，因为AEM Forms工作区必须知道在提交任务时，它才能清除任务窗口。

**AEM Forms工作区到第三方应用程序通信**

如果AEM Forms工作区的直接操作按钮可见，则它会调用`window.[External-App-Name].getMessage([Action])`，其中从`routeActionMap`读取`[Action]`。 第三方应用程序必须侦听此接口，然后通过`postMessage ()` API通知AEM Forms工作区。

例如，Flex应用程序可以定义`ExternalInterface.addCallback('getMessage', listener)`来支持此通信。 如果第三方应用程序希望通过自己的按钮处理表单提交，则您应该指定`hideDirectActions = true() in the runtimeMap`，并且可以跳过此侦听器。 因此，此结构是可选的。

您可以在[在AEM Forms工作区中集成通信管理](/help/forms/using/integrating-correspondence-management-html-workspace.md)中阅读有关通信管理的第三方应用程序集成的更多信息。
