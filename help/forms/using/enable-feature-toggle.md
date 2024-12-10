---
title: 启用功能切换以集成早期采用者和预发行版功能
description: 功能切换是AEM中的一项功能，它允许管理员在运行时环境中启用新功能。
feature: Adaptive Forms, Foundation Components
role: User, Developer
hidefromtoc: true
source-git-commit: 794d93d890ba752f9036a85831f7cbc8391fb545
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 2%

---

# Adobe Experience Manager (AEM) 6.5中的功能切换{#enable-feature-toggle-aem-forms-65}

功能切换是AEM中的一项功能，它允许管理员动态启用或禁用特定功能。 此功能在管理&#x200B;**早期采用者功能**&#x200B;和&#x200B;**预发行功能**&#x200B;时特别有用，无需对代码库进行主要部署或更改。 它可确保灵活性和控制AEM环境中可访问的功能。

## 启用功能切换 {#enable-feature-toggle-65}

早期采用者的功能切换或新功能可以通过&#x200B;**AEM Web Console**&#x200B;进行配置，具体步骤如下：

1. 登录到您的AEM Forms实例。
2. 导航到 `http://<author-instance-url>:portnumber/system/console/configMgr`。
3. 在配置管理器中搜索&#x200B;**AdobeGranite动态切换提供程序**。
4. 单击图标![铅笔图标](assets/illustratorcc_penciltool_cur_edit_2_17.png)。
5. 在[!UICONTROL 已启用切换]部分中，单击![铅笔图标](assets/aem6forms_add.png)。
6. 为功能添加功能切换ID，如下图所示。
   ![添加切换开关](assets/add_toggle_number_forms.png)

   >[!NOTE]
   >
   >您可以在文档中找到特定于早期采用者功能的功能切换ID。

7. 单击“保存”。

## 禁用功能切换 {#disable-feature-toggle-65}

要禁用启用了切换功能的功能切换，请执行以下步骤：

1. 登录到您的AEM Forms实例。
2. 导航到 `http://<author-instance-url>:portnumber/system/console/configMgr`。
3. 在配置管理器中搜索&#x200B;**AdobeGranite动态切换提供程序**。
4. 单击图标![铅笔图标](assets/illustratorcc_penciltool_cur_edit_2_17.png)。
5. 在[!UICONTROL 已禁用的切换]部分中，单击![铅笔图标](assets/aem6forms_add.png)。
6. 为要禁用的功能添加切换号码。
   ![删除切换](assets/remove_toggle_feature_forms.png)
7. 单击“保存”。

## 技术考虑

功能切换特定于环境，在运行时进行管理，因此它们不需要重新启动服务器。 但是，某些功能可能需要刷新相关页面或清除缓存以反映更改。
您可以通过`http://<author-instance-url>:4502/etc.clientlibs/toggles.json`访问为您的环境通过功能切换启用的功能列表。