---
title: 为JEE上的AEM Forms的自定义组件API记录一个事务。
description: 了解如何使用TransactionRecorder API记录自定义组件的事务。
feature: Transaction Reports
exl-id: 33e1868a-2a7f-4785-8571-95651e661e21
role: Admin, User, Developer
solution: Experience Manager, Experience Manager Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: bcb3e79d-a57e-59a4-ad50-e03803c9f153
    internal-label: Transaction Reports
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 5%
---
# 为JEE上的AEM Forms的自定义组件API记录事务 {#record-a-transaction-for-custom-components}

在自定义组件中使用可计费API时，可以为组件启用事务报告。 要启用事务报告，请修改组件的`component.xml`文件，并在必须启用事务报告的操作下添加下面给定的标记。

**标记**： `<transaction-operation-type>CONVERT</transaction-operation-type> // Supported values are SUBMIT, CONVERT, RENDER.`

| 旧操作标记 | 新建操作标记 |
| ----------- | ----------- |
| `<operation>`<br> `<.... tags`<br>`<...>`<br>`<operation>` | `<operation>`<br> `<.... tags`<br>`<...>`<br>`<transaction-operation-type>CONVERT</transaction-operation-type`<br>`<operation>` |

如果您必须捕获一个API的多个事务（例如批处理API，其中的事务计数随输入计数的数量而变化），请在API级别处理事务计数。

**要记录可变事务计数：**

1. 导入代码中的类`"com.adobe.idp.dsc.InvocationContextStack"`。 该类是`adobe-livecycle-client.jar` sdk文件的一部分。 sdk文件位于`<AEM_Forms_JEE_Install>\sdk\client-libs\common`

   >[!NOTE]
   > 使用新文件更新上述在客户端项目中共享的客户端文件（如果已经捆绑）。

1. 在必须为其记录可变事务的API中：
   1. 添加逻辑，以便可以将事务计数存储在一个整数变量中，如`transaction_count`。
   1. 操作成功后，添加`InvocationContextStack.recordTransactionCount(transaction_count)`。

<!--
For example, you can set count for your custom component by importing class `"com.adobe.idp.dsc.InvocationContextStack"` in the code available at `adobe-livecycle-client.jar`  and determine the transaction count basis API input/result and add (In this case we add count is equal to 3):
`InvocationContextStack.recordTransactionCount(<count>).` to 
`InvocationContextStack.recordTransactionCount(3)`.
-->

## 相关文章

* [在JEE上启用和查看AEM Forms的交易报表](/help/forms/using/transaction-report-overview-jee.md)
* [JEE 上的 AEM Forms 的可计费 API 列表](/help/forms/using/transaction-reports-billable-apis-jee.md)
