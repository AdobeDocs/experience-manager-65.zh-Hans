---
title: 更新部署的许可证类型
seo-title: 更新部署的许可证类型
description: 使用管理控制台中的“更改许可证”页面更新部署的许可证类型。
seo-description: 使用管理控制台中的“更改许可证”页面更新部署的许可证类型。
uuid: 0152635e-2c00-4944-b9b6-64b368589a91
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e4f31377-ccc9-4986-a3bf-ef2e83d12448
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 更新部署的许可证类型 {#update-the-license-type-for-the-deployment}

在AEM表单安装过程中，您使用配置管理器配置和部署所需的AEM表单模块。 默认情况下，这些模块配置有60天的评估许可证。 使用管理控制台中的“更改许可证”页可更改部署的许可证类型。 当前部署的模块显示在“更改许可证”页面上。

“更改许可证”页面显示有关许可证的信息：

* 当前许可证类型
* 上次更新许可证的日期和时间
* 执行上次更新的人员
* 许可证的当前状态
* AEM表单的安装日期
* 当前许可证的到期日

>[!NOTE]
>
>许可证更改适用于所有已部署的模块。 在更改许可证类型之前，请取消部署任何未获得许可的模块。 如果部署的模块列表包含的模块不是您从Adobe购买的模块，请不要选择生产许可证类型。

## 更新许可证类型 {#update-the-license-type}

1. 在管理控制台中，单击“授权许可”。
1. 阅读AEM表单最终用户许可协议，如果您同意协议条款，请选择“我接受”，然后单击“下一步”。
1. 在“更改许可证”页面上，选择许可证类型：

   * **** EVAL:60天评估许可证
   * **** 开发人员：永久开发许可证
   * **** NFR:2年评估许可证
   * **** 视频：1年订阅Adobe开发人员计划
   * **** 生产：永久许可证

1. 选择是，许可证更改对所有已部署模块有效。
1. 单击“确认许可证更改”。 将显示一条消息，指明许可证已成功更新。

