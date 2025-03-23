---
title: CIF产品和类别选取器的用法
description: 了解如何在客户商务组件中使用CIF产品和类别选取器，以支持作者和营销人员高效地使用商务产品和目录数据。
sub-product: Commerce
topics: Development
version: Experience Manager as a Cloud Service
activity: develop
audience: developer
feature: Commerce Integration Framework
exl-id: 1e7c3748-92b5-45f1-8dd9-f1816e3e34aa
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: a45b09c52d780a954e606d4cae73a3a02a8a6aa4
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# AEM Content和Commerce创作选取器 {#cif-pickers}

AEM内容和Commerce创作提供了一系列创作工具，可帮助AEM作者和营销人员高效地使用商业产品数据和目录。 产品选取器和类别选取器是CIF加载项的一部分，由CIF核心组件使用。 项目可以在任何组件对话框中使用这些选取器来选择产品或类别。

## 产品选取器 {#product-picker}

要在项目组件中使用产品选取器，开发人员必须将`commerce/gui/components/common/cifproductfield`添加到组件对话框。 例如，对`cq:dialog`使用以下对象：

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

product字段允许导航到用户希望通过不同视图选择的产品。 默认情况下， product字段会返回产品的ID，但可以使用`selectionId`属性对其进行配置。

产品选取器字段支持以下可选属性：

- selectionId(id、uid、sku、slug、combinedSlug、combinedSku) — 允许您选择将由选取器返回的产品属性（默认为id）。 在使用combinedSku时，使用sku会返回所选产品的sku并返回诸如base#variant之类的字符串以及基础产品和所选变体的sku；如果选择基础产品，则返回单个sku。
- filter (folderOrProduct， folderOrProductOrVariant) — 筛选要在导航产品树时由选取器呈现的内容。 folderOrProduct — 呈现文件夹和产品。 folderOrProductOrVariant — 呈现文件夹、产品和产品变体。 如果呈现了产品或产品变体，它也会在选取器中变为可选状态。 （默认为folderOrProduct）
- 多个(true， false) — 允许选择一个或多个产品（默认值= false）
- emptyText — 配置选取器字段的空文本值

此外，也支持标准对话框字段属性，如`name`、`fieldLabel`或`fieldDescription`。

>[!CAUTION]
>
>`cifproductfield`组件需要`cif.shell.picker`客户端库。 要将clientlib添加到对话框，您可以使用extraClientlibs属性。
>[!CAUTION]
>
>从CIF核心组件版本2.0.0开始，删除了`id`的支持并将其替换为`uid`。 Adobe建议使用`sku`或`slug`作为产品标识符。 Adobe仍仅对使用CIF核心组件版本1.x的项目支持`id`。

在[CIF核心组件](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml)项目中可以找到`cifproductfield`的完整工作示例。 另请参阅AEM核心组件文档的[自定义对话框](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs)。

## 类别选取器 {#category-picker}

类别选取器可以在组件对话框中使用，其使用方式与产品选取器类似。

以下代码片段可以在cq：dialog配置中使用：

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

类别选取器字段支持以下可选属性：

- selectionId(id， uid， slug， urlPath， idAndUrlPath _（已弃用）_， uidAndUrlPath _（已弃用）_) — 允许您选择选择器要返回的类别属性（默认为id）。
- multiple (true， false) — 启用一个或多个类别的选择（默认值= false）

此外，也支持标准对话框字段属性，如`name`、`fieldLabel`或`fieldDescription`。

>[!CAUTION]
>
>与`cifproductfield`组件相同，`cifcategoryfield`组件还需要`cif.shell.picker` clientlib。 要将clientlib添加到对话框，您可以使用`extraClientlibs`属性。 请参阅AEM核心组件文档的[自定义对话框](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs)。
>[!CAUTION]
>
>从CIF核心组件版本2.0.0开始，删除了`id`的支持并将其替换为`uid`。 Adobe建议使用`uid`或`urlPath`作为类别标识符。 Adobe仍仅对使用CIF核心组件版本1.x的项目支持`id`和`idAndUrlPath`。

在[CIF核心组件](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml)项目中可以找到`cifcategoryfield`的完整工作示例。
