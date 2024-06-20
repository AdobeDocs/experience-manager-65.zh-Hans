---
title: “教程：创建表单数据模型”
description: 了解如何将MySQL配置为数据源、创建表单数据模型(FDM)、配置它以及测试AEM Forms。
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
docset: aem65
exl-id: 40bc5af6-9023-437e-95b0-f85d3df7d8aa
solution: Experience Manager, Experience Manager Forms
feature: Form Data Model
role: Admin, User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1533'
ht-degree: 1%

---

# 教程：创建表单数据模型 {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

本教程是 [创建您的第一个自适应表单](../../forms/using/create-your-first-adaptive-form.md) 系列。 Adobe建议您按照时间顺序跟踪系列，以了解、执行和演示完整的教程用例。

## 关于教程 {#about-the-tutorial}

AEM [!DNL Forms] 数据集成模块允许您从不同的后端数据源(如AEM用户配置文件、RESTful Web服务、基于SOAP的Web服务、OData服务和关系数据库)创建表单数据模型。 您可以在表单数据模型中配置数据模型对象和服务，并将其与自适应表单关联。 自适应表单字段绑定到数据模型对象属性。 这些服务使您能够预填充自适应表单并将提交的表单数据写回数据模型对象。

有关表单数据集成和表单数据模型的更多信息，请参阅 [AEM Forms数据集成](../../forms/using/data-integration.md).

本教程将指导您完成准备、创建、配置表单数据模型并将其与自适应表单关联的步骤。 在本教程结束时，您将能够：

* [将MySQL数据库配置为数据源](#config-database)
* [使用MySQL数据库创建表单数据模型](#create-fdm)
* [配置表单数据模型](#config-fdm)
* [测试表单数据模型](#test-fdm)

表单数据模型将类似于以下内容：

![form-data-model_l](assets/form-data-model_l.png)

**答：** 配置的数据源 **B.** 数据源架构 **C.** 可用服务 **D.** 数据模型对象 **E.** 配置的服务

## 先决条件 {#prerequisites}

在开始之前，请确保您具备以下条件：

* [!DNL MySQL] 包含示例数据的数据库，如的先决条件部分所述 [创建您的第一个自适应表单](../../forms/using/create-your-first-adaptive-form.md)
* 适用于的OSGi包 [!DNL MySQL] JDBC驱动程序，如中所述 [捆绑JDBC数据库驱动程序](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)
* 自适应表单，如第一个教程中所述 [创建自适应表单](/help/forms/using/create-adaptive-form.md)

## 步骤1：将MySQL数据库配置为数据源 {#config-database}

您可以配置不同类型的数据源来创建表单数据模型。 在本教程中，您将配置已配置并填充了示例数据的MySQL数据库。 有关其他受支持的数据源以及如何配置这些数据源的信息，请参阅 [AEM Forms数据集成](../../forms/using/data-integration.md).

执行以下操作以配置您的 [!DNL MySQL] 数据库：

1. 将数据库的 [!DNL MySQL] JDBC 驱动程序作为 OSGi 捆绑包安装：

   1. [!DNL MySQL]从 下载 `http://www.java2s.com/ref/jar/download-orgosgiservicejdbc100jar-file.html`JDBC 驱动程序 OSGi 捆绑包。<!-- This URL is an insecure link but using https is not possible -->
   1. 登录到AEM [!DNL Forms] 以管理员身份创作实例，然后转到AEM Web控制台包。 默认URL为 [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).

   1. 选择 **[!UICONTROL 安装/更新]**. An [!UICONTROL 上传/安装包] 出现对话框。

   1. 选择 **[!UICONTROL 选择文件]** 以浏览并选择 [!DNL MySQL] JDBC驱动程序OSGi包。 选择 **[!UICONTROL 开始捆绑包]** 和 **[!UICONTROL 刷新包]**，并选择 **[!UICONTROL 安装或更新]**. [!DNL Oracle Corporation's]确保 的 [!DNL MySQL] JDBC 驱动程序处于活动状态。驱动程序已安装。

1. 将数据库配置为 [!DNL MySQL] 数据源：

   1. 转到位于 https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) 的 [AEM Web 控制台。
   1. 找到 **Apache Sling 连接池数据源** 配置。 选择此项可在编辑模式下打开配置。
   1. 在配置对话框中，指定以下详细信息：

      * **数据源名称：** 您可以指定任意名称。 例如，指定 **WeRetailMySQL**.
      * **数据源服务属性名称**：指定包含DataSource名称的服务属性的名称。 在将数据源实例注册为OSGi服务时指定它。 例如， **数据源名称**.
      * **JDBC驱动程序类**：指定JDBC驱动程序的Java™类名。 对象 [!DNL MySQL] 数据库，指定 **com.mysql.jdbc.Driver**.
      * **JDBC 连接 URI：**&#x200B;指定数据库的连接 URL。 对于 [!DNL MySQL] 在端口 3306 和 `weretail`架构上运行的数据库，URL 为： `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`

      >[!NOTE]
      >
      > [!DNL MySQL]当数据库位于防火墙后面时，数据库主机名不是公共 DNS。必须将数据库的 IP 地址添加到 *AEM 主机的 /etc/hosts* 文件中。

      * **用户名：** 数据库的用户名。 需要启用 JDBC 驱动程序才能与数据库建立连接。
      * **密码：** 数据库的密码。 必须启用JDBC驱动程序才能与数据库建立连接。

      >[!NOTE]
      >
      >AEM Forms不支持的NT身份验证 [!DNL MySQL]. 转到 https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) 的[AEM Web控制台，然后搜索“Apache Sling连接池数据源”。对于“JDBC 连接 URI”属性，请将“integratedSecurity”的值设置为 False，并使用创建的用户名和密码与数据库连接 [!DNL MySQL] 。

      * **借用时测试：** 启用 **[!UICONTROL 借用]** 时测试选项。
      * **退货时测试：**&#x200B;启用退货&#x200B;****&#x200B;时测试选项。
      * **验证查询：** 指定一个SQL SELECT查询来验证池中的连接。 查询必须至少返回一行。 例如， **选择 &#42; 来自customerdetails**.
      * **事务隔离**：将值设置为 **读取已提交**.

        将其他属性保留为默认值 [值](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) 并选择 **[!UICONTROL 保存]**.

        将创建类似于以下内容的配置。

        ![关系数据库数据源配置](assets/relational-database-data-source-configuration.png)

## 步骤2：创建表单数据模型 {#create-fdm}

AEM [!DNL Forms] 提供直观的用户界面，用于 [创建表单数据模型](data-integration.md) 来自配置的数据源。 您可以在表单数据模型中使用多个数据源。 对于此用例，您可以使用配置的 [!DNL MySQL] 数据源。

执行以下操作以创建表单数据模型：

1. 在AEM创作实例中，导航到 **[!UICONTROL Forms]** > **[!UICONTROL 数据集成]**.
1. 选择 **[!UICONTROL 创建]** > **[!UICONTROL 表单数据模型]**.
1. 在创建表单数据模型对话框中，指定 **name** 用于表单数据模型。 例如， **customer-shipping-billing-details**. 选择&#x200B;**[!UICONTROL 下一步]**。
1. 选择数据源屏幕列出了所有已配置的数据源。 选择 **WeRetailMySQL** 数据源并选择 **[!UICONTROL 创建]**.

   ![数据源选择](assets/data-source-selection.png)

此 **customer-shipping-billing-details** 创建表单数据模型。

## 步骤3：配置表单数据模型 {#config-fdm}

配置表单数据模型涉及：

* 添加数据模型对象和服务
* 配置数据模型对象的读写服务

执行以下操作以配置表单数据模型：

1. 在AEM创作实例上，导航到 **[!UICONTROL Forms]** > **[!UICONTROL 数据集成]**. 默认URL为 [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. 此 **customer-shipping-billing-details** 此处列出了您之前创建的表单数据模型。 在编辑模式下将其打开。

   所选数据源 **WeRetailMySQL** 在表单数据模型中配置。

   ![default-fdm](assets/default-fdm.png)

1. 展开WeRailMySQL数据源树。 从中选择以下数据模型对象和服务 **Weretail** > **customerdetails** 架构以便于形成数据模型：

   * **数据模型对象**：

      * id
      * name
      * shippingAddress
      * 城市
      * 州/省
      * 邮政编码

   * **服务：**

      * get
      * 更新

   选择 **添加选定项** 将选定的数据模型对象和服务添加到表单数据模型。

   ![WeRetail架构](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >为JDBC数据源提供的默认get、update和insert服务是现成的表单数据模型。

1. 配置数据模型对象的读取和写入服务。

   1. 选择 **customerdetails** 数据模型对象并选择 **[!UICONTROL 编辑属性]**.
   1. 选择 **[!UICONTROL get]** 从“读取服务”下拉列表中进行访问。 此 **id** 参数，将自动添加customerdetails数据模型对象中的主键。 选择 ![aem_6_3_edit](assets/aem_6_3_edit.png) 并按照以下方式配置参数。

      ![读取默认值](assets/read-default.png)

   1. 同样，选择 **[!UICONTROL 更新]** 作为写入服务。 此 **customerdetails** 对象会自动添加为参数。 参数的配置如下所示。

      ![write-default](assets/write-default.png)

      按如下方式添加和配置 **id** 参数。

      ![id-arg](assets/id-arg.png)

   1. 选择“完成&#x200B;]**”**[!UICONTROL &#x200B;以保存数据模型对象属性。然后，选择 **[!UICONTROL 保存]** 以保存表单数据模型。

      此 **[!UICONTROL get]** 和 **[!UICONTROL 更新]** 服务作为数据模型对象的默认服务添加。

      ![data-model-object](assets/data-model-object.png)

1. 转到 **[!UICONTROL 服务]** 选项卡和配置 **[!UICONTROL get]** 和 **[!UICONTROL 更新]** 服务。

   1. 选择 **[!UICONTROL get]** 服务和选择 **[!UICONTROL 编辑属性]**. 将打开属性对话框。
   1. 在“编辑属性”对话框中指定以下内容：

      * **标题**：指定服务的标题。 例如：检索送货地址。
      * **描述**：指定包含服务详细功能的描述。 例如：

        本服务从以下位置检索送货地址和其他客户详细信息： [!DNL MySQL] 数据库

      * **输出模型对象**：选择包含客户数据的架构。 例如：

        customerdetail架构

      * **返回数组**：禁用 **返回数组** 选项。
      * **参数**：选择名为的参数 **ID**.

      选择 **[!UICONTROL 完成]**. 用于从MySQL数据库检索客户详细信息的服务已配置。

      ![shiping-address-retrieval](assets/shiiping-address-retrieval.png)

   1. 选择 **[!UICONTROL 更新]** 服务和选择 **[!UICONTROL 编辑属性]**. 将打开属性对话框。

   1. 在 [!UICONTROL 编辑属性] 对话框：

      * **标题**：指定服务的标题。 例如，更新送货地址。
      * **描述**：指定包含服务详细功能的描述。 例如：

        此服务更新MySQL数据库中的送货地址和相关字段

      * **输入模型对象**：选择包含客户数据的架构。 例如：

        customerdetail架构

      * **输出类型**：选择 **布尔型**.

      * **参数**：选择参数名称 **ID** 和 **customerdetails**.

      选择 **[!UICONTROL 完成]**. 此 **[!UICONTROL 更新]** 服务以更新客户详细信息，请参见 [!DNL MySQL] 数据库已配置。

      ![shiping-address-update](assets/shiiping-address-update.png)

配置表单数据模型中的数据模型对象和服务。 您现在可以测试表单数据模型。

## 步骤4：测试表单数据模型 {#test-fdm}

您可以测试数据模型对象和服务，以验证是否正确配置了表单数据模型。

执行以下操作以运行测试：

1. 转到 **[!UICONTROL 模型]** 选项卡，选择 **customerdetails** 数据模型对象，并选择 **[!UICONTROL 测试模型对象]**.
1. 在 [!UICONTROL 测试模型/服务] 窗口，选择 **[!UICONTROL 读取模型对象]** 从 **[!UICONTROL 选择模型/服务]** 下拉菜单。
1. 在 **customerdetails** 部分，指定值 **id** 已配置中存在的参数 [!DNL MySQL] 数据库和选择 **[!UICONTROL 测试]**.

   系统将获取与指定ID关联的客户详细信息，并将其显示在 **[!UICONTROL 输出]** 部分，如下所示。

   ![test-read-model](assets/test-read-model.png)

1. 同样，您可以测试Write模型对象和服务。

   在以下示例中，更新服务成功地更新了数据库中ID 7102715的地址详细信息。

   ![test-write-model](assets/test-write-model.png)

   现在，如果您再次测试id 7107215的读取模型服务，它将获取并显示更新的客户详细信息，如下所示。

   ![已读取已更新](assets/read-updated.png)


>[!NOTE]
>
> 您可以使用自适应表单中的表单数据模型创建和使用SharePoint列表配置，以在SharePoint列表中保存数据或生成的记录文档。 请参阅 [将自适应表单连接到Microsoft® SharePoint列表](/help/forms/using/configuring-submit-actions.md#create-a-sharepoint-list-configuration)，以了解详细步骤。