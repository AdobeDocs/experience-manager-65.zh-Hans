---
title: 创作移动设备应用程序
seo-title: Authoring Mobile Applications
description: AEM Mobile功能板允许您创建、构建和部署移动应用程序、创建、删除和编辑应用程序元数据。 请阅读本页以了解更多信息。
seo-description: he AEM Mobile Dashboard allows you to create, build and deploy your mobile application, create, delete and edit application metadata. Follow this page to learn more.
uuid: 293b5d29-df7e-42dd-ae64-8c677317e7a5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: abfeea65-102d-4800-abeb-304d61afcc13
exl-id: 073daff7-0c1d-4715-bfd4-3e2336e4cb88
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 0%

---

# 创作移动设备应用程序{#authoring-mobile-applications}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md).

利用AEM Mobile功能板，可创建、构建和部署移动应用程序、创建、删除和编辑应用程序元数据。 应用程序上线后，您可以分析应用程序分析，包括生命周期和使用量度，以提高客户转化和品牌忠诚度。

要构建AEM Mobile应用程序，请参阅 [构建移动设备应用程序](/help/mobile/building-app-mobile-phonegap.md) 页面。

要设置环境并开始操作，请参阅 [管理AEM以使用AEM PhoneGap Enterprise](/help/mobile/administer-phonegap.md).

## AEM Mobile应用程序目录 {#the-aem-mobile-apps-catalog}

的 [AEM Mobile应用程序目录](http://localhost:4502/aem/apps.html/content/phonegap) 显示在AEM中管理的所有移动设备应用程序。

将此目录视为AEM Mobile的“登录页面”，在该页面中，管理员可以通过基于模板创建或上传由移动设备开发人员已启动的现有应用程序来启动新的AEM Mobile应用程序。

请按照以下步骤访问应用程序目录登录页面：

1. 浏览到 **导航** 然后选择 **移动设备**.

1. 选择 **应用程序** 打开应用程序目录。

![AEM Mobile应用程序目录](assets/chlimage_1-135.png)

## AEM Mobile应用程序功能板 {#the-aem-mobile-app-dashboard}

从目录中选择AEM Mobile应用程序时，会显示其功能板。 在这里，您可以管理应用程序、查看统计信息、构建、部署和管理移动应用程序内容。

您可以展开到AEM Mobile功能板中的每个图块，以通过单击“……”来查看或编辑详细信息 在右下角。

![AEM Mobile应用程序命令中心](assets/chlimage_1-136.png)

### 管理应用程序拼贴 {#the-manage-app-tile}

“管理应用程序拼贴”会显示您的应用程序图标、名称、描述、受支持的平台、有关更新URL和版本信息的呼叫主页。 您可以深入到此区块中，以编辑和维护PhoneGap应用程序配置(config.xml)，并准备应用程序以提交到各种应用程序存储区进行分发。

单击 [此处](/help/mobile/phonegap-app-details-tile.md) 以了解详细信息。

![chlimage_1-137](assets/chlimage_1-137.png)

### 管理页面内容拼贴 {#the-manage-page-content-tile}

可以在AEM Mobile中创建、更新和删除内容，其方式与在AEM Sites中执行相同操作的方式大致相同。 的 **管理页面内容拼贴** 显示托管内容和上次修改时间的页数。 您可以通过单击拼贴中的每个记录来深入内容以创建、复制、移动、删除和更新页面。 内容更新后，您可以通过 **管理内容包拼贴。**

![内容拼贴](assets/chlimage_1-138.png)

### 管理内容包拼贴 {#the-manage-content-packages-tile}

通过管理页面内容拼贴添加或修改内容后，您便可以通过内容发布更新将这些更改推送给客户。

内容包允许AEM应用程序作者在AEM中管理页面内容，并让开发团队对您的PhoneGap Shell应用程序（即应用程序框架或基础架构）进行更改，然后将这些更改快速推送给客户，而无需让开发人员重新提交到各种商店进行分发。

内容包会为每次更新创建一个ZIP文件，该文件被视为内容发行包。 这些资源包包含在渲染应用程序时生成的html资源和html页面，并且智能到足以仅打包自上次更新以来修改的文件。

管理内容包拼贴的 **类型** 列会显示“应用程序”来表示应用程序Shell内容（例如由开发人员管理的应用程序的框架或基础结构），或显示“内容”来表示由内容作者管理的页面内容。

内容可以表示为一种语言，或表示为应用程序中使用多个内容发布包的特定部分。 如何捆绑内容的选择是灵活的，完全取决于您希望如何管理应用程序的内容。

的 **已修改** 列指示页面最近修改的时间。

的 **暂存** 列显示上次内容更新的创建时间。 要创建内容更新并暂存您所做的更改，请打开拼贴中的任何记录并创建更新。

的 **已发布** 列显示上次内容更新的发布时间，以供客户使用。 要发布内容，您必须先暂存该内容，然后通过钻取此图块并从“内容发布详细信息”控制台中发布来发布更新。

![内容发布拼贴](assets/chlimage_1-139.png) ![应用程序Shell的ContentSync包](do-not-localize/chlimage_1-5.png)

此图标表示应用程序Shell的内容发行包

![](do-not-localize/chlimage_1-6.png)

这些图标表示应用程序内容的内容发布包

### PhoneGap Build拼贴 {#the-phonegap-build-tile}

的 **PhoneGap Build拼贴** 连接 [https://build.phonegap.com](https://build.phonegap.com) 来构建和托管远程内部版本。 构建后，该内部版本即可下载获取，或通过二维码直接提供给您的设备。

或者，您也可以下载设备源，以通过 [PhoneGap CLI](https://docs.phonegap.com/en/3.5.0/guide_cli_index.md.html).

![PhoneGap Build拼贴](assets/chlimage_1-140.png)

### 量度拼贴 {#the-metrics-tile}

>[!CAUTION]
>
>只有在您配置云服务后，才会显示“量度”拼贴。
>
>请参阅 [配置AdobeMobile ServicesCloud Service](/help/mobile/configure-adobe-mobile-cloud-service.md) 以了解详细信息。

AEM Mobile通过 [AdobeMobile Services SDK](https://experienceleague.adobe.com/docs/mobile.html?lang=en) (AMS)。

控制中心 **量度拼贴** 显示从AMS中提取的应用程序概要分析。 您可以通过单击“……”来深入查看分析功能板 在右下方。

![量度拼贴](assets/chlimage_1-141.png)

### 管理实体内容拼贴 {#the-manage-entity-content-tile}

通过管理实体内容拼贴，您可以添加和管理应用程序定义。 应用程序定义是一种确定哪些空间（和其他配置）适合应用程序的方法。 这样，就可以添加新空间，而无需重新编译应用程序。 应用程序定义将会更新，其中包含任何新空间的信息。

单击 [此处](/help/mobile/phonegap-app-definitions.md) 创建和管理应用程序定义。

您可以通过单击“……”深入到管理实体内容功能板 在右下方。

![chlimage_1-142](assets/chlimage_1-142.png)

#### 其他资源 {#additional-resources}

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [使用AEM为Adobe PhoneGap企业进行开发](/help/mobile/developing-in-phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的内容](/help/mobile/administer-phonegap.md)
