---
title: 收藏集、代码片段和代码片段模板的多租户
description: 了解多租户功能如何让您根据客户组织分离CRX存储库中的内容，以防止未经授权的访问。
contentOwner: AG
role: Architect, Admin, Leader
feature: Collections
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# 收藏集、代码片段和代码片段模板的多租户 {#multi-tenancy-for-collections-snippets-and-snippet-templates}

通过多租户功能，您可以根据组织前缀和组织ID在CRX中分隔内容，以防其他组织的用户未经授权访问内容。

[!DNL Adobe Experience Manager Assets]以不同的路径存储每个组织的数据。 每个特定于组织的路径由组织前缀和组织ID标识
这些资源包括在传统位置，在CRX中存储不同类型的资源。

例如，如果您创建名为`Demo`的文件夹，[!DNL Experience Manager]资源通常将该文件夹存储在`../content/dam/Demo`中。 启用多租户后，您现在可以在`../content/dam/<organization prefix>/<organization id>Demo`处存储数据

例如，如果对于分配给`aodpremium`组织的[!DNL Assets]的[!DNL Adobe Marketing Cloud]用户（按需），您可以使用多租户功能配置`../content/dam/<mac>/<aodpremium>Demo`路径以分离其内容。 在此示例中，`mac`是组织前缀，`aodpremium`是组织ID。

根据用户的组织和ID，此限定路径将显示在[!DNL Assets]界面和各种向导中，包括用于强制实施隔离的移动和代码片段创建向导。

多租户功能允许您分隔以下类型的资源和组件：

* 收藏集
* 公共收藏集
* 目录（包括“添加/选择页面”向导）
* 模板
* 代码片段模板
* 灯箱
