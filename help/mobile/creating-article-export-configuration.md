---
title: 创建文章导出配置
description: 请参阅此页面，了解如何从Adobe Experience Manager (AEM)导出内容以供上传到AEM Mobile。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 5295f383-3b46-4456-9177-65de68e39a85
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# 创建文章导出配置{#creating-article-export-configuration}

{{ue-over-mobile}}

>[!CAUTION]
>
>**预修课程**：
>
>在了解如何创建和修改共享资源之前，请参阅[内容同步](/help/mobile/mobile-ondemand-contentsync.md)以了解基本概念。

AEM Mobile用户使用Content Sync将实时内容导出到静态内容以供在移动设备应用程序中使用，当内容从AEM Mobile上传到Mobile On-Demand Services时，会发生此导出。

上表中提到的属性&#x200B;***dps-exportTemplate***&#x200B;定义了应用程序导出配置的路径。 设置此属性以创建和修改共享资源。

以下资源介绍了如何从Adobe Experience Manager (AEM)导出内容以供上传到AEM Mobile。

文章包含需要导出和上传的内容。 这些内容中的一部分可在文章之间共享。

使用[ContentSync](/help/mobile/mobile-ondemand-contentsync.md)将内容收集在一起并创建&#x200B;***共享资源***&#x200B;包。

在&#x200B;**&lt;dps-exportTemplate>/dps-article>**&#x200B;处找到的ContentSync配置应配置为导出设备上属性静态呈现所需的全部内容和项目。

>[!CAUTION]
>
>只有在具备以下条件时，您才可以执行以下步骤来查看共享资源的示例：
>
>* 已安装示例内容
>* 运行AEM实例
>* 没有已配置的自定义上下文或其他端口
>

要查看共享资源的示例，请参阅以下步骤：

1. 在AEM服务器上打开CRXDE Lite。
1. 浏览到此路径[/etc/contentsync/templates/dps-we-unlimited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article)，以查看共享资源示例。

   您可以查看创建共享资源所需的所有属性，如下图所示：

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>当文章内容发生变化时，应将文章上传或导出到AEM Mobile On-demand Services。
