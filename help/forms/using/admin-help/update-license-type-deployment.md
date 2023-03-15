---
title: 更新部署的许可证类型
seo-title: Update the license type for the deployment
description: 使用管理控制台中的“更改许可证”页面更新部署的许可证类型。
seo-description: Update the license type for the deployment by using the Change License page in administration console.
uuid: 0152635e-2c00-4944-b9b6-64b368589a91
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e4f31377-ccc9-4986-a3bf-ef2e83d12448
exl-id: 6b975aa1-9270-4098-9af5-c5cc67cb7b5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# 更新部署的许可证类型 {#update-the-license-type-for-the-deployment}

在AEM表单安装过程中，您使用配置管理器配置和部署所需的AEM表单模块。 默认情况下，这些模块配置有60天的评估许可证。 使用管理控制台中的“更改许可证”页面可更改部署的许可证类型。 当前部署的模块将显示在“更改许可证”页面上。

“更改许可证”页面显示有关您的许可证的信息：

* 当前许可证类型
* 上次更新许可证的日期和时间
* 上次更新的执行者
* 许可证的当前状态
* 安装AEM表单的日期
* 当前许可证的到期日期

>[!NOTE]
>
>许可证更改适用于所有已部署的模块。 在更改许可证类型之前，请取消部署任何未获得许可的模块。 如果部署的模块列表包含的模块不是您从Adobe购买的模块，请勿选择生产许可证类型。

## 更新许可证类型 {#update-the-license-type}

1. 在管理控制台中，单击许可。
1. 阅读AEM Forms最终用户许可协议，选择“I Accept（我接受）”（如果您同意协议条款），然后单击“Next（下一步）”。
1. 在“更改许可证”页面上，选择许可证类型：

   * **估计：** 60天试用许可证
   * **开发：** 永久开发许可证
   * **NFR：** 2年评估许可证
   * **IDEV：** 订购Adobe Developer计划1年
   * **生产：** 永久许可证

1. 选择是，许可证更改对所有已部署的模块有效。
1. 单击Confirm License Change。 出现一条消息，说明许可证已成功更新。
