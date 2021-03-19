---
title: 创建通信
seo-title: 创建通信
description: 在创建了信件模板后，您可以使用它管理数据、内容和附件，在AEM Forms中创建通信。
seo-description: 在创建了信件模板后，您可以使用它管理数据、内容和附件，在AEM Forms中创建通信。
uuid: 48cf2b26-c9b4-4127-9ea0-1b36addbff60
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 87742cb2-357b-421f-b79d-e355887ddec0
docset: aem65
feature: 通信管理
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3722'
ht-degree: 0%

---


# 创建通信{#create-correspondence}

## 在“创建通信”用户界面{#create-correspondence-in-the-create-correspondence-user-interface}中创建通信

在“通信管理”](../../forms/using/create-letter.md)中创建[字母模板后，最终用户/代理/声明调整器可以在“创建通信”用户界面中打开该字母，并通过输入数据、设置内容和管理附件创建通信。 最后，理赔员或代理人可以在预览模式下管理内容并提交信件。

### 预览通信{#preview-a-correspondence}

使用以下步骤选择要预览的信函：

1. 在“字母”页面上，点按&#x200B;**选择**。
1. 点按相应的字母以选择它。

   ![选择字母](assets/1_selectletter.png)

   选择字母

1. 对于基于预览的字母，选择&#x200B;**预览** > **数据**。 或者，对于非基于Data-Dictionary的字母，选择&#x200B;**预览**。 您还可以将鼠标悬停在字母上（未选择它），然后点按字母预览图标以预览它。

   >[!NOTE]
   >
   >如果数据字典与字母不关联，则字母预览将打开。 否则，如果字母是基于预览字典的，则Correspondence Management会在“预览”菜单中显示“”和“自定义”选项，您可以选择两个选项之一。 还可以将测试数据与数据字典相关联。 当[数据字典具有关联的测试数据](../../forms/using/data-dictionary.md#p-working-with-test-data-p)时，选择“预览”选项后，将打开普通预览，并填充测试数据。

1. 要在预览通信时渲染通信，您应是管理员或以下某个组的一部分：

   * 表单用户(到创作实例预览)
   * cm-agent-users（用于发布实例上的再现）

   如果您没有所需的权限，请请求管理员提供相应的访问权限。 有关创建用户和将用户添加到用户组的详细信息，请参阅[将用户或用户组添加到用户组](/help/sites-administering/security.md)。 如果您尝试在没有相应权限的情况下渲染通信，将显示404错误页。

1. 如果已选择&#x200B;**预览** > **自定义**，将打开一个对话框。 在对话框中，选择与数据字典对应的预览文件，将字母与之，然后选择&#x200B;**预览**。 根据特定字母的数据字典创建数据文件。 有关数据文件的详细信息，请参阅[数据字典](../../forms/using/data-dictionary.md#p-working-with-test-data-p)。

   ![预览字母](assets/8_previewcustomdatafile.png)

1. 默认情况下，将打开字母HTML预览(移动表单预览)，其中“数据”选项卡具有焦点。

   有关移动表单及其支持的功能的详细信息，请参阅[移动Forms与PDF forms之间的功能区别](https://helpx.adobe.com/livecycle/help/mobile-forms/feature-differentiation-mobile-forms-pdf.html)。

   有三个选项卡：数据、内容和附件。 如果没有数据元素（占位符变量和布局字段），则将在中直接打开字母，并显示“内容”选项卡。 只有在存在附件或启用库访问时，“附件”选项卡才可用。

   >[!NOTE]
   >
   >有关在字母预览的HTML或PDF再现模式之间切换的详细信息，请参阅[更改字母](#changerenditionmode)的再现模式。 有关Correspondence Management和AEM中PDF支持的详细信息，请参阅[停止NPAPI浏览器插件及其影响](https://helpx.adobe.com/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html)和[对HTML5 Forms](https://helpx.adobe.com/aem-forms/kb/pdf-forms-to-html5-forms.html)的PDF forms。

### 输入数据{#enterdata}

在“数据”选项卡中，填写可用的布局字段和占位符。

1. 根据需要在字段中输入数据和内容变量。 填写标有星号(*)的所有必填字段，以启用&#x200B;**提交**&#x200B;按钮。

   点按HTML字母预览中的数据字段值，以在“数据”选项卡中高亮显示相应的数据字段。

   ![在字母2_](assets/2_enterdata.png) ![1_enterdata中输入数据](assets/2_1_enterdata.png)

### 管理内容 {#managecontent}

在“内容”选项卡中，管理字母中的内容，如文档片段和内容变量。

1. 选择&#x200B;**内容**。 “对应管理”显示信件的内容选项卡。

   ![“内容”选项卡 — 内容中的高亮模块](assets/3_content.png)

1. 根据需要，在“内容”选项卡中编辑内容模块。 要将焦点置于内容层次结构中的相关内容模块，您可以点按字母预览中的相关行或段落，或直接点按内容层次结构中的内容模块。

   例如，在下图中选择了行“我们已审阅……”，在“内容”选项卡中选择了相关内容模块。

   ![4_highlightmoduleincontent](assets/4_highlightmoduleincontent.png)

   在“内容”或“数据”选项卡中，通过点按HTML字母预览左上角的“高亮选定的模块”(![highlightselectedmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png))，可以禁用或启用在字母预览中选择相关文本、段落或数据字段时转至内容/数据模块的功能。

   有关“创建通信”用户界面中各个模块可用的操作的详细信息，请参阅“创建通信”用户界面](#actions-and-info-available-in-the-create-correspondence-content-tab)中的“操作和信息”。[

1. 要查找内容模块，请使用“查找”字段。 输入内容模块的完整或部分名称或标题，以在通信中搜索内容模块。
1. 点按列表、文本、条件或目标区域前面的显示图标(![display](assets/display.png))，以在字母中显示或隐藏它。
1. 要编辑内联或可编辑的文本模块，请点按相关的&#x200B;**编辑**&#x200B;图标(![edittextmodule](assets/edittextmodule.png))或多次单击字母预览中的相关文本模块。

   系统显示一个文本编辑器以编辑文本并设置其格式。

   浏览器中的默认拼写检查器在文本编辑器中检查拼写。 要管理拼写检查和语法检查，您可以编辑浏览器的拼写检查设置或安装浏览器插件/加载项来检查拼写和语法。

   您还可以使用文本编辑器中的各种键盘快捷键管理、编辑文本和设置文本格式。 有关“Correspondence Management Keyboard Shortcuts”中[“Text Editor](/help/forms/using/keyboard-shortcuts.md#correspondence-management)”键盘快捷键的详细信息。

   ![5_edittextmodule](assets/5_edittextmodule.png)

   您可能希望重复使用在另一个文档应用程序中存在的多个文本段落之一。 您可以直接复制和粘贴文本，如来自MS Word、HTML页面或任何其他应用程序的文本。

   您可以在可编辑的文本模块中复制和粘贴一个或多个文本段落。 例如，您可能有一个MS Word文档，其项目符号列表为可接受的居住验证，如下所示：

   ![pastextword](assets/pastetextmsword.png)

   您可以直接将MS Word文档中的文本复制并粘贴到可编辑的文本模块。 项目符号列表、字体和文本颜色等格式将保留在文本模块中。

   ![pastetexteditmodule](assets/pastetexteditablemodule.png)

   >[!NOTE]
   >
   >但是，粘贴文本的格式设置有一些[限制](https://helpx.adobe.com/aem-forms/kb/cm-copy-paste-text-limitations.html)。

   可以使用Tab键缩进字母中的文本和数字。 例如，可以使用Tab键将列表中的多列文本对齐为表格格式。

   ![tabspace](assets/tabspaces.png)

   示例：使用Tab键将多列文本对齐为表格格式

   >[!NOTE]
   >
   >有关设置文本模块和字母的制表符间距的详细信息，请参阅[有关使用制表符间距排列文本的详细信息](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html)。

1. 如果需要，请在通信中插入特殊字符。 例如，可以使用“特殊字符”调板插入：

   * 货币符号，如€、¥和英镑
   * 数学符号，如∑、√、∂和^
   * 标点符号，如&quot;和&quot;

   ![特殊字符](assets/specialcharacters.png)

   Corresponce Management内置了210个特殊字符。 管理员可以通过自定义](../../forms/using/custom-special-characters.md)添加对更多/自定义特殊字符的支持。[

1. 要在可编辑的内嵌模块中突出显示\突出部分文本，请选择文本并点按高亮颜色。

   ![背景颜色](assets/letterbackgroundcolor.png)

   您可以直接点按“基本颜色”调板中显示的基本颜色`**[A]**`，或使用滑块`**[B]**`选择&#x200B;**后点按**&#x200B;以选择相应的颜色阴影。

   或者，您也可以转到“高级”选项卡，选择适当的“色相”、“亮度”和“饱和度”`**[C]**`以创建精确的颜色，然后点按“选择”`**[D]**`以应用颜色以高亮显示文本。

   ![textbackgroundcolor](assets/textbackgroundcolor.png)

1. 进行适当的内容和格式更改，然后点按&#x200B;**保存**。 点按(![editnextmoduleccr](assets/editnextmoduleccr.png))可在可编辑的文本模块之间移动，或点按&#x200B;**保存并下一个**&#x200B;可保存更改并移至下一个可编辑的文本模块。
1. 系统还显示每个分支的未填充变量。 当没有未填充的变量时，未填充的变量将显示为0。 如果存在未填充的变量，您可以点按分支以展开它并找到未填充的变量。 使用内容工具栏可删除内容、增加/减少内容缩进以及在内容前后插入分页符。

   您可以在数据模块上方和下方插入分页符，即使它们是列表和条件的一部分时也是如此。

1. 点按打开/关闭内容变量(![opencontentvariables](assets/opencontentvariables.png))以打开内容变量并相应地填写它们。
1. 正确填充未填充的变量后，未填充变量的计数将设置为0。

   在“创建对应”用户界面中，未填充的变量计数显示在包含至少一个变量的任何模块的层次结构的每个级别。 如果模块包含未填充的变量，则计数将显示在变量、模块、目标区域和字母模板级别。

   未填充的变量计数包括：

   * 仅不受保护的数据字典和占位符变量。 变量计数不包括布局或受保护的数据字典变量。
   * 必填字段。
   * 布局字段（如果为必填字段）并绑定到用户。
   * 仅唯一变量实例。 如果模块、目标区域或字母模板包含同一变量的两个或多个实例，则计数将显示为1(1)。 但是，对于每个实例，计数显示为1。

   未填充的变量计数不包括取消选择的模块。 如果某个模块包含在字母模板中，但不在字母中，则不会显示此模块中未填充变量的计数。

   对于目标区域、模块和变量，计数显示在字母模板中每个对象的右侧。 但是，对于完整模板，计数将显示在“创建对应”状态栏中。

   字母模板中的模块显示未填充的变量计数，如下所述：

   * **文** 本显示文本模块中包含的唯一未填充占位符变量和数据字典元素的和。
   * **条** 件显示条件中包含的唯一未填充条件变量和生成模块中包含的变量的总和。
   * **列** 表显示分配给列表的模块中包含的所有唯一未填充变量的总和。
   * **目标** 区域显示分配给目标区域的模块中包含的所有唯一未填充变量的和。

   请注意以下关于具有默认值的变量：

   * 布尔变量字段默认为&#x200B;*false*。 但是，该变量被视为未填充。 这意味着变量计数包括值&#x200B;*false*&#x200B;的所有布尔变量字段。

   * 数字变量字段默认为&#x200B;*0（零）*。 但是，该变量被视为未填充。 这意味着变量计数包括值&#x200B;*0（零）*&#x200B;的所有数值变量字段。



#### “创建对应内容”选项卡{#actions-and-info-available-in-the-create-correspondence-content-tab}中的“操作和信息”

**目标区域**

* 插入空行：插入新的空行。
* 插入内联文本：插入新文本模块。
* 订单锁定（信息）：指示无法更改内容的顺序。
* 未填充值（信息）：指示目标区中未填充变量的数量。

**模块**

* 选择（眼睛图标）：Includes\excludes module from the letter.
* 跳过项目符号(适用于列表模块及其子模块):跳过特定模块中的项目符号。
* 分页前(适用于目标区域的子模块):在模块前插入分页符。
* 分页符后(适用于目标区域的子模块):在模块前插入分页符。
* 未填充值（信息）：指示目标区中未填充变量的数量。
* 编辑（仅文本模块）：打开富文本编辑器以编辑文本模块。
* 数据面板（文本和条件模块）：打开模块的所有变量。

**列表模块**

* 插入空行：插入新的空行。
* 内容库：打开内容库以向列表添加模块。
* 列表设置(仅限嵌套列表):
* 订单锁定（信息）：指示无法更改列表项的顺序。

### 管理附件{#manage-attachments}

1. 选择&#x200B;**附件**。 Oracle Correspondence Management会按创建信函模板时的设置显示可用附件。
1. 您可以点按视图图标，选择不随函件一起提交附件，并点按附件中的叉号，将其从函件中删除。 对于指定的附件，在创建字母模板时，“强制”图标将禁用“视图”和“删除”图标。
1. 点按库访问（![库访问](assets/libraryaccess.png)）图标以访问内容库以将DAM资产作为附件插入。

   >[!NOTE]
   >
   >“库访问”图标可用，但在创作信件时只启用了库访问。

1. 如果在创建通信时未锁定附件的顺序，则可以通过选择附件并点按向下和向上箭头对附件重新排序。

   有关详细信息，请参阅[附件投放](#attachmentdelivery)。

### 在预览中管理内容并提交字母{#manage-content-in-preview-and-submit-the-letter}

您可以进行布局和内容相关更改，以确保信件的外观符合您的预期并提交到各种帖子流程。

1. 要高亮显示字母中的所有可编辑内容，请点按&#x200B;**高亮显示可编辑部分**。

   字母的可编辑内容以灰色背景高亮显示。

   ![突出显示可编辑内容](assets/4_highlightmoduleincontent-1.png)

1. 根据需要，在“内容”选项卡中编辑内容模块。 要将焦点置于内容层次结构中的相关内容模块，您可以点按字母预览中的相关行或段落，或直接点按内容层次结构中的内容模块。

   例如，行“允许我们访问……” 在下图中选中，并在“内容”选项卡中选择相应的内容模块。

   通过点按内容中的高亮显示选定模块(![highlightselectedmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png))，当在字母预览中点击相关文本、段落或数据字段时，可以禁用或启用在“内容”选项卡中高亮显示内容模块的功能。

   有关“创建通信”用户界面中各个模块可用的操作的详细信息，请参阅“创建通信”用户界面](#actions-and-info-available-in-the-create-correspondence-content-tab)中的“操作和信息”。[

1. 要将分页符添加到字母中，请点按要插入分页符的位置，然后选择“分页前”或“分页后”（![分页前后](assets/pagebreakbeforeafter.png)）。

   将在字母中插入显式分页符占位符。 要视图显式分页符对字母的影响，请参阅拼合的PDF预览。

   >[!NOTE]
   >
   >由于移动表单不支持分页，因此页眉和页脚只显示一次。 但是，您可以在布局（每页）中显式设置页眉和页脚，使其显示在移动表单预览中。 此外，信件中的空白页面（如果有）不会显示在移动表单预览中。

   ![显式分页符](assets/8_pagebreak.png)

1. 要将字母另存为草稿（您可以在以后继续工作），请点按另存为草稿。 要使用此选项，您的字母必须[已发布](../../forms/using/publishing-unpublishing-forms.md#publishanasset)。 有关详细信息，请参阅[保存草稿和提交字母实例](#savingdrafts)下的草稿实例。

   ![saveasdraft](assets/saveasdraft.png)

   将出现“起草字母名称”对话框，其中包含字母实例id。 您可以（可选）编辑此ID。 记下字母Id，然后点按&#x200B;**完成**。 以后可以使用此ID来[重新加载草稿字母](submit-letter-topostprocess.md#reloaddraft)。

1. 要将字母预览为拼合PDF，并且其布局和分页符与提交时完全相同，请点按(![预览](assets/preview.png))预览。

   该字母将显示为拼合的PDF。 拼合的PDF是字母的精确表示形式，因为它将使用字母的正确字体、分隔符和布局提交。

   >[!NOTE]
   >
   >如果您使用的是Mozilla Firefox和HTML再现类型，要将字母预览为拼合PDF，请确保使用本机浏览器插件，而不是Acrobat插件。 要选择本机浏览器插件，请转至Mozilla Firefox的设置，对于内容类型PDF，在Firefox中选择“预览”。

1. 如果您认为拼合的PDF预览令人满意，请点按&#x200B;**提交**&#x200B;以提交该信函。 要更改字母，请点按&#x200B;**退出预览**，返回至字母的“创建对应UI”预览以更改字母。 点按提交时，如果在发布实例上启用了管理信函实例配置，则会生成提交信函实例。

   有关详细信息，请参阅保存草稿和提交信函实例下的草稿实例。

   您还可以将字母另存为草稿，以便稍后更改字母。

   进行所需的更改后，您可以提交HTML5预览中的字母或再次点按预览以查看拼合的PDF输出。

   有关HTML5表单与PDF forms之间差异的信息，请参阅[HTML5表单与PDF forms之间的功能区别](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md)。

## 保存草稿并提交字母实例{#savingdrafts}

在“创建通信”用户界面中呈现信件时，可以将信件保存为被查看。

可以保存两种类型的字母实例：草稿实例和提交实例。

* **草稿实例**:草稿实例捕获您正在预览的字母的当前状态。要保存草稿实例，请首先确保字母和字母引用的所有资产处于“已发布”状态。 有关发布字母的信息，请参阅[发布资产](../../forms/using/publishing-unpublishing-forms.md#publishanasset)。 您需要先发布一个字母，然后才能将其保存为草稿，因为当您发布字母时，您会在此时创建该字母、其从属资产和数据的版本。 您或其他用户无法编辑信件的已发布版本，可以在以后恢复信件时不会与已发布版本有任何意外差异。 您可以稍后返回到此实例并从离开的位置继续。

* **提交实例**:提交实例会在提交时捕获信件的状态。提交实例存储在处理函数实例后的PDF状态以及用户在“创建通信”用户界面中输入的数据。

仅当在发布实例上查看信函时，才能保存此类实例。 默认情况下，保存实例处于关闭状态。 要启用字母实例的保存，请执行以下步骤。

1. 在AEM中，使用以下URL为您的服务器打开Adobe Experience Manager Web控制台配置：https://&lt;server>:&lt;port>/&lt;contextpath>/system/console/configMgr
1. 找到&#x200B;**[!UICONTROL Corresponse Management Configurations]**&#x200B;并单击它。
1. 选中&#x200B;**[!UICONTROL 管理Publish]**&#x200B;配置上的字母实例，然后单击&#x200B;**[!UICONTROL 保存]**。

打开字母实例的保存时，您可以选择保存字母实例的位置。 保存字母实例有两种选项：本地保存或远程保存。

### 本地保存{#local-save}

字母实例将保存在发布实例中，并在作者实例上反向复制。

### 远程保存{#remote-save}

此选项适用于担心在发布实例上保存用户数据的用户，通常情况下，在公司防火墙之外。 打开远程保存时，字母实例不会保存在发布实例中，而是远程保存在通过LiveCycle Client SDK配置指定的处理作者中。

#### 启用远程保存{#enable-remote-save}

1. 在AEM中，使用以下URL为您的服务器打开Adobe Experience Manager Web控制台配置：`https://<server>:<port>/<contextpath>/system/console/configMgr`
1. 搜索&#x200B;**[!UICONTROL Correspondence Management Configurations]**&#x200B;并单击它。
1. 找到&#x200B;**[!UICONTROL 远程保存]**&#x200B;配置，选中它，然后单击&#x200B;**[!UICONTROL 保存]**。

#### 指定处理作者设置{#specify-processing-author-settings}

1. 在AEM中，使用以下URL为您的服务器打开Adobe Experience Manager Web控制台配置：`https://<server>:<port>/<contextpath>/system/console/configMgr`

   ![Adobe Experience Manager Web控制台配置](assets/2configmanager.png)

1. 在此页上，找到Adobe LiveCycle客户端SDK配置，然后单击以展开它。

1. 在处理服务器URL中，输入LiveCycle服务器的名称，提供登录信息，然后单击&#x200B;**保存**。

   ![输入LiveCycle服务器的名称和登录信息](assets/3configmanager.png)

1. 如有必要，请设置要访问服务器的用户名和密码。

#### 附件投放{#attachmentdelivery}

* 信函附件在PDF中是可用的后期处理，PDF是在提交信函后创建的。
* 使用服务器端API将书信渲染为交互式或非交互式PDF时，渲染的PDF包含附件作为PDF附件。
* 当使用“创建通信”用户界面将与信件模板关联的后期处理作为“提交”或“完成通信”操作的一部分加载时，附件将作为AttachmentDocs参数中的列表&lt;com.adobe.idp.文档>传递。
* 开箱即用的投放机制（如电子邮件和打印）也会随生成的通信的PDF一起发送附件。

## 字母预览的再现模式：移动表单预览和PDF预览{#rendition-modes-of-letter-preview-mobile-forms-preview-and-pdf-preview}

AEM Forms Correspondence Management在“创建通信UI”中将字母显示为HTML。 但是，Correspondence Management仍支持恢复为PDF预览，而不是HTML预览。 有关在HTML和PDF模式之间切换预览的详细信息，请参阅[更改字母](#changerenditionmode)的再现模式。

以下是HTML和PDF预览中提供的优势和功能。

**移动表单/HTML预览的优势**

* **点按数据字段值以突出显示相应的数据字段**:在“创建对应”用户界面中，您可以点按字母中的数据字段值，以在“数据”选项卡中突出显示相应的数据字段。有关详细信息，请参阅[输入数据](#enterdata)。

* **浏览器支持**:浏览器逐渐支持NPAPI撤回，这会影响PDF字母预览。HTML/移动表单预览字母不受此影响。
* **突出显示字母中的可编辑内容**:在“创建对应内容”用户界面中，您可以点按“高亮显示可编辑内容”以灰色突出显示字母中的所有可编辑内容。有关详细信息，请参阅[管理内容](#managecontent)。

`<li>` `<li>Benefits of HTML preview  <ul>   <li>Right to left</li>   <li>NPAPI</li>   <li>Highlight Editable Content</li>  </ul> </li>` `<li>Benefits of PDF preview  <ul>   <li>Page Break</li>   <li>Final Preview</li>  </ul> </li>`
`<li>` `<li>Benefits of HTML preview  <ul>   <li>Right to left</li>   <li>NPAPI</li>   <li>Highlight Editable Content</li>  </ul> </li>` `<li>Benefits of PDF preview  <ul>   <li>Page Break</li>   <li>Final Preview</li>  </ul> </li>`  **PDF预览的优势**

* **分页符**:在PDF预览中，您可以准确视图字母中的分页对其输出的影响。
* **最终预览**:在PDF预览中，您可以视图字母在输出中显示时的格式和外观。

有关PDF forms中脚本支持的信息，请参阅[脚本支持](https://help.adobe.com/en_US/livecycle/11.0/ScriptingSupport/index.html)。

有关HTML5表单中脚本支持的详细信息，请参阅[HTML5表单脚本支持](/help/forms/using/scripting-support.md)。

### 更改字母{#changerenditionmode}的再现模式

默认情况下，创建对应UI使用HTML或移动表单来呈现字母预览。 移动表单预览在任何浏览器中呈现时均无问题，因为它使用浏览器的本机插件，并且不需要任何附加插件。 您可以将字母预览模式更改为PDF。 但是，浏览器限制可能会为信件的交互式PDF预览的不同功能创建问题。

有关浏览器与字母预览兼容性的详细信息，请参阅[停止NPAPI浏览器插件及其影响](https://helpx.adobe.com/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html)。

要更改字母的预览模式，请完成以下步骤：

1. 转到`https://[system]:'port'/system/console/configMgr`，如有必要，以管理员身份登录。
1. 转至&#x200B;**[!UICONTROL 对应管理配置]** > **[!UICONTROL 再现类型]**，然后选择&#x200B;**HTML再现**（默认）或&#x200B;**PDF再现**。
1. 单击&#x200B;**[!UICONTROL 保存]**。

