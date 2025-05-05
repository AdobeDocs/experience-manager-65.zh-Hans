---
title: 管理收藏集
description: 收藏表示一个定义良好的存储段，其中填充了适合封面主题的文章或横幅等内容。 关注此页面以了解更多信息。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: 0b4aa1a4-449a-4882-8f7c-3ceea6ac7f83
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# 管理收藏集{#managing-collections}

{{ue-over-mobile}}

内容管理操作是构建块，有助于在应用程序中创建和管理内容。 对应用程序中的内容执行以下操作。

## 收藏集概述 {#collections-overview}

收藏集表示一个明确定义的&#x200B;*存储桶*，其中包含适合封面主题的文章或横幅等内容。

>[!NOTE]
>
>请参阅联机帮助中的以下资源，以了解AEM Mobile应用程序中的以下主题：
>
>* [设计注意事项](https://helpx.adobe.com/cn/digital-publishing-solution/help/design-app.html)
>
>* [管理收藏集](https://helpx.adobe.com/cn/digital-publishing-solution/help/creating-collections.html)
>

## 创建收藏集 {#creating-a-collection}

创建收藏集的常规工作流如下所示：

1. 从侧边栏中选择&#x200B;**移动设备**。
1. 在Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 单击&#x200B;**管理收藏集**&#x200B;拼贴右上角的向下箭头。
1. 完成向导的每个步骤以继续创建新文章。
1. 准备就绪后，单击&#x200B;**创建**。
1. 您的新文章出现在&#x200B;**管理收藏集**&#x200B;拼贴中。

![chlimage_1-1](assets/chlimage_1-1.gif)

## 导入新收藏集 {#importing-a-new-collection}

现有Mobile On-Demand内容可以从Mobile On-Demand下载（导入）到AEM。 这允许编辑和查看本地内容。

>[!NOTE]
>
>导入不包括图像。

用于导入新收藏集的工作流

1. 在Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 单击&#x200B;**管理收藏集**&#x200B;拼贴右上角的向下箭头，然后选择“导入收藏集”。
1. 单击对话框中的&#x200B;**导入收藏集**，然后关闭。
1. 您的Mobile On-Demand收藏集现在显示在&#x200B;**管理收藏集**&#x200B;拼贴中。

>[!CAUTION]
>
>首先关联Mobile On-Demand连接。

## 编辑收藏集 {#editing-a-collection}

使用内置的AEM拖放编辑器添加或更改文章。 可以添加/删除文本和图像等组件。 可以插入DAM Assets中的图像。

用于编辑收藏集的工作流：

1. 在Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 从&#x200B;**管理收藏集**&#x200B;拼贴中选择源自AEM的文章。
1. 从列表视图中单击高亮显示的收藏集，以在内容编辑器中打开它。
1. 使用内容编辑器拖动收藏集内容（手稿、图像、文本等）。

### 查看和编辑收藏集中的元数据 {#viewing-and-editing-the-metadata-within-a-collection}

收藏集具有许多属性，例如标题、描述和图像。 此操作用于查看和修改此类属性。 或者，这些更改可以在保存时上传到Mobile On-Demand。

查看/编辑收藏集的常规工作流：

1. 在Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 从&#x200B;**管理收藏集**&#x200B;拼贴中选择收藏集。

1. 从操作栏中选择&#x200B;**属性**。
1. 查看该文章的所有可用元数据。
1. 如果需要，编辑元数据，完成后单击&#x200B;**保存**。
1. （可选）将更改立即上载到Mobile On-Demand。

## 上传收藏集 {#uploading-a-collection}

上传操作会复制所选内容并将其添加到Mobile On-Demand项目。 现有的Mobile On-Demand内容将由新版本替换。

上传收藏集的常规工作流：

1. 从&#x200B;**Mobile**&#x200B;中，从目录中选择您的Mobile On-Demand应用程序。
1. 在&#x200B;**管理收藏集**&#x200B;拼贴中，选择要上传到Mobile On-Demand的文章。
1. 如果需要，可从列表视图添加更多收藏集。
1. 从操作栏中选择&#x200B;**上传**，然后在对话框中单击“上传”。
1. 您的收藏集现已上传至Mobile On-Demand。

## 删除收藏集 {#deleting-a-collection}

此操作会从Mobile On-Demand和（可选）本地AEM实例中删除所选集合。

用于删除收藏集的常规工作流：

1. 在Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 在&#x200B;**管理收藏集**&#x200B;拼贴中选择要删除的文章。
1. 确保在列表中选中它；根据需要选择要删除的其他项。
1. 单击操作栏中的&#x200B;**删除**。
1. 检查是否要从AEM和Mobile On-Demand中删除。
1. 单击&#x200B;**删除**。
1. 您的收藏集现已从列表中删除。

## 将内容添加到收藏集 {#adding-content-to-collections}

收藏集本质上是一类相关内容。 它们将文章、横幅等内容收集到定义应用程序导航结构的包中。 收藏集可嵌套。

>[!NOTE]
>
>在将内容添加到收藏集之前，必须将其上传到Mobile On-Demand。

收藏集本质上是一类相关内容：它们将文章、横幅等内容收集到一起，成为定义应用程序导航结构的包。 收藏集可嵌套。

1. 在Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 选择之前上传的文章（或横幅/收藏集）
1. 从操作栏中选择“添加到”。
1. 从对话框中选择之前上传的收藏集。
1. 单击&#x200B;**更新**&#x200B;将内容添加到收藏集。

![chlimage_1-2](assets/chlimage_1-2.gif)

### 后续步骤 {#the-next-steps}

有关管理收藏集的详情，请参阅

* [管理横幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [上传共享资源](/help/mobile/mobile-on-demand-shared-resources.md)
* [发布/取消发布内容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用Preflight预览](/help/mobile/aem-mobile-manage-ondemand-services.md)
