---
title: 为JEE上的AEM Forms的自定义组件API记录一个事务。
description: 了解如何使用TransactionRecorder API记录自定义组件的事务。
feature: Transaction Reports
exl-id: 33e1868a-2a7f-4785-8571-95651e661e21
source-git-commit: bf99ad3710638ec823d3b17967e1c750d0405c77
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# 为JEE上的AEM Forms的自定义组件API记录事务 {#record-a-transaction-for-custom-components}

在自定义组件中使用可计费API时，可以为组件启用事务报告。 要启用交易报告，请修改 `component.xml` 文件，并在必须为其启用事务报告的操作下添加下面给定的标记。

**标记**： `<transaction-operation-type>CONVERT</transaction-operation-type> // Supported values are SUBMIT, CONVERT, RENDER.`

| 旧操作标记 | 新建操作标记 |
| ----------- | ----------- |
| `<operation>`<br> `<.... tags`<br>`<...>`<br>`<operation>` | `<operation>`<br> `<.... tags`<br>`<...>`<br>`<transaction-operation-type>CONVERT</transaction-operation-type`<br>`<operation>` |

如果您必须捕获一个API的多个事务（例如批处理API，其中的事务计数随输入计数的数量而变化），请在API级别处理事务计数。

**要记录可变事务处理计数，请执行以下操作：**

1. 导入类 `"com.adobe.idp.dsc.InvocationContextStack"` 在代码中。 该类是 `adobe-livecycle-client.jar` sdk文件。 sdk文件位于 `<AEM_Forms_JEE_Install>\sdk\client-libs\common`

   >[!NOTE]
   > 使用新文件更新上述在客户端项目中共享的客户端文件（如果已经捆绑）。

1. 在必须为其记录可变事务的API中：
   1. 添加逻辑，以便将事务计数存储在一个整数变量中，例如， `transaction_count`.
   1. 操作成功后，添加 `InvocationContextStack.recordTransactionCount(transaction_count)`.

<!--For example, you can set count for your custom component by importing class `"com.adobe.idp.dsc.InvocationContextStack"` in the code available at `adobe-livecycle-client.jar`  and determine the transaction count basis API input/result and add (In this case we add count is equal to 3):
`InvocationContextStack.recordTransactionCount(<count>).` to 
`InvocationContextStack.recordTransactionCount(3)`.-->

## 相关文章

* [在JEE上启用和查看AEM Forms的交易报表](/help/forms/using/transaction-report-overview-jee.md)
* [适用于AEM Forms on JEE的可计费API列表](/help/forms/using/transaction-reports-billable-apis-jee.md)
