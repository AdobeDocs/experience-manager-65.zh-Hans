---
title: Java&trade；包名称中的命名约定
description: 了解命名惯例以及Java&trade；包名称中连字符的使用。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
solution: Experience Manager
feature: Communities
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 1%
---
# 命名惯例 {#naming-conventions}

## Java™包名称中的连字符 {#hyphens-in-java-package-name}

在创建Java™类的位置时，包名称必须与存储库文件夹位置的名称匹配，并且路径中的所有连字符都应正确转义。

虽然在AEM开发中，建议在存储库项目的名称中使用连字符，但Java™包名称中的连字符非法。

基础CRX平台必须能够区分实际下划线`_ `和连字符`-`。 因此，在JCR中，连字符必须替换为其Unicode值(u002d)，并使用下划线`_`进行转义。

例如，如果存储库路径为&#x200B;**/apps/my-example/component/info/Info.java**，则包名称应为`java package apps.my_002dexample.component.info;`

请注意，下划线同样必须转义，这样`_`将变为`_005f`。
