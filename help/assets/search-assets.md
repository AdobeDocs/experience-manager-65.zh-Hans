---
title: 在 [!DNL Adobe Experience Manager]中搜索数字资源和图像
description: 了解如何使用“筛选器”面板在 [!DNL Adobe Experience Manager] 中查找所需的资产，以及如何使用搜索中显示的资产。
contentOwner: AG
mini-toc-levels: 1
feature: Search, Metadata
role: User
exl-id: 588433b2-564a-430f-9d04-480465ece2ad
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 7c1aeec18f35b019a63d0385ada248b26a0df9de
workflow-type: tm+mt
source-wordcount: '5664'
ht-degree: 4%

---

# 在[!DNL Adobe Experience Manager]中搜索数字资源 {#search-assets-in-aem}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/assets/manage/search-assets) |
| AEM 6.5 | 本文 |

[!DNL Adobe Experience Manager Assets]提供了强大的资源发现方法，可帮助您实现更高的内容速度。 您的团队可以使用开箱即用的功能和自定义方法，通过无缝、智能的搜索体验缩短上市时间。 搜索资产是使用数字资产管理系统的核心，无论它是供创意人员进一步使用、供商业用户和营销人员稳健管理资产，还是DAM管理员进行管理。 您可以通过[!DNL Assets]用户界面或其他应用和表面执行的简单、高级和自定义搜索有助于完成这些用例。

[!DNL Experience Manager Assets]支持以下用例，本文介绍这些用例的使用情况、概念、配置、限制和疑难解答。

| 搜索资产 | 配置和管理搜索功能 | 使用搜索结果 |
|---|---|---|
| [基本搜索](#searchbasics) | [搜索索引](#searchindex) | [排序结果](#sort) |
| [了解搜索UI](#searchui) | [视觉或相似性搜索](#configvisualsearch) | [检查资源的属性和元数据](#checkinfo) |
| [搜索建议](#searchsuggestions) | [必需的元数据](#mandatorymetadata) | [下载](#download) |
| [了解搜索结果和行为](#searchbehavior) | [修改搜索彩块化](#searchfacets) | [批量元数据更新](#metadataupdates) |
| [搜索排名和提升](#searchrank) | [文本提取](#extracttextupload) | [智能收藏集](#collections) |
| [高级搜索：筛选和搜索范围](#scope) | [自定义谓词](#custompredicates) | [了解意外结果并排除其故障](#unexpected-results) |
| [从其他解决方案和应用中搜索](#search-assets-other-surfaces)：<ul><li>[Adobe Asset Link](#aal)</li><li>[Brand Portal](#brand-portal)</li><li>[Experience Manager桌面应用程序](#desktop-app)</li><li>[Adobe Stock图像](#adobe-stock)</li><li>[Dynamic Media资源](#dynamic-media)</li></ul> | | |
| [资产选择器](#asset-picker) | | |
| [限制](#limitations)和[提示](#tips) | | |
| [图示示例](#samples) | | |

使用[!DNL Experience Manager] Web界面顶部的Omnisearch字段搜索数字资源。 转到&#x200B;**[!UICONTROL 中的]** Assets **[!UICONTROL >]**&#x200B;文件[!DNL Experience Manager]，单击顶部栏中的![search_icon](assets/do-not-localize/search_icon.png)，输入搜索关键字，然后选择`Return`。 或者，使用关键字快捷键`/`（正斜杠）打开Omnisearch字段。 已预选择`Location:Assets`以将搜索限制在DAM资源中。 [!DNL Experience Manager]会在您开始键入搜索关键字时提供建议。

使用&#x200B;**[!UICONTROL 筛选器]**&#x200B;面板搜索资源、文件夹、标记和元数据。 您可以根据各种选项（谓词）筛选搜索结果，例如文件类型、文件大小、上次修改日期、资源状态、分析数据和Adobe Stock许可。 您可以使用[搜索Facet](/help/assets/search-facets.md)自定义“筛选器”面板以及添加或删除搜索谓词。 [!UICONTROL 筛选器]面板中的[!UICONTROL 文件类型]筛选器包含混合状态复选框。 因此，除非选择所有嵌套的谓词（或格式），否则将部分选中第一级复选框。

[!DNL Experience Manager]搜索功能支持搜索收藏集和搜索收藏集中的资源。 请参阅[搜索收藏集](/help/assets/manage-collections.md)。

## 了解搜索界面 {#searchui}

熟悉搜索界面和可用的操作。

![了解Experience Manager Assets搜索结果界面](assets/aem_search_results.png)

*图：了解[!DNL Experience Manager Assets]搜索结果界面。*

**A.**&#x200B;将搜索另存为智能收藏集。 **B.**&#x200B;筛选条件或谓词以缩小搜索结果。 **C.**&#x200B;显示文件、文件夹或两者。 **D.** 单击“过滤器”以打开或关闭左边栏。**E.** 搜索位置为 DAM。**F.**&#x200B;具有用户提供的搜索关键字的Omnisearch字段。 **G.**&#x200B;选择加载的搜索结果。 **小时**&#x200B;显示的搜索结果数占总搜索结果数。 **I.**&#x200B;关闭搜索。 **J.**&#x200B;在卡片视图和列表视图之间切换。

### 动态搜索Facet {#dynamicfacets}

您可以使用搜索Facet中预期搜索结果的动态更新数量，更快地从搜索结果页面发现所需的资产。 即使在应用搜索过滤器之前，预计的资源数量也会更新。 查看筛选器的预期计数可帮助您快速高效地浏览搜索结果。

![在搜索Facet中查看不筛选搜索结果的大致资源数。](assets/asset_search_results_in_facets_filters.png)

*图：在搜索Facet中查看不筛选搜索结果的大致资源数。*

## 了解搜索结果和行为 {#searchbehavior}

### 基本搜索词和结果 {#searchbasics}

您可以从OmniSearch字段运行关键字搜索。 关键词搜索不区分大小写，是一种全文搜索（跨常用元数据字段）。 如果使用多个关键字，`AND`是关键字之间的默认运算符。

结果按相关性排序，从最接近的匹配项开始。 对于多个关键字，更相关的结果是在其元数据中包含这两个术语的资源。 在元数据中，显示为智能标记的关键字的排名高于显示在其他元数据字段中的关键字。 [!DNL Experience Manager]允许为特定搜索词赋予更高的权重。 此外，还可以[提升特定搜索词的少数目标资产的排名](#searchrank)。

为快速找到相关资产，丰富的界面提供了筛选、排序和选择机制。 您可以根据多个条件筛选结果，并查看各种筛选条件的搜索资源数。 或者，您可以通过更改Omnisearch字段中的查询来重新运行搜索。 当您更改搜索词或筛选器时，其他筛选器仍将应用以保留您的搜索上下文。

当结果为多个资产时，[!DNL Experience Manager]在卡片视图中显示前100个，在列表视图中显示前200个。 用户滚动时，会加载更多资源。 这是为了改进性能。 观看视频演示[显示的资源数](https://www.youtube.com/watch?v=LcrGPDLDf4o)。

有时，您可能会在搜索结果中看到一些意外的资产。 有关详细信息，请参阅[意外结果](#unexpected-results)。

[!DNL Experience Manager]可以搜索多种文件格式，并且可以自定义搜索筛选器以满足您的业务要求。 请联系您的管理员，了解您的DAM存储库有哪些搜索选项可用，以及您的帐户具有哪些限制。

### 使用和不使用增强型智能标记的结果 {#withsmarttags}

默认情况下，[!DNL Experience Manager]搜索将搜索词与AND子句组合在一起。 例如，考虑搜索关键字woman running。 默认情况下，搜索结果中仅显示元数据中同时包含女性和运行关键字的资源。 当关键字中使用特殊字符（句点、下划线或破折号）时，将保留相同的行为。 以下搜索查询返回相同的结果：

* `woman running`
* `woman.running`
* `woman-running`

但是，查询`woman -running`返回其元数据中不带`running`的资源。
使用智能标记会添加额外的`OR`子句，以将任何搜索词作为应用的智能标记进行查找。 使用智能标记以`woman`或`running`标记的资产也出现在这样的搜索查询中。 所以搜索结果是，

* 元数据中包含`woman`和`running`关键字的Assets（默认行为）。

* 使用任一关键字（“智能标记”行为）标记的Assets智能标记。

### 键入内容时搜索建议 {#searchsuggestions}

当您开始键入关键字时，[!DNL Experience Manager]将建议可能的搜索关键字或短语。 这些建议基于现有资源的元数据。 [!DNL Experience Manager]对所有元数据字段编制索引以帮助搜索。 为了提供搜索建议，系统使用以下几个元数据字段的值。 要提供搜索建议，请考虑使用相应的关键字填充以下字段：

* 资产标记。 （映射到`jcr:content/metadata/cq:tags`）
* 资源标题。 （映射到`jcr:content/metadata/dc:title`）
* 资源描述。 （映射到`jcr:content/metadata/dc:description`）
* JCR存储库中的标题。 该值可能会映射到资源标题。 （映射到`jcr:content/jcr:title`）
* JCR存储库中的描述。 该值可能会映射到资产描述。 （映射到`jcr:content/jcr:description`）

要接收多个搜索关键字的建议，请继续键入所有关键字，而无需为单个关键字选择任何建议。

![键入多个关键字以查看适合所有关键字的建议](assets/search_suggestionsmanykeywords.gif)

*图：键入多个关键字以查看适合所有关键字的建议。*

### 搜索排名和提升 {#searchrank}

首先显示与元数据字段中的所有搜索词匹配的搜索结果，随后显示与智能标记中的任何搜索词匹配的搜索结果。 在上述示例中，搜索结果的大致显示顺序为：

1. 各种元数据字段中的`woman running`的匹配项。
1. 智能标记中的`woman running`的匹配项。
1. 在智能标记中匹配`woman`或`running`。

您可以改善特定资产的关键字相关性，以帮助提高基于关键字的搜索量。 换言之，当基于这些关键字进行搜索时，为其升级特定关键字的图像将显示在搜索结果的顶部。

1. 从[!DNL Assets]用户界面中，打开资产的属性页面。 单击&#x200B;**[!UICONTROL 高级]**，然后单击&#x200B;**[!UICONTROL 提升搜索关键字]**&#x200B;下的&#x200B;**[!UICONTROL 添加]**。
1. 在&#x200B;**[!UICONTROL 搜索提升]**&#x200B;框中，指定要提升图像搜索的关键字，然后单击&#x200B;**[!UICONTROL 添加]**。 您可以按相同方式指定多个关键字。
1. 单击&#x200B;**[!UICONTROL 保存并关闭]**。 您针对此关键字提升的资产将显示在排名最前的搜索结果中。

利用这种方法，您可以提升目标关键词搜索结果中某些资产的排名。 请观看下面的示例视频。 有关详细信息，请参阅[搜索 [!DNL Experience Manager]](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/assets/search-and-discovery/search-boost)。

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*视频：了解搜索结果的排名方式以及排名会受到何种影响。*

## 高级搜索 {#scope}

[!DNL Experience Manager]提供了多种方法（如适用于所搜索资产的筛选条件），以帮助您更快地找到所需的资产。 下面介绍了一些常用方法。 下面提供了一些[示例](#samples)。

**搜索文件或文件夹**：在搜索结果中，查看文件和/或文件夹。 从&#x200B;**[!UICONTROL 筛选器]**&#x200B;面板中，您可以选择相应的选项。 请参阅[搜索界面](#searchui)。

**在文件夹中搜索资源**：您可以将搜索限制为特定文件夹。 在&#x200B;**[!UICONTROL 筛选器]**&#x200B;面板中，添加文件夹的路径。 一次只能选择一个文件夹。

![通过在“筛选器”面板中添加文件夹路径将搜索结果限制为文件夹](assets/search_folder_select.gif)

*图：通过在“筛选器”面板中添加文件夹路径，将搜索结果限制为文件夹。*

### 查找相似图像 {#visualsearch}

要查找与用户选择的图像视觉上相似的图像，请从图像的卡片视图或工具栏中单击&#x200B;**[!UICONTROL 查找类似]**&#x200B;选项。 [!DNL Experience Manager] 会从 DAM 存储库中显示与用户所选图像相似的智能标记图像。请参阅[如何配置相似性搜索](#configvisualsearch)。

![使用卡片视图中的选项查找类似图像](assets/search_find_similar.png)

*图：使用卡片视图中的选项查找类似图像。*

### Adobe Stock图像 {#adobe-stock}

在[!DNL Experience Manager]用户界面中，用户可以搜索[Adobe Stock资源](/help/assets/aem-assets-adobe-stock.md)并许可所需的资源。 在Omnisearch栏中添加`Location: Adobe Stock`。 您还可以使用过滤器面板查找所有许可或未许可的资源，或使用Adobe Stock文件号搜索特定资源。

### Dynamic Media资产 {#dmassets}

您可以通过选择&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中的 **[!UICONTROL Dynamic Media]** > **[!UICONTROL 集]**&#x200B;来过滤 Dynamic Media 图像。该操作可过滤并显示图像集、轮播集、混合媒体集和旋转集等资产。

### 使用元数据字段中的特定值的GQL搜索 {#gql-search}

您可以根据元数据字段（如标题、描述和创建者）的精确值搜索数字资源。 GQL全文搜索功能仅会获取其元数据值与搜索查询完全匹配的资源。 属性的名称（创建者、标题等）和值区分大小写。

| 元数据字段 | Facet值和使用情况 |
|---|---|
| 标题 | 标题:John |
| 创建者 | 创建者:John |
| 位置 | 位置:NA |
| 描述 | description：&quot;Sample Image&quot; |
| 创建者工具 | creatortool：&quot;Adobe Photoshop&quot; |
| 版权所有者 | 版权所有：“Adobe Inc” |
| 参与者 | 参与者:John |
| 使用条款 | 使用条款：“保留复制权利” |
| 创建 | 已创建:YYYY-MM-DDTHH |
| 过期日期 | 过期:YYYY-MM-DDTHH |
| 准时 | ontime:YYYY-MM-DDTHH |
| 关闭时间 | offtime:YYYY-MM-DDTHH |
| 时间范围(expires dateontime，offtime) | Facet字段：下限……上行 |
| 路径 | /content/dam/&lt;文件夹名称> |
| PDF 标题 | pdftitle：&quot;Adobe文档&quot; |
| 主题 | 主题：“培训” |
| 标记 | 标记：“位置和旅游” |
| 类型 | 类型：&quot;image\png&quot; |
| 图像宽度 | 宽度:lowerbound..上行 |
| 图像高度 | 高度:lowerbound..上行 |
| 人员 | 人员:John |

属性`path`、`limit`、`size`和`orderby`不能将`OR`运算符与任何其他属性一起使用。

<!-- TBD: Where are the limit, size, orderby properties defined?
-->

用户生成的属性的关键字是属性编辑器中的字段标签（小写），其中删除空格。

以下是复杂查询的搜索格式的一些示例：

* 要显示具有多个Facet字段的所有资源(例如： title=John Doe和creator tool = Adobe Photoshop)： `title:"John Doe" creatortool:Adobe*`
* 在Facet值不是单个单词而是句子时显示所有资产（例如：title=Scott Reynolds）： `title:"Scott Reynolds"`
* 要显示具有单个属性的多个值的资产（例如：title=Scott Reynolds或John Doe），请执行以下操作： `title:"Scott Reynolds" OR "John Doe"`
* 要显示属性值以特定字符串开头的资产（例如：标题为Scott Reynolds）： `title:Scott*`
* 要显示其属性值以特定字符串结尾的资产（例如：title是Scott Reynolds）： `title:*Reynolds`
* 要显示其属性值包含特定字符串的资产（例如：标题=巴塞尔会议室）： `title:*Meeting*`
* 要显示包含特定字符串并具有特定属性值的资源(例如：在title=John Doe的资源中搜索字符串Adobe)，请执行以下操作： `*Adobe* title:"John Doe"`

## 从其他[!DNL Experience Manager]产品或界面搜索数字资产 {#search-assets-other-surfaces}

[!DNL Adobe Experience Manager]将DAM存储库连接到各种其他[!DNL Experience Manager]解决方案，以提供对数字资产的更快访问并简化创意工作流。 任何资源发现都从浏览或搜索开始。 在各种表面和解决方案中，搜索行为在很大程度上保持不变。 某些搜索方法会随着目标受众、用例和用户界面在所有[!DNL Experience Manager]解决方案中的不同而有所变化。 通过下面的链接，为各个解决方案记录了具体方法。 本文记录了一些普遍适用的提示和行为。

### 从Adobe Asset Link面板搜索数字资源 {#aal}

使用Adobe Asset Link，创意专业人士现在无需离开受支持的Adobe Creative Cloud应用程序即可访问[!DNL Experience Manager Assets]中存储的内容。 创意人员可以使用[!DNL Adobe Creative Cloud]应用[!DNL Adobe Photoshop]、[!DNL Adobe Illustrator]和[!DNL Adobe InDesign]中的应用内面板无缝浏览、搜索、签出和签入资源。 Asset Link还允许用户搜索视觉上类似的结果。 可视化搜索显示结果由Adobe AI机器学习算法提供支持，并帮助用户查找美学上相似的图像。 请参阅[使用Adobe Asset Link搜索和浏览资源](https://helpx.adobe.com/cn/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink)。

### 在[!DNL Experience Manager]桌面应用程序中搜索数字资产 {#desktop-app}

Creative专业人员使用桌面应用程序让[!DNL Experience Manager Assets]易于搜索并在其本地桌面(Win或Mac)上可用。 创意人员可以轻松地在Mac Finder或Windows资源管理器中显示所需的资源，这些资源在桌面应用程序中打开，并在本地进行更改 — 这些更改将在存储库中创建新版本后保存回[!DNL Experience Manager]。 应用程序支持使用一个或多个关键字、`*`和`?`通配符以及`AND`运算符进行基本搜索。 请参阅桌面应用程序中的[浏览、搜索和预览资源](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-desktop-app/using/using#browse-search-preview-assets)。

### 在[!DNL Brand Portal]中搜索数字资源 {#brand-portal}

业务线用户和营销人员使用Brand Portal与其扩展的内部团队、合作伙伴和经销商高效、安全地共享获得批准的数字资源。 请参阅[在Brand Portal](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching)中搜索资源。

### 搜索[!DNL Adobe Stock]图像 {#adobe-stock1}

在[!DNL Experience Manager]用户界面中，用户可以搜索Adobe Stock资源并许可所需的资源。 在Omnisearch字段中添加`Location: Adobe Stock`。 您还可以使用&#x200B;**[!UICONTROL 筛选器]**&#x200B;面板查找所有许可或未许可的资源，或使用Adobe Stock文件号搜索特定资源。 查看[中的 [!DNL Adobe Stock] 管理 [!DNL Experience Manager]](/help/assets/aem-assets-adobe-stock.md#usemanage)图像。

### 搜索[!DNL Dynamic Media]资源 {#dynamic-media}

您可以通过选择&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中的 **[!UICONTROL Dynamic Media]** > **[!UICONTROL 集]**&#x200B;来过滤 Dynamic Media 图像。该操作可过滤并显示图像集、轮播集、混合媒体集和旋转集等资产。在创作网页时，作者可以在内容查找器中搜索集。弹出菜单中提供集的过滤器。

### 创作网页时在Content Finder中搜索数字资产 {#content-finder}

作者可以使用内容查找器在DAM存储库中搜索相关资产，并在他们创建的网页中使用资产。 此外，作者还可以使用“连接的Assets”功能搜索远程[!DNL Experience Manager]部署中可用的资源。 然后，作者可以在本地[!DNL Experience Manager]部署的网页中使用这些资源。 请参阅[使用远程资产](/help/assets/use-assets-across-connected-assets-instances.md#use-remote-assets)。

### 搜索收藏集 {#collections}

[!DNL Experience Manager]搜索功能支持搜索收藏集和搜索收藏集中的资源。 请参阅[搜索收藏集](/help/assets/manage-collections.md)。

## 资源选择器 {#asset-picker}

>[!NOTE]
>
>在早期版本的[中，资产选择器称为](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions)资产选取器[!DNL Adobe Experience Manager]。

资产选择器允许您以特殊方式搜索、过滤和浏览DAM资产。 资源选择器位于`https://[aem_server]:[port]/aem/assetpicker.html`。 您可以获取使用资源选择器选择的资源的元数据。 您可以通过受支持的请求参数启动它，例如资产类型（图像、视频、文本）和选择模式（单选或多选）。 这些参数为特定搜索实例设置资产选择器的上下文，并在整个选择过程中保持不变。

资源选择器使用HTML5 `Window.postMessage`消息将选定资源的数据发送给收件人。 它仅在浏览模式下工作，并且仅适用于Omnisearch结果页面。

在URL中传递以下请求参数，以在特定上下文中启动资产选择器：

| 名称 | 值 | 示例 | 用途 |
|---|---|---|---|
| 资源后缀(B) | 文件夹路径作为URL中的资源后缀： [https://localhost:4502/aem/assetpicker.html/&lt;folder_path>](https://localhost:4502/aem/assetpicker.html) | 要在选定特定文件夹（例如选定文件夹`/content/dam/we-retail/en/activities`）的情况下启动资产选择器，URL应采用以下形式： `https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images` | 如果在启动资产选择器时要求选择特定文件夹，请将其作为资源后缀传递。 |
| `mode` | 单个，多个 | <ul><li>`https://localhost:4502/aem/assetpicker.html?mode=single`</li><li>`https://localhost:4502/aem/assetpicker.html?mode=multiple`</li></ul> | 在多个模式下，您可以使用资产选择器同时选择多个资产。 |
| `dialog` | true， false | [https://localhost:4502/aem/assetpicker.html？dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | 使用这些参数以Granite对话框形式打开资产选择器。 仅当通过Granite路径字段启动资产选择器，并将其配置为pickerSrc URL时，此选项才适用。 |
| `root` | &lt;文件夹路径> | `https://localhost:4502/aem/assetpicker.html?assettype=images&root=/content/dam/we-retail/en/activities` | 使用此选项可指定资源选择器的根文件夹。 在这种情况下，资产选择器允许您仅选择根文件夹下的子资产（直接/间接）。 |
| `viewmode` | 搜索 | | 要在搜索模式下启动资产选择器，请使用`assettype`和`mimetype`参数。 |
| `assettype` | 图像、文档、多媒体、存档。 | <ul><li>`https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents` </li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia` </li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives` </li></ul> | 使用选项可根据提供的值筛选资源类型。 |
| `mimetype` | 资产的MIME类型(`/jcr:content/metadata/dc:format`)（也支持通配符）。 | <ul><li>`https://localhost:4502/aem/assetpicker.html?mimetype=image/png`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*png`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*presentation`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&mimetype=*png`</li></ul> | 使用它根据MIME类型筛选资源。 |

要访问资产选择器界面，请转到`https://[aem_server]:[port]/aem/assetpicker`。 导航到所需的文件夹，然后选择一个或多个资产。 或者，从Omnisearch框中搜索所需的资源，根据需要应用过滤器，然后选择它。

![在资源选择器中浏览并选择资源](assets/assetpicker.png)

*图：在资源选择器中浏览并选择资源。*

## 限制 {#limitations}

[!DNL Experience Manager Assets]中的搜索功能具有以下限制：

* 请勿在搜索查询中输入前导空格，否则搜索将不起作用。
* 从搜索结果中选择资产的属性然后取消搜索后，[!DNL Experience Manager]可以继续显示搜索词。<!-- (CQ-4273540) -->
* 在搜索文件夹或文件和文件夹时，搜索结果不能按任何参数排序。
* 如果您选择`Return`而未在Omnisearch栏中键入，[!DNL Experience Manager]将返回仅包含文件而不包含文件夹的列表。 如果您专门搜索未使用关键字的文件夹，[!DNL Experience Manager]不会返回任何结果。
* 您可以对文件夹执行全文搜索。 指定要使搜索起作用的搜索词。

可视搜索或相似性搜索具有以下限制：

* 可视搜索最适合大型存储库。 虽然没有获得良好结果所需的最小图像数量，但少量图像的匹配质量不如大型存储库中的匹配质量。
* 您无法更改模型或训练[!DNL Experience Manager]以查找类似图像。 例如，向少数资产添加或删除智能标记不会更改模型。 资源将从视觉上相似的搜索结果中排除。

在以下场景中，搜索功能可能存在性能限制：

* 与列表视图相比，卡片视图的加载时间更短，可显示搜索结果。

## 搜索提示 {#tips}

* 在监控资产的审核状态时，使用相应的选项查找已批准的资产或待批准的资产。
* 使用分析谓词，根据从各种Creative应用程序获得的使用情况统计数据，搜索支持的资源。 使用情况数据按使用情况得分、展示次数、点击次数和媒体渠道进行分组，资产在这些渠道中显示类别。
* 使用&#x200B;**[!UICONTROL 全选]**&#x200B;复选框选择搜索到的资源。 [!DNL Experience Manager]最初在卡片视图中显示100个资源，在列表视图中显示200个资源。 滚动搜索结果时会加载更多资源。 您可以选择比已加载的资源更多的资源。 选定资源的计数将显示在搜索结果页面的右上角。 您可以对选择进行操作，例如，下载所选资源，批量更新所选资源的元数据属性，或将所选资源添加到收藏集。 当选择的资源多于显示的资源时，会对所有选定的资源应用操作，或者显示应用操作的资源数的对话框。 要将操作应用于未加载的资源，请确保已显式选择所有资源。
* 要搜索不包含必需元数据的资源，请参阅[必需元数据](#mandatorymetadata)。
* 搜索使用所有元数据字段。 一般搜索（例如搜索12）通常会返回许多结果。 为了获得更好的结果，请使用双引号（而非单引号）或确保数字与不带特殊字符（例如，`shoe12`）的单词相邻。
* 全文搜索支持`-`和`^`等运算符。 要将这些字母搜索为字符串文字，请用双引号将搜索表达式括起来。 例如，使用`"Notebook - Beauty"`而不是`Notebook - Beauty`。
* 如果搜索结果太多，请将所需资源的搜索[范围](#scope)限制为零。 当您知道如何更好地查找所需资源（例如，特定文件类型、特定位置、特定元数据等）时，这种方法最有效。

* **标记**：标记可帮助您对可以更高效地浏览和搜索的资源进行分类。 标记有助于将相应的分类传播给其他用户和工作流。 [!DNL Experience Manager]提供了使用Adobe AI服务自动标记资源的方法，这些方法有助于更好地通过使用和培训标记资源。 搜索资产时，如果帐户中启用了智能标记功能，则会将智能标记考虑在内。 它与内置搜索功能配合使用。 请参阅[搜索行为](#searchbehavior)。 要优化搜索结果的显示顺序，您可以[提升几个选定资产的搜索排名](#searchrank)。

* **索引**：搜索结果中只返回已编制索引的元数据和资源。 为了获得更好的覆盖率和性能，请确保正确编制索引并遵循最佳实践。 请参阅[索引](#searchindex)。

* 要从搜索结果中排除特定资源，请在Lucene索引中使用`excludedPath`属性。

## 一些说明搜索的示例 {#samples}

在关键字周围使用双引号可查找包含精确短语的资源，其顺序与用户指定的顺序完全一致。

![带引号和不带引号的搜索行为](assets/search_with_quotes.gif)

*图：带引号和不带引号的搜索行为。*

**使用星号通配符搜索**：要扩大搜索范围，请在搜索词前后使用星号以匹配任意数量的字符。 例如，搜索没有星号的运行不会返回包含单词任何变体的资产（包括元数据中的）。 星号可替代任意数量的字符。 例如，

* `run`返回带有精确运行关键字的资源
* `run*`返回具有`running`、`run`、`runaway`等的资源。
* `*run`返回具有`outrun`、`rerun`等的资源。
* `*run*`返回所有可能的组合。

![举例说明在资产搜索中使用星号通配符](assets/search_with_asterisk_run.gif)

*图：使用示例说明在资产搜索中使用星号通配符。*

**使用问号通配符搜索**：要扩大搜索范围，请使用一个或多个“？” 个字符以匹配确切的字符数。 例如，在下图中，

* `run???`查询不匹配任何资源。

* `run????`查询在`running`之后匹配4个字符的单词`run`。

* `??run`查询与`rerun`前具有两个字符的单词`run`匹配。

![使用示例](assets/search_with_questionmark_run.gif)说明在资产搜索中使用问号通配符

*图：使用示例说明在Asset搜索中使用问号通配符。*

**排除关键字**：使用短划线搜索不包含关键字的资源。 例如，`running -shoe`查询返回包含`running`但不包含`shoe`的资源。 同样，`camp -night`查询返回包含`camp`但不包含`night`的资源。 查询`camp-night`返回同时包含`camp`和`night`的资源。

![使用短划线搜索不包含排除关键字的资源](assets/search_dash_exclude_keyword.gif)

*图：使用短划线搜索不包含排除关键字的资源。*

## 与搜索功能相关的配置和管理任务 {#configadmin}

### 搜索索引配置 {#searchindex}

资产发现依赖于DAM内容（包括元数据）的索引。 更快、更准确地发现资产依赖于优化的索引和适当的配置。 查看[搜索索引](/help/assets/performance-tuning-guidelines.md#search-indexes)、[Oak查询和索引](/help/sites-deploying/queries-and-indexing.md)以及[最佳实践](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。

要从搜索结果中排除特定资源，请在Lucene索引中使用`excludedPath`属性。

### 视觉或相似性搜索 {#configvisualsearch}

可视化搜索使用智能标记。 配置智能标记功能后，请执行以下步骤。

1. 在[!DNL Experience Manager] CRXDE的`/oak:index/lucene`节点中，添加以下属性和值并保存更改。

   * 值为`costPerEntry`的类型`Double`的`10`属性。
   * 值为`costPerExecution`的类型`Double`的`2`属性。
   * 值为`refresh`的类型`Boolean`的`true`属性。

   此配置允许从相应的索引进行搜索。

1. 要创建Lucene索引，请在CRXDE中的`/oak:index/damAssetLucene/indexRules/dam:Asset/properties`处创建类型为`imageFeatures`的名为`nt-unstructured`的节点。 在`imageFeatures`节点中，

   * 添加值为`name`的类型为`String`的`jcr:content/metadata/imageFeatures/haystack0`属性。
   * 添加值为`nodeScopeIndex`的类型为`Boolean`的`true`属性。
   * 添加值为`propertyIndex`的类型为`Boolean`的`true`属性。
   * 添加值为`useInSimilarity`的类型为`Boolean`的`true`属性。

   保存更改。

1. 访问`/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags`并添加值为`similarityTags`的`Boolean`类型的`true`属性。
1. 将智能标记应用于[!DNL Experience Manager]存储库中的资源。 请参阅[如何配置智能标记](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/assets/configuring/tagging#configuring)。
1. 在CRXDE的`/oak-index/damAssetLucene`节点中，将`reindex`属性设置为`true`。 保存更改。
1. （可选）如果已自定义搜索表单，请将`/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch`节点复制到`/conf/global/settings/dam/search/facets/assets/jcr:content/items`。 保存更改。

有关相关信息，请参阅[了解Experience Manager中的智能标记](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/assets/metadata/image-smart-tags)和[如何管理智能标记](/help/assets/enhanced-smart-tags.md)。

>[!CAUTION]
>
>如果Lucene索引在[!DNL Adobe Experience Manager]内完成，则基于智能标记的搜索无法按预期工作。

### 必需元数据 {#mandatorymetadata}

业务用户、管理员或DAM库管理员可以将某些元数据定义为必需元数据，这些元数据是业务流程正常运行所必需的。 出于各种原因，某些资产可能缺少此元数据，例如旧版资产或批量迁移的资产。 根据索引的元数据属性，检测和报告包含缺失或无效元数据的Assets。 要配置它，请参阅[必需的元数据](/help/assets/metadata-schemas.md#define-mandatory-metadata)。

### 修改搜索彩块化 {#searchfacets}

为了提高发现速度，[!DNL Experience Manager Assets]提供了搜索Facet，您可以使用它来筛选搜索结果。 默认情况下，“筛选器”面板包含几个标准方面。 管理员可以自定义“筛选器”面板，以使用内置谓词修改默认Facet。 [!DNL Experience Manager]提供了一个良好的内置谓词集合和一个用于自定义Facet的编辑器。 查看[搜索Facet](/help/assets/search-facets.md)。

### 上传资产时提取文本 {#extracttextupload}

您可以将[!DNL Experience Manager]配置为在用户上传资源(如PSD或PDF文件)时从资源中提取文本。 [!DNL Experience Manager]对提取的文本编制索引，并帮助用户根据提取的文本搜索这些资源。 查看[上传资源](/help/assets/manage-assets.md#uploading-assets)。

如果对于部署而言，文本提取变得过于耗费资源，请考虑禁用文本提取。

### 用于筛选搜索结果的自定义谓词 {#custompredicates}

谓词用于创建Facet。 管理员可以使用预配置的谓词自定义过滤器面板中的搜索彩块化。 可以使用叠加自定义这些谓词。 请参阅[创建自定义谓词](/help/assets/searchx.md)。

您可以根据以下一个或多个属性搜索数字资产。 默认情况下，适用于其中一些属性的过滤器可用，也可以自定义创建某些其他过滤器以应用于其他属性。

| 搜索字段 | 搜索属性值 |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------|
| MIME 类型 | 图像、文档、多媒体、存档或其他。 |
| 上次修改 | Hour、Day、Week、Month或Year。 |
| 文件大小 | 小、Medium或大。 |
| 发布状态 | 已发布或已取消发布。 |
| 批准状态 | 已批准或已拒绝。 |
| 方向 | “水平”、“垂直”或“方形”。 |
| 样式 | 彩色或黑白。 |
| 视屏高度 | 指定为最小值和最大值。 值仅存储在视频演绎版的元数据中。 |
| 视频宽度 | 指定为最小值和最大值。 值仅存储在视频演绎版的元数据中。 |
| 视频格式 | DVI、Flash、MPEG4、MPEG、OGG Theora、QuickTime、Windows Media。 值存储在源视频和任何演绎版的元数据中。 |
| 视频编解码器 | x264。 值仅存储在视频演绎版的元数据中。 |
| 视频比特率 | 指定为最小值和最大值。 值仅存储在视频演绎版的元数据中。 |
| 音频编解码器 | Libvorbis、Lame MP3、AAC编码。 值仅存储在视频演绎版的元数据中。 |
| 音频比特率 | 指定为最小值和最大值。 值仅存储在视频演绎版的元数据中。 |

## 使用资源搜索结果 {#aftersearch}

您可以使用在[!DNL Experience Manager]中搜索的资源执行以下操作：

* 查看元数据属性和其他信息。
* 下载一个或多个资源。
* 使用桌面操作在桌面应用程序中打开这些资产。
* 创建智能收藏集。
* 创建一个版本
* 启动工作流
* 关联或取消关联资源
* 使用执行搜索后自动显示的过滤器面板应用过滤器以缩小搜索结果。

### 对搜索结果排序 {#sort}

对搜索结果进行排序，更快地发现所需的资源。 只有在从&#x200B;**[[!UICONTROL 筛选器]](#searchui)**&#x200B;面板中选择&#x200B;**[!UICONTROL 文件]**&#x200B;时，才能对列表视图中的搜索结果进行排序。 [!DNL Assets]使用服务器端排序快速对文件夹或搜索查询结果中的所有资产（无论数量多少）进行排序。 与客户端排序相比，服务器端排序提供更快、更准确的结果。

在列表视图中，您可以对搜索结果进行排序，就像对任何文件夹中的资源排序一样。 排序仅对以下列起作用 — 名称、标题、状态、维度、大小、评级、使用情况、已创建、已修改、已发布、工作流和已签出。

有关排序功能的限制，请参阅[限制](#limitations)。

### 检查资产的详细信息 {#checkinfo}

您可以从搜索结果页面检查搜索到的资源的详细信息。

要查看某个资源的所有元数据，请选择该资源，然后单击工具栏中的&#x200B;**[!UICONTROL 属性]**。

要检查对资源或资源版本历史记录的注释，请单击资源以打开大型预览。 打开左边栏中的时间轴，然后选择&#x200B;**[!UICONTROL 注释]**&#x200B;或&#x200B;**[!UICONTROL 版本]**。 您还可以按时间顺序对时间轴活动（如注释或版本）进行排序。

![对搜索资产的时间线条目进行排序](assets/sort_timeline_search_results.gif)

*图：对搜索资源的时间线条目排序。*

### 下载搜索到的资源 {#download}

您可以下载搜索到的资源及其演绎版，就像从文件夹下载常规资源一样。 从搜索结果中选择一个或多个资源，然后单击工具栏中的&#x200B;**[!UICONTROL 下载]**。

### 批量更新元数据属性 {#metadataupdates}

可以对多个资源的常用元数据字段进行批量更新。 从搜索结果中，选择一个或多个资源。 单击工具栏中的&#x200B;**[!UICONTROL 属性]**，并根据需要更新元数据。 完成后单击&#x200B;**[!UICONTROL 保存并关闭]**。 更新字段中先前存在的元数据将被覆盖。

对于单个文件夹或收藏集中可用的资产，无需使用搜索功能，更容易[批量](/help/assets/metadata.md)更新元数据。 对于跨文件夹可用的资源或符合通用标准的资源，通过搜索批量更新元数据会更快。

### 智能收藏集 {#smart-collections}

收藏集是一组经过排序的资源，可以包含来自不同位置的资源，因为收藏集仅包含对这些资源的引用。 收藏集属于以下两种类型：

* 资源、文件夹和其他收藏集的静态引用列表。
* 根据搜索条件填充收藏集中资产的动态列表（智能收藏集）。

您可以根据搜索条件创建智能收藏集。从&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中，选择&#x200B;**[!UICONTROL 文件]**，然后单击&#x200B;**[!UICONTROL 保存智能收藏集]**。请参阅[管理收藏集](/help/assets/manage-collections.md)。

### 创建一个版本 {#create-version}

为搜索结果中显示的资源创建版本。 选择资产并单击&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 版本]**。 添加可选标签或评论，然后单击&#x200B;**[!UICONTROL 创建]**。 您还可以选择多个资源并同时为其创建版本。

### 创建工作流 {#create-workflow}

与创建版本功能类似，您也可以为搜索结果中显示的资产创建工作流。 选择资产并单击&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 工作流]**。 选择工作流模型，指定工作流的标题，然后单击&#x200B;**[!UICONTROL 开始]**。

### 关联和取消关联资源 {#relate-unrelate-assets}

关联和取消关联搜索结果中显示的资源。 选择资源并单击&#x200B;**[!UICONTROL 相关]**&#x200B;或&#x200B;**[!UICONTROL 取消相关]**。

## 意外的搜索结果和问题 {#unexpected-results}

| 错误、问题、症状 | 可能的原因 | 对问题的可能修复或了解 |
|---|---|---|
| 搜索缺少元数据的资源时，结果不正确。 | 在搜索缺少必需元数据的资源时，[!DNL Experience Manager]可能会显示一些具有有效元数据的资源。 结果基于索引的元数据属性。 | 元数据更新后，需要重新索引以反映资源元数据的正确状态。 请参阅[必需的元数据](metadata-schemas.md#define-mandatory-metadata)。 |
| 搜索结果过多。 | 广泛搜索参数。 | 考虑限制搜索[的](#scope)范围。 使用智能标记可能会为您提供比预期更多的搜索结果。 查看带有智能标记的[搜索行为](#withsmarttags)。 |
| 不相关或部分相关的搜索结果。 | 使用智能标记可更改搜索行为。 | 了解[智能标记后搜索如何更改](#withsmarttags)。 |
| 没有针对资产的自动完成建议。 | 新上传的资产尚未编制索引。 当您开始在Omnisearch栏中输入搜索关键字时，元数据无法立即作为建议使用。 | [!DNL Experience Manager]将等待超时时间（默认为一小时）到期，然后再运行后台作业，为所有新上传或更新后的资源索引元数据，然后将元数据添加到建议列表中。 |
| 无搜索结果。 | <ul><li>匹配您的查询的Assets不存在。 </li><li> 在搜索查询之前添加了空格。 </li><li> 不支持的元数据字段包含您搜索的关键字。</li><li> 在资产空闲时间进行的搜索。 </li></ul> | <ul><li>使用其他关键词进行搜索。 或者，使用智能标记或相似性搜索来改进搜索结果。 </li><li>[已知限制](#limitations)。</li><li>搜索不考虑所有元数据字段。 查看[作用域](#scope)。</li><li>稍后搜索或修改所需资源的开始时间和结束时间。</li></ul> |
| 搜索过滤器或谓词不可用。 | <ul><li>未配置搜索筛选器。</li><li>它不适用于您的登录信息。</li><li>（不太可能）未在您使用的部署中自定义搜索选项。</li></ul> | <ul><li>请与管理员联系以检查搜索自定义项是否可用。</li><li>请与管理员联系以检查您的帐户是否具有使用此自定义设置的权限。</li><li>请与管理员联系，并检查您正在使用的[!DNL Assets]部署的可用自定义项。</li></ul> |
| 搜索视觉上相似的图片时，缺少预期的图片。 | <ul><li>图像在[!DNL Experience Manager]中不可用。</li><li>图像未编制索引。 通常是在最近上传时。</li><li>图像未智能标记。</li></ul> | <ul><li>将图像添加到[!DNL Assets]。</li><li>请与管理员联系以重新索引存储库。 此外，请确保使用相应的索引。</li><li>请与管理员联系以智能标记相关资产。</li></ul> |
| 当搜索视觉上相似的图像时，显示不相关的图像。 | 视觉搜索行为。 | [!DNL Experience Manager]显示尽可能多的潜在相关资源。 不太相关的图像（如果有）会添加到结果中，但搜索排名较低。 向下滚动搜索结果时，搜索资源的匹配质量和相关性会降低。 |
| 选择并操作搜索结果时，不会操作所有搜索到的资产。 | [!UICONTROL 全选]选项仅选择卡片视图中的前100个搜索结果和列表视图中的前200个搜索结果。 | |

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 搜索实施指南](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/sites/developing/search-tutorial-develop)
>* [高级配置以提升搜索结果](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/assets/search-and-discovery/search-boost)

