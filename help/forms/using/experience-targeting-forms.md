---
title: 在AEM Forms中创建目标体验
description: 在AEM Forms中使用Target为目标客户创建自定义体验。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
exl-id: fdc91054-3f7e-4cbf-bdfa-7d7a621747f1
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# 在AEM Forms中创建目标体验 {#create-targeted-experiences-in-aem-forms}

## 将Adobe Target与AEM Forms集成 {#integrate-adobe-target-with-aem-forms}

Adobe Target与AEM集成后，您可以创建针对目标受众自定义的体验。 借助Adobe Target，您可以创建A/B测试、测量用户响应并为目标用户生成自定义的Web内容。 您可以将Adobe Target与AEM Forms集成，以定位自适应表单和交互式通信的图像组件。

在AEM中配置Adobe Target以将其用于自适应表单和交互式通信，请参阅[在AEM中创建Target配置](/help/sites-administering/target.md)和[添加框架](/help/sites-administering/target.md)。

>[!NOTE]
>
>在使用主机名或IP地址呈现自适应表单或交互式通信时，定位可正常工作。 使用localhost呈现自适应表单或交互式通信时，失败。

## 创建Target活动 {#creating-a-target-activity}

1. 选择&#x200B;**Adobe Experience Manager > Personalization >活动**。

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. 在“活动”页面中，选择&#x200B;**创建>创建品牌**。
1. 系统会要求您选择模板并输入属性。

   选择模板，然后选择&#x200B;**下一步。**&#x200B;在“属性”部分输入品牌标题，然后选择&#x200B;**创建。**
您的品牌现在已列在活动页面中。

1. 在“活动”页面中选择您的品牌。
1. 在品牌的主区域内，选择&#x200B;**创建** > **创建活动**。

   在创建活动时，您可以指定其详细信息、目标和设置。

   详细信息部分包括名称、定位引擎和目标。 选择Adobe Target作为定位引擎时，您将启用Target云配置选项。 选择您的Target云配置，选择活动类型，提供活动目标，然后选择&#x200B;**下一步**。 交互式通信仅支持体验定位活动类型。

   通过Target部分，可添加受众体验并将其命名为。 单击&#x200B;**添加体验**&#x200B;以启用&#x200B;**选择受众**&#x200B;和&#x200B;**命名体验**&#x200B;选项。 选择&#x200B;**选择受众**&#x200B;可查看受众及其源的列表。 从“受众名称”列表中选择一个受众。 选择&#x200B;**添加体验**&#x200B;以命名体验，然后选择&#x200B;**下一步**。

   通过“目标和设置”部分，您可以安排活动并设置其优先级。 设置活动的开始日期、结束日期和优先级、目标量度、其他量度，然后选择&#x200B;**保存**。

   该活动现在列在您的品牌页面中。

   >[!NOTE]
   >
   >您可以忽略错误“您的活动已保存，但未同步到Target。 原因：以下体验没有选件（如果在保存活动时遇到这种情况）。

1. 要启用target，请编辑.jsp文件以包含您的自适应表单模板使用的客户端库。

   例如，在现成的实现中，单击&#x200B;**工具** > **CRXDE Lite**。

   在CRXDE Lite地址栏中，键入/libs/fd/af/components/page/base/head.jsp以编辑head.jsp文件。

   此实施使用simpleEnrollment模板。 在此实现中，修改head.jsp文件以包含以下客户端库：

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. 要为自适应表单启用Target框架，请导航到您的表单或交互式通信，并以编辑模式打开它。

   要在编辑模式下打开表单或交互式通信，请选择&#x200B;**选择**，然后选择&#x200B;**打开**。

   或者，当您将指针移动到表单或交互式通信图标上而不选择它时，会出现四个按钮。 您可以选择显示的&#x200B;**编辑**&#x200B;按钮，以在编辑模式下打开表单。

1. 在页面工具栏中，选择&#x200B;**页面信息** ![主题选项](assets/theme-options.png) > **打开属性**。
1. 在“常规”选项卡中，选择&#x200B;**Adobe Target**&#x200B;字段的配置。 选择&#x200B;**保存并关闭**。

## 将创建的活动应用于自适应表单图像或交互式通信图像 {#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}

1. 打开自适应表单和交互式通信进行编辑。 如果要打开交互式通信，请打开Web渠道。

1. 在交互式通信或自适应表单的创作模式下，添加要定位的图像。

   >[!NOTE]
   >
   >AEM Forms仅支持定位图像组件。 确保托管图像组件的面板不包含任何其他组件，并且面板的列数设置为1。

1. 从&#x200B;**编辑**&#x200B;模式切换到&#x200B;**定位**&#x200B;模式。 切换模式的选项位于右上角附近。
1. 选择&#x200B;**品牌**，选择&#x200B;**活动**，然后选择&#x200B;**开始定位**。 **受众**&#x200B;菜单显示在编辑器的右侧。

   ![定位菜单](assets/targeting-menu.png)

1. 从&#x200B;**受众**&#x200B;菜单中选择一个受众，然后选择要定位的图像。 出现一个菜单。 在菜单中，选择&#x200B;**目标**。 选择图像并选择&#x200B;**配置**。 在属性窗口中，选择要为所选受众显示的图像。 对所有受众重复该步骤。 为交互式通信或自适应表单中的图像启用了体验定位。

## 检查创建的活动是否与Target服务器同步 {#check-if-the-created-activity-syncs-with-the-target-server}

用于定位与Target服务器同步的活动。 要检查您的活动是否与目标服务器同步，请在品牌页面中检查您的活动的状态。

确保活动的状态为“已同步”。

## 验证Target行为 {#validate-target-behavior}

验证Target行为：

* 在创作模式下对`wcmmode preview`使用定位
* 在发布模式下对`wcmmode preview`和`wcmmode disabled`使用定位

## 监控图像组件的定位 {#monitor-targeting-for-the-image-component}

要监控表单上图像组件的定位，请发布图像、活动和自适应表单。

## 未结问题 {#open-issues}

可见性表达式，为自适应表单上的目标图像设置焦点失败。
