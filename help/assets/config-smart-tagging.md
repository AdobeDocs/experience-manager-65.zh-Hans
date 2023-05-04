---
title: 使用智能内容服务配置资产标记
description: 了解如何在 [!DNL Adobe Experience Manager]，使用智能内容服务。
contentOwner: AG
role: Admin
feature: Tagging,Smart Tags
exl-id: 9f68804f-ba15-4f83-ab1b-c249424b1396
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '2245'
ht-degree: 25%

---

# 准备 [!DNL Assets] 用于智能标记 {#configure-asset-tagging-using-the-smart-content-service}

在开始使用智能内容服务标记资产之前，请先集成 [!DNL Experience Manager Assets] 与Adobe Developer Console一起使用 [!DNL Adobe Sensei]. 配置完毕后，可使用一些图像和标记来培训服务。

>[!NOTE]
>
>* 智能内容服务不再可用于新 [!DNL Experience Manager Assets] 内部部署客户。 已启用此功能的现有内部部署客户可以继续使用智能内容服务。
>* 智能内容服务适用于现有 [!DNL Experience Manager Assets] 已启用此功能的Managed Services客户。
>* 新建 [!DNL Experience Manager Assets] Managed Services客户可以按照本文中所述的说明来设置智能内容服务。


在使用智能内容服务之前，请确保：

* [使用 Adobe 开发人员控制台进行集成](#integrate-adobe-io).
* [培训智能内容服务](#training-the-smart-content-service).

* 安装最新 [[!DNL Experience Manager] Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html).

## 使用 Adobe 开发人员控制台进行集成 {#integrate-adobe-io}

当您与Adobe Developer控制台集成时， [!DNL Experience Manager] 服务器在将您的请求转发到智能内容服务之前，会使用Adobe Developer Console网关验证您的服务凭据。 要进行集成，您需要具有组织管理员权限的Adobe ID帐户，以及为贵组织购买并启用的智能内容服务许可证。

要配置智能内容服务，请执行以下顶级步骤：

1. 要生成公钥， [创建智能内容服务](#obtain-public-certificate) 配置 [!DNL Experience Manager]. 为 OAuth 集成[获取公共证书](#obtain-public-certificate)。

1. [在 Adobe 开发人员控制台中创建集成](#create-adobe-i-o-integration)，并上传生成的公共密钥。

1. [配置部署](#configure-smart-content-service) 使用Adobe Developer Console中的API密钥和其他凭据。

1. [测试配置](#validate-the-configuration)。

1. （可选） [在资产上传时启用自动标记](#enable-smart-tagging-in-the-update-asset-workflow-optional).

### 通过创建智能内容服务配置获取公共证书 {#obtain-public-certificate}

公共证书允许您在 Adobe 开发人员控制台上验证配置文件。

1. 在 [!DNL Experience Manager] 用户界面，访问 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL 旧版Cloud Services]**.

1. 在“Cloud Services”页面中，单击 **[!UICONTROL 立即配置]** 在 **[!UICONTROL 资产智能标记]**.

1. 在 **[!UICONTROL 创建配置]** 对话框，为智能标记配置指定标题和名称。 单击&#x200B;**[!UICONTROL 创建]**。

1. 在 **[!UICONTROL AEM Smart Content Service]** 对话框，请使用以下值：

   **[!UICONTROL 服务 URL]**: `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`

   例如， `https://smartcontent.adobe.io/apac`. 您可以指定 `na`, `emea`，或 `apac` 作为托管Experience Manager创作实例的区域。

   >[!NOTE]
   >
   >如果Experience Manager托管服务是在2022年9月01日之前配置的，请使用以下服务URL:
   >`https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 授权服务器]**: `https://ims-na1.adobelogin.com`

   暂时将其他字段留空（稍后提供）。 单击&#x200B;**[!UICONTROL 确定]**。

   ![Experience Manager智能内容服务对话框，用于提供内容服务URL](assets/aem_scs.png)


   *图：用于提供内容服务URL的智能内容服务对话框*

   >[!NOTE]
   >
   >提供的URL [!UICONTROL 服务URL] 无法通过浏览器访问，并生成404错误。 配置与 [!UICONTROL 服务URL] 参数。 有关整体服务状态和维护计划，请参阅 [https://status.adobe.com](https://status.adobe.com).

1. 单击 **[!UICONTROL 下载用于OAuth集成的公共证书]**，并下载公共证书文件 `AEM-SmartTags.crt`.

   ![为智能标记服务创建的设置的表示形式](assets/smart-tags-download-public-cert.png)


   *图：智能标记服务的设置。*

#### 证书过期后重新配置 {#certrenew}

证书过期后，将不再受信任。 无法续订已过期的证书。要添加证书，请执行以下步骤。

1. 以管理员身份登录 [!DNL Experience Manager] 部署。单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 用户]**。

1. 找到并单击 **[!UICONTROL dam-update-service]** 用户。单击 **[!UICONTROL 密钥库]** 选项卡。

1. 删除包含已过期证书的现有 **[!UICONTROL similaritysearch]** KeyStore。单击&#x200B;**[!UICONTROL 保存并关闭]**。

   ![删除Keystore中的现有相似性搜索条目以添加安全证书](assets/smarttags_delete_similaritysearch_keystore.png)


   *图：删除现有 `similaritysearch` 密钥库中的条目，以添加安全证书。*

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 云服务]** > **[!UICONTROL 旧版云服务]**。单击 **[!UICONTROL 资产智能标记]** >显 **[!UICONTROL 示配置]** >可 **[!UICONTROL 用配置]**。 单击所需的配置。

1. 要下载公共证书，请单击 **[!UICONTROL 下载用于OAuth集成的公共证书]**.

1. 访问 [https://console.adobe.io](https://console.adobe.io) ，并导航到 **[!UICONTROL 集成]** 页面。 上传新证书。 有关更多信息，请参阅 [创建Adobe Developer控制台集成](#create-adobe-i-o-integration).

### 创建Adobe Developer控制台集成 {#create-adobe-i-o-integration}

要使用智能内容服务API，请在Adobe Developer控制台中创建集成以获取 [!UICONTROL API密钥] (生成于 [!UICONTROL 客户端ID] 字段)、 [!UICONTROL 技术帐户ID], [!UICONTROL 组织ID]和 [!UICONTROL 客户端密钥] 表示 [!UICONTROL 资产智能标记服务设置] 云配置在 [!DNL Experience Manager].

1. 在浏览器中访问 [https://console.adobe.io](https://console.adobe.io/)。选择相应的帐户并验证关联的组织角色是否为系统管理员。

1. 创建具有任何所需名称的项目。单击&#x200B;**[!UICONTROL 添加 API]**。

1. 在&#x200B;**[!UICONTROL 添加 API]** 页面中，依次选择 **[!UICONTROL Experience Cloud]** 和&#x200B;**[!UICONTROL 智能内容]**。单击&#x200B;**[!UICONTROL 下一步]**。

1. 选择&#x200B;**[!UICONTROL 上传您的公共密钥]**。提供从 [!DNL Experience Manager] 下载的证书文件。此时将显示“[!UICONTROL 公共密钥上传成功]”消息。单击&#x200B;**[!UICONTROL 下一步]**。

   [!UICONTROL 创建新的服务帐户(JWT)凭据] 页面显示服务帐户的公共密钥。

1. 单击&#x200B;**[!UICONTROL 下一步]**。

1. 在&#x200B;**[!UICONTROL 选择产品配置文件]**&#x200B;页面上，选择&#x200B;**[!UICONTROL 智能内容服务]**。单击&#x200B;**[!UICONTROL 保存配置的 API]**。

   页面会显示有关配置的更多信息。保持此页面处于打开状态，以复制这些值并将其添加到 [!UICONTROL 资产智能标记服务设置] 云配置在 [!DNL Experience Manager] 配置智能标记。

   ![在“概述”选项卡中，您可以查看为集成提供的信息。](assets/integration_details.png)


   *图：Adobe Developer控制台中集成的详细信息*

### 配置智能内容服务 {#configure-smart-content-service}

要配置集成，请使用 [!UICONTROL 技术帐户ID], [!UICONTROL 组织ID], [!UICONTROL 客户端密钥]和 [!UICONTROL 客户端ID] 字段。 创建智能标记云配置后，可以对 [!DNL Experience Manager] 部署。

1. 在 [!DNL Experience Manager]，导航到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL 旧版Cloud Services]** 打开 [!UICONTROL Cloud Services] 控制台。

1. 在 **[!UICONTROL 资产智能标记]**，打开上面创建的配置。 在“服务设置”页面上，单击 **[!UICONTROL 编辑]**.

1. 在 **[!UICONTROL AEM 智能内容服务]**&#x200B;对话框中，为&#x200B;**[!UICONTROL 服务 URL]** 和&#x200B;**[!UICONTROL 授权服务器]**&#x200B;字段使用预填充的值。

1. 对于字段 [!UICONTROL Api密钥], [!UICONTROL 技术帐户ID], [!UICONTROL 组织ID]和 [!UICONTROL 客户端密钥]，复制并使用在 [Adobe Developer控制台集成](#create-adobe-i-o-integration).

   | [!UICONTROL 资产智能标记服务设置] | [!DNL Adobe Developer Console] 集成字段 |
   |--- |--- |
   | [!UICONTROL API 键] | [!UICONTROL 客户端ID] |
   | [!UICONTROL 技术帐户 ID] | [!UICONTROL 技术帐户ID] |
   | [!UICONTROL 组织 ID] | [!UICONTROL 组织 ID] |
   | [!UICONTROL 客户端密钥] | [!UICONTROL 客户端密钥] |

### 验证配置 {#validate-the-configuration}

完成配置后，可使用JMX MBean验证配置。 要验证，请执行以下步骤。

1. 访问 [!DNL Experience Manager] 服务器位置 `https://[aem_server]:[port]`.

1. 转到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]** 打开OSGi控制台。 单击 **[!UICONTROL 主要] > [!UICONTROL JMX]**.

1. 单击 `com.day.cq.dam.similaritysearch.internal.impl`. 随即会打开 **[!UICONTROL 相似性搜索其他任务]**.

1. 单击 `validateConfigs()`. 在 **[!UICONTROL 验证配置]** 对话框，单击 **[!UICONTROL 调用]**.

验证结果将显示在同一对话框中。

### 在 [!UICONTROL DAM更新资产] 工作流（可选） {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. 在 [!DNL Experience Manager]，转到 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**.

1. 在&#x200B;**[!UICONTROL 工作流模型]**&#x200B;页面上，选择 **[!UICONTROL DAM 更新资产]**&#x200B;工作流模式。

1. 单击工具栏中的&#x200B;**[!UICONTROL 编辑]**。

1. 展开侧面板以显示步骤。拖动 DAM 工作流部分中可用的&#x200B;**[!UICONTROL 智能标记资产]**&#x200B;步骤，并将其放在&#x200B;**[!UICONTROL 流程缩略图]**&#x200B;步骤之后。

   ![在 DAM 更新资产工作流中的流程缩略图步骤之后添加智能标记资产步骤](assets/smart-tag-in-dam-update-asset-workflow.png)

   *图：在 DAM 更新资产工作流中的流程缩略图步骤之后添加智能标记资产步骤。*

1. 在编辑模式下打开该步骤。在&#x200B;**[!UICONTROL 高级设置]**&#x200B;下，确保选中&#x200B;**[!UICONTROL 处理程序前进]**&#x200B;选项。

   ![配置DAM更新资产工作流并添加智能标记步骤](assets/smart-tag-step-properties-workflow1.png)


   *图：配置DAM更新资产工作流并添加智能标记步骤*

1. 在&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡中，如果希望完成工作流，请选择&#x200B;**[!UICONTROL 忽略错误]**，即使自动标记步骤失败也是如此。

   ![配置DAM更新资产工作流以添加智能标记步骤并选择处理程序高级](assets/smart-tag-step-properties-workflow2.png)


   *图：配置DAM更新资产工作流以添加智能标记步骤并选择处理程序高级*

   要在上传资产时标记资产，而不考虑是否对文件夹启用了智能标记，请选择&#x200B;**[!UICONTROL 忽略智能标记标志]**。

   ![配置DAM更新资产工作流以添加智能标记步骤，然后选择忽略智能标记标记](assets/smart-tag-step-properties-workflow3.png)


   *图：配置DAM更新资产工作流以添加智能标记步骤，然后选择忽略智能标记标记。*

1. 单击&#x200B;**[!UICONTROL 确定]**，以关闭流程步骤，然后保存工作流。

## 培训智能内容服务 {#training-the-smart-content-service}

为使智能内容服务能够识别您的业务分类，请在一组资产上运行该分类，这些资产已经包含与您的业务相关的标记。 为了有效地标记您的品牌图像，智能内容服务要求培训图像符合特定准则。 培训后，该服务可以对类似的资产集应用相同的分类。

您可以对服务进行多次培训，以提高其应用相关标记的能力。 在每个培训周期后，运行标记工作流并检查您的资产是否进行了正确标记。

您可以定期或根据需要培训智能内容服务。

>[!NOTE]
>
>培训工作流仅在文件夹上运行。

### 培训准则 {#guidelines-for-training}

为获得最佳结果，培训集中的图像符合以下准则：

**数量和大小：**&#x200B;每个标记至少 30 张图像。长边至少 500 像素。

**一致性**:用于特定标记的图像在视觉上相似。

例如，将所有这些图像标记为 `my-party` （用于培训），因为它们在视觉上并不相似。

![示例图像以说明培训准则](/help/assets/assets/do-not-localize/coherence.png)

**覆盖**:在培训中对图像使用足够的多样性。 其理念是提供几个但相当多样化的示例，以便Experience Manager学会专注于正确的事情。 如果您对视觉上不相似的图像应用相同的标记，请至少包含每种类型的五个示例。

例如，对于标记 *模型 — 下姿态*，为服务包含更多与下面突出显示的图像类似的培训图像，以便在标记期间更准确地识别类似图像。

![示例图像以说明培训准则](/help/assets/assets/do-not-localize/coverage_1.png)

**干扰/阻碍**:该服务能够更好地训练分散注意力的图像（突出的背景、不相关的伴奏，如主题的物体/人）。

例如，对于标记 *休闲鞋*&#x200B;第二张图像不是好的训练候选者。

![示例图像以说明培训准则](/help/assets/assets/do-not-localize/distraction.png)

**完整性：**&#x200B;如果图像符合多个标记的条件，请在包含培训图像之前添加所有适用的标记。例如，对于 `raincoat` 和 `model-side-view` 等标记，在将其加入培训之前，在符合条件的资产上添加这两个标记。

![示例图像以说明培训准则](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>智能内容服务是否能够在您的标记上进行培训并将其应用于其他图像，取决于您用于培训的图像质量。 为获得最佳结果，Adobe建议您使用视觉上相似的图像来为每个标记培训服务。

### 定期培训 {#periodic-training}

您可以启用智能内容服务，以便对文件夹中的资产和关联的标记进行定期培训。 打开 [!UICONTROL 属性] 页面，选择 **[!UICONTROL 启用智能标记]** 下 **[!UICONTROL 详细信息]** ，然后保存更改。

![enable_smart_tags](assets/enable_smart_tags.png)

为文件夹选择此选项后， [!DNL Experience Manager] 自动运行培训工作流，以在文件夹资产及其标记上培训智能内容服务。 默认情况下，培训工作流每周在星期六凌晨12:30运行。

### 按需培训 {#on-demand-training}

您可以根据需要从工作流控制台中培训智能内容服务。

1. 在 [!DNL Experience Manager] 界面，转到 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**.
1. 从 **[!UICONTROL 工作流模型]** 页面，选择 **[!UICONTROL 智能标记培训]** 工作流，然后单击 **[!UICONTROL 启动工作流]** 中。
1. 在 **[!UICONTROL 运行工作流]** 对话框中，浏览到包含标记资产的有效负荷文件夹，以培训服务。
1. 指定工作流的标题并添加评论。 然后，单击 **[!UICONTROL 运行]**. 将提交资产和标记以供培训。

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>在处理文件夹中的资产以进行培训后，只会在后续培训周期中处理已修改的资产。

### 查看培训报告 {#viewing-training-reports}

要检查是否在资产培训集中的标记上对智能内容服务进行了培训，请从报表控制台中查看培训工作流报表。

1. 在 [!DNL Experience Manager] 界面，转到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 报表]**.
1. 在 **[!UICONTROL 资产报表]** 页面，单击 **[!UICONTROL 创建]**.
1. 选择 **[!UICONTROL 智能标记培训]** 报表，然后单击 **[!UICONTROL 下一个]** 中。
1. 指定报表的标题和描述。在&#x200B;**[!UICONTROL 计划报告]**&#x200B;下，保持选中&#x200B;**[!UICONTROL 立即]**&#x200B;选项。如果要安排以后的计划报告，请选择&#x200B;**[!UICONTROL 稍后]**，然后指定日期和时间。然后，单击 **[!UICONTROL 创建]** 中。
1. 在&#x200B;**[!UICONTROL 资产报表]**&#x200B;页面中，选择生成的报表。要查看报表，请单击 **[!UICONTROL 查看]** 中。
1. 查看报告的详细信息。

   报表显示您培训的标记的培训状态。**[!UICONTROL 培训状态]**&#x200B;列中的绿色表示已为标记培训“智能内容服务”。黄色表示服务未针对特定标记进行完整培训。在这种情况下，使用特定标记添加更多图像并运行培训工作流以在标签上完整地培训服务。

   如果在此报表中未看到标记，请再次为这些标记运行培训工作流。

1. 要下载报表，请从列表中选择该报表，然后单击 **[!UICONTROL 下载]** 中。 报表将下载为Microsoft Excel电子表格。

## 限制 {#limitations}

* 增强型智能标记基于图像及其标记的学习模型。 这些模型并非总能很好地识别标记。 智能内容服务的当前版本具有以下限制：

   * 无法识别图像中的细微差异。 例如，纤薄的衬衫与普通的衬衫。
   * 无法根据图像的微小模式/部分来识别标记。 例如，T恤上的徽标。
   * 区域设置支持标记 [!DNL Experience Manager] 支持。

* 要搜索带有智能标记（常规或增强）的资产，请使用 [!DNL Assets] Omnisearch（全文搜索）。 智能标记没有单独的搜索谓词。

>[!MORELIKETHIS]
>
>* [智能标记概述和如何培训智能标记](enhanced-smart-tags.md)
>* [有关智能标记的视频教程](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)

