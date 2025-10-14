---
title: '[!DNL Experience Manager Assets]与 [!DNL Adobe Workfront]集成'
description: ' [!DNL Assets] 和 [!DNL Workfront]之间的集成简介'
role: Admin,Leader,Architect
feature: Workfront Integrations and Apps
exl-id: 57e2bffe-8094-4557-99c8-7b482681687e
hide: true
solution: Experience Manager, Workfront
source-git-commit: 5ccac0aadce3971e66da052d393cbd33b61e94f7
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 9%

---

# [!DNL Adobe Experience Manager Assets]与[!DNL Adobe Workfront]集成 {#assets-integration-overview}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-integrations.html?lang=zh-Hans) |
| AEM 6.5 | 本文 |

[!DNL Adobe Workfront]是一个工作管理应用程序，它帮助您在一个地方管理整个工作生命周期。 [!DNL Workfront]和[!DNL Adobe Experience Manager Assets]之间的集成使组织能够通过将工作和数字资产管理内在地连接起来，提高内容速度和上市时间。 在Workfront中管理其工作的情况下，用户有权访问所需的文档和图像。

[!DNL Workfront for Experience Manager enhanced connector]支持具有端到端工作流的增强业务流程，并提供个性化的端到端客户端体验和中央存储。 Adobe提供了一个标准连接器和一个增强型连接器，用于集成这两个解决方案。 查看以下支持的功能以进行比较，并查看[&#x200B; [!DNL enhanced connector]](https://one.workfront.com/s/csh?context=2467&pubname=the-new-workfront-experience)中的新增功能。

[!DNL Workfront for Experience Manage enhanced connector]使您的组织能够：

* 在Workfront中自动创建链接的Experience Manager文件夹，并根据WorkfrontPortfolio、程序和项目整理这些文件夹。
* 将Workfront项目元数据与链接的Experience Manager文件夹同步。
* 使用新版本Experience Manager元数据更新。
* 使用Experience Manager工作流根据可配置条件设置Workfront对象状态。
* 将Publish资源用于Experience Manager发布环境或Brand Portal。

查看增强型连接器的平台支持和[先决条件](https://one.workfront.com/s/csh?context=2467&pubname=the-new-workfront-experience)。

>[!IMPORTANT]
>
>* Adobe仅需要通过认证合作伙伴或[!DNL Adobe Professional Services]来部署和配置[!DNL Adobe Workfront for Experience Manager enhanced connector]。 如果未使用认证合作伙伴或[!DNL Adobe Professional Services]进行部署和配置，则Adobe不支持该功能。
>
>* Adobe可能会发布使此连接器冗余的[!DNL Adobe Workfront]和[!DNL Adobe Experience Manager]更新；如果发生这种情况，客户可能需要从使用此连接器过渡。
>
>* Adobe支持增强型连接器版本1.7.4及更高版本。 不支持以前的预发行版和自定义版本。 要检查增强型连接器版本，请导航到[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hans)的左窗格中可用的`digital.hoodoo`组。
>
>* 查看Experience Manager Assets增强型连接器的[Workfront合作伙伴认证考试](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)。 有关考试的信息，请参阅[考试指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/)。

## 比较[!DNL Assets]和[!DNL Workfront]之间的不同集成 {#feature-parity-matrix}

以下是[!DNL Assets]和[!DNL Workfront]之间通过各种集成类型提供的功能的详细信息。

| 专题 | 描述 | [!DNL Workfront]和[!DNL Assets Essentials] *无连接器（现成）* | [!DNL Workfront for Experience Manager enhanced connector] *需要连接器* | Workfront和[!DNL Experience Manager as a Cloud Service] *无连接器（现成）* |
|----|----|----|-----|-----|
| 部署方法 | 适用于哪个[!DNL Assets]产品。 | Assets Essentials | AdobeManaged Services，内部部署 | Cloud Service |
| **常规** |
| 将数字文件从[!DNL Workfront]发送到[!DNL Assets] | WF文档的最新版本可以上传到AEM Assets，该版本作为文档的新版本链接。 | ✓ | ✓ | ✓ |
| 手动将AEM文件夹链接到Workfront对象 | 现有AEM文件夹可以链接为Workfront文件夹，其子资产可以链接为新的Workfront文档。 | ✓ | ✓ | ✓ |
| 将[!DNL Assets]链接到Workfront对象 | AEM中的现有资源可以链接到新的Workfront文档，或作为现有文档的新版本。 | ✓ | ✓ | ✓ |
| 添加到链接文件夹的Assets会自动发送到AEM | 如果将文档添加到链接的文件夹，则会自动将关联的资源作为新资源上传到AEM Assets。 | ✓ | ✓ | ✓ |
| 从Workfront下载链接的AEM Assets | 在Workfront中链接资源时，用户可以下载资源的字节。 | ✓ | ✓ | ✓ |
| 在Workfront中搜索AEM Assets | Workfront中的AEM Assets选择器允许全文搜索资源。 | ✓ | ✓ | ✓ |
| 在Workfront中搜索AEM文件夹 | Workfront中的AEM Assets选择器允许全文搜索文件夹。 | ✓ | ✓ | ✓ |
| 在Workfront中查看和导航AEM文件夹层次结构 | Workfront中的AEM Assets选择器允许浏览受限制的AEM Assets层级。   用户在AEM中设置的关联访问控制和权限。 | ✓ | ✓ | ✓ |
| 在AEM时间线中跟踪资源版本 | 维护Workfront和AEM之间的文档版本历史记录。 | ✓ | ✓ | ✓ |
| 在Workfront中从AEM Assets取消Assets的链接 | 可以取消关联Workfront文档中来自AEM的现有链接资源的链接。 这不会删除AEM中的原始资源。 | ✓ | ✓ | ✓ |
| 将新版本化的资源从Workfront添加到AEM Assets | 在Workfront的文档中添加新添加的版本时，用户可以向AEM发送新版本以替换现有版本。 | ✓ | ✓ | ✓ |
| 单击直接用户访问AEM时Workfront中链接的Assets | 用户将被定向到AEM，以便在Workfront中预览链接的资源。 | ✓ | ✓ | 近期 |
| 在Workfront中自动创建链接的AEM文件夹 | 使用项目状态在Workfront中自动创建链接的AEM文件夹。 根据WorkfrontPortfolio、程序和项目自动配置AEM文件夹。 | 否 | ✓ | 否 |
| 从Workfront直接导航到AEM存储库 | 允许用户导航到在Workfront中配置的可用AEM存储库。 | ✓ | 否 | ✓ |
| 在Workfront中创建链接的AEM文件夹 | 使用“文档”选项卡中提供的选项，在Workfront中手动创建链接的AEM文件夹。 | ✓ | 否 | ✓ |
| 评论同步 | 自动将资源注释从[!DNL Workfront]同步到[!DNL Assets] | 否 | ✓ | 否 |
| 支持多个Workfront环境连接到单个AEM环境 | 来自多个Workfront环境的用户可以连接到单个AEM环境。 | ✓ | 否 | ✓ |
| 支持多个AEM环境连接到单个Workfront环境 | 单个Workfront环境中的用户可以在多个AEM环境之间发送或链接资源。 | ✓ | ✓ | ✓ |
| **元数据** |
| 将Workfront资源元数据映射到AEM Assets | Workfront对象和自定义表单属性可以映射到AEM资源元数据属性。 值在初始上传/链接时推送。 | ✓ | ✓ | ✓ |
| 在Workfront中自动创建文档自定义Forms | 使用AEM工作流将自定义表单附加到Workfront文档、任务和问题。 | 否 | ✓ | 否 |
| AEM Assets和Workfront之间的元数据双向自动更新 | 在AEM Assets和Workfront之间自动更新元数据。 资源最初必须从Workfront推送到AEM，并且Workfront资源元数据必须映射到AEM资源，才能正确进行双向元数据更新。 | 否 | ✓ | 否 |
| Workfront中的将元数据映射到AEM的实时视图 | 在Workfront的“文档详细信息”和“文档摘要”面板中，查看更新后的映射到AEM的元数据。 | ✓ | 否 | ✓ |
| 将更新的Workfront元数据实时推送到AEM | 自动将映射的Workfront元数据更新到AEM，而无需重新推送资源或资源的新版本。 | ✓ | 否 | ✓ |
| 将Workfront元数据映射到AEM Assets文件夹 | 将Workfront项目元数据与链接的AEM文件夹同步。 | 否 | ✓ | ✓ |
| 新版本的AEM元数据更新 | 可以对AEM进行配置，以确定Workfront中新版本化的资源是否也会推送对其元数据所做的任何更改。 | 否 | ✓ | 否 |
| 在Workfront中更改自定义Forms时自动更新AEM元数据 | AEM允许您订阅Workfront中文档表单的更新。 因此，对Workfront文档自定义表单元数据的任何更新都会编辑映射的AEM元数据字段的值。 | 否 | ✓ | 否 |
| **工作流（现成）** |
| 在链接的Assets上创建新验证版本 | 在Workfront中关联资源时，可以自动生成验证。 | 否 | 自定义 | 否 |
| 在Workfront对象上设置状态 | 使用AEM工作流基于可配置条件设置Workfront对象状态 | 否 | ✓ | 近期 |
| Publish Assets到AEM Publish Environment或Brand Portal | 为Workfront用户提供了将链接的资源自动发布到AEM Publish环境或Brand Portal的选项。 | 否 | ✓ | 近期 |
