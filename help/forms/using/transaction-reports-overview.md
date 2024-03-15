---
title: 交易报表概述
description: 记录已提交的所有表单、已渲染的交互式通信、已转换为另一种格式的文档及其他内容的计数
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Transaction Reports
exl-id: bb812614-f4d8-4f57-bea2-8f7d31457039
source-git-commit: d0db00de6b767a12a9492bbbcec49a8c5d25ff27
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# OSGi上AEM Forms的交易报表 {#transaction-reports-overview}

<!--## Introduction {#introduction}

Transaction reports in AEM Forms let you keep a count of all transactions taken place since a specified date on your AEM Forms deployment. The objective is to provide information about product usage and help business stakeholders understand their digital processing volumes. Examples of a transaction include:

* Submission of an adaptive form, an HTML5 Form, or a form set
* Rendition of a print or a web version of an interactive communication
* Conversion of a document from one file format to another

For more information on what is considered a transaction, see [Billable APIs](../../forms/using/transaction-reports-billable-apis.md).-->

默认情况下，事务记录处于禁用状态。 您可以 [启用事务记录](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports) 从AEM Web控制台。 您可以查看有关创作、处理或发布实例的事务报表。 查看有关所有事务汇总的创作或处理实例的事务报表。 查看发布实例上的事务报告，了解仅在该报告运行所在的发布实例上发生的所有事务的计数。

请勿在同一AEM实例上创作内容（创建自适应表单、交互式通信、主题和其他创作活动）和处理文档（使用工作流、文档服务和其他处理活动）。 对于用于创作内容的AEM Forms服务器，请保持禁用事务录制。 为用于处理文档的AEM Forms服务器保持启用事务记录。

![sample-transaction-report-author-1](assets/sample-transaction-report-author-1.png)

事务在缓冲区中保留指定的时间段（刷新缓冲区时间+反向复制时间）。 默认情况下，事务计数大约需要90秒才能反映在事务报表中。

提交PDF表单、使用代理UI预览交互式通信或使用非标准表单提交方法等操作不计为交易。 AEM Forms提供了一个API来记录此类交易。 从自定义实施中调用API以记录交易。

## 支持的拓扑 {#supported-topology}

事务报表仅在OSGi环境上的AEM Forms上可用。 它支持author-publish 、 author-processing-publish ，并且仅支持处理拓扑。 例如，拓扑，请参见 [AEM Forms的架构和部署拓扑](../../forms/using/transaction-reports-overview.md).

事务计数将从发布实例反向复制到创作实例或处理实例。 下面显示了指示性的作者 — 发布拓扑：

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>AEM Forms事务报表不支持仅包含发布实例的拓扑。

### 使用交易报告的准则 {#guidelines-for-using-transaction-reports}

* 禁用所有创作实例上的事务报表，因为创作实例上的报表包含在创作活动期间注册的事务。
* 启用 **仅显示发布中的事务** 创作实例上的选项，用于查看所有发布实例的累积事务。 您还可以查看每个发布实例上的事务报告，了解仅特定发布实例上的实际事务。
* 请勿使用创作实例来运行工作流和处理文档。
* 在使用事务报表之前，如果您拥有发布服务器的拓扑，请确保为所有发布实例启用反向复制。
* 事务数据将从发布实例反向复制到仅相应的创作或处理实例。 创作或处理实例无法进一步将数据复制到另一个实例。 例如，如果您有author-processing-publish拓扑，则聚合的事务数据将仅复制到处理实例。

## 相关文章 {#related-articles}

* [在OSGi上查看和了解AEM Forms的交易报告](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [OSGi上AEM Forms的交易报告可计费API](../../forms/using/transaction-reports-billable-apis.md)
* [在OSGi上记录AEM Forms的自定义实施交易](/help/forms/using/record-transaction-custom-implementation.md)
