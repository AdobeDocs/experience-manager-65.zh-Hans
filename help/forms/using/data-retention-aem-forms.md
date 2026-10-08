---
title: AEM Forms中的数据保留
description: 了解Adobe Experience Manager (AEM) Forms在默认情况下如何充当传递服务器，并且不会存储支持数据隐私的最终用户数据。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin, User
solution: Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ca1448119778a2bcfeca7189aab5b360d992d99d
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 0%
---
# AEM Forms中的数据保留 {#data-retention-in-aem-forms}

AEM Forms是否存储表单数据？ 默认情况下，不会。 Adobe Experience Manager (AEM) Forms充当通过Adaptive Forms捕获的数据的传递服务器，不会将最终用户数据存储在AEM存储库中。 相反，服务器会将提交的数据传递到您拥有并配置的目标。 此默认行为可帮助您实现数据隐私和合规目标，适用于OSGi上的AEM Forms和JEE上的AEM Forms 。

由于AEM Forms是一个可扩展的平台，因此您可以自定义AEM以更改此默认行为。 如果您的自定义设置将通过自适应表单提交的数据存储在AEM存储库中或写入AEM日志，则必须确保此类数据不会保留在生产系统和暂存系统中。

## 具有现成功能的默认行为 {#default-behavior}

当您使用现成的自适应Forms功能时，AEM Forms不会存储最终用户数据。 服务器会将提交的数据直接传递到您拥有并配置的目标位置。

将表单连接到您拥有目标的现成机制包括表单数据模型(FDM)、现成连接器和提交操作。 由于其中的每个报表都会将数据发送到您拥有并配置的位置，因此不会保留在AEM存储库中。 表单还可以从规则或提交操作调用外部或第三方服务（例如REST API），并在不将数据保留在AEM上的情况下将数据转发到该服务。

如果您使用AEM工作流和涉及审批步骤的长时间流程，AEM Forms可能会将数据保存在内存和临时存储中，以完成操作。 有关如何阻止将此数据保存在AEM上的信息，请参阅[长期工作流中的数据](#long-lived-workflow-processes)部分。

Forms Portal提交操作会保留通过自适应Forms捕获或提交的数据，但会将数据保存到您提供并拥有的存储位置，而不保存在AEM存储库或日志中。 有关详细信息，请参阅[表单门户保存的安全数据提交操作](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-data-saved-by-forms-portal-submit-action)。

## 正在传输的数据 {#data-in-transit}

尽管AEM Forms默认不会存储最终用户数据，但数据仍会在最终用户、AEM Forms和您配置的目标之间移动。 使用传输层安全性(TLS)保护此流量，以便传输时对数据进行加密。

要保护浏览器与AEM之间的连接，请在AEM实例上启用HTTPS。 有关步骤，请参阅默认为[SSL/TLS](/help/sites-administering/ssl-by-default.md)。

此外，请确保AEM Forms将数据发送到的端点（如云配置、提交操作URL和表单数据模型数据源）使用安全的HTTPS端点。 由于AEM Forms不会存储它传递的数据，因此静态加密不适用于该数据。 有关保护连接的更多指导，请参阅[安全传输层](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-transport-layer)。

## 外部数据存储的表单数据模型 {#form-data-model}

要读取数据并将其写入数据存储，请使用表单数据模型(FDM)。 FDM是将表单连接到您拥有并管理的数据源（如数据库或RESTful Web服务）的推荐机制。

有关详细信息，请参阅[AEM Forms数据集成简介](/help/forms/using/data-integration.md)。 有关保护FDM处理的数据安全的指导，请参阅[由表单数据模型(FDM)处理的安全数据](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-data-handled-by-form-data-model-fdm)。

## 长期工作流进程中的数据 {#long-lived-workflow-processes}

如果您使用长期工作流程，AEM可以临时保存数据作为工作流有效负载的一部分。 承载此有效负载的工作流变量存储在AEM存储库的工作流实例元数据中，它们可以包含最终用户在填写自适应表单时提供的个人身份信息(PII)或敏感个人数据(SPD)。

要将此数据保留在您拥有并管理的存储库（如Azure Blob存储）中，而不是存储在AEM上，请使用AEM的数据外部化功能。 将变量外部化时，数据不会保存在AEM存储库中，而是存储在您自己的数据存储库中。

有关将数据外部化的步骤，请参阅[将敏感数据参数化到工作流变量并存储在外部数据存储中](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables)。

## 自定义和记录 {#customization-and-logging}

AEM是一种可自定义的解决方案。 如果您自定义AEM，请确保您的自定义不会在AEM存储库或日志中存储任何数据。

使用默认功能时，AEM Forms不会将表单最终用户数据写入日志。

自定义代码可以将数据写入日志。 如果在开发期间添加跟踪或日志记录，则在将代码部署到暂存和生产环境之前，请删除发送到日志的跟踪和数据。

## 有关AEM Forms数据保留的常见问题解答 {#faq}

**AEM Forms是否存储表单数据？**

不会。 默认情况下，Adobe Experience Manager (AEM) Forms充当通过Adaptive Forms捕获的数据的直通服务器，不会将最终用户数据存储在AEM存储库中。 服务器将提交的数据传递到您拥有并配置的目标，例如表单数据模型数据源、提交操作目标或外部API。 此默认行为同时适用于OSGi上的AEM Forms和JEE上的AEM Forms 。

**自适应表单数据的存储位置？**

提交的自适应表单数据存储在您拥有并配置的目标中，而不是存储在Adobe Experience Manager (AEM)存储库中。 现成的机制(如表单数据模型(FDM)、连接器和提交操作)将数据发送到您自己的位置。 表单还可以将数据转发到外部服务（如REST API），而无需将数据保留在AEM上。 Forms Portal提交操作还会将数据保存到您提供并拥有的存储位置。

**长期工作流是否存储表单数据？**

Adobe Experience Manager (AEM) Forms中的长期工作流可以临时将数据保存为工作流有效负荷的一部分，该有效负荷存储在AEM存储库的工作流实例元数据中。 若要将此数据保存在您拥有并管理的存储库（如Azure Blob Storage）中，而不是存储在AEM上，请为工作流变量使用[AEM数据外部化功能](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables)。

**AEM Forms是否将数据写入日志？**

不会。 使用默认功能，Adobe Experience Manager (AEM) Forms不会将最终用户数据写入日志。 由于AEM是一个可自定义的平台，因此自定义代码可以将数据写入日志。 如果在开发期间添加跟踪或日志记录，请在部署到暂存和生产环境之前删除这些跟踪和任何记录的数据。 自定义不得将数据存储在AEM存储库或日志中。

**如何保护传输中的数据？**

在Adobe Experience Manager (AEM) Forms中，使用传输层安全性(TLS)保护传输中的数据。 在AEM实例上启用HTTPS，以保护浏览器与AEM之间的连接。 此外，请确保AEM Forms将数据发送到的端点（如云配置、提交操作URL和表单数据模型数据源）使用安全的HTTPS端点。 由于AEM Forms不会存储它传递的数据，因此静态加密不适用于该数据。

## 相关资源 {#related-resources}

* [AEM Forms 数据集成简介](/help/forms/using/data-integration.md)
* [将敏感数据参数化为工作流变量并存储在外部数据存储中](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables)
* [配置提交操作](/help/forms/using/configuring-submit-actions.md)
* [在OSGi环境中强化和保护AEM Forms](/help/forms/using/hardening-securing-aem-forms-environment.md)
