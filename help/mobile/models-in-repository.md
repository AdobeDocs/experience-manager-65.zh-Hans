---
title: 存储库中的模型
seo-title: 存储库中的模型
description: 'null'
seo-description: 'null'
uuid: 54f81180-4178-4e33-a6f0-e9e6ea50798e
contentOwner: User
content-type: reference
discoiquuid: ae1a72f4-d8c1-4c75-ba2c-7322f3743b17
noindex: true
redirecttarget: /content/help/en/experience-manager/6-4/mobile/using/administer-mobile-apps
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444

---


# 存储库中的模型{#models-in-repository}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

模型包含一组数据类型，这些数据类型定义了内容服务最终呈现的属性。 模型还定义了其他模型之间的关系，以增强数据完整性。

作为开发人员，您应该熟悉存储库中的模型结构。 您可以根据应用程序要求创建自己的模型和实体。

## 创建模型类型 {#creating-model-types}

在 */libs/settings/mobileapps/model-types下有两种系统提供的型号类型*。 如果要覆盖系统型号类型，则需要在您希望进行覆盖的配置节点下创建 *mobileapps/model-types* 节点。

例如，如果您已在 */conf/myconf1* 和 */conf/myconf2* 中创建配置并且希望仅在 *conf1上覆盖系统模型，则您会创建Conf1设置下的***** mobileeapps/模型类型-Model-Apps节点(Settings of Conf1)。

如果要允许将数据类型添加到模型，则模型类型必须有一个名为“scaffolding”的类型为“cq:Page”的子节点和一个资源类型为 *wcm/scaffolding/components/scaffolding*。

基架页面还必须在PageContent节 *点上包含dataTypesConfig* 属性，该属性指示将允许使用此类型创建的数据类型模型。

>[!NOTE]
>
>基 **架** (Scaffolding)是定义可由实体基于模型编辑的数据类型的页面。 还可以配置每个数据类型以定义字段在UI中的显示方式以及数据值的保留方式。

### 数据类型配置 {#data-types-config}

数据类型配置节点包含数据类型项的列表。 每个数据类型项指定数据类型在模型编辑器中的显示方式，以及数据类型在最终由实体呈现时需要如何保持。

| **属性名称** | **描述** |
|---|---|
| fieldIcon | 表示数据类型的CoralUI图标类 |
| fieldPropResourceType | 用于显示用于配置数据类型的所有属性的组件 |
| fieldProperties | fieldPropResourceType为mobileapps/caas/gui/components/models/editor/datatypes/field时使用的属性组件的多值列表 ** |
| fieldResourceType | resourceType数据类型（即将在实体编辑器中呈现属性的组件）的保留节点的类型 |
| fieldViewResourceType | 组件，用于在模型编辑器视图中呈现数据类型（如果忽略此属性，则使用fieldResourceType） |
| fieldTitle | 将在模型编辑器中显示的数据类型的名称 |
| multiFieldResourceType | 选择多值时要在持久节点上使用的资源类型 |
| renderType | 客户端渲染提示 |

### 数据类型配置叠加 {#data-types-config-overlay}

“dataTypesConfig”属性支持Sling资源合并。 这意味着，系统模型类型（甚至自定义模型类型）使用的数据类型可以通过使用叠加节点进行自定义。

需要创建 */libs/settings/mobileapps/models/formbuilderconfig/datatypes的叠加* ，然后根据需要进行自定义。

例如，可以添加String数据类型的叠加，以将fieldResourceType更改为自定义组件。

有关Sling Resource Merging的更多信息，请参阅 [在AEM中使用Sling Resource Merging](/help/sites-developing/sling-resource-merger.md)。

![chlimage_1-7](assets/chlimage_1-7.png)

### 数据类型 {#data-types}

模型数据类型是一种表单组件，其能够包括发布表单时要包括的数据。 数据类型组件可以根据需要进行复杂处理。 自定义数据类型的示例可能是特定国家／地区的地址块，以避免使用简单数据类型始终重新创建它。

作为自定义数据类型的示例，请参见“/libs/mobileapps/caas/components/form/contentreference”。

所有原始数据类型都利用现有的Granite表单组件。 请参阅： [https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html)

然后，任何自定义数据类型都可以添加到数据类型配置中以供模型编辑器使用。

## 创建模型 {#creating-models}

开发所有所需的模型类型和数据类型后，即可开始创建模型。 作者最终将使用模型创建实体，内容服务使用这些实体来呈现其数据。

创建模型包括根据当前配置选取允许的模型类型，然后提供标题和说明。

要了解如何从功能板创建和管理模型，请参阅“移动应 [用程序”的创作部分下的创建模型](/help/mobile/administer-mobile-apps.md) 。

### 模型的属性 {#properties-of-a-model}

下表显示了为模型定义的属性：

| **属性名称** | **描述** |
|---|---|
| 模型标题 | 模型的名称 |
| 描述 | 模型的描述 |
| 缩略图 | 模型的缩览图图像 |
| 模型类型 | 模型类型（这可以是简单字符串或实际组件的路径） |
| 允许的子项 | 允许作为此模板子项的模板的路径 |
| 允许的父项 | 允许作为此模板父项的模板的路径 |

>[!NOTE]
>
>允 *许的子项*** 和允许的父项属性遵循与页面模板相同的规则。 有关详细信息，请参阅 [页面模板](/help/sites-developing/page-templates-static.md)。
>
>参照“模 *型类型* ”属性，所有模型都必须具有超类型的 *mobileapps/caas/components/data/entity* ，但可以具有允许自定义内容交付的子类型。 确保所有模型类型都是独一无二的还有助于内容服务的客户区分数据中的对象。

### 编辑模型 {#editing-a-model}

编辑模型涉及打开与模型关联的基架对话框表单以进行编辑。 通常，基架是模型的子节点，但如果需要，它可以通过使用“cq:scaffolding”属性指定其路径来位于模型之外。 如果您希望在需要具有不同属性的多个模型之间共享相同的基架，则此功能非常有用。

当模型的基架位于该位置时，模型编辑器将呈现“jcr:content/cq:dialog/content”下找到的任何内容。 目前，客户端formbuilder引擎仅支持最多3列的固定布局。 呈现的表单对话框右侧将显示在数据类型配置中指定的所有数据类型的列表。 可通过单击数据类型来编辑它们。 然后，右边栏将切换到所选数据类型的属性选项卡。 可通过将新数据类型拖动到预览画布上来添加它们。 单击“保存”(Save)将更改传播到服务器。 单击“取消”(Cancel)可关闭模型编辑器。

>[!NOTE]
>
>所有模型都是模板，因此它们遵循所有AEM模板规则。 这允许使用allowedParens和allowedChildren **&#x200B;等属 *性* 。 在基于模型创建新图元时，这些参数非常有效。 模板规则将确保实体只能基于某些模型，具体取决于其层次结构。
>
>要了解如何从仪表板中编辑模型，请参阅“移动 [应用程序”的创作部分下的](/help/mobile/administer-mobile-apps.md) “创建模型”。

### 系统模型 {#system-models}

提供了两种类型的预定义系统模型，以便简单地重复使用内容。 不能编辑这些模型。

**页面模型** “页面”模型提供了一种快速方法，可重复使用站点中的现有内容，以便按内容服务交付。

基于页面模型的实体的resourceType为：mobileapps/caas/components/data/pages

路径：站点页面的路径。 来自此路径的内容（及其子项）将由内容服务处理程序呈现。

**资产模型** “资产”模型提供了一种快速方法，可以重复使用资产中的现有内容，以便按内容服务交付。

基于页面模型的实体的resourceType为： *mobileapps/caas/components/data/assets。*

资产列表：资产路径列表。 每个资产将添加为一个子实体节点，其resourceType为 *wcm/foundation/components/image*。

>[!NOTE]
>
>要进一步了解如何使用这些模板从仪表板中创建模型，请参阅“移动应 [用程序”的创作部分中的创建模型](/help/mobile/administer-mobile-apps.md) 。
