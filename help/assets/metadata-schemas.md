---
title: 元数据架构
description: 元数据架构定义属性页面的布局以及为资产显示的元数据属性。 了解如何创建自定义元数据架构、编辑元数据架构以及如何将元数据架构应用到资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: d15273e9308926ca4745fc1045e2da9fe8ed91d4

---


# 元数据架构 {#metadata-schemas}

在Adobe Experience Manager(AEM)资产中，元数据架构定义属性页面的布局以及为使用特定架构的资产显示的元数据属性。 元数据属性包括标题、描述、MIME类型、标记等。

您可以使用元数据架构表单编辑器修改现有架构或添加自定义元数据架构。

1. 要查看资产的属性页面，请在卡片视图中单击或点按资产拼贴上 **[!UICONTROL 的快速操作]** ，中的查看属性图标。

   ![chlimage_1-34](assets/chlimage_1-170.png)

   或者，在UI中选择资产，然后单击或点按工具栏中 **[!UICONTROL 的]** “属性”图标。

   ![chlimage_1-35](assets/chlimage_1-171.png)

1. 在各种选项卡下编辑各种元数据属性。 但是，您无法在属性页面中修改资产类型。

   ![您无法更改资产属性基本选项卡中的资产类型](assets/asset-properties-basic-tab.png)

   *图：资产属性上的“基本”选项卡*


   要修改资产的MIME类型，请使用自定义元数据架构表单或修改现有表单。 有关详 [细信息，请参阅编辑元数据架构表单](/help/assets/metadata-schemas.md#edit-metadata-schema-forms) 。 如果修改了某些MIME类型的元数据架构，则将修改当前MIME类型和所有资产子类型的资产的属性页面布局。 例如，修改jpeg架构时，只 `default/image` 会修改MIME类型资产的元数据布局（资产属性） `image/jpeg`。 但是，如果您编辑默认架构，则所做的更改将修改所有类型资产的元数据布局。

1. 要查看表单/模板列表，请单击 AEM 徽标，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 元数据架构]**。

   ![chlimage_1-37](assets/chlimage_1-173.png)

   AEM提供了以下现成模板：
   * **default**:资产的基本元数据架构表单。

      以下子表单继承默认表单的属性：

      1. **图像**:此架构表单用于MIME类型为“image”(例如， `image/jpeg`、 `image/png`等)的资产。

         “图像”表单具有以下子表单模板：
         * **jpeg**:子类型资产的架构表单 `jpeg`。
         * **tiff**:子类型资产的架构表单 `tiff`。
      1. **应用程序**:此架构表单用于MIME类 `application`型的资产， `application/pdf`例如 `application/zip`，等等。
         * **pdf**:子类型资产的架构表单 `pdf`。
      1. **视频**:此架构表单用于MIME类 `video`型(如 `video/avi`、 `video/mp4`等)的资产。
   * **集合**:集合的架构表单。
   * **contentfragment:** 内容片段的架构表单。
   * **表单**:此架构表单与 [Adobe Experience Manager Forms相关](/help/forms/home.md)。

>[!NOTE]
>
>要查看架构表单的子表单，请单击／点按架构表单名称。

## Add a metadata schema form {#add-a-metadata-schema-form}

1. 要将自定义模板添加到列表，请单击工 **[!UICONTROL 具栏中]** 的创建。

   >[!NOTE]
   >
   >未编辑的模板前面有一个锁图标。如果自定义任何模板，则模板前面的锁图标会消失。

1. In the dialog, enter the title of the Schema form, and then click **[!UICONTROL Create]** to complete the form creation process.

   ![chlimage_1-38](assets/chlimage_1-174.png)

## 编辑元数据架构表单 {#edit-metadata-schema-forms}

可以编辑新添加的或现有的元数据架构表单。元数据架构表单包括：

* 选项卡
* 选项卡中的表单项目

您可以将这些表单项映射到／配置到CRX存储库中元数据节点内的字段。

可以向元数据架构表单中添加新的选项卡或表单项目。从父项派生的选项卡和表单项目处于锁定状态。 无法从子级别更改它们。

1. 在“架构表单”页面中，选中表单前面的复选框，然后单击工具栏上的编辑图标。

   ![chlimage_1-39](assets/chlimage_1-175.png)

1. 在元数 **[!UICONTROL 据架构编辑器页中]** ，通过将“构建表单”选项卡中的组件类型列表中的一个或多个组件拖至“基本”选项卡，自定义资产的属性页 ******** 。

   ![将构建表单中的组件添加到元数据架构编辑器以自定义资产属性](assets/metadata-schema-editor.png)


   *图：元数据架构编辑器的“基本”选项卡*

1. To configure a component, select it and modify its properties in the **Settings** tab.

### “构建表单”选项卡内的组件{#components-within-the-build-form-tab}

The **[!UICONTROL Build Form]** tab lists form items that you use in your schema form. The **[!UICONTROL Settings]** tab provides the attributes of each item that you select in the **[!UICONTROL Build Form]** tab. The following table lists the form items available in the **[!UICONTROL Build Form]** tab:

| 组件名称 | 描述 |
|---|---|
| [!UICONTROL 章节标题] | 为常用组件列表添加章节标题。 |
| [!UICONTROL 单行文本] | 添加单行文本属性。它存储为字符串。 |
| [!UICONTROL 多值文本] | 添加多值文本属性。它存储为字符串数组。 |
| [!UICONTROL 数字] | 添加数字组件。 |
| [!UICONTROL 日期] | 添加日期组件。 |
| [!UICONTROL 下拉列表] | 添加下拉列表。 |
| [!UICONTROL 标准标记] | 添加标记. |
| [!UICONTROL 智能标记] | 通过自动添加元数据标记来增强搜索功能。 |
| [!UICONTROL 隐藏字段] | 添加隐藏字段。在保存资产时，它将作为POST参数发送。 |
| [!UICONTROL 资产引用对象] | 添加此组件可查看资产引用的资产列表。 |
| [!UICONTROL 资产引用] | 添加可显示引用资产的资产列表。 |
| [!UICONTROL 产品引用] | 添加以显示与资产关联的产品列表。 |
| [!UICONTROL 资产评级] | 添加到资产评级的显示选项。 |
| [!UICONTROL 上下文元数据] | 添加以控制资产属性页面中其他元数据选项卡的显示。 |

#### 编辑元数据组件 {#edit-the-metadata-component}

To edit the properties of a metadata component on the form, click the component and edit all or a subset of the following properties in the **[!UICONTROL Settings]** tab.

**字段标签**:资产的属性页面上显示的元数据属性的名称。

**映射到属性**:此属性指定资产节点在CRX存储库中保存的相对路径／名称。 It starts with `./` because indicating that the path is under the asset&#39;s node.

以下是此属性的有效值：

以下是此属性的有效值：

* `./jcr:content/metadata/dc:title`：将该值作为属性 `dc:title` 存储在资产的元数据节点中。

* `./jcr:created`:在资产的节点上显示JCR属性。 如果您在视图属性上配置这些属性，我们建议您将这些属性标记为“禁用编辑”，因为它们是受保护属性。Otherwise, the error [!UICONTROL Asset(s) failed to modify] results when you save the asset&#39;s properties.

要确保在元数据架构表单中正确显示组件，属性路径不应包括任何空格。

**占位符**:使用此属性可指定与元数据属性相关的占位符文本。
**必需**:使用此属性可在属性页面上将元数据属性标记为必填。
**禁用编辑**:使用此属性可使元数据属性在属性页面上不可编辑。
**在只读模式下显示空字段**:标记此属性可在属性页面上显示元数据属性，即使它没有值也是如此。默认情况下，当元数据属性没有值时，不会在属性页面上列出该属性。
**显示有序列表**:使用此属性可显示选项的有序列&#x200B;**表**:使用此属性可指定列表描述中的选&#x200B;**项** :使用此属性可为元数据组件添加简短说明。
**类**:属性关联的对象类。
**删除**:单击此图标可从架构表单中删除组件。

![chlimage_1-41](assets/chlimage_1-177.png)

>[!NOTE]
>
>隐藏字段组件不包括这些属性。 而是包括属性，如名称、值、字段标签和说明。 无论何时保存资产，都会将“隐藏字段”组件的值作为 POST 参数进行发送。该组件的值不会作为资产的元数据进行保存。

如果选择&#x200B;**[!UICONTROL 必需]**&#x200B;选项，则可以搜索缺少必需元数据的资产。从&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中，展开&#x200B;**[!UICONTROL 元数据验证]**&#x200B;谓词，然后选择&#x200B;**[!UICONTROL 无效]**&#x200B;选项。搜索结果中显示的资产缺少您通过架构表单配置的必需元数据。

![chlimage_1-42](assets/chlimage_1-178.png)

如果将上下文元数据组件添加到任何架构表单的任何选项卡，则该组件将作为列表显示在应用特定架构的资产的属性页面中。 该列表包括除您应用了上下文元数据组件的选项卡之外的所有其他选项卡。 目前，此功能提供了基本功能，用于根据上下文控制元数据的显示。

![chlimage_1-43](assets/chlimage_1-179.png)

要显示属性页面中的任意选项卡以及应用上下文元数据组件的选项卡，请从列表中选择该选项卡。 该选项卡会添加到属性页面。

![从上下文元数据列表中选择要在属性页面上显示的选项卡](assets/contextual-metadata-asset-properties.png)

*图：资产属性页面中的上下文元数据*

### 在JSON文件中指定属性 {#specify-properties-in-json-file}

您还可以通过指定相应的键值对在 JSON 文件中定义选项，而不是为&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中的选项指定属性。在 **[!UICONTROL JSON 路径]**&#x200B;字段中指定 JSON 文件的路径。

#### 在架构表单中添加或删除选项卡 {#adding-deleting-a-tab-in-the-schema-form}

通过架构编辑器，可以添加或删除选项卡。默认架构表单包括&#x200B;**[!UICONTROL 基本]**、**[!UICONTROL 高级]**、**[!UICONTROL IPTC]** 和 **[!UICONTROL IPTC 扩展]**&#x200B;选项卡（默认情况下）。

![chlimage_1-45](assets/chlimage_1-181.png)

Click `+` to add a new tab on a schema form. By default, the new tab has the name `Unnamed-1`. You can modify the name from the **[!UICONTROL Settings]** tab.

Click `X` to delete a tab.

![chlimage_1-46](assets/chlimage_1-182.png)

## 删除元数据架构表单 {#delete-metadata-schema-forms}

AEM仅允许您删除自定义架构表单。 您无法删除默认的架构表单/模板。但是，您可以删除对这些表单所做的任何自定义更改。

要删除表单，请选择一个表单，然后单击删除图标。

![chlimage_1-47](assets/chlimage_1-183.png)
<!--![chlimage_1-47](assets/chlimage_1-177.png) -->
>[!NOTE]
>
>删除对默认表单的自定义更改后，在元数据架构界面上，表单前面会重新显示锁图标，以指示表单已恢复为默认状态。

>[!NOTE]
>
>您无法删除AEM资产中的现成元数据架构表单。

## Schema forms for MIME types {#schema-forms-for-mime-types}

AEM资产为各种开箱即用的MIME类型提供默认表单。 但是，您可以为各种MIME类型的资产添加自定义表单。

### Add new forms for MIME types {#add-new-forms-for-mime-types}

在相应的表单类型下创建新表单。例如，要为 **image/png** 子类型添加新模板，请在“image”表单下创建表单。架构表单的标题是子类型名称。在这种情况下，标题为“png.**”**

#### Use an existing schema template for various MIME types {#use-an-existing-schema-template-for-various-mime-types}

您可以为不同的 MIME 类型使用现有模板。For example, use the `image/jpeg` form for assets of MIME type `image/png`.

In this case, create a new node at `/etc/dam/metadataeditor/mimetypemappings` in the CRX repository. 指定节点的名称并定义以下属性：

| 名称 | 描述 | 类型 | 值 |
|---|---|---|---|
| `exposedmimetype` | 要映射的现有表单的名称 | `String` | `image/jpeg` |
| `mimetypes` | List of MIME types that use the form defined in the `exposedmimetype` attribute | `String` | `image/png` |

AEM 资产映射以下 MIME 类型和架构表单：

| 架构表单 | MIME类型 |
|---|---|
| image/jpeg | image/pjpeg |
| image/tiff | image/x-tiff |
| application/pdf | application/postscript |
| application/x-ImageSet | Multipart/Related; type=application/x-ImageSet |
| application/x-SpinSet | Multipart/Related; type=application/x-SpinSet |
| application/x-MixedMediaSet | Multipart/Related; type=application/x-MixedMediaSet |
| video/quicktime | video/x-quicktime |
| video/mpeg4 | video/mp4 |
| video/avi | video/avi、video/msvideo、video/x-msvideo |
| video/wmv | video/x-ms-wmv |
| video/flv | video/x-flv |

## Grant access to metadata schemas {#grant-access-to-metadata-schemas}

元数据架构功能仅适用于管理员。不过，管理员可以通过修改一些权限，向非管理员用户提供访问权限。The non administrator should have create, modify, and delete permissions on the `/conf` folder.

## 应用特定于文件夹的元数据 {#apply-folder-specific-metadata}

AEM资产允许您定义元数据架构的变体，并将其应用到特定文件夹。

例如，您可以定义默认元数据架构的变体并将其应用到文件夹。 应用修改后的架构时，它将覆盖应用于文件夹内资产的原始默认元数据架构。

只有上传到应用此架构的文件夹的资产才会与变体元数据架构中定义的修改后的元数据保持一致。

应用原始架构的其他文件夹中的资产将继续与原始架构中定义的元数据保持一致。

按资产划分的元数据继承基于应用于层次结构中第一级文件夹的架构。 换句话说，如果文件夹不包含子文件夹，则文件夹内的资产将继承应用到该文件夹的架构中的元数据。

如果文件夹有子文件夹，则子文件夹内的资产将继承子文件夹级别所应用的架构中的元数据（如果在子文件夹级别应用了其他架构）。 但是，如果子文件夹级别未应用架构或同一架构，则子文件夹资产将从父文件夹级别应用的架构继承元数据。

1. 单击 AEM 徽标，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 元数据架构]**。此时会显示&#x200B;**[!UICONTROL 元数据架构表单]**&#x200B;页面。
1. 选中表单前面的复选框（例如默认元数据表单），然后单击或点按复制图标并将其另存为自定义表单。 例如，指定表单的自定义名称 `my_default`。 或者，您也可以创建自定义表单。
   ![chlimage_1-184](assets/chlimage_1-184.png)

1. 在“元数 **[!UICONTROL 据架构表单]** ”页中，选择表 `my_default` 单，然后单击“编 **[!UICONTROL 辑]** ”图标。

   ![chlimage_1-49](assets/chlimage_1-185.png)

1. 在“元数 **[!UICONTROL 据架构编辑器]** ”页中，向架构表单添加一个文本字段。 例如，添加一个带有标签“类别”的 **[!UICONTROL 字段]**。

   ![向元数据架构表单编辑器添加文本字段](assets/text-field-metadata-schema-editor.png)

   *图：向元数据架构表单编辑器添加的文本字段*

1. 单击&#x200B;**[!UICONTROL 保存]**。修改后的表单列在“元数据架构表 **[!UICONTROL 单”页面中]** 。
1. 单击／点 **[!UICONTROL 按工具栏中的应用到文件夹]** ，以将自定义元数据应用到文件夹。

   ![chlimage_1-51](assets/chlimage_1-187.png)

1. 选择要应用修改后的架构的文件夹，然后单击／点按应 **[!UICONTROL 用]**。

   ![chlimage_1-52](assets/chlimage_1-188.png)

1. 如果文件夹应用了其他元数据架构，则会显示一条消息，警告您将覆盖现有元数据架构。 单击“ **覆盖**”。
1. Click **OK** to close the success message.
1. 导航到应用了修改后的元数据架构的文件夹。

## 定义必填元数据 {#define-mandatory-metadata}

您可以在文件夹级别定义必填字段，该字段强制用于上传到该文件夹的资产。 如果您上传的资产中前面定义的必填字段缺少元数据，则卡片视图中的资产上会显示缺失元数据的可视指示。

>[!NOTE]
>
>可以根据其他字段的值将元数据字段定义为必填字段。 在“卡”视图中，AEM不显示有关此类强制元数据字段缺失元数据的警告消息。

1. 单击 AEM 徽标，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 元数据架构]**。此时会显示&#x200B;**[!UICONTROL 元数据架构表单]**&#x200B;页面。
1. 将默认元数据表单另存为自定义表单。 例如，将其另存为 `my_default`。

   ![chlimage_1-53](assets/chlimage_1-189.png)

1. 编辑自定义表单。 添加必填字段。 例如，添加“ **[!UICONTROL 类别]** ”字段并将该字段设为必填字段。

   ![将字段添加到元数据表单中，并在“规则”选项卡中选择“必需”，以强制执行此操作](assets/mandatory-field-metadata-schema-editor.png)

   *图：元数据架构表单编辑器中的必填字段*

1. 单击&#x200B;**[!UICONTROL 保存]**。修改后的表单列在“元数据架构表 **[!UICONTROL 单”页面中]** 。 选择表单，然后单击或点按工 **[!UICONTROL 具栏中的应用到文件夹]** ，以将自定义元数据应用到文件夹。

   ![chlimage_1-55](assets/chlimage_1-191.png)

1. 导航到文件夹，然后上传一些资产，其中缺少您添加到自定义表单的必填字段的元数据。 资产的卡片视图上会显示必填字段缺少元数据的消息。

   ![chlimage_1-56](assets/chlimage_1-192.png)

1. （可选）访问 `https://[server]:[port]/system/console/components/`。 配置并启 `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` 用默认禁用的组件。 设置AEM检查资产中元数据有效性的频率。

   此配置向资产添 `hasValidMetadata` 加一 `jcr:content` 个属性。 使用此属性，AEM可以筛选搜索结果。

   >[!NOTE]
   >
   >如果资产是在计划检查后添加的，则直到下次计划检查后，资产才 `hasValidMetadata` 会被标记为旗标。 资产不会显示在中间搜索结果中。

   >[!CAUTION]
   >
   >元数据验证检查会占用大量资源，并可能会影响系统性能。 相应地安排检查。 如果服务器无法处理负载，请尝试禁用此作业。
