---
title: 将资源导入和导出到AEM Forms
seo-title: Importing and exporting assets to AEM Forms
description: 您可以从中导入自适应表单和模板，也可以从中将其导出到AEM实例。 这有助于迁移表单或跨系统移动表单。
seo-description: You can import and export adaptive forms and templates from and in to AEM instances. This helps in migrating forms or moving them across systems.
uuid: 937daedd-56f3-4e02-b695-b194b494d9bf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 69210727-dde3-495a-87b7-2e8173e6b664
docset: aem65
role: Admin
exl-id: b5f6a54e-92d1-4631-a1d1-184f37d174b6
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '2511'
ht-degree: 0%

---

# 将资源导入和导出到AEM Forms{#importing-and-exporting-assets-to-aem-forms}

您可以在不同AEM Forms实例之间移动表单和相关资源、主题、数据字典、文档片段和字母。 将系统迁移或将表单从暂存服务器移动到生产服务器时，需要执行此类移动。 对于支持通过AEM Forms UI上传和导入的资源，建议使用Forms UI进行导出或导入。 不建议使用AEM包管理器导出或导入此类资源。

>[!NOTE]
>
>* 在AEM 6.4 Forms中，crx-repository的结构和路径发生了更改。 如果您将资源从早期版本导入AEM 6.4 Forms，并且表单与早期结构存在某些依赖关系，则必须手动导出这些依赖关系。 有关存储库结构和路径中更改的详细信息，请参阅 [AEM中的存储库重组](/help/sites-deploying/repository-restructuring.md).
>

## 下载或上传Forms &amp; Documents资源 {#download-or-upload-forms-amp-documents-assets}

通过AEM Forms用户界面，可将资源下载为AEM CRX包或二进制文件，从而从AEM实例导出资源。 然后，您可以将下载的AEM CRX包或二进制文件导入到另一个AEM实例中。

除自适应表单模板和自适应表单内容策略之外，所有资源都支持通过AEM Forms用户界面导出和导入。 因此，在从AEM Forms UI导出自适应表单时，不会像其他相关的资源一样自动导出相关的自适应表单模板和内容策略。

对于这些资源类型，必须使用AEM包管理器在源AEM服务器上创建CRX包，并在目标服务器上安装该包。 有关创建和安装软件包的信息，请参见 [使用包](/help/sites-administering/package-manager.md).

### 下载Forms和文档资源 {#download-forms-amp-documents-assets}

要下载Forms和文档资源，请执行以下操作：

1. 登录到AEM Forms实例。
1. 点按Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 图标>导航 ![指南针](assets/compass.png) 图标> Forms > Forms和文档。
1. 选择表单资产并点按 **下载** 图标。
1. 在下载资产中，选择以下选项之一，然后点按 **下载**.

   * **下载为CRX包：** 使用相关选项下载所有选定的资源和相关依赖项，并将其从AEM Forms实例移动到另一个实例。 它将所有资源和文件夹下载为crx包。 任何表单资源(包括在AEM中创作的表单（自适应表单、交互式通信和自适应表单片段）、表单集、表单模板、PDF文档和资源（XSD、XFS、图像）都可以从AEM Forms UI中作为包下载。
将资源下载为包的优势在于，它还可以下载选定要下载的资源已使用的资源。 例如，如果您有一个自适应表单，该表单使用表单模板、XSD和图像。 当您选择此自适应表单并将其下载为包时，下载的包中还包含表单模板、XSD和图像。 与资源关联的所有元数据属性（包括自定义属性）也会下载。

   * **将资产下载为二进制文件：** 使用选项可仅下载表单模板(XDP)、PDF forms(PDF)、文档(PDF)和资源（图像、架构、样式表）。 您可以使用外部应用程序编辑这些资源。 它将具有二进制文件的表单资源(如XSD、XDP、图像、PDF和XDP)下载为.zip文件。
您无法使用以下内容下载自适应表单、交互式通信、自适应表单片段、主题和表单集 **将资产下载为二进制文件** 选项。 要下载这些资源，您应使用 **下载为CRX包** 选项。

   选定的资产将下载为存档（.zip文件）。

   >[!NOTE]
   >
   >AEM包和二进制文件都将作为存档（.zip文件）下载。 资产的模板不会与资产一起下载。 您需要单独导出资产模板。

### 上传Forms和文档资源 {#upload-forms-amp-documents-assets}

要上传Forms和文档资源，请执行以下操作：

>[!VIDEO](https://vimeo.com/)

1. 登录到AEM Forms实例。
1. 点按Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 图标>导航 ![指南针](assets/compass.png) 图标>Forms>Forms和文档。
1. 点按 **创建** >**文件上传**. 此时会显示上传表单或资源包对话框。
1. 在对话框中，浏览并选择要导入的软件包或存档。 您还可以选择PDF文档、XSD、图像、样式表和XDP表单。 点按 **打开**. 您选择的文件夹或文件名不得包含任何特殊字符。

   在对话框中，验证要上传的资源的详细信息，然后点击 **上传**.

   如果上传现有的表单资源，则会更新该资源。

   >[!NOTE]
   >
   >上传包不会替换现有文件夹层次结构。 例如，如果您在一台服务器上的位置/content/dam/formsanddocuments具有一个名为“Training”的自适应表单。 您下载自适应表单并将表单上传到其他服务器。 第二台服务器还在同一位置/content/dam/formsanddocuments具有一个名为“Training”的文件夹。 上传失败。

## 下载或上传主题 {#downloading-or-uploading-a-theme}

通过AEM Forms，您可以创建、下载或上传主题。 创建主题的方式与创建表单、文档和信件等其他资产类似。 您可以创建主题，下载主题，然后将其上传到单独的实例上以重复使用。 有关主题的更多信息，请参阅 [AEM Forms中的主题](../../forms/using/themes.md).

### 下载主题 {#downloading-a-theme}

您可以在AEM Forms中导出可用于其他项目或实例的主题。 AEM允许您将主题下载为zip文件，并可在实例上上上传。

要下载主题，请执行以下操作：

1. 登录到AEM Forms实例。
1. 点按Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 图标>导航 ![指南针](assets/compass.png) 图标>Forms>主题。
1. 选择主题并点按 **下载**. 主题将下载为存档（.zip文件）。

### 上传主题 {#uploading-a-theme}

您可以在项目中将创建的主题与样式预设一起使用。 您可以通过将其他人创建的主题包上传到您的项目来导入这些主题包。

要上传主题，请执行以下操作：

1. 在Experience Manager中，导航到 **Forms >主题**.
1. 在“主题”页面中，单击 **“创建”>“文件上传”**.
1. 在“文件上传”提示符下，浏览并选择计算机上的主题包，然后单击 **上传**.
上传的主题可在主题页面中找到。

1. 登录到AEM Forms实例。
1. 点按Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 图标>导航 ![指南针](assets/compass.png) 图标>Forms>主题。
1. 单击 **创建** > **文件上传**. 在“文件上传”提示符下，浏览并选择计算机上的主题包，然后单击 **上传**. 主题已上传。

## 在通信管理中导入和导出资源 {#import-and-export-assets-in-correspondence-management}

要在两个不同的通信管理实施之间共享资产（如数据字典、信件和文档片段），您可以创建和共享.cmp文件。 .cmp文件可以包含一个或多个数据字典、字母、文档片段和表单。

### 导出文档片段、信件和/或数据字典 {#export-document-fragments-letters-and-or-data-dictionaries}

1. 在信件、文档片段或数据字典页面中，点按并选择要导出到单个包的资产，然后点按队列以供下载。 资源已排队准备导出。
1. 根据需要，重复上述步骤以添加字母、文档片段和数据字典。
1. 点按 **下载**.
1. 通信管理会显示“下载资产”对话框，其中包含导出列表中的资产列表。

   ![导出](assets/export.png)

1. 要查看导出的依赖项，请点按“解析”。 或者跳到下一步。 即使不点击“解析”，依赖关系仍会导出。
1. 要下载.cmp文件，请点击 **确定**.
1. 通信管理会将.cmp文件下载到您的计算机。

   .cmp文件包含导出的资产。 您可以与其他人共享.cmp文件。 其他用户可以在其他服务器中导入.cmp文件，以获取新服务器中的所有资源。

### 将所有相应的管理资产导出为资源包 {#export-all-the-correspondence-management-assets-as-a-package}

使用此选项可以从AEM Forms实例中作为包下载所有相应的管理资源和相关依赖项。

例如，如果通信管理具有一个使用图像和文本的字母，则下载的包还包含与字母相关的图像和文本。 与资源关联的所有元数据属性（包括自定义属性）也会下载。 下载包(.cmp)后，您可以 [将资源包导入其他AEM Forms实例](../../forms/using/import-export-forms-templates.md#p-upload-forms-documents-assets-p).

要将所有相应的管理资产和相关依赖项下载为包，请完成以下步骤：

1. 以表单用户身份登录AEM Forms服务器。
1. 点按 **Adobe Experience Manager** 在全局导航栏中。
1. 点按工具( ![工具](assets/tools.png))，然后点击 **Forms**.
1. 点按 **导出相应的管理资源**.

   ![publish-cmp-assets-1](assets/publish-cmp-assets-1.png)

   (“导出所有通信管理资产”页面出现，其中显示有关上次尝试导出过程的信息以及下载上次成功导出的包的链接。

   ![export-last-run-details](assets/export-last-run-details.png)

1. 点按 **导出** 然后，在确认消息中，点击 **确定**.

   批处理完成后，将更新上次运行详细信息和下载包的链接。 这包括管理员登录信息以及批处理是否成功运行的信息。 资产将导出到资源包，并显示“下载导出的资源包”链接。

   >[!NOTE]
   >
   >导出所有资产流程一旦启动便无法取消。 此外，在导出所有操作的过程中，请勿创建、删除、修改或发布任何资产，也不要启动发布所有资产流程。a

1. 点按 **下载导出的包** 用于下载包文件的链接。

   要将包中的资产添加到通信管理的另一个实例， [将资源包导入到AEM Forms实例](../../forms/using/import-export-forms-templates.md#p-upload-forms-documents-assets-p).

### 将文档片段、信件和/或数据字典导入通信管理 {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

您可以导入导出到.cmp文件中的资产。 .cmp文件可以包含一个或多个字母、数据字典、文档片段和从属资源。

>[!NOTE]
>
>在导入旧的通信管理资产以进行迁移时，请使用管理员帐户登录。 有关迁移旧通信管理资产的更多信息，请参阅 [将相应的管理资源迁移到AEM 6.1表单](/help/forms/using/migration-utility.md).

1. 在数据字典、字母或文档片段页面上，点按 **“创建”>“文件上传”** 并选择.cmp文件。
1. 通信管理会显示“导入资源”对话框，其中包含已导入的资源的列表。 点按 **导入**.

   导入资产后，资产的以下属性将更新，而其他属性将保持不变：

   * 作者：显示将资产导入服务器的用户的ID
   * 已修改：将资产导入服务器的时间

   >[!NOTE]
   >
   >为了能够上传XDP（作为cmp文件的一部分或其他内容），您需要成为forms-power-users组的一部分。 有关访问权限，请联系管理员。

## 导出工作流应用程序 {#export-a-workflow-application}

您可以使用AEM包管理器导出工作流应用程序。 此过程如下所示：

1. 打开AEM Forms包管理器。 包管理器的URL为https://&lt;server>：&lt;port>/crx/packmgr.
1. 单击 **[!UICONTROL 创建包]**. 此 **[!UICONTROL 新建包]** 对话框。
1. 指定包的名称、版本和组。 单击&#x200B;**[!UICONTROL 确定]**。
1. 单击 **[!UICONTROL 编辑]** 然后打开 **[!UICONTROL 过滤器]** 选项卡。 单击 **[!UICONTROL 添加筛选器]**. 指定工作流应用程序的路径。 例如，/etc/fd/dashboard/startpoints/homemortgage。 单击 **[!UICONTROL 添加规则]**.

1. 打开&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。选择 **[!UICONTROL 合并]** 或 **[!UICONTROL 覆盖]** 在ACL处理字段中。 单击&#x200B;**[!UICONTROL 保存]**。
1. 单击 **[!UICONTROL 生成]** 以创建包。

   生成包后，您可以下载包并将其导入其他服务器。 工作流应用程序会出现在上传包的服务器上。

   >[!NOTE]
   >
   >为使工作流应用程序正常工作，还要将相应的自适应表单和工作流模型导出到工作应用程序。

## 文件夹和组织资源 {#folders-and-organizing-assets}

AEM Forms用户界面使用文件夹来排列资源。 这些文件夹用于排列在AEM Forms用户界面中创建的资源。 您可以重命名、创建子文件夹并将资源和文档存储在这些文件夹中。 通过将文档和资产组织到文件夹中，您可以将文件分组在一起以便于管理。 您可以选择文件夹，然后选择下载或删除该文件夹。

要创建文件夹，请完成以下步骤：

### 创建文件夹 {#create-a-folder}

1. 登录到AEM Forms用户界面，网址为 `https://<server>:<port>/aem/forms.html`.
1. 导航到要创建文件夹的位置。
1. 点按创建>文件夹。
1. 输入以下详细信息：

   * **标题：** 文件夹的显示名称
   * **名称：** *（必需）* 要在存储库中存储文件夹的节点名称

   >[!NOTE]
   >
   >默认情况下，“名称”字段的值会自动从标题中填充。 名称只能包含字母数字字符，或连字符(-)和下划线(_)特殊字符。 在标题中输入的任何其他特殊字符都会自动替换为连字符，并提示您确认新名称。 您可以选择使用建议的名称继续操作或进一步编辑它。

1. 具有您定义的标题的新文件夹将显示在资产列表中的当前位置。

   如果存在具有指定名称的文件夹，则提交会失败并出现错误。 您可以通过将鼠标悬停在错误上来查看错误消息 ![aem6forms_error_alert](assets/aem6forms_error_alert.png) 显示在“名称”字段旁边的图标。

   您可以点按新创建的文件夹，以进入该文件夹，并在该文件夹中创建资产或文件夹。 此外，您还可以选择一个文件夹，并选择将该文件夹排入下载队列、删除或编辑其名称。

   ![editdeletedownloadafolder](assets/editdeletedownloadafolder.png)

### 创建一个或多个资源或信件的副本 {#create-copies-of-one-or-more-assets-or-letters}

您可以使用现有资源和信件快速创建具有相似属性、内容和继承资源的资源和信件。 您可以复制并粘贴数据字典、文档片段和字母。

完成以下步骤以创建资产和信件的副本：

1. 在相关的资产或信件页面中，选择一个或多个资产/信件。 UI会显示复制图标。
1. 点按复制。UI将显示“粘贴”图标。 在粘贴之前，您还可以选择在文件夹内进行导航/导航。 不同的文件夹可以包含具有相同名称的资源。 有关文件夹的详细信息，请参阅 [文件夹和组织资源](#folders-and-organizing-assets).
1. 点按粘贴。 将显示“粘贴”对话框。 系统会自动为资产/信函的新副本生成名称和标题，但您可以编辑资产/信函的标题和名称。

   如果您将资产/信件复制并粘贴到同一位置，则会将后缀“ — CopyXX”添加到资产/信件的现有名称中。 如果复制的资产/信件不存在标题，则自动生成的标题字段将保持空白。

1. 如果需要，请编辑要用于保存资产/信件副本的标题和名称。
1. 点按粘贴。 将创建复制资产的新副本。

## 搜索 {#search-forms}

通过AEM Forms UI，您可以搜索内容。 使用顶部栏，您可以点按搜索 **[A]** 在内容中搜索资源和文档。

搜索资源时，AEM Forms会显示侧面板。 您也可以点按 ![assets-browser-content-only](assets/assets-browser-content-only.png) >筛选器 **[B]** 以调用侧面板。 使用侧面板中的各种过滤器，可以缩小搜索范围。 侧面板还允许您保存搜索。

![search_topbar](assets/search_topbar.png)

**答：** Search **B.** 筛选

![侧面板 — 过滤器](assets/search_sidepanel.png)

侧面板 — 过滤器

在侧面板上，您可以使用以下内容缩小搜索结果的范围：

* 搜索目录
* 标记
* 搜索条件；例如，修改日期、发布状态、LiveCopy状态。

侧面板还允许您使用所选名称保存搜索设置。

有关使用搜索、过滤器、保存的搜索和侧面板的更多信息和说明，请参阅 [Search](/help/sites-authoring/search.md).
