---
title: 为JEE上的AEM Forms的自定义组件API记录一个事务。
description: 使用TransactionRecorder API记录自定义组件的事务。
feature: Transaction Reports
source-git-commit: d0db00de6b767a12a9492bbbcec49a8c5d25ff27
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# 为JEE上的AEM Forms的自定义组件API记录事务 {#record-a-transaction-for-custom-components}

在自定义组件中使用可计费API时，可以为组件启用事务报告。 要启用交易报告，请修改 `component.xml` 文件，并在需要启用事务报告的操作下添加下面给定的标记。

**标记**： `<transaction-operation-type>CONVERT</transaction-operation-type> // Supported values are SUBMIT, CONVERT, RENDER.`

| 旧操作标记 | 新建操作标记 |
| ----------- | ----------- |
| `<operation>`<br> `<.... tags`<br>`<...>`<br>`<operation>` | `<operation>`<br> `<.... tags`<br>`<...>`<br>`<transaction-operation-type>CONVERT</transaction-operation-type`<br>`<operation>` |

如果需要为API捕获多个事务（例如，在批处理API中，事务计数可能随输入计数而变化），在这些情况下，您需要在API级别处理事务计数。 下面是记录可变事务处理计数的给定步骤：

1. 导入类 `"com.adobe.idp.dsc.InvocationContextStack"` 在代码中。 该类是 `adobe-livecycle-client.jar` sdk文件。 sdk文件位于 `<AEM_Forms_JEE_Install>\sdk\client-libs\common`

   >[!NOTE]
   > 使用新文件更新上述在客户端项目中共享的客户端文件（如果已经捆绑）。

1. 在需要记录各种事务的API中：
   1. 添加逻辑以将事务计数存储在某些整数变量中，例如 `transaction_count`.
   1. 操作成功后，添加 `InvocationContextStack.recordTransactionCount(transaction_count)`.

<!--For example, you can set count for your custom component by importing class `"com.adobe.idp.dsc.InvocationContextStack"` in the code available at `adobe-livecycle-client.jar`  and determine the transaction count basis API input/result and add (In this case we add count is equal to 3):
`InvocationContextStack.recordTransactionCount(<count>).` to 
`InvocationContextStack.recordTransactionCount(3)`.-->

## 相关文章

* [在JEE上启用和查看AEM Forms的交易报告](/help/forms/using/transaction-report-overview-jee.md)
* [适用于AEM Forms on JEE的可计费API列表](/help/forms/using/transaction-reports-billable-apis-jee.md)


