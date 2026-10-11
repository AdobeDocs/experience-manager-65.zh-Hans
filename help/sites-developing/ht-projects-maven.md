---
title: 如何使用 Apache Maven 构建 AEM 项目
description: 本文档介绍了如何设置基于Apache Maven的AEM项目
exl-id: 451913bf-bb1e-4444-aee5-968ac30b5c9d
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 24%
---
# 如何使用 Apache Maven 构建 AEM 项目 {#how-to-build-aem-projects-using-apache-maven}

AEM 6.5遵循有关包管理和项目结构的最新最佳实践，这些实践由适用于本地和AMS实施的最新AEM项目原型实施。

>[!TIP]
>
>有关更多详细信息，请参阅：
>
>* AEM as a Cloud Service文档中的[AEM项目结构](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=zh-Hans)一文，介绍了如何构建现代AEM项目。
>* 有关如何使用原型启动新的AEM项目的[AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hans)文档。
>* 有关如何部署Adobe应用程序的AEM as a Cloud Service文档中的[AEM内容包Maven插件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developer-tools/maven-plugin.html?lang=zh-Hans#developer-tools)文章。
>
>所有三个文档都适用于AEM 6.5。
