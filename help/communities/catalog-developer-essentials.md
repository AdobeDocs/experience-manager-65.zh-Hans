---
title: Catalog Essentials
seo-title: Catalog Essentials
description: 目录概述
seo-description: 目录概述
uuid: 788512bb-fa38-48fb-a769-1eaae6bb95a1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 542467ef-3793-4347-8424-c365c5a166f6
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Catalog Essentials {#catalog-essentials}

本页提供了有关使用Enablement Community站点的目录功能的基本信息。

目录功能（当包含在社区站点中时）允许社区成员浏览并选择目录中列出的启用资源。

该组 [ 件允许社区成员访问 `enablement catalog` 启用资源目录](catalog.md)[](resources.md)。 使用AEM标记是管理目录中启用资源外观的重要部分。

请参阅 [标记启用资源](tag-resources.md)。

## 客户端必备工具 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/enablement/components/hbs/catalog</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.catalog<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learningpath</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/enablement/components/hbs/catalog/catalog.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/enablement/components/hbs/catalog/clientlibs/catalog.css</td>
  </tr>
  <tr>
   <td><strong> 属性</strong></td>
   <td>请参阅 <a href="catalog.md">目录功能</a></td>
  </tr>
 </tbody>
</table>

## 服务器端必备工具 {#essentials-for-server-side}

### 目录功能 {#catalog-function}

包含“目录”功能的社区站 [点结构](functions.md#catalog-function)，包括已配置的 `enablement catalog` 组件。

### 预过滤器 {#pre-filters}

将目录功能添加到社区站点后，可以通过指定预过滤器来限制目录中显示的启用资源和学习路径。 这是通过为站点设置目录资源实例的属性来完成的。

使用Enablement Tutorial的 [示例](getting-started-enablement.md):

* 论作者
* 使用 [CRXDE](../../help/sites-developing/developing-with-crxde-lite.md)

   * 例如 [https://&lt;server>:&lt;port>/crx/de](http://localhost:4502/crx/de)

* 导览至目录页面上的目录资源

   * For example, `/content/sites/enable/en/catalog/jcr:content/content/primary/catalog`

* 添加子过滤器节点

   * 选择节 `catalog`点
   * 选择 **[!UICONTROL 创建节点]**

      * 名称: `filters`
      * 类型: `nt:unstructured`
   * 选择 **[!UICONTROL 全部保存]**


* 向节 `se_resource-tags` 点添加属 `filters` 性

   * 选择节 `filters` 点
   * 添加多属性

      * 名称: `se_resource-tags`
      * 类型：字符串
      * 值： *&lt;输入[TagID](#pre-filter-tagids)>*
      * 选择多 **[!UICONTROL 个]**
      * 选择添 **[!UICONTROL 加]**

         * 在弹出对话框中，选 `+` 择以添加其他预过滤TagID

* 重新发布社区站点

![chlimage_1-189](assets/chlimage_1-189.png)

#### 预过滤标记ID {#pre-filter-tagids}

预过滤器 [TagID必须与应用于](../../help/sites-developing/framework.md#tagid) enablement资源的标记完全匹配。 这些属性在站 `resources` 点的文件夹中显示为属性值 `se_resource-tags`。

![chlimage_1-190](assets/chlimage_1-190.png)

### 参考API {#reference-apis}

* [Enablement API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/api/package-summary.html)

* [报告API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/api/package-summary.html)

* [Reporting Analytics API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/analytics/api/package-summary.html)

