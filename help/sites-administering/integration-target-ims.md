---
title: 使用IMS与Adobe Target集成
description: 了解如何使用IMS将AEM与Adobe Target集成。
exl-id: 8ddd86d5-a5a9-4907-b07b-b6552d7afdc8
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
hide: true
hidefromtoc: true
index: false
source-git-commit: 3ccf41ed2c413171ea55a63e969e72e18c189fb7
workflow-type: tm+mt
source-wordcount: '1533'
ht-degree: 40%

---


# 使用IMS与Adobe Target集成{#integration-with-adobe-target-using-ims}

通过Target Standard API将AEM与Adobe Target集成需要使用Adobe Developer控制台配置Adobe IMS (Identity Management System)。

>[!NOTE]
>
>AEM 6.5中新增了对Adobe Target Standard API的支持。Target Standard API使用IMS身份验证。
>
>为了向后兼容，仍支持在AEM中使用Adobe Target Classic API。 此 [Target Classic API使用用户凭据](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).
>
>API 选择由用于 AEM/Target 集成的身份验证方法驱动。
>另请参阅 [租户ID和客户端代码](#tenant-client) 部分。

## 前提条件 {#prerequisites}

开始此过程之前：

* [Adobe 支持部门](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support)必须针对以下项目配置您的帐户：

   * Adobe Console
   * Adobe Developer Console
   * Adobe Target 和
   * Adobe IMS (Identity Management System)

* 您组织的系统管理员应使用 Admin Console 将您组织中所需的开发人员添加到相关的产品配置文件中。

   * 这将为特定开发人员提供在Adobe Developer控制台中启用集成的权限。
   * 请参阅 [管理开发人员](https://helpx.adobe.com/enterprise/using/manage-developers.html).


## 配置 IMS 配置 – 生成公钥 {#configuring-an-ims-configuration-generating-a-public-key}

配置的第一阶段是在 AEM 中创建 IMS 配置并生成公钥。

1. 在 AEM 中，打开&#x200B;**工具**&#x200B;菜单。
1. 在 **安全性** 部分，选择 **Adobe IMS配置**.
1. 选择&#x200B;**创建**，打开 **Adobe IMS 技术帐户配置**。
1. 使用&#x200B;**云配置**&#x200B;下的下拉列表，选择 **Adobe Target**。
1. 激活&#x200B;**新建证书**&#x200B;并输入新别名。
1. 选择&#x200B;**创建证书**&#x200B;来确认。

   ![Adobe IMS技术帐户配置向导](assets/integrate-target-io-01.png)

1. 选择&#x200B;**下载**（或&#x200B;**下载公钥**）以将文件下载到本地驱动器，以便在[为 Adobe Target 与 AEM 的集成配置 IMS](#configuring-ims-for-adobe-target-integration-with-aem) 时方便使用。

   >[!CAUTION]
   >
   >保持此配置处于打开状态；出现以下情况时再次需要： [在AEM中完成IMS配置](#completing-the-ims-configuration-in-aem).

   ![用于在Adobe I/O上添加证书的信息消息](assets/integrate-target-io-02.png)

## 为 Adobe Target 与 AEM 的集成配置 IMS {#configuring-ims-for-adobe-target-integration-with-aem}

使用Adobe Developer Console，通过AEM可以使用的Adobe Target创建项目（集成），然后分配所需的权限。

### 创建项目 {#creating-the-project}

要使用AEM可以使用的Adobe Target创建项目，请打开Adobe Developer Console：

>[!CAUTION]
>
>目前，Adobe仅支持Adobe Developer控制台的 **服务帐户(JWT)** 凭据类型。
>
>不要使用 **OAuth 服务器到服务器**&#x200B;凭据类型（以后将支持此类型）。

1. 为项目打开 Adobe Developer Console：

   [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

1. 您拥有的任何项目都会显示出来。选择 **创建新项目**  — 位置和使用情况取决于以下因素：

   * 如果您不具有任何项目，**新建项目**会位于底部中心。
     ![新建项目 – 第一个项目](assets/integration-target-io-02.png)
   * 如果您已经拥有现有项目，则会列出和 **创建新项目** 在右上角。
     ![新建项目 – 多个项目](assets/integration-target-io-03.png)


1. 依次选择 **添加到项目**&#x200B;和 **API**：

   ![Adobe Developer控制台](assets/integration-target-io-10.png)

1. 依次选择 **Adobe Target** 和&#x200B;**下一步**：

   >[!NOTE]
   >
   >如果您已订阅 Adobe Target，但它并未列出，您应查看[先决条件](#prerequisites)。

   ![单击“下一步”](assets/integration-target-io-12.png)

1. **上传公钥**，完成后，选择&#x200B;**下一步**：

   ![使用开发人员控制台添加集成](assets/integration-target-io-13.png)

1. 查看凭据，然后选择&#x200B;**下一步**：

   ![创建项目](assets/integration-target-io-15.png)

1. 选择所需的产品配置文件，然后选择&#x200B;**保存配置的 API**：

   >[!NOTE]
   >
   >显示的产品配置文件取决于您是否拥有：
   >
   >* Adobe Target Standard – 仅&#x200B;**默认工作区**&#x200B;可用
   >* Adobe Target Premium – 列出了所有可用的工作区，如下所示

   ![选择要添加的API](assets/integration-target-io-16.png)

1. 这会确认创建。

<!--
1. The creation is confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![integrate-target-io-07](assets/integrate-target-io-07.png)
-->

### 将权限分配给集成 {#assigning-privileges-to-the-integration}

现在，将所需权限分配给集成：

1. 打开 Adobe **Admin Console**：

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. 导航到&#x200B;**产品**（顶部工具栏），然后选择 **Adobe Target – &lt;*your-tenant-id*>**（从左侧面板）。
1. 选择&#x200B;**产品配置文件**，然后从提供的列表中选择所需的工作区。例如，默认工作区。
1. 选择 **API 凭据**，然后选择所需的集成配置。
1. 选择&#x200B;**编辑者**&#x200B;作为&#x200B;**产品角色**；而不是选择&#x200B;**观察者**。

## 为 Adobe Developer Console 集成项目存储的详细信息 {#details-stored-for-the-ims-integration-project}

从“Adobe Developer Console – 项目”中，您可以查看所有集成项目的列表：

* [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

要显示有关配置的更多详细信息，请选择 **视图** （特定项目条目右侧）。 其中包括：

* 项目概述
* 见解
* 凭据
   * 服务帐户 (JWT)
      * 凭据详细信息
      * 生成 JWT
* APIS
   * 例如，Adobe Target

其中某些组件必须在基于IMS的AEM中完成Adobe Target的集成。

## 在 AEM 中完成 IMS 配置 {#completing-the-ims-configuration-in-aem}

通过返回到AEM，您可以添加针对Target的Adobe Developer控制台集成中所需的值来完成IMS配置：

1. 返回到 [AEM 中打开的 IMS 配置](#configuring-an-ims-configuration-generating-a-public-key)。
1. 选择&#x200B;**下一步**。

1. 在这里，您可以使用 [Adobe Developer Console 中项目配置的详细信息](#details-stored-for-the-ims-integration-project)：

   * **标题**：您的文本。
   * **授权服务器**：复制并粘贴以下&#x200B;**有效负载**&#x200B;分区中 `aud` 行的内容，例如，以下示例中的 `https://ims-na1.adobelogin.com`
   * **API密钥**：从以下位置复制此 [概述](#details-stored-for-the-ims-integration-project) 部分
   * **客户端密码**：在中生成此 [概述](#details-stored-for-the-ims-integration-project) 部分，并复制
   * **有效负载**：从[生成 JWT](#details-stored-for-the-ims-integration-project) 部分中复制此有效负载

   ![技术帐户配置](assets/integrate-target-io-10.png)

1. 选择&#x200B;**创建**&#x200B;来确认。

1. 您的 Adobe Target 配置会显示在 AEM 控制台中。

   ![Adobe IMS 技术帐户配置](assets/integrate-target-io-11.png)

## 确认 IMS 配置 {#confirming-the-ims-configuration}

要确认配置是否按预期运行，请执行以下操作：

1. 打开：

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   例如：

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`

1. 选择您的配置。
1. 从工具栏中选择&#x200B;**检查运行状况**，然后选择&#x200B;**查看**。

   ![Adobe IMS配置](assets/integrate-target-io-12.png)

1. 如果成功，您将看到以下消息：

   ![检查配置](assets/integrate-target-io-13.png)

## 配置Adobe TargetCloud Service {#configuring-the-adobe-target-cloud-service}

现在可为Cloud Service引用配置以使用Target Standard API：

1. 打开 **工具** 菜单。 然后，在 **Cloud Service** 部分，选择 **旧版Cloud Service**.
1. 向下滚动到 **Adobe Target** 并选择 **立即配置**.

   此 **创建配置** 对话框打开。

1. 输入 **标题** 如果你愿意，还有 **名称** （如果留空，则从标题生成）。

   您还可以选择所需的模板（如果有多个模板可用）。

1. 选择&#x200B;**创建**&#x200B;来确认。

   此 **编辑组件** 对话框打开。

1. 请在以下位置输入详细信息 **Adobe Target设置** 选项卡：

   * **身份验证**： IMS

   * **租户ID**：Adobe IMS租户ID。 另请参阅 [租户ID和客户端代码](#tenant-client) 部分。

     >[!NOTE]
     >
     >对于IMS，必须从Target本身获取此值。 您可以登录Target并从URL中提取租户ID。
     >
     >例如，如果URL为：
     >
     >`https://experience.adobe.com/#/@yourtenantid/target/activities`
     >
     >然后您使用 `yourtenantid`.

   * **客户代码**：请参阅 [租户ID和客户端代码](#tenant-client) 部分。

   * **IMS配置**：选择IMS配置的名称

   * **API类型**：REST

   * **A4T Analytics Cloud配置**：选择用于Target活动目标和量度的Analytics Cloud配置。 如果您在定位内容时使用Adobe Analytics作为报表源，则需要此项。 如果您看不到云配置，请参阅中的注释 [配置A4T Analytics Cloud配置](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration).

   * **使用准确定位**：默认情况下，此复选框处于选中状态。 如果选中，云服务配置会等待上下文加载完后再加载内容。 请参阅以下注释。

   * **从Adobe Target同步区段**：选择此选项可下载在Target中定义的分段，以便在AEM中使用它们。 当API类型属性为REST时，选择此选项，因为内联区段不受支持，并且您必须始终使用Target中的区段。 (AEM术语“区段”等同于Target“受众”。)

   * **客户端库**：选择是需要AT.js客户端库，还是mbox.js（已弃用）。

   * **使用Tag Management System提供客户端库**：使用DTM（已弃用）、AdobeLaunch或任何其他标签管理系统。

   * **自定义AT.js**：如果选中Tag Management框或使用默认的AT.js，则保留为空。 或者，上传您的自定义AT.js。 仅当您选择了AT.js时才显示。

   >[!NOTE]
   >
   >[配置使用Target Classic API的Cloud Service](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) 已弃用(使用Adobe Recommendations的“设置”选项卡)。

1. 单击 **连接到Target** 初始化与Adobe Target的连接。

   如果连接成功，则消息为 **连接成功** 将显示。

1. 选择 **确定** 在消息上，后接 **确定** ，以便您确认配置。

1. 您现在可以继续访问 [添加Target框架](/help/sites-administering/target-configuring.md#adding-a-target-framework) 以配置发送到Target的ContextHub或ClientContext参数。 请注意，将AEM体验片段导出到Target时可能不需要此项。

### 租户ID和客户端代码 {#tenant-client}

替换为 [Adobe Experience Manager 6.5.8.0](/help/release-notes/release-notes.md)，则Client Code字段已添加到Target配置窗口中。

配置租户ID和客户端代码字段时，请注意以下事项：

1. 对于大多数客户来说，租户 ID 和客户代码是相同的。这意味着，这两个字段包含相同的信息并且是相同的。确保在这两个字段中输入租户 ID。
2. 对于遗留问题，您还可以在“租户 ID”和“客户端代码”字段中输入不同的值。

在这两种情况下，请注意以下事项：

* 默认情况下，客户端代码（如果首先添加）也会自动复制到“租户 ID”字段中。
* 您可以选择更改默认租户ID集。
* 因此，对Target的后端调用基于租户ID，而客户端对Target的调用基于客户端代码。

如前所述，对于AEM 6.5，第一种情况最常见。无论哪种方式，确保 **两者** 字段包含正确的信息，具体取决于您的要求。

>[!NOTE]
>
>如果要更改现有 Target 配置，请：
>
>1. 重新输入租户 ID。
>2. 重新连接到 Target。
>3. 保存配置。
