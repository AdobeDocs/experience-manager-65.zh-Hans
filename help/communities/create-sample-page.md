---
title: 创建示例页面
description: 了解如何创建仅包含“页面”功能的社区站点模板，帮助您创建简单的社区站点。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: developing
exl-id: d66fc1ff-a669-4a2c-b45a-093060facd97
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# 创建示例页面 {#create-a-sample-page}

自AEM 6.1 Communities起，创建示例页面的最简单方法是创建一个简单的社区站点，其中只包含一个Page函数。

这包含一个parsys组件，以便您可以[启用用于创作的组件](basics.md#accessing-communities-components)。

探索示例组件的另一个选项是使用[社区组件指南](components-guide.md)中提供的功能。

## 创建社区站点 {#create-a-community-site}

这类似于[AEM Communities快速入门](getting-started.md)中描述的创建站点。

主要区别在于，本教程创建一个仅包含[页面函数](functions.md#page-function)的社区站点模板来创建简单的社区站点。 它不使用其他功能（除了所有社区站点均通用的预布线功能之外）。

### 创建新站点模板 {#create-new-site-template}

若要开始，请创建一个简单的[社区站点模板](sites.md)。

从创作实例的全局导航中，选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 社区]** > **[!UICONTROL 站点模板]**。

![create-site-template](assets/create-site-template1.png)

* 选择`Create button`
* 基本信息

   * `Name`：单页模板
   * `Description`：包含单页函数的模板。
   * 选择`Enabled`

![site-template-editor](assets/site-template-editor.png)

* 结构

   * 将`Page`函数拖到模板生成器中
   * 有关配置功能详细信息，请输入

      * `Title`：单页
      * `URL`：页面

![site-template-editor-structure](assets/site-template-editor1.png)

* 为配置选择&#x200B;**`Save`**
* 为站点模板选择&#x200B;**`Save`**

### 创建新社区站点 {#create-new-community-site}

现在，基于简单站点模板创建一个社区站点。

创建站点模板后，从全局导航中选择&#x200B;**[!UICONTROL 社区>站点]**。

![create-community-site](assets/create-community-site1.png)

* 选择&#x200B;**`Create`**&#x200B;图标

* 步骤 `1 - Site Template`

   * `Title`：简单社区站点
   * `Description`：包含用于试验的单个页面的社区站点。
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name`：示例

      * url = http://localhost:4502/content/sites/sample

      * `Template`：选择`Single Page Template`

     ![create-community-site-template](assets/create-community-site-template.png)

* 选择`Next`
* 步骤 `2 - Design`

   * 选择任意设计

* 选择`Next`
* 选择`Next`

  （接受所有默认设置）

* 选择`Create`

  ![create-community-site](assets/create-community-site.png)

## Publish站点 {#publish-the-site}

![发布站点](assets/publish-site.png)

从[社区站点控制台](sites-console.md)中，选择发布图标以发布站点，默认情况下为http://localhost:4503。

## 在编辑模式下在作者上打开站点 {#open-the-site-on-author-in-edit-mode}

![开放站点](assets/open-site.png)

选择打开站点图标，以便您可以在编辑模式下查看站点。

URL是[http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)

![作者站点](assets/author-site.png)

在简单的主页上，可以看到通过社区功能和模板预先连接的内容，并可以在添加和配置社区组件方面有所作为。

## 在Publish上查看站点 {#view-site-on-publish}

发布页面后，在[发布实例](http://localhost:4503/content/sites/sample/en.html)上打开该页面，以匿名网站访客、登录成员或管理员身份尝试这些功能。 在创作环境中可见的管理链接不会出现在发布环境中，除非管理员登录。
