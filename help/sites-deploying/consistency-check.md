---
title: 一致性与遍历检查
description: 了解如何执行一致性和遍历检查。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
feature: Configuring
exl-id: 10dde29b-5dc7-4d4e-80ae-3d4fd0397f7e
solution: Experience Manager, Experience Manager Sites
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 523b1ccd-901e-5e3b-9fa7-f3dfd82463d5
    internal-label: Configuring
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 6%
---
# 一致性与遍历检查{#consistency-and-traversal-checks}

升级时，可能会由于工作区不一致而出现问题。 您可以运行测试升级以查看这是否是问题，也可以将一致性检查作为预防性操作运行。

如果运行因工作区不一致而失败的测试升级，则会在crx-quickstart/logs/crx/error.log中看到与以下内容类似的条目：

```xml
*ERROR* TarPersistenceManager: No bundle found for uuid 'deadbeef-cafe-babe-cafe-babecafebabe'
 ...
*ERROR* RepositoryImpl: Failed to initialize workspace 'crx.default'
javax.jcr.RepositoryException: Error indexing workspace: Error indexing workspace: Error indexing workspace
...
```

## 执行一致性检查 {#perform-a-consistency-check}

要执行一致性检查，请导航到JMX Mbean **com.adobe.granite （存储库）**&#x200B;的管理页面。 从AEM主屏幕，转到：

**工具> Web控制台> Main（位于菜单栏上）> JMX > com.adobe.granite（存储库）**

在默认安装中，可在此处找到它： **[|显示给我|](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

在该页的&#x200B;**操作**&#x200B;部分中，您找到两种方法： **`traversalCheck`**&#x200B;和&#x200B;**`consistencyCheck`**。 要运行检查，请单击操作并输入所需的参数。

![chlimage_1-117](assets/chlimage_1-117.png)
