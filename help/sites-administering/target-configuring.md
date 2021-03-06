---
title: 手动配置与Adobe Target的集成
seo-title: Manually Configuring the Integration with Adobe Target
description: 了解如何手动配置与Adobe Target的集成。
seo-description: Learn how to manually configure the integration with Adobe Target.
uuid: 0bb76a65-f981-4cc5-bee8-5feb3297137c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 20c8eb1d-5847-4902-b7d3-4c3286423b46
exl-id: 0f710685-dc4f-4333-9847-d002b2637d08
source-git-commit: 813441a61baa560c9d317a5519b9e0c0d1da7a6e
workflow-type: tm+mt
source-wordcount: '2209'
ht-degree: 4%

---

# 手动配置与Adobe Target的集成 {#manually-configuring-the-integration-with-adobe-target}

您可以修改在使用向导时执行的选择加入向导配置，也可以不使用向导手动与Adobe Target集成。

## 修改选择加入向导配置 {#modifying-the-opt-in-wizard-configurations}

的 [选择加入向导](/help/sites-administering/opt-in.md) the [将AEM与Adobe Target集成](/help/sites-administering/target.md) 自动创建名为“已配置的Target配置”的Target云配置。 该向导还会为名为已配置的Target框架的云配置创建Target框架。 您可以根据需要修改云配置和框架的属性。

通过配置A4T Adobe Target配置，您还可以将Analytics Cloud配置为在定位内容时使用Adobe Target作为报表源。

要找到云配置和框架，请导航到 **Cloud Services** 通过 **工具** > **部署** > **云**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))在Adobe Target下，单击或点按 **显示配置**.

### 已配置的Target配置属性 {#provisioned-target-configuration-properties}

在选择加入向导创建的已配置Target配置云配置中使用以下属性值：

* **客户端代码：** 在选择加入向导中输入。
* **电子邮件：** 在选择加入向导中输入。
* **密码：** 在选择加入向导中输入。
* **API类型：** REST
* **同步来自Adobe Target的区段：** 已选择。

* **客户端库：** mbox.js.
* **使用DTM交付客户端库：** 未选择。 如果您 [使用DTM](/help/sites-administering/dtm.md) 或其他标签管理系统来托管mbox.js或AT.js文件。 Adobe建议您使用DTM而不是AEM来交付库。

* **自定义mbox.js:** 未指定任何内容，以便使用默认的mbox.js文件。 根据需要指定要使用的自定义mbox.js文件。 仅当您选择了mbox.js时，才会显示。
* **自定义AT.js:** 未指定任何内容，以便使用默认的AT.js文件。 根据需要指定要使用的自定义AT.js文件。 仅当您选择了AT.js时，才会显示。

>[!NOTE]
>
>在AEM 6.3中，您可以选择Target库文件： [AT.JS](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/mbox-implement/mbox-download.html)，这是适用于Adobe Target的新实施库，专为典型的Web实施和单页应用程序而设计。
>
>与mbox.js库相比，AT.js提供了以下几项改进：
>
>* 缩短了Web实施的页面加载时间
>* 增强的安全性
>* 为单页应用程序提供更好的实施选项
>* AT.js包含target.js中包含的组件，因此不再需要调用target.js


### 已配置的Target框架属性 {#provisioned-target-framework-properties}

选择加入向导创建的已配置Target框架已配置为从配置文件数据存储发送上下文数据。 默认情况下，商店的年龄和性别数据项会发送到Target。 您的解决方案可能需要发送其他参数。

![chlimage_1-158](assets/chlimage_1-158.png)

您可以配置框架以将其他上下文信息发送到Target，如 [添加Target框架](/help/sites-administering/target-configuring.md#adding-a-target-framework).

### 配置A4T Analytics Cloud配置 {#configuring-a-t-analytics-cloud-configuration}

您可以将Adobe Target配置为在定位内容时使用Adobe Analytics作为报表源。

>[!NOTE]
>
>用户凭据身份验证（旧版）不适用于A4T（适用于Target和Analytics）。 因此，客户应使用IMS身份验证，而不是用户凭据身份验证。

为此，您需要指定要将Adobe Target云配置与以下项连接的A4T云配置：

1. 导航到 **Cloud Services** 通过 **AEM徽标** > **工具** > **部署** > **Cloud Services**.
1. 在 **Adobe Target** ，单击 **立即配置**.
1. 重新连接到Adobe Target配置。
1. 在 **A4T Analytics Cloud配置** 下拉菜单中，选择框架。

   >[!NOTE]
   >
   >只有为A4T启用的Analytics配置才可用。
   >
   >使用AEM配置A4T时，您可能会看到缺少条目的配置引用。 要选择分析框架，请执行以下操作：
   >
   >1. 导航到 **工具** > **常规** > **CRXDE Lite**.
   1. 导航到 [A4T Analytics配置对话框](#a4t-analytics-config-dialog) （见下文）
   1. 设置属性 **禁用** to **false**.
   1. 点按或单击 **全部保存**.


#### A4T Analytics配置对话框 {#a4t-analytics-config-dialog}

```xml
/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig
```

![AdobeTargetSettings](assets/adobe-target-settings.jpg)

单击&#x200B;**确定**。使用Adobe Target定位内容时，您能够 [选择报表源](/help/sites-authoring/content-targeting-touch.md).

## 手动与Adobe Target集成 {#manually-integrating-with-adobe-target}

手动与Adobe Target集成，而不是使用选择加入向导。

>[!NOTE]
目标库文件， [AT.JS](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/mbox-implement/mbox-download.html)，是适用于Adobe Target的新实施库，专为典型的Web实施和单页应用程序而设计。 Adobe建议您使用AT.js而不是mbox.js作为客户端库。
与mbox.js库相比，AT.js提供了以下几项改进：
* 缩短了Web实施的页面加载时间
* 增强的安全性
* 为单页应用程序提供更好的实施选项
* AT.js包含target.js中包含的组件，因此不再需要调用target.js
>
您可以在 **客户端库** 下拉菜单。

### 创建Target云配置 {#creating-a-target-cloud-configuration}

要启用AEM与Adobe Target的交互，请创建Target云配置。 要创建配置，请提供Adobe Target客户端代码和用户凭据。

您只能创建一次Target云配置，因为您可以将该配置与多个AEM促销活动关联。 如果您有多个Adobe Target客户端代码，请为每个客户端代码创建一个配置。

您可以配置云配置以同步来自Adobe Target的区段。 如果启用同步，则在保存云配置后，系统会立即从后台的Target中导入区段。

请按照以下过程在AEM中创建Target云配置：

1. 导航到 **Cloud Services** 通过 **AEM徽标** > **工具** > **部署** > **Cloud Services**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   的 **Adobe Marketing Cloud** 将打开“概述”页面。

1. 在 **Adobe Target** ，单击 **立即配置**.
1. 在 **创建配置** 对话框：

   1. 为配置指定 **标题**.
   1. 选择 **Adobe Target配置** 模板。
   1. 单击&#x200B;**创建**。

   将打开编辑对话框。

   ![AdobeTargetSettings](assets/adobe-target-settings.jpg)

   >[!NOTE]
   使用AEM配置A4T时，您可能会看到缺少条目的配置引用。 要选择分析框架，请执行以下操作：
   1. 导航到 **工具** > **常规** > **CRXDE Lite**.
   1. 导航到 **/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig**
   1. 设置属性 **禁用** to **false**.
   1. 点按或单击 **全部保存**.


1. 在对话框中，提供这些属性的值。

   * **客户端代码**:目标帐户客户端代码
   * **电子邮件**:Target帐户电子邮件。
   * **密码**:目标帐户密码。
   * **API类型**:REST或XML
   * **A4T Analytics Cloud配置**:选择用于定位活动目标和量度的Analytics云配置。 如果您在定位内容时使用Adobe Analytics作为报表源，则需要使用此功能。 如果您看不到云配置，请参阅 [配置A4T Analytics Cloud配置](#configuring-a-t-analytics-cloud-configuration).

   * **使用准确定位：** 默认情况下，此复选框处于选中状态。 如果选中此选项，云服务配置将等待上下文加载后再加载内容。 请参阅以下注释。
   * **同步来自Adobe Target的区段：** 选择此选项可下载在Target中定义的区段，以在AEM中使用它们。 当API类型属性为REST时，您必须选择此选项，因为不支持内联区段，您始终需要使用Target中的区段。 (请注意，“区段”的AEM术语等同于Target“受众”。)
   * **客户端库：** 选择您希望使用mbox.js还是AT.js客户端库。
   * **使用DTM交付客户端库**  — 选择此选项可从DTM或其他标签管理系统中使用AT.js或mbox.js。 您必须 [配置DTM集成](/help/sites-administering/dtm.md) ，以使用此选项。 Adobe建议您使用DTM而不是AEM来交付库。
   * **自定义mbox.js**:如果您选中DTM框或使用默认的mbox.js，请将留空。 或者，上传您的自定义mbox.js。 仅当您选择了mbox.js时，才会显示。
   * **自定义AT.js**:如果您选中DTM框或使用默认AT.js，请将留空。 或者，上传您的自定义AT.js。 仅当您选择了AT.js时，才会显示。

   >[!NOTE]
   默认情况下，当您选择加入Adobe Target配置向导时，将启用“准确定位”。
   准确定位意味着云服务配置在加载内容之前会等待上下文加载。 因此，就性能而言，准确定位可能会在加载内容之前造成几毫秒的延迟。
   创作实例始终启用准确定位。 但是，在发布实例上，您可以通过清除云服务配置中准确定位旁边的复选标记(**http://localhost:4502/etc/cloudservices.html**)。 无论云服务配置中的设置如何，您仍可以为各个组件打开和关闭准确定位。
   如果 ***已经*** 创建目标组件后，如果更改了此设置，则所做的更改不会影响这些组件。 您必须直接对这些组件进行任何更改。

1. 单击 **连接到Target** 以初始化与Target的连接。 如果连接成功，则显示消息 **连接成功** 中。 单击 **确定** ，然后 **确定** 对话框。

   如果您无法连接到Target，请参阅 [疑难解答](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) 中。

### 添加Target框架 {#adding-a-target-framework}

配置Target云配置后，添加Target框架。 该框架可识别从可用 [Client Context](/help/sites-administering/client-context.md) 或 [ContextHub](/help/sites-developing/ch-configuring.md) 组件。 Target使用参数来确定应用于当前上下文的区段。

您可以为单个Target配置创建多个框架。 当您需要为网站的不同部分向Target发送一组不同的参数时，多个框架非常有用。 为您需要发送的每组参数创建一个框架。 将网站的每个部分与相应的框架相关联。 请注意，网页一次只能使用一个框架。

1. 在Target配置页面上，单击 **+** 可用框架旁边的（加号）。
1. 在创建框架对话框中，指定 **标题**，选择 **Adobe Target框架**，然后单击 **创建**.

   ![chlimage_1-161](assets/chlimage_1-161.png)

   将打开框架页面。 Sidekick提供表示 [Client Context](/help/sites-administering/client-context.md) 或 [ContextHub](/help/sites-developing/ch-configuring.md) 你可以映射的。

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. 拖动表示要用于映射到拖放目标的数据的Client Context组件。 或者，拖动&#x200B;**ContextHub存储** 组件。

   >[!NOTE]
   映射时，参数会通过简单字符串传递到mbox。 无法从ContextHub映射数组。

   例如，要使用 **用户档案数据** 关于网站访客以控制Target营销活动，请将 **用户档案数据** 组件。 此时会显示可用于映射到Target参数的配置文件数据变量。

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. 通过选择 **共享** 复选框。

   ![chlimage_1-164](assets/chlimage_1-164.png)

   >[!NOTE]
   只有从AEM到Adobe Target同步参数的一种方式。

将创建框架。 要将框架复制到发布实例，请使用 **激活框架** 选项。

### 将活动与Target云配置关联  {#associating-activities-with-the-target-cloud-configuration}

关联您的 [AEM活动](/help/sites-authoring/activitylib.md) 配置，以便能够镜像 [Adobe Target](https://docs.adobe.com/content/help/en/target/using/experiences/offers/manage-content.html).

>[!NOTE]
可用的活动类型由以下因素决定：
* 如果对 AEM 端上用来连接到 Adobe Target 的 Adobe Target 租户 (clientcode) 启用了 **xt_only** 选项，则您&#x200B;**只**&#x200B;能在 AEM 中创建 XT 活动。
* 如果&#x200B;**未**&#x200B;对 Adobe Target 租户 (clientcode) 启用 **xt_only** 选项，则可以在 AEM 中创建 XT 活动&#x200B;**和** A/B 活动。
>
**另请注意：****xt_only** 选项是对特定 Target 租户 (clientcode) 应用的设置，只能直接在 Adobe Target 中进行修改。您无法在 AEM 中启用或禁用此选项。

### 将Target框架与您的站点关联 {#associating-the-target-framework-with-your-site}

在AEM中创建Target框架后，将网页与框架关联。 页面上的目标组件会将框架定义的数据发送到Adobe Target以进行跟踪。 (请参阅 [内容定位](/help/sites-authoring/content-targeting-touch.md).)

将页面与框架关联后，子页面将继承该关联。

1. 在 **站点** 控制台中，导航到要配置的站点。
1. 使用 [快速操作](/help/sites-authoring/basic-handling.md#quick-actions) 或 [选择模式](/help/sites-authoring/basic-handling.md)，选择 **查看属性。**
1. 选择 **Cloud Services** 选项卡。
1. 点按/单击 **编辑**.
1. 点按/单击 **添加配置** 在 **Cloud Service配置** 选择 **Adobe Target**.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 选择所需的框架 **配置参考**.

   >[!NOTE]
   确保选择 **框架** 而不是创建该云配置的Target云配置中的任何值。

1. 点按/单击 **完成**.
1. 激活网站的根页面以将其复制到发布服务器。 (请参阅 [如何发布页面](/help/sites-authoring/publishing-pages.md).)

   >[!NOTE]
   如果尚未激活您附加到页面的框架，则会打开一个向导，通过该向导也可以发布页面。

## Target连接问题疑难解答 {#troubleshooting-target-connection-problems}

执行以下任务，以解决连接到Target时出现的问题：

* 确保您提供的用户凭据正确无误。
* 确保AEM实例可以连接到Target服务器。 例如，确保防火墙规则不会阻止出站AEM连接，或者将AEM配置为使用必要的代理。
* 在AEM错误日志中查找有用的消息。 error.log文件位于 **crx-quickstart/logs** 安装AEM的目录。
* 在Adobe Target中编辑活动时，URL将指向localhost。 通过将AEM外部器设置为正确的URL来解决此问题。
