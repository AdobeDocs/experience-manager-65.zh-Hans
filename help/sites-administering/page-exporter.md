---
title: 页面导出程序
description: 了解如何使用Adobe Experience Manager (AEM)页面导出程序。
exl-id: 15d08758-cf75-43c0-9818-98a579d64183
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 0%

---

# 页面导出程序{#the-page-exporter}

Adobe Experience Manager (AEM)允许您将页面导出为包括图像、`.js`和`.css`文件的完整网页。

配置完毕后，您可以通过将URL中的`html`替换为`export.zip`来请求从浏览器导出页面。 这将生成一个存档(zip)文件，其中包含以html格式呈现的页面以及引用的资产。 页面中的所有路径（例如，图像的路径）将被重写，以指向存档中包含的文件或服务器上的资源。 随后可以从浏览器下载存档(zip)文件。

>[!NOTE]
>
>根据您的浏览器和设置，下载内容为：
>
>* 存档文件(`<page-name>.export.zip`)
>* 文件夹(`<page-name>`)；实际上存档文件已展开

## 导出页面 {#exporting-a-page}

以下步骤描述了如何导出页面，并假定站点存在导出模板。 导出模板定义了页面的导出方式并特定于您的站点。 要创建导出模板，请参阅[为站点创建页面导出程序配置](#creating-a-page-exporter-configuration-for-your-site)。

要导出页面，请执行以下操作：

1. 导航到&#x200B;**站点**&#x200B;控制台中的所需页面。

1. 选择页面，然后打开&#x200B;**属性**&#x200B;对话框。

1. 选择&#x200B;**高级**&#x200B;选项卡。

1. 展开&#x200B;**导出**&#x200B;字段以选择导出模板。
为您的站点选择所需的模板，然后使用&#x200B;**确定**&#x200B;进行确认。

1. 选择&#x200B;**保存并关闭**&#x200B;以关闭页面属性对话框。

1. 请求导出页面，在URL中将后缀`html`替换为`export.zip`。

   例如：
   * localhost：4502/content/we-retail/language-masters/en.html

   访问方式：
   * localhost：4502/content/we-retail/language-masters/en.export.zip

1. 将存档文件下载到您的文件系统。

1. 在文件系统中，根据需要解压缩文件。 展开后，将有一个与选定页面同名的文件夹。 此文件夹包含：

   * 子文件夹`content`，它是反映存储库中页面路径的一系列子文件夹的根

      * 在此结构中有选定页面(`<page-name>.html`)的html文件

   * 根据导出模板中的设置，可以找到其他资源（`.js`个文件、`.css`个文件、图像等）

1. 在浏览器中打开页面html文件(`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`)，以便检查渲染。

## 为站点创建页面导出程序配置 {#creating-a-page-exporter-configuration-for-your-site}

页面导出程序基于[内容同步框架](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/package-summary.html)。 **页面属性**&#x200B;对话框中可用的配置是导出模板，这些模板定义了页面所需的依赖项。

触发页面导出时，将引用导出模板。 页面路径和设计路径都会动态应用。 然后，使用标准的内容同步功能创建zip文件。

现成的AEM安装在`/etc/contentsync/templates/default`下包含默认模板。

* 此模板是在存储库中未找到导出模板时的回退模板。

* `default`模板显示了如何配置页面导出，以便用作新导出模板的基础。

* 要在浏览器中以JSON格式查看模板的节点结构，请请求以下URL：
  `http://localhost:4502/etc/contentsync/templates/default.json`

创建页面导出程序模板的最简单方法是：

* 复制`default`模板，

* 为您的站点分配一个合适的新名称，

* 然后进行所需的更新。

要创建全新的模板，请执行以下操作：

1. 在&#x200B;**CRXDE Lite**&#x200B;中，在`/etc/contentsync/templates`下创建节点：

   * `Name`：适用于您的网站的名称；例如，`<mysite>`。 选择页面导出程序模板时，该名称将显示在页面属性对话框中。

   * `Type`：`nt:unstructured`

2. 在调用此处`mysite`的模板节点下，使用下述配置节点创建节点结构。

## 为页面激活页面导出器模板 {#activating-a-page-exporter-configuration-for-your-pages}

配置模板后，使其可用：

1. 在CRXDE中，导航到`/content`分支中的所需页面。 这可以是单个页面，也可以是子树的根页面。

1. 在页面的`jcr:content`节点上，创建属性：
   * `Name`：`cq:exportTemplate`
   * `Type`：`String`
   * `Value`：模板的路径；例如： `/etc/contentsync/templates/mysite`

### 页面导出程序配置节点 {#page-exporter-configuration-nodes}

模板由节点结构组成，因为它使用[Content Sync框架](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/package-summary.html)。 每个节点都有一个`type`属性，该属性定义了zip文件创建过程中的特定操作。

<!-- For more details about the type property, see the Overview of configuration types section in the Content Sync framework page.
-->

以下节点可用于构建导出模板：

* `page`
页面节点用于将页面html复制到zip文件。 它具有以下特性：

   * 必需节点。
   * 位于`/etc/contentsync/templates/<mysite>`下。
   * 使用属性`Name`设置为`page`进行定义。
   * 节点类型为`nt:unstructured`

  `page`节点具有以下属性：

   * 值为`pages`的`type`属性集。

   * 它没有`path`属性，因为当前页面路径已动态复制到配置。
  <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
重写节点定义如何在导出的页面中重写链接。 重写的链接可以指向zip文件中包含的文件或服务器上的资源。
  <!-- See the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
设计节点用于复制用于导出页面的设计。 它具有以下特性：

   * 可选。
   * 位于`/etc/contentsync/templates/<mysite>`下。
   * 定义时属性`Name`设置为`design`。
   * 节点类型为`nt:unstructured`。

  `design`节点具有以下属性：

   * `type`属性设置为值`copy`。

   * 它没有`path`属性，因为当前页面路径被动态复制到配置。

* `generic`
通用节点用于将clientlibs `.js`或`.css`文件等资源复制到zip文件。 它具有以下特性：

   * 可选。
   * 位于`/etc/contentsync/templates/<mysite>`下。
   * 无特定名称。
   * 节点类型为`nt:unstructured`。
   * 具有`type`属性和`type`相关属性。<!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

  例如，以下配置节点将`mysite.clientlibs.js`文件复制到zip文件：

  ```xml
  "mysite.clientlibs.js": {
      "extension": "js",
      "type": "clientlib",
      "path": "/etc/designs/mysite/clientlibs",
      "jcr:primaryType": "nt:unstructured"
  }
  ```

**实施自定义配置**

也可以使用自定义配置。

<!--
As you may have noticed in the node structure, the **Geometrixx** page export template has a `logo` node with a `type` property set to `image`. This is a special configuration type that has been created to copy the image logo to the zip file. 
-->

为了满足某些特定要求，请实施[自定义更新处理程序](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/handler/package-summary.html)。

<!-- To meet some specific requirements, you may need to implement a custom `type` property. To do so, see the Implementing a custom update handler section in the Content Sync page.
-->

## 以编程方式导出页面 {#programmatically-exporting-a-page}

若要以编程方式导出页面，您可以使用[PageExporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI服务。 此服务允许您：

* 导出页面并写入HTTP servlet响应。
* 导出页面并在特定位置保存zip文件。

绑定到`export`选择器和`zip`扩展的servlet使用PageExporter服务。

## 疑难解答 {#troubleshooting}

如果您在下载zip文件时遇到问题，可以删除存储库中的`/var/contentsync`节点，然后再次发送导出请求。
