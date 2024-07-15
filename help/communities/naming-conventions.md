---
title: Java&amp；贸易；包名称中的命名约定
description: 了解命名惯例以及Java&amp；trade；包名称中连字符的使用。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 1%

---

# 命名约定 {#naming-conventions}

## Java™包名称中的连字符 {#hyphens-in-java-package-name}

在创建Java™类的位置时，包名称必须与存储库文件夹位置的名称匹配，并且路径中的所有连字符都应正确转义。

虽然在AEM开发中，建议在存储库项目的名称中使用连字符，但Java™包名称中的连字符非法。

基础CRX平台必须能够区分实际下划线`_ `和连字符`-`。 因此，在JCR中，连字符必须替换为其Unicode值(u002d)，并使用下划线`_`进行转义。

例如，如果存储库路径为&#x200B;**/apps/my-example/component/info/Info.java**，则包名称应为`java package apps.my_002dexample.component.info;`

请注意，下划线同样必须转义，这样`_`将变为`_005f`。
