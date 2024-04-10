---
title: 在生产就绪模式下运行AEM
description: 了解如何在生产就绪模式下运行AEM。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 3c342014-f8ec-4404-afe5-514bdb651aae
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 3%

---

# 在生产就绪模式下运行AEM{#running-aem-in-production-ready-mode}

通过AEM 6.1，Adobe引入了新的 `"nosamplecontent"` 运行模式，旨在自动执行准备AEM实例以在生产环境中部署所需的步骤。

新的运行模式不仅会自动配置实例以遵循安全核对清单中所述的安全最佳实践，还会在此过程中删除所有示例Geometrixx应用程序和配置。

>[!NOTE]
>
>由于实际的原因，AEM生产就绪模式将仅涵盖保护实例所需的大多数任务，因此强烈建议您查阅 [安全核对清单](/help/sites-administering/security-checklist.md) 在生产环境上线之前。
>
>另请注意，以生产就绪模式运行AEM将有效地禁用对CRXDE Lite的访问。 如果您出于调试目的而需要它，请参阅 [在AEM中启用CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

![chlimage_1-83](assets/chlimage_1-83a.png)

要在生产就绪模式下运行AEM，您必须添加 `nosamplecontent` 通过 `-r` 运行模式切换到现有的启动参数：

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

例如，您可以使用生产就绪启动具有MongoDB持久性的创作实例，如下所示：

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## 更改部分生产就绪模式 {#changes-part-of-the-production-ready-mode}

更具体地说，当AEM以生产就绪模式运行时，将执行以下配置更改：

1. 此 **CRXDE支持捆绑包** ( `com.adobe.granite.crxde-support`)在生产就绪模式下默认处于禁用状态。 可以随时从Adobe的公共Maven存储库安装它。 AEM 6.1需要版本3.0.0。

1. 此 **Apache Sling对存储库的简单WebDAV访问** ( `org.apache.sling.jcr.webdav`)包将仅在 **作者** 实例。

1. 新创建的用户需要在首次登录时更改密码。 这不适用于管理员用户。
1. **生成调试信息** 已为禁用 **Apache Sling JavaScript处理程序**.

1. **映射的内容** 和 **生成调试信息** 已禁用 **Apache Sling JSP脚本处理程序**.

1. 此 **Day CQ WCM过滤器** 设置为 `edit` 日期 **作者** 和 `disabled` 日期 **发布** 实例。

1. 此 **AdobeGraniteHTML库管理器** 进行了以下设置：

   1. **缩小：** `enabled`
   1. **调试：** `disabled`
   1. **Gzip：** `enabled`
   1. **计时：** `disabled`

1. 此 **Apache SlingGETServlet** 设置为默认支持安全配置，如下所示：

| **配置** | **作者** | **Publish** |
|---|---|---|
| TXT演绎版 | 已禁用 | 已禁用 |
| HTML演绎版 | 已禁用 | 已禁用 |
| JSON演绎版 | 已启用 | 已启用 |
| XML演绎版 | 已禁用 | 已禁用 |
| json.maximumresults | 1000 | 100 |
| 自动索引 | 已禁用 | 已禁用 |
