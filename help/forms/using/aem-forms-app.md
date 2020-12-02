---
title: AEM Forms应用
seo-title: AEM Forms应用
description: AEM Forms应用程序使现场工作人员能够在其移动设备上使用自适应表单。
seo-description: AEM Forms应用程序使现场工作人员能够在其移动设备上使用自适应表单。
uuid: fac976c8-b713-4492-b153-f567e7a11ceb
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e18aa345-034c-473b-b4c2-01678bb10616
translation-type: tm+mt
source-git-commit: af326f2d2b278fe36df05afc8c172f74c99a064c
workflow-type: tm+mt
source-wordcount: '2470'
ht-degree: 0%

---


# AEM Forms应用程序简介{#aem-forms-app}

## 概述 {#overview}

AEM Forms应用支持根据您的服务器在移动设备上同步自适应表单、移动表单和表单。 您可以在OSGi](/help/forms/using/aem-forms-workflow.md)上定义[以Forms为中心的工作流，或在JEE上定义Forms工作流。 例如，您运营着一家银行，并使用AEM Forms管理客户应用程序和通信。 您的客户填写表单并提交以供验证。 如果在移动设备上启用表单，客户可以在AEM Forms应用程序中填写表单。 您还可以通过在移动设备上启用验证表单来管理验证工作流。 现场工作人员可以将移动设备传送给客户，验证详细信息，并提交表单。 AEM Forms应用程序与AEM Forms服务器同步，并获取为移动设备启用的表单。 如果应用程序处于脱机状态，则它将数据存储在本地。

客户可通过软件分发获得AEM Forms应用程序的源代码。 软件分发中的源代码包可以通过以下方式获得：`adobe-aemfd-forms-app-src-pkg-<version>.zip`。

AEM Forms应用程序在iOS、Android和Windows设备上受支持。 您可以从Google Play安装适用于Android的AEM Forms应用程序，从App Store安装iOS，从Windows应用商店安装Windows。

    [ ![google_play](assets/google_play.png)](https://play.google.com/store/apps/details?id=com.adobe.aem.forms)
    
    [ ![app_store](assets/app_store.png)](https://itunes.apple.com/us/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8)
    
    [ ![microsoft-badge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/en-us/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

要在iOS、Android或Windows设备上安装、自定义和分发应用程序，请参阅[自定义、构建和分发AEM Forms应用程序](#customize-build-distribute)。

## 前提条件 {#prerequisites}

AEM Forms应用需要AEM Forms服务器。 用户可以渲染您在AEM Forms创建的表单
服务器、填写、另存为草稿并提交。 应用程序连接到服务器并从中获取已启用的表单。 AEM Forms应用程序与服务器同步，一旦表单加载到应用程序中，用户便可脱机工作。 如果应用程序处于脱机状态，则数据将保存在设备上，并且当应用程序处于联机状态时，数据将与服务器同步。

### AEM Forms应用程序(带有使用AEM Forms工作流{#aem-forms-app-with-servers-using-aem-forms-workflow}的服务器)

如果您有AEM Forms工作流服务器，则可以在AEM Forms应用程序中以任务形式呈现表单。 例如，您运营着一家银行，客户填写应用程序来使用您的服务。 该应用程序是一种自适应表单，可接受客户提供的信息并将其存储为供审阅的提交文件。 管理员审阅应用程序并将验证请求转发给现场工作者。 转发的应用程序将现场工作人员的应用程序中的验证表单作为任务启用。 现场工作人员将移动设备运送给客户并验证详细信息。

### AEM Forms应用程序，在OSGi {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}上使用以Forms为中心的工作流程

如果您有AEM Forms服务器，则可以将自适应表单渲染为AEM收件箱应用程序，并在AEM Forms应用程序中呈现任务。 例如，您运营着一家银行，客户填写应用程序来使用您的服务。 该应用程序与自适应表单关联，该表单接受客户提供的信息并将其存储为提交以供审阅。 管理员会审核任务，并批准对现场工作人员的验证请求。 现场工作人员将移动设备运送给客户并验证详细信息。

### 独立表单或AEM Forms应用程序(带有不带AEM Forms工作流的服务器){#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

未使用AEM Forms工作流的AEM Forms服务器是OSGi上的AEM Forms服务器，或者是独立的移动表单或自适应表单。 AEM Forms应用程序可与您在[OSGi](/help/sites-deploying/configuring-osgi.md)上的AEM Forms实施配合使用。 Forms，您的应用程序中提供AEM Forms应用程序的启用和发布功能。

表单将下载到您的应用程序中，并可脱机使用。 例如，您运营的是一家银行，客户填写您网站上的一个应用程序。 该应用程序是一种自适应表单，可接受客户提供的信息并将其存储以供审阅。 管理员会查看表单，并在AEM作者实例中创建验证表单。 管理员启用表单与AEM Forms应用程序同步并发布。 如果验证表单在AEM Forms应用程序中可用，您的现场代理可以使用移动设备验证客户的详细信息。 移动设备与服务器同步，验证表单加载到应用程序中。 您的现场代理可以访问您的客户、验证详细信息、将数据保存为草稿或提交验证表单。 只要应用程序处于联机状态，表单就会与服务器同步。

要在AEM Forms应用程序中同步表单：

1. 在创作实例中，选择一个表单，然后单击&#x200B;**[!UICONTROL 视图属性]**。

1. 在属性页面中，单击&#x200B;**[!UICONTROL 高级]**。
1. 在“高级”下，启用选项：**[!UICONTROL 与AEM FormsApp]**&#x200B;同步，然后点按&#x200B;**[!UICONTROL 保存]**。

发布表单后，应用程序将与服务器同步并获取表单。 要同步多个表单，请在创作实例中，在表单管理器中选择多个表单，然后点按&#x200B;**[!UICONTROL 与AEM FormsApp]**&#x200B;同步。

## 移动设备支持{#mobile-device-support}

请参阅[AEM Forms应用程序（以前称为Mobile Workspace）](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)

## AEM Forms应用程序{#key-features-of-aem-forms-app}的主要功能

### AEM Forms应用程序(AEM Forms服务器{#aem-forms-app-with-aem-forms-servers})

您可以将您的应用程序与AEM Forms服务器同步，并可在移动设备上处理表单。

借助AEM Forms工作流服务器，表单可以与工作台流程和AEM收件箱应用程序中的起始点关联。 AEM收件箱应用程序可以有一个与其关联的自适应表单。 起点可以具有与其关联的自适应表单、HTML5表单或表单集。 起点可以作为任务提交，或者任务可以另存为草稿。 有关AEM Inbox应用程序与起点之间差异的详细信息，请参阅[OSGi和AEM FormsJEE工作流上以表单为中心的AEM工作流的操作和功能](capabilities-osgi-jee-workflows.md)。

如果AEM Forms服务器没有AEM Forms工作流程，则启用在应用程序中同步的表单将在AEM Forms应用程序中呈现。 Forms位于应用程序的“Forms”选项卡中，可提交或另存为草稿。 应用程序支持自适应表单和移动表单。

1. **将任务或表单另存为草稿**

   另存为草稿选项保存任务或表单的快照以及已填写的数据以及关联表单中附加的文件。 草稿将保存到移动设备，并与AEM Forms服务器同步以备以后检索。

   请参阅[将任务或表单另存为草稿](/help/forms/using/save-as-draft.md)。

1. **将表单另存为模板**

   有时，当用户填写表单时，对几个字段的输入保持不变。 对于此类情况，您可以在每个实例中填写需要相同值的字段，并将表单或草稿另存为模板。 现在，每次创建模板实例时，指定的字段都已填写模板中指定的值。 它可以帮助您节省填写表单所需的时间和精力。

   请参阅[将表单另存为模板](/help/forms/using/save-forms-and-start-points-as-templates.md)。

### 使用任务和表单{#working-with-tasks-and-forms}

您可以将应用程序与AEM Forms工作流服务器同步，并可在移动设备上处理任务和表单。

移动设备上的任务包含自适应表单、HTML5表单或表单集，还可包含附件和[摘要URL](/help/forms/using/getting-task-variables-summary-url.md)。 默认情况下，分配给您的任务会放在&#x200B;**[!UICONTROL 任务]**&#x200B;文件夹中。 处理任务时，可以更改任务并在AEM Forms服务器上保存任务的草稿副本。

移动设备上的表单可以是自适应表单或移动表单。 Forms在表单应用程序中启用同步功能，可在Forms文件夹中找到。 您可以同步在AEM Forms服务器中启用的表单，而无需AEM Forms工作流(OSGi上的AEM Forms)。

请参阅：

* [打开任务](/help/forms/using/open-task.md)
* [使用表单](/help/forms/using/working-with-form.md)

### 脱机工作{#working-offline}

您可以在脱机模式下使用移动设备。 即使没有网络连接，您也可以登录到应用程序，并且可以处理上次联机时与设备同步的所有表单。 有关如何同步表单的详细信息，请参阅[同步应用程序](/help/forms/using/sync-app.md)。 如果选择同步与表单关联的附件，则还可以在脱机模式下打开附件。 您可以在脱机模式下编辑表单、添加批注以及提交或保存表单。 表单在您下次联机时与AEM Forms服务器同步。

有关详细信息，请参阅[在脱机模式下工作](/help/forms/using/work-offline-mode.md)。

### 添加注释{#adding-annotations}

您可以在移动设备上向表单中添加以下附件

* **备注**-您可以使用“备注”功能在表单中添加手绘或文本备注。有关详细信息，请参阅[添加注释](/help/forms/using/add-attachments.md#adding-a-note)。

* **图片**-AEM Forms应用程序包含使用相机功能或移动设备画廊的功能。使用照片附件，您可以添加具有关联表单的照片。 有关详细信息，请参阅[添加照片](/help/forms/using/add-attachments.md#adding-a-photograph)。

### 自动保存{#autosave}

当用户在AEM Forms应用程序中输入数据时，自动保存功能会定期保存数据。 AEM Forms应用程序中的自动保存功能可帮助您避免因电池电量不足等情况关闭应用程序时的数据丢失。

请参阅[在AEM Forms应用程序中使用自动保存](/help/forms/using/autosave-data-app.md)。

## AEM Inbox和AEM Forms应用程序功能之间的区别{#differences-between-aem-inbox-and-aem-forms-app-features}

启动以Forms为中心的工作流的两种主要方法是使用[AEM收件箱](/help/forms/using/manage-applications-inbox.md)和AEM Forms应用程序。 但是，AEM Inbox和AEM Forms应用程序的功能不同。 AEM Inbox只能用于[以Forms为中心的工作流](/help/forms/using/aem-forms-workflow.md)，而AEM Forms应用程序可用于以Forms为中心的工作流和流程管理。 有关AEM Inbox和AEM Forms应用程序功能之间差异的详细信息，请参阅[OSGi和AEM FormsJEE工作流上以表单为中心的AEM工作流的操作和功能](capabilities-osgi-jee-workflows.md)。

## 支持的表单{#supported-forms}

AEM Forms应用程序中支持的表单类型：

### 自适应表单 {#adaptive-form}

AEM Forms应用支持动态适应用户输入的自适应表单。 还支持延迟加载的自适应表单。

### 移动表单{#mobile-form}

您可以在AEM Forms为移动设备创建表单。 移动表单在移动设备中呈现为可根据显示设备进行调整的HTML表单。

### 表单集 {#formset}

使用表单集，可以将与服务或流程相关的多个表单进行分组，以自动处理业务流程并呈现给最终用户。 在这种情况下，用户可以将整个集合作为一个来填写，无需对单个表单或流程进行文件、提交和跟踪。

>[!NOTE]
>
>需要AEM Forms工作流(JEE上的AEM Forms)。

## AEM Forms应用程序的工作方式{#how-aem-forms-app-works}

AEM Forms应用为现场工作人员提供移动解决方案来处理分配给他们的表单。 应用程序缓存来自服务器的完整数据并通过在本地保存所有工作提供有效的用户体验。 通过及时同步更新将来自磁盘的数据发送到服务器。

AEM Forms应用是一个基于PhoneGap 5.0的应用程序，其中Backbone模型可高效地通过视图呈现存储在模型中的数据。 所有本机操作都通过PhoneGap插件执行。

## 自定义、构建和分发AEM Forms应用程序{#customize-build-distribute}

>[!NOTE]
>
>仅当您使用AEM Forms应用程序源代码构建应用程序时适用。

AEM Forms应用程序易于自定义以满足特定组织的需求。 应用程序的源代码与AEM Forms一起提供。 您可以更改源代码并构建自己的移动员工解决方案。 您还可以使用您自己的企业密钥对应用程序进行签名。

### 自定义 {#customize}

您可以为以下对象自定义您的应用程序：

**品牌**:在AEM Forms应用程序中更改应用程序图标、应用程序名称、启动图像和页面。您还可以更改文本以本地化特定区域的应用程序。 有关AEM Forms应用程序品牌的详细信息，请参阅[品牌自定义](/help/forms/using/branding-customization.md)。

**主题**:在AEM Forms应用程序用户界面中更改颜色、字体和间距等样式。有关详细信息，请参阅[主题自定义](/help/forms/using/theme-customization.md)。

**手势**:在AEM Forms应用程序用户界面中更改右轻扫和左轻扫等手势。有关详细信息，请参阅[手势自定义](/help/forms/using/gesture-customization.md)。

有关设置AEM Forms应用程序项目进行自定义的详细信息，请参阅：

* [为AEM Forms应用程序设置环境](/help/forms/using/setup-environment-mobile-workspace.md)
* [设置Visual Studio项目并构建Windows应用程序](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [设置Xcode项目并构建iOS应用程序](/help/forms/using/setup-xcode-project-build-installer.md)
* [设置Eclipse项目并构建Android应用程序](/help/forms/using/setup-eclipse-project-build-installer.md)

### 构建和分发{#build-and-distribute}

可以从`adobe-lc-mobileworkspace-src.zip`中提取AEM Forms应用程序的源代码，该代码作为软件分发上AEM Forms应用程序源包的一部分提供。

要获取AEM Forms应用程序源，请执行以下步骤：

1. 打开[软件分发](https://experience.adobe.com/downloads)。 您需要Adobe ID才能登录软件分发。
1. 点按标题菜单中的&#x200B;**[!UICONTROL Adobe Experience Manager]**。
1. 在&#x200B;**[!UICONTROL 过滤器]**&#x200B;部分中：
   1. 从&#x200B;**[!UICONTROL 解决方案]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL Forms]**。
   2. 选择包的版本和类型。 您还可以使用&#x200B;**[!UICONTROL 搜索下载]**&#x200B;选项筛选结果。
1. 点按适用于您的操作系统的程序包名称，选择&#x200B;**[!UICONTROL 接受EULA条款]**，然后点按&#x200B;**[!UICONTROL 下载]**。
1. 打开[包管理器](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html)并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
1. 选择软件包，然后单击&#x200B;**[!UICONTROL 安装]**。

**对于iOS**:

有关如何创建iOS应用程序(.ipa)的详细信息，请参阅[设置Xcode项目并构建iOS应用程序](/help/forms/using/setup-xcode-project-build-installer.md)。

有关如何使用您的供应用户档案对AEM Forms应用程序进行签名的详细信息，请参阅[iOS代码签名设置、流程和疑难解答](https://developer.apple.com/support/code-signing/)。

**对于Android**:

有关如何创建Android应用程序(.apk)的详细信息，请参阅[设置Eclipse项目并构建Android应用程序](/help/forms/using/setup-eclipse-project-build-installer.md)。

有关如何对AEM Forms应用程序进行签名的详细信息，请参阅[对应用程序进行签名](https://developer.android.com/tools/publishing/app-signing.html)。

**对于Windows**:

有关如何创建Windows应用程序(.appx)的详细信息，请参阅[设置Visual Studio项目并构建Windows应用程序](/help/forms/using/setup-visual-studio-project-build-installer.md)。

有关如何通过MDM分发应用程序的详细信息，请参阅[分发AEM Forms应用程序](/help/forms/using/distribute-mobile-workspace-app.md)。 通过MDM分发应用程序仅适用于iOS和Android。

## Recommendations将将移动工作区升级到AEM Forms应用程序{#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

如果您要升级到最新版AEM Forms应用程序，请确保阅读以下内容：

* **如果您从Android上的play store安装了该应用程序的早期版**
本，则可以直接从play store升级该应用程序。

* **如果应用程序的早期版本是使用源代码构建和安装的（适用于iOS和Android）**:

   安装新应用程序前，请将所有数据与AEM Forms服务器同步。 同步数据后，请卸载应用程序的早期版本，然后安装新应用程序。

