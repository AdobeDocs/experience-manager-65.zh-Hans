---
title: 添加附件
description: 在AEM Forms应用程序中将照片和涂鸦笔记作为批注添加到您的任务
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 82282e2d-63a1-47e9-b2ec-f50a4bd32bd3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# 添加附件{#adding-attachments}

## 在与AEM Forms Workflow Server (JEE上的AEM Forms)同步的表单中添加附件 {#adding-annotations}

通过AEM Forms应用程序，您可以将图像、手写笔记和文本注释附加到与AEM Forms JEE服务器同步的表单中。 如果表单是从AEM Forms Workflow服务器加载的，则附件会添加到表单中。 您可以选择附件按钮![attachments-app](assets/attachments-app.png)以一起查看表单中的所有附件。 红色通知指定表单中的附件数量。 如果表单中没有附件，您将看不到红色通知按钮。 如果表单中没有附件，则当您选择附件按钮![attch](assets/attch.png)时，您将获得附加照片或涂鸦的选项。

您的选项包括：

* **图片库**：允许您从设备上保存的图片中添加图片。

* **摄像头**：允许您拍摄照片并将其添加到表单中。

* **备注**：允许您添加涂鸦或文本备注。 使用![涂鸦](assets/scribble.png)添加涂鸦，使用![键盘](assets/keyboard.png)添加文本备注。

>[!NOTE]
>
>一个用户添加的附件可对其他AEM Forms应用程序用户可见。 其他用户无法删除用户添加的附件。
>

### “附件”屏幕 {#the-attachments-screen}

若要在一个位置查看所有附件，请选择![attachments-app](assets/attachments-app.png)。 您可以在此处添加、重命名和删除附件。

![一个位置中的所有附件](assets/attachments-screen.png)

您可以使用“附件”屏幕中的&#x200B;**+**&#x200B;按钮附加其他图片、涂鸦或文本。

### 添加照片 {#adding-a-photograph}

您可以使用移动设备的相机或设备中保存的图片在表单中附加图片。

1. 选择窗口底部的附件按钮![attch](assets/attch.png)。
1. 在显示的弹出窗口中选择&#x200B;**图库**&#x200B;或&#x200B;**摄像头**。
1. 根据您选择的选项，执行以下操作：

   1. 如果您选择&#x200B;**摄像头**。

      拍张照片。 然后选择&#x200B;**Use** ![use-pic](assets/use-pic.png)按钮。

      或者选择&#x200B;**Retake** ![retake](assets/retake.png)按钮以重新拍摄照片。

   1. 如果您选择&#x200B;**图库**。

      此时会弹出设备的图像浏览器。 在设备的图片浏览器中，选择要附加的图片。

### 添加注释 {#adding-a-note}

**注释**&#x200B;选项允许您在表单中添加手绘涂鸦和文本附件。

1. 选择窗口底部的附件按钮![attch](assets/attch.png)。
1. 在显示的弹出窗口中选择&#x200B;**注释**。
1. 在启动的Notes用户界面中，捕获手绘涂鸦。

   ![涂鸦界面](assets/scribble-ui.png)

   涂鸦

   您可以在Scribble界面中使用以下选项：

   * **清除**：清除屏幕。
   * **完成按钮**：附加当前涂鸦。
   * **取消按钮**：放弃当前涂写并退出涂写用户界面。
   * ![键盘](assets/keyboard.png)：清除涂写并允许添加文本注释。

   ![AEM Forms应用程序中的键盘涂鸦](assets/keyboard-inapp.png)

## 表单中的附件与不具有AEM Forms Workflow (OSGi上的AEM Forms)的AEM Forms服务器同步 {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

与AEM Forms OSGi服务器同步的移动表单附件与AEM Forms JEE服务器的工作方式类似。

从AEM Forms OSGi服务器加载到应用程序中的自适应表单不支持表单级附件。 要附加图像或文本注释，请在创作表单时启用表单中的字段级附件。 从组件浏览器中将文件附件组件拖放到字段上。

如果有自适应表单，您可以在记录文档(DoR)中查看附加文件。 请参阅[为非XFA自适应表单生成记录文档](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)。
