---
title: 自动保存自适应表单
description: 您可以将自适应表单配置为根据事件或预定义的时间间隔自动开始保存内容
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms,Foundation Components
exl-id: ff9bf466-228d-40e6-9389-15c1f2ed1d2e
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 7%

---

# 自动保存自适应表单 {#auto-save-an-adaptive-form}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

您可以配置自适应表单，以根据事件或预定义的时间间隔自动开始保存内容。 默认情况下，自适应表单的内容会在用户操作时保存，例如按保存按钮时。 自动保存选项在以下方面很有用：

* 自动为匿名和登录用户保存内容
* 保存表单内容而不需要用户干预或用户干预最少
* 开始基于用户事件保存表单内容
* 在指定的时间间隔后重复保存表单的内容

## 为自适应表单启用自动保存 {#enable-autosave-for-an-adaptive-form}

对于自适应表单，不会现成启用自动保存选项。 您可以在自适应表单的属性的&#x200B;**自动保存**&#x200B;部分中启用自动保存选项。 **自动保存**&#x200B;部分还提供了几个其他配置选项。 执行以下步骤以启用和配置自适应表单的自动保存选项：

1. 要访问属性中的自动保存部分，请选择一个组件，然后选择![字段级](assets/field-level.png) > **[!UICONTROL 自适应表单容器]**，然后选择![cmppr](assets/cmppr.png)。
1. 在&#x200B;**[!UICONTROL 自动保存]**&#x200B;部分中，**[!UICONTROL 启用]**&#x200B;自动保存选项。
1. 在&#x200B;**[!UICONTROL 自适应表单事件]**&#x200B;框中，指定1或TRUE以在浏览器中加载表单时自动开始保存表单。 您还可以为事件指定条件表达式，该表达式在触发并返回true时开始保存表单的内容。
1. 指定触发器。 根据您的配置触发自动保存。 您的选项包括：

   * **[!UICONTROL 基于时间：]**&#x200B;选择选项，以根据特定时间间隔开始保存内容。
   * **[!UICONTROL 基于事件：]**&#x200B;选择在触发事件时开始保存内容的选项。

   选择触发器后，将启用“策略配置”框。 通过“策略配置”框，您可以：

   * 如果您选择&#x200B;**[!UICONTROL 基于时间的]**&#x200B;触发器，请指定时间间隔。
   * 如果您选择&#x200B;**[!UICONTROL 基于事件的]**&#x200B;触发器，请指定事件名称。

   您还可以创建自己的自定义策略并将其添加到列表中。 有关详细信息，请参阅[实施自定义策略以自动保存表单](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p)。

1. （仅限基于时间的自动保存）执行以下步骤来配置基于时间的自动保存选项。

   1. 在&#x200B;**[!UICONTROL 在此时间间隔]**&#x200B;时自动保存框中，以秒为单位指定时间间隔。 在间隔框中指定的秒数过后，将重复保存该表单。

1. （仅限基于事件的自动保存）执行以下步骤来配置用于基于事件的自动保存的选项。

   1. 在此事件&#x200B;**之后的**&#x200B;自动保存框中，指定一个[GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html)事件。 每当表达式的计算结果为TRUE时，将保存表单。

1. （可选）要自动保存匿名用户的内容，请选择&#x200B;**为匿名用户启用自动保存**&#x200B;选项，然后单击&#x200B;**[!UICONTROL 确定]**。

   >[!NOTE]
   >
   >要使自动保存选项适用于匿名用户，请确保将Forms通用配置服务配置为允许所有用户预览、验证和签署表单。
   >
   >要配置该服务，请转到位于`https://server:port/system/console/configMgr`的AEM Web控制台配置并编辑&#x200B;**[!UICONTROL Forms Common Configuration Service]**&#x200B;以选择&#x200B;**[!UICONTROL 允许]**&#x200B;字段中的&#x200B;**[!UICONTROL 所有用户]**&#x200B;选项，并保存配置。

## 实施自定义策略以启用自适应表单的自动保存 {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

您可以实施自定义事件以触发自动保存功能。 执行以下步骤以创建和实施自定义事件：

1. 创建客户端库和客户端库文件夹。 有关详细步骤，请参阅[使用客户端库文档](/help/sites-developing/clientlibs.md)。

   例如，以下脚本使用自定义`emailFocusChange`事件触发自动保存功能：

   ```javascript
   window.addEventListener("bridgeInitializeStart", function (){
       guideBridge.connect(function () { guideBridge.on("elementFocusChanged", function (event,data) {
           if(data.target.name === 'Email') {
               guideBridge.trigger("emailFocusChange");
           }
       });
      });
   });
   ```

   >[!NOTE]
   >
   >在创建客户端库文件夹时定义类别属性。 随时准备分配给类别属性的值。

1. 在创作模式下打开自适应表单。

1. 在编辑模式下，选择一个组件，然后选择![字段级](assets/field-level.png) > **[!UICONTROL 自适应表单容器]**，然后选择![cmppr](assets/cmppr.png)。
1. 在属性中，打开&#x200B;**[!UICONTROL 基本]**&#x200B;部分。 在&#x200B;**[!UICONTROL 客户端库类别]**&#x200B;框中，输入创建客户端库文件夹时定义的类别属性的值。
1. 打开自动保存部分。 在此事件&#x200B;]**之后的**[!UICONTROL &#x200B;自动保存框中，指定已在客户端库中定义的自定义事件。 单击&#x200B;**[!UICONTROL 确定]**。
