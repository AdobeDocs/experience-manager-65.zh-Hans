---
title: 组合PDF文档
description: 使用Assembler服务将多个PDF文档组合为一个PDF文档，或将一个PDF文档分解为多个PDF文档。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 991f5a4e-4752-4c0d-9926-de7e4855ecd1
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# 组合PDF文档 {#assembling-pdf-documents}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

**关于汇编程序服务**

组合器服务可以将多个PDF文档组合到一个PDF文档中，或将一个PDF文档分解到多个PDF文档中。 Assembler服务可以通过多种方式操作文档，例如更改页面大小和旋转内容。 它可以插入其他内容，如页眉、页脚和目录，并可以保留、导入或导出现有内容，如注释、文件附件和书签。

从LiveCycleES 8.0及更高版本开始，Assembler服务中提供了对PDF包的支持。

>[!NOTE]
>
>有关Assembler服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。
