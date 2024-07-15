---
title: 设置活动
description: 设置新的营销活动需要创建品牌来举办营销活动，创建营销活动来举办体验，最后定义新营销活动的属性。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 1b607a52-f065-4e35-8215-d54df7c8403d
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '2194'
ht-degree: 0%

---

# 设置活动{#setting-up-your-campaign}

设置新营销活动包括以下（通用）步骤：

1. [创建品牌](#creating-a-new-brand)以举办您的营销活动。
1. 如有必要，您可以[为新的品牌](#defining-the-properties-for-your-new-brand)定义属性。
1. [创建营销活动](#creating-a-new-campaign)以包含体验；例如，Teaser页面或新闻稿。
1. 如有必要，您可以[为新营销活动](#defining-the-properties-for-your-new-campaign)定义属性。

然后，根据您创建的体验类型，您必须[创建体验](#creating-a-new-experience)。 体验的详细信息及其创建后的操作取决于您要创建的体验类型：

* 如果创建Teaser：

   1. [创建Teaser体验](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingateaserexperience)。
   1. [将内容添加到您的Teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttoyourteaser)。
   1. [为您的Teaser创建接触点](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatouchpointforyourteaser)（将您的Teaser添加到内容页面）。

* 如果创建新闻稿：

   1. [创建新闻稿体验](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatinganewsletterexperience)。
   1. [向新闻稿添加内容。](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttonewsletters)
   1. [将新闻稿个性化。](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#personalizingnewsletters)
   1. [创建引人注目的新闻稿登陆页面](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#settingupanewsletterlandingpage)。
   1. [向订阅者或潜在客户发送新闻稿](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#sendingnewsletters)。

* 如果创建Adobe Target（以前称为Test&amp;Target）选件：

   1. [创建Adobe Target选件体验](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatesttargetofferexperience)。
   1. [与 Adobe Target 集成](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#integratewithadobetesttarget)

>[!NOTE]
>
>有关定义区段的详细说明，请参阅[分段](/help/sites-administering/campaign-segmentation.md)。

## 创建新品牌 {#creating-a-new-brand}

1. 打开&#x200B;**MCM**&#x200B;并在左窗格中选择&#x200B;**营销活动**。

1. 选择&#x200B;**新建……**&#x200B;以输入用于新品牌的&#x200B;**标题**&#x200B;和&#x200B;**名称**&#x200B;和模板：

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. 单击&#x200B;**创建**。您的新品牌将显示在MCM中（带有默认图标）。

### 定义新品牌的属性 {#defining-the-properties-for-your-new-brand}

1. 从左窗格中的&#x200B;**促销活动**，在右窗格中选择您的新品牌图标，然后单击&#x200B;**属性……**

   您可以输入&#x200B;**标题**、**描述**&#x200B;和要用作图标的图像。

   ![chlimage_1-18](assets/chlimage_1-18.png)

1. 单击&#x200B;**确定**&#x200B;进行保存。

### 创建新营销活动 {#creating-a-new-campaign}

1. 从&#x200B;**营销活动**&#x200B;中，在左窗格中选择您的新品牌，或双击右窗格中的图标。

   此时会显示概述（如果品牌是新的，则为空）。

1. 单击&#x200B;**新建……**，并指定要用于新营销活动的&#x200B;**标题**、**名称**&#x200B;和模板。

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. 单击&#x200B;**创建**。您的新营销活动将显示在MCM中。

### 定义新营销活动的属性 {#defining-the-properties-for-your-new-campaign}

配置控制行为的营销活动属性：

* **优先级：**&#x200B;此营销活动相对于其他营销活动的优先级。 当多个营销活动同时开启时，具有最高优先级的营销活动控制访客体验。
* **开启和结束时间：**&#x200B;这些属性控制促销活动控制访客体验的时段。 开启时间属性控制营销活动开始控制体验的时间。 “关闭时间”属性控制营销活动何时停止控制体验。
* **图像：**&#x200B;在AEM中表示营销活动的图像。
* **Cloud Services：**&#x200B;与促销活动集成的Cloud Service配置。 (请参阅[与Adobe Marketing Cloud集成](/help/sites-administering/marketing-cloud.md)。)

* **Adobe Target：**&#x200B;属性，用于配置与Adobe Target集成的营销活动。 (请参阅[与Adobe Target集成](/help/sites-administering/target.md)。)

1. 从&#x200B;**营销活动**&#x200B;中，选择您的品牌。 在右窗格中，选择您的营销活动，然后单击&#x200B;**属性**。

   您可以输入各种属性，包括&#x200B;**Title**、**Description**&#x200B;以及您想要的任何&#x200B;**Cloud Service**。

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. 单击&#x200B;**确定**&#x200B;进行保存。

### 创建新体验 {#creating-a-new-experience}

创建体验的过程取决于体验类型：

* [创建Teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingateaser)
* [创建新闻稿](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatinganewsletter)
* [创建Adobe Target选件](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatesttargetoffer)

>[!NOTE]
>
>与以前的版本一样，仍可以在&#x200B;**网站**&#x200B;控制台中创建体验作为页面（并且仍完全支持在以前的版本中创建的任何此类页面）。
>
>现在，建议的做法是使用MCM创建体验。

### 配置您的新体验 {#configuring-your-new-experience}

现在您已经为体验创建了基本框架，接下来需要根据体验类型继续执行以下操作：

* [Teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers)：

   * [将Teaser页面连接到访客区段。](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#applyingasegmenttoyourteaser)
   * [为您的Teaser创建接触点](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatouchpointforyourteaser)（将您的Teaser添加到内容页面）。

* [新闻稿](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters)：

   * [向新闻稿添加内容。](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttonewsletters)
   * [将新闻稿个性化。](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#personalizingnewsletters)
   * [向订阅者或潜在客户发送新闻稿](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#sendingnewsletters)。
   * [创建引人注目的新闻稿登陆页面](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#settingupanewsletterlandingpage)。

* [Adobe Target选件](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#testtargetoffers)：

   * [与 Adobe Target 集成](/help/sites-administering/target.md)

### 添加新接触点 {#adding-a-new-touchpoint}

如果您拥有现有体验，则可以直接从MCM的日历视图添加接触点：

1. 为您的营销活动选择日历视图。

1. 单击&#x200B;**添加接触点……**&#x200B;以打开对话框。 指定要添加的体验：

   ![chlimage_1-21](assets/chlimage_1-21.png)

1. 单击&#x200B;**确定**&#x200B;进行保存。

## 使用潜在客户 {#working-with-leads}

>[!NOTE]
>
>Adobe不打算进一步增强此功能（管理潜在客户）。
>建议使用[Adobe Campaign以及与AEM](/help/sites-administering/campaign.md)的集成。

在AEM MCM中，您可以通过手动输入潜在客户或导入逗号分隔的列表（例如邮件列表）来整理和添加潜在客户。 生成潜在客户的其他方法来自新闻稿注册或社区注册（如果配置，这些方法可能会触发填充潜在客户的工作流）。

通常，潜在客户会被分类并放入列表中，以便您以后可以对整个列表执行操作，例如，向特定列表发送自定义电子邮件。

在仪表板中，通过单击左窗格中的&#x200B;**潜在客户**&#x200B;来访问所有潜在客户。 您还可以从&#x200B;**列表**&#x200B;窗格访问潜在客户。

![screen_shot_2012-02-21at114748am](assets/screen_shot_2012-02-21at114748am.png)

>[!NOTE]
>
>要添加或修改用户头像，请打开点击流云(Ctrl+Alt+c)，加载配置文件，然后单击&#x200B;**编辑**。

### 创建新潜在客户 {#creating-new-leads}

创建新潜在客户后，请务必[激活它们](#activating-or-deactivating-leads)，以便您可以跟踪它们在发布实例上的活动并个性化其体验。

要人工创建销售线索，请执行以下操作：

1. 在AEM中，导航到MCM。 在仪表板中，单击&#x200B;**潜在客户**。
1. 单击&#x200B;**新建**。 将打开&#x200B;**新建**&#x200B;窗口。

   ![screen_shot_2012-02-21at115008am](assets/screen_shot_2012-02-21at115008am.png)

1. 根据需要，在字段中输入信息。 单击&#x200B;**地址**&#x200B;选项卡。

   ![screen_shot_2012-02-21at115045am](assets/screen_shot_2012-02-21at115045am.png)

1. 输入相应的地址信息。 单击&#x200B;**保存**&#x200B;以保存潜在客户。 如果需要添加其他潜在客户，请单击&#x200B;**保存并新建**。

   新销售线索将出现在“销售线索”窗格中。 单击该条目时，所有输入的信息都会显示在右窗格中。 创建潜在客户后，可将其添加到列表中。

   ![screen_shot_2012-02-21at120307pm](assets/screen_shot_2012-02-21at120307pm.png)

### 激活或停用潜在客户 {#activating-or-deactivating-leads}

激活潜在客户可帮助您跟踪他们在发布实例上的活动，并允许您个性化其体验。 当您不再希望跟踪其活动时，可以取消激活它们。

要激活或停用潜在客户，请执行以下操作：

1. 在AEM中，导航到MCM并单击&#x200B;**潜在客户**。

1. 选择要激活或取消激活的销售机会，然后单击&#x200B;**激活**&#x200B;或&#x200B;**取消激活**。

   ![screen_shot_2012-02-21at120620pm](assets/screen_shot_2012-02-21at120620pm.png)

   与AEM页面一样，发布状态显示在&#x200B;**已发布**&#x200B;列中。

   ![screen_shot_2012-02-21at122901pm](assets/screen_shot_2012-02-21at122901pm.png)

### 导入新潜在客户 {#importing-new-leads}

在导入新潜在客户时，您可以将其自动添加到现有列表中，或创建列表以包含这些潜在客户。

要从以逗号分隔的列表导入潜在客户，请执行以下操作：

1. 在AEM中，导航到MCM并单击&#x200B;**潜在客户**。

   >[!NOTE]
   >
   >或者，可通过执行以下操作之一来导入潜在客户：
   >
   >* 在仪表板中，在&#x200B;**列表**&#x200B;窗格中单击&#x200B;**导入潜在客户**
   >* 单击&#x200B;**列表**，在&#x200B;**工具**&#x200B;菜单中，选择&#x200B;**导入潜在客户**。

1. 在&#x200B;**工具**&#x200B;菜单中，选择&#x200B;**导入** **潜在客户**。

1. 按照示例数据中的说明输入信息。 可以导入以下字段：email、familyName、givenName、gender、aboutMe、city、country、phoneNumber、postalCode、region、streetAddress

   >[!NOTE]
   >
   >CSV列表中的第一行是预定义的标签，必须完全按照以下示例编写该标签：
   >
   >
   >`email,givenName,familyName` — 例如，如果写为`givenname`，系统将无法识别它。
   >
   >

   ![screen_shot_2012-02-21at123055pm](assets/screen_shot_2012-02-21at123055pm.png)

1. 单击&#x200B;**“下一个”。**&#x200B;在此，您可以预览潜在客户以确保其准确性。

   ![screen_shot_2012-02-21at123104pm](assets/screen_shot_2012-02-21at123104pm.png)

1. 单击&#x200B;**“下一个”。**&#x200B;选择要这些潜在客户所属的列表。 如果您不希望它们属于某个列表，请删除字段中的信息。 默认情况下，AEM会创建一个包含日期和时间的列表名称。 单击&#x200B;**导入**。

   ![screen_shot_2012-02-21at123123pm](assets/screen_shot_2012-02-21at123123pm.png)

   新销售线索将出现在“销售线索”窗格中。 如果单击该条目，则所有输入的信息都会显示在右窗格中。 创建潜在客户后，可将其添加到列表中。

### 将潜在客户添加到列表 {#adding-leads-to-lists}

要将潜在客户添加到预先存在的列表，请执行以下操作：

1. 在MCM中，单击&#x200B;**潜在客户**&#x200B;以查看所有可用的潜在客户。

1. 通过选中潜在客户旁边的复选框，选择要添加到列表中的潜在客户。 您可以添加任意数量的潜在客户。

   ![screen_shot_2012-02-21at123835pm](assets/screen_shot_2012-02-21at123835pm.png)

1. 在&#x200B;**工具**&#x200B;菜单中，选择&#x200B;**添加到列表....** **添加到列表**&#x200B;窗口打开。

   ![screen_shot_2012-02-21at124019pm](assets/screen_shot_2012-02-21at124019pm.png)

1. 选择要向哪个列表添加潜在客户，然后单击&#x200B;**确定**。 潜在客户将添加到相应的列表中。

### 查看潜在客户信息 {#viewing-lead-information}

要查看销售线索信息，请在MCM中单击该销售线索旁边的复选框，此时将打开一个右窗格，其中显示了所有销售线索的信息，包括列表隶属关系。

![screen_shot_2012-02-21at124228pm](assets/screen_shot_2012-02-21at124228pm.png)

### 修改现有潜在客户 {#modifying-existing-leads}

要修改现有潜在客户信息，请执行以下操作：

1. 在MCM中，单击&#x200B;**潜在客户**。 从潜在客户列表中，选中要编辑的潜在客户旁边的复选框。 所有潜在客户信息都将显示在右窗格中。

   ![screen_shot_2012-02-21at124514pm](assets/screen_shot_2012-02-21at124514pm.png)

   >[!NOTE]
   >
   >一次只能编辑一个潜在客户。 如果需要修改属于同一列表的销售线索，您可以改为修改该列表。

1. 单击&#x200B;**编辑**。 将打开&#x200B;**编辑潜在客户**&#x200B;窗口。

   ![screen_shot_2012-02-21at124609pm](assets/screen_shot_2012-02-21at124609pm.png)

1. 根据需要进行编辑，然后单击&#x200B;**保存**&#x200B;以保存更改。

   >[!NOTE]
   >
   >要更改潜在客户头像，请转到用户配置文件。 您可以通过按CTRL+ALT+c，单击&#x200B;**加载**，然后选择配置文件在Clickstream云中加载配置文件。

### 删除现有潜在客户 {#deleting-existing-leads}

要删除MCM中的现有潜在客户，请选中该潜在客户旁边的复选框，然后单击&#x200B;**删除**。 商机将从商机列表和所有相关列表中删除。

>[!NOTE]
>
>在删除之前，AEM会确认您要删除现有潜在客户。 删除后，将无法检索到它。

## 使用列表 {#working-with-lists}

>[!NOTE]
>
>Adobe不打算进一步增强此功能（管理列表）。
>建议使用[Adobe Campaign以及与AEM](/help/sites-administering/campaign.md)的集成。

列表可让您将潜在客户组织到组中。 通过列表，您可以将营销活动定位到选定的用户组，例如，您可以向列表发送定向的新闻稿。 列表在MCM中可见，无论是在功能板中还是通过单击&#x200B;**列表**&#x200B;均可。 两者都会为您提供列表名称和成员数。

![screen_shot_2012-02-21at125021pm](assets/screen_shot_2012-02-21at125021pm.png)

如果单击&#x200B;**列表**，您还可以查看该列表是否是另一个列表的成员，并查看说明。

![screen_shot_2012-02-21at124828pm](assets/screen_shot_2012-02-21at124828pm.png)

### 创建新列表 {#creating-new-lists}

1. 在MCM仪表板中，单击&#x200B;**新建列表……**，或者在&#x200B;**列表**&#x200B;中，单击&#x200B;**新建**...将打开“创建列表”窗口。

   ![screen_shot_2012-02-21at125147pm](assets/screen_shot_2012-02-21at125147pm.png)

1. 输入名称（必需），如果需要，输入说明，然后单击&#x200B;**保存**。 该列表出现在&#x200B;**列表**&#x200B;窗格中。

   ![screen_shot_2012-02-21at125320pm](assets/screen_shot_2012-02-21at125320pm.png)

### 修改现有列表 {#modifying-existing-lists}

1. 在MCM中，单击&#x200B;**列表**。

1. 从列表中，选中要编辑的列表旁边的复选框，然后单击&#x200B;**编辑**。 将打开&#x200B;**编辑列表**&#x200B;窗口。

   ![screen_shot_2012-02-21at125452pm](assets/screen_shot_2012-02-21at125452pm.png)

   >[!NOTE]
   >
   >一次只能编辑一个列表。

1. 根据需要进行编辑，然后单击&#x200B;**保存**&#x200B;以保存更改。

### 删除现有列表 {#deleting-existing-lists}

要删除现有列表，请在MCM中，选中列表旁边的复选框，然后单击&#x200B;**删除**。 该列表将被删除。 不会删除与列表关联的潜在客户，只会删除与列表关联的潜在客户。

>[!NOTE]
>
>在删除之前，AEM会确认您要删除现有列表。 删除后，将无法检索到它。

### 合并列表 {#merging-lists}

您可以将现有列表与另一个列表合并。 执行此操作时，要合并的列表将成为另一个列表的成员。 它仍作为单独的实体存在，不应删除。

如果您在两个不同的位置有相同的会议，并且希望将它们合并到所有会议的与会者列表中，则可以合并列表。

要合并现有列表，请执行以下操作：

1. 在MCM中，单击&#x200B;**列表**。

1. 通过选中列表旁边的复选框，选择要与另一列表合并的列表。

1. 在&#x200B;**工具**&#x200B;菜单中，选择&#x200B;**合并列表**。

   >[!NOTE]
   >
   >一次只能合并一个列表。

1. 在&#x200B;**合并列表**&#x200B;窗口中，选择要合并的列表，然后单击&#x200B;**确定**。

   ![screen_shot_2012-02-21at10259pm](assets/screen_shot_2012-02-21at10259pm.png)

   您合并的列表应增加一个成员。 要查看您的列表已合并，请选择已合并的列表，然后在&#x200B;**工具**&#x200B;菜单中，选择&#x200B;**显示潜在客户**。

1. 重复该步骤，直到合并所有需要的列表为止。

   ![screen_shot_2012-02-21at10538pm](assets/screen_shot_2012-02-21at10538pm.png)

>[!NOTE]
>
>从成员资格中删除合并列表与从列表中删除潜在客户相同。 打开&#x200B;**列表**&#x200B;选项卡，选择包含合并列表的列表，然后单击列表旁边的红色圆圈来移除成员资格。

### 查看列表中的潜在客户 {#viewing-leads-in-lists}

您可以随时通过浏览或搜索成员来查看哪些潜在客户属于特定列表。

要查看列表中的潜在客户，请执行以下操作：

1. 在MCM中，单击&#x200B;**列表**。

1. 选中要查看其成员的列表旁边的复选框。

1. 在&#x200B;**工具**&#x200B;菜单中，选择&#x200B;**显示潜在客户**。 AEM显示属于该列表成员的潜在客户。 您可以浏览列表或搜索成员。

   >[!NOTE]
   >
   >此外，您还可以通过选择潜在客户，然后单击&#x200B;**删除成员资格**，将其从列表中删除。

   ![screen_shot_2012-02-21at10828pm](assets/screen_shot_2012-02-21at10828pm.png)

1. 单击&#x200B;**关闭**&#x200B;以返回MCM。
