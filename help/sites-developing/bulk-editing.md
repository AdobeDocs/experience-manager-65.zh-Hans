---
title: 配置页面以批量编辑页面属性
seo-title: 配置页面以批量编辑页面属性
description: 批量编辑页面属性允许您一次编辑多个页面的属性
seo-description: 批量编辑页面属性允许您一次编辑多个页面的属性
uuid: 1ad403d2-4b93-4943-ae45-74bf20705b81
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: fe61ee4b-51b6-4a6f-91d8-1c02b29cc1db
translation-type: tm+mt
source-git-commit: b08149e00c418319ebacec71c56472ad4e8e1089
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 7%

---


# 配置页面以批量编辑页面属性{#configuring-your-page-for-bulk-editing-of-page-properties}

[批量编辑页](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) 面属性允许您一次编辑多个页面的属性。

由于可能有不同的值，因此默认情况下不启用页面属性进行批量编辑。 必须明确允许（启用）它们。 在定义可批量编辑的页面属性时，您需要考虑某些含义，例如：

* 某些字段通常是唯一的；例如页面标题。 您必须决定何时启用这些字段进行批量编辑是否有意义。
* 某些字段可能有多个值——这在渲染时需要有意义的表示。

   例如，一个复选框，其中指示“准备发布”。 在批量编辑之前，这可能有几个值（例如，就绪、正在审阅、正在进行）。

>[!CAUTION]
>
>批量编辑页面属性为：
>
>* 经典UI中不可用。
>* Live Copy中的页面不可用。
>* 仅适用于具有相同资源类型的页面。

>



>[!NOTE]
>
>也可以对资产进行批量编辑。 其操作大体相同，只有少数几点差别。有关完整的信息，请参阅[编辑多个资产的属性](/help/assets/metadata.md)。您可以使用[模式编辑器](/help/assets/metadata-schemas.md)自定义资产批量元数据编辑器中的字段。

## 启用字段{#enabling-a-field}

>[!NOTE]
>
>某些字段可能有多个值——这在渲染时需要有意义的表示。 因此，您只应启用以下字段类型：
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`

>



在页面组件上启用字段（模板上不是&#x200B;*）:*

1. 使用CRXDE Lite（或等效方法）打开页面组件。

   例如：`/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >此示例假定实例上已安装核心组件，即当实例与We.Retail示例内容一起运行时。 有关详细信息，请参阅[核心组件文档](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。

1. 导览至`cq:dialog`定义中的必填字段。
1. 在字段节点上定义以下属性：

   * **名称**: `allowBulkEdit`
   * **类型**: `Boolean`
   * **值**:  `true`

   例如，对于标准页[foundation component](/help/sites-authoring/default-components-foundation.md):

   `/libs/foundation/components/page`

   该属性将定义在：

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >您&#x200B;***必须***&#x200B;不要更改`/libs`路径中的任何内容。
   >
   >这是因为下次升级实例时，`/libs`的内容会被覆盖（当您应用修补程序或功能包时，很可能会被覆盖）。
   >
   >建议的配置和其他更改方法是：
   >
   >    1. 在`/apps`下重新创建所需项（即，它存在于`/libs`中）
   >    1. 在`/apps`中进行任何更改


1. 选择&#x200B;**全部保存**&#x200B;以保留更新。

