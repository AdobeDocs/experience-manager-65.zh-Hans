---
title: 将Adobe Experience Manager与Dynamic Media Classic集成
description: 了解如何将Adobe Experience Manager与Dynamic Media Classic集成。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: f244cfb5-5550-4f20-92f0-bb296e2bf76e
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: tm+mt
source-wordcount: '5405'
ht-degree: 0%

---

# 将Adobe Experience Manager与Dynamic Media Classic集成 {#integrating-with-dynamic-media-classic-scene}

Adobe Dynamic Media Classic是一个托管解决方案，用于管理、增强、发布富媒体资产，并将其交付给Web、移动设备、电子邮件和连接到Internet的显示和打印。

要使用Dynamic Media Classic，您必须配置云配置，以便Dynamic Media Classic和Adobe Experience Manager Assets可以相互交互。 本文档介绍了如何配置Experience Manager和Dynamic Media Classic。

有关在页面上使用所有Dynamic Media Classic组件以及使用视频的信息，请参阅[使用Dynamic Media Classic](../assets/scene7.md)。

>[!NOTE]
>
>* Dynamic Media Classic的DHTML查看器平台于2014年1月31日正式终止使用。 有关详细信息，请参阅[DHTML查看器生命周期结束常见问题解答](../sites-administering/dhtml-viewer-endoflifefaqs.md)。
>* 在配置Dynamic Media Classic以使用Experience Manager之前，请参阅[将Dynamic Media Classic与Experience Manager集成的最佳实践](#best-practices-for-integrating-scene-with-aem)。
>* 如果您将Dynamic Media Classic与自定义代理配置一起使用，则必须同时配置HTTP客户端代理配置，因为Experience Manager的某些功能使用3.x API，而其他功能使用4.x API。 3.x使用[http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)进行配置，而4.x使用[http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)进行配置。
>

## Experience Manager/Dynamic Media Classic集成与Dynamic Media {#aem-scene-integration-versus-dynamic-media}

要与Dynamic Media配合使用，Experience Manager用户可以在两个解决方案之间进行选择。 您可以使用以下任一选项：

* 将Experience Manager实例与Dynamic Media Classic集成。
* 使用集成到Experience Manager中的Dynamic Media。

使用以下标准确定要选择的解决方案：

* 您是否是&#x200B;**现有的**&#x200B;个Dynamic Media Classic客户，其资产驻留在Dynamic Media Classic中以用于发布和交付，但您希望将这些资产与Sites (WCM)创作或Experience Manager Assets集成，或同时与这两者集成？ 如果是这样的话，请使用本文档中介绍的[Experience Manager/Dynamic Media Classic点对点集成](#aem-scene-point-to-point-integration)。

* 如果您是&#x200B;**新**&#x200B;的Experience Manager客户，具有富媒体交付需求，请选择[Dynamic Media选项](#aem-dynamic-media)。 如果您没有现有的S7帐户且系统中没有存储许多资产，则此选项最有意义。

* 在某些情况下，同时使用这两种解决方案。 [双重使用方案](/help/sites-administering/scene7.md#dual-use-scenario)描述了该方案。

### Experience Manager/Dynamic Media Classic点对点集成 {#aem-scene-point-to-point-integration}

在此解决方案中使用资产时，需要执行以下操作之一：

* 将资源直接上传到Dynamic Media Classic，然后通过&#x200B;**Dynamic Media Classic**&#x200B;内容浏览器进行访问以进行页面创作或
* 上传至Experience Manager Assets，然后启用自动发布至Dynamic Media Classic；您可以通过&#x200B;**Assets**&#x200B;内容浏览器访问以进行页面创作

在[设计模式](/help/sites-authoring/author-environment-tools.md#page-modes)的&#x200B;**Dynamic Media Classic**&#x200B;组件区域中找到用于此集成的组件。

### Experience Manager Dynamic Media {#aem-dynamic-media}

Experience Manager Dynamic Media是直接在Experience Manager平台中统一的Dynamic Media Classic功能。

在此解决方案中使用资产时，请遵循以下工作流程：

1. 将单个图像和视频资源直接上传到Experience Manager。
1. 直接在Experience Manager中对视频进行编码。
1. 直接在Experience Manager中构建基于图像的集。
1. 如果适用，请为图像或视频添加交互性。

在[设计模式](/help/sites-authoring/author-environment-tools.md#page-modes)的&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;组件区域中找到用于Dynamic Media的组件。 它们包括：

* **[!UICONTROL Dynamic Media]** - **[!UICONTROL Dynamic Media]**&#x200B;组件是智能的 — 根据您添加的是图像还是视频，您有各种选项。 该组件支持图像预设、基于图像的查看器（例如图像集、旋转集、混合媒体集和视频）。 此外，查看器具有响应性 — 屏幕大小根据屏幕大小自动更改。 所有查看者都是HTML5查看者。

* **[!UICONTROL 交互式媒体]** - **[!UICONTROL 交互式媒体]**&#x200B;组件适用于轮播横幅、交互式图像和交互式视频等资产。 此类资源具有交互性，可在其中使用热点或图像映射。 此组件是智能的。 也就是说，根据您添加的是图像还是视频，您有各种不同的选项。 此外，查看器具有响应性 — 屏幕大小根据屏幕大小自动更改。 所有查看者都是HTML5查看者。

### 两用方案 {#dual-use-scenario}

开箱即用地同时使用Experience Manager的Dynamic Media和Dynamic Media Classic集成功能。 以下用例表描述了何时打开和关闭某些区域。

要同时使用Dynamic Media和Dynamic Media Classic，请执行以下操作：

1. 在Cloud Service中配置[Dynamic Media Classic](#creating-a-cloud-configuration-for-scene)。
1. 按照用例的特定说明进行操作：

   <table>
    <tbody>
    <tr>
    <td> </td>
    <td> </td>
    <td><strong>Dynamic Media</strong></td>
    <td> </td>
    <td><strong>Dynamic Media Classic集成</strong></td>
    <td> </td>
    </tr>
    <tr>
    <td><strong>如果您……</strong></td>
    <td><strong>用例工作流</strong></td>
    <td><strong>成像/视频</strong></td>
    <td><strong>动态媒体组件</strong></td>
    <td><strong>S7内容浏览器和组件</strong></td>
    <td><strong>从Assets自动上传到S7</strong></td>
    </tr>
    <tr>
    <td>初次使用Sites和Dynamic Media</td>
    <td>将资源上传到Experience Manager并使用Experience Manager Dynamic Media组件在站点页面上创作资源</td>
    <td><p>在</p> <p>（请参阅步骤3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">在</a></td>
    <td>关闭</td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>零售业中，以及初次接触站点和Dynamic Media</td>
    <td>将非产品资产上传到Experience Manager以进行管理和交付。 将产品资产上传到Dynamic Media Classic，并使用Experience Manager中的Dynamic Media Classic内容浏览器和组件在站点上创作产品详细信息页面。</td>
    <td><p>在</p> <p>（请参阅步骤3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">在</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">在</a></td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>初次使用Assets和Dynamic Media</td>
    <td>将资源上传到Experience Manager Assets并使用从Dynamic Media发布的URL/嵌入代码</td>
    <td><p>在</p> <p>（请参阅步骤3）</p> </td>
    <td>关闭</td>
    <td>关闭</td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>初次使用Dynamic Media和模板</td>
    <td>使用Dynamic Media进行成像和视频处理。 在Dynamic Media Classic中创作图像模板，并使用Dynamic Media Classic内容查找器在Sites页面中包含模板。</td>
    <td><p>在</p> <p>（请参阅步骤3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">在</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">在</a></td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>现有Dynamic Media Classic客户和不熟悉Sites</td>
    <td>将资源上传到Dynamic Media Classic，并使用Experience Manager Dynamic Media Classic内容浏览器在站点页面上搜索和创作资源</td>
    <td>关闭</td>
    <td>关闭</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">在</a></td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>现有Dynamic Media Classic客户，并且是网站和Assets的新客户</td>
    <td>将资源上传到DAM并自动发布到Dynamic Media Classic以进行交付。 使用Experience Manager Dynamic Media Classic内容浏览器在站点页面上搜索和创作资源。</td>
    <td>关闭</td>
    <td>关闭</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">在</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">在</a></p> <p>（请参阅步骤4）</p> </td>
    </tr>
    <tr>
    <td>现有Dynamic Media Classic客户和Assets新客户</td>
    <td><p>将资源上传到Experience Manager并使用Dynamic Media生成演绎版以供下载/共享。 自动将Experience Manager资源发布到Dynamic Media Classic以进行交付。</p> <p><strong>重要信息：</strong>发生重复处理，并且在Experience Manager中生成的呈现版本未同步到Dynamic Media Classic</p> </td>
    <td><p>在</p> <p>（请参阅步骤3）</p> </td>
    <td>关闭</td>
    <td>关闭</td>
    <td><p><a href="#configuringautouploadingfromaemassets">在</a></p> <p>（请参阅步骤4）</p> </td>
    </tr>
    </tbody>
    </table>

1. （可选；请参阅用例表） — 设置[Dynamic Media云配置](/help/assets/config-dynamic.md)和[启用Dynamic Media服务器](/help/assets/config-dynamic.md)。
1. （可选；请参阅用例表） — 如果选择启用从Assets到Dynamic Media Classic的自动上传，则必须添加以下内容：

   1. 设置自动上传至Dynamic Media Classic。
   1. 在&#x200B;***Dam更新资产**&#x200B;工作流(`https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`)末尾的所有Dynamic Media工作流步骤*&#x200B;之后添加&#x200B;**Dynamic Media Classic上传**&#x200B;步骤
   1. （可选）在[https://&lt;服务器>：&lt;端口>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl)中按MIME类型限制Dynamic Media Classic资源上传。 此列表中未包含的资源MIME类型不会上传到Dynamic Media Classic服务器。
   1. （可选）在Dynamic Media Classic配置中设置视频。 您可以同时为Dynamic Media和/或Dynamic Media Classic启用视频编码。 在Experience Manager实例中，动态演绎版用于本地预览和播放，而Dynamic Media Classic视频演绎版则生成并存储在Dynamic Media Classic服务器上。 为Dynamic Media和Dynamic Media Classic设置视频编码服务时，请将[视频处理配置文件](/help/assets/video-profiles.md)应用于Dynamic Media Classic资源文件夹。
   1. （可选） [在Dynamic Media Classic中配置安全预览](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)。

#### 限制 {#limitations}

同时启用Dynamic Media Classic和Dynamic Media时，存在以下限制：

* 通过在Experience Manager页面上选择资源并将其拖动到Dynamic Media Classic组件来手动上传到Dynamic Media Classic不起作用。
* 即使在Assets中编辑Experience Manager-Dynamic Media Classic同步的资源时，该资源会自动更新到Dynamic Media Classic，但回滚操作不会触发新的上传。 因此，Dynamic Media Classic不会在回滚后立即获取最新版本。 解决方法是在回滚完成后再次编辑。
* 您是否需要将Dynamic Media用于一个用例，将Dynamic Media Classic集成用于另一个用例，以便Dynamic Media资源不会与Dynamic Media Classic系统交互？ 如果是这样的话，请不要将Dynamic Media Classic配置应用于Dynamic Media文件夹。 此外，请勿将Dynamic Media配置（处理配置文件）应用于Dynamic Media Classic文件夹。

## 将Dynamic Media Classic与Experience Manager集成的最佳实践 {#best-practices-for-integrating-scene-with-aem}

将Dynamic Media Classic与Experience Manager集成时，必须遵守以下方面的一些重要最佳实践：

* 测试推动您的集成
* 建议在某些情况下直接从Dynamic Media Classic上传资源

请参阅[已知限制](#known-limitations-and-design-implications)。

### 测试推动集成 {#test-driving-your-integration}

Adobe建议您让根文件夹仅指向子文件夹，而不是指向整个公司，来测试集成。

>[!CAUTION]
>
>从现有Dynamic Media Classic公司帐户导入资源可能需要很长时间才能在Experience Manager中显示。 确保在Dynamic Media Classic中指定一个没有太多资源的文件夹（例如，根文件夹通常拥有太多资源，可能会使系统崩溃）。

### 从Experience Manager Assets上传资源与从Dynamic Media Classic上传资源 {#uploading-assets-from-aem-assets-versus-from-scene}

您可以使用Assets（数字资产管理）功能上传资产，也可以直接通过Dynamic Media Classic内容浏览器在Experience Manager中访问Dynamic Media Classic 。 选择哪种方式取决于以下因素：

* 必须通过Dynamic Media Classic内容浏览器，直接从Dynamic Media Classic将Experience Manager Assets尚不支持的Dynamic Media Classic资产类型添加到Experience Manager网站。 例如，图像模板。
* 对于Experience Manager Assets和Dynamic Media Classic都支持的资源类型，决定如何上传它们取决于以下因素：

   * 资产当前所在的位置，以及
   * 在公共存储库中管理这些组件有多重要

假设这些资源已在Dynamic Media Classic中，在公共存储库中管理它们并不重要。 如果是这种情况，则将资产导出到Experience Manager Assets以仅将其同步回Dynamic Media Classic以进行交付是不必要的往返过程。 Adobe建议您将资产保留在单个存储库中，并同步到Dynamic Media Classic以便仅进行交付。

## 配置Dynamic Media Classic集成 {#configuring-scene-integration}

您可以配置Experience Manager以将资源上传到Dynamic Media Classic。 CQ目标文件夹中的Assets可以（自动或手动）从Experience Manager上传到Dynamic Media Classic公司帐户。

>[!NOTE]
>
>Adobe建议您仅使用指定的目标文件夹来导入Dynamic Media Classic资源。 位于目标文件夹之外的数字资产只能在已启用Dynamic Media Classic配置的页面上的Dynamic Media Classic组件中使用。 此外，它们还被放置在Dynamic Media Classic的按需文件夹中。 按需文件夹未与Experience Manager同步(但可在Dynamic Media Classic内容浏览器中搜索资产)。

**要将Dynamic Media Classic配置为与Experience Manager集成：**

1. [定义云配置](#creating-a-cloud-configuration-for-scene) — 定义Dynamic Media Classic文件夹和Assets文件夹之间的映射。 即使只想进行单向(Experience Manager Assets到Dynamic Media Classic)同步，请完成此步骤。
1. [启用&#x200B;**Adobe CQ s7dam Dam侦听器**](#enabling-the-adobe-cq-scene-dam-listener) — 在[!UICONTROL OSGi]控制台中完成。
1. 如果您希望Experience Manager Assets自动上传到Dynamic Media Classic，则必须打开该选项并将Dynamic Media Classic添加到[!UICONTROL DAM更新资产]工作流。 您还可以手动上传资源。
1. 将Dynamic Media Classic组件添加到Sidekick。 通过此功能，用户可在其Experience Manager页面上使用Dynamic Media Classic组件。
1. [将配置映射到Experience Manager中的页面](#enabling-scene-for-wcm) — 要查看您在Dynamic Media Classic中创建的任何视频预设，需要执行此步骤。 如果您必须执行从CQ Target文件夹外部将资源发布到Dynamic Media Classic，也需要使用该字段。

本节介绍如何执行所有这些步骤，并列出重要限制。

### Dynamic Media Classic与Experience Manager Assets之间的同步的工作原理 {#how-synchronization-between-scene-and-aem-assets-works}

在设置Experience Manager Assets和Dynamic Media Classic同步时，请务必了解以下内容：

#### 从Experience Manager Assets上传至Dynamic Media Classic {#uploading-to-scene-from-aem-assets}

* Experience Manager中有一个指定的同步文件夹用于Dynamic Media Classic上传。
* 如果将数字资源放在指定的同步文件夹中，则可以自动上传到Dynamic Media Classic。
* Experience Manager中的文件夹和子文件夹结构会在Dynamic Media Classic中进行复制。

>[!NOTE]
>
>Experience Manager在将所有元数据上传到XMP之前将其嵌入为Dynamic Media Classic，因此元数据节点上的所有属性在Dynamic Media Classic as XMP中均可用。

#### 已知限制和设计影响 {#known-limitations-and-design-implications}

在Experience Manager Assets和Dynamic Media Classic之间同步时，当前存在以下限制/设计影响：

<table>
 <tbody>
  <tr>
   <td><strong>限制/设计影响</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>一个指定的同步（目标）文件夹</td>
   <td>在Experience Manager中，每个公司只能有一个指定的文件夹用于Dynamic Media Classic上传。 如果您必须有权访问Dynamic Media Classic中的多个公司帐户，则可以创建多个配置。</td>
  </tr>
  <tr>
   <td>文件夹结构</td>
   <td>如果您删除与资源同步的文件夹，则将删除所有Dynamic Media Classic远程资源，但会保留该文件夹。</td>
  </tr>
  <tr>
   <td>按需文件夹</td>
   <td>位于Target文件夹以外且WCM中手动上传到Dynamic Media Classic的Assets会自动放置在Dynamic Media Classic上的单独按需文件夹中。 您可以在Experience Manager的云配置中配置此文件夹。</td>
  </tr>
  <tr>
   <td>混合媒体</td>
   <td>混合媒体集显示在Experience Manager中，但Experience Manager不支持它们。</td>
  </tr>
  <tr>
   <td>PDF</td>
   <td>从Dynamic Media Classic中的eCatalogs生成的PDF将导入到CQ目标文件夹中。</td>
  </tr>
  <tr>
   <td>UI刷新</td>
   <td>在Experience Manager和Dynamic Media Classic之间同步时，请确保刷新用户界面以查看更改。 </td>
  </tr>
  <tr>
   <td>视频缩略图</td>
   <td>如果通过Dynamic Media Classic将视频上传到Experience Manager Assets进行编码，则视频缩略图和编码的视频可能需要一些时间才能在Experience Manager Assets中使用，具体取决于视频处理时间。</td>
  </tr>
  <tr>
   <td>目标子文件夹</td>
   <td><p>如果在目标文件夹中使用子文件夹，请确保为每个资源使用唯一名称（不考虑位置）。 此外，请确保将Dynamic Media Classic（在“设置”区域中）配置为不覆盖资源，而不管位置如何。</p> <p>否则，虽然会上传上传上传到Dynamic Media Classic目标子文件夹的同名资源，但会删除目标文件夹中的同名资源。 </p> </td>
  </tr>
 </tbody>
</table>

### 配置Dynamic Media Classic服务器 {#configuring-scene-servers}

如果您在代理后运行Experience Manager或具有特殊的防火墙设置，则必须明确启用不同区域的主机。 服务器在`/etc/cloudservices/scene7/endpoints`中的内容中进行管理，并且可以根据需要进行自定义。 选择一个URL，然后进行编辑以更改该URL（如有必要）。 在Experience Manager的早期版本中，这些值进行了硬编码。

如果导航到`/etc/cloudservices/scene7/endpoints.html`，您将看到列出的服务器（可以通过点按URL来编辑它们）：

![chlimage_1-296](assets/chlimage_1-296.png)

### 为Dynamic Media Classic创建云配置 {#creating-a-cloud-configuration-for-scene}

云配置定义Dynamic Media Classic文件夹和Experience Manager Assets文件夹之间的映射。 必须将其配置为将Experience Manager Assets与Dynamic Media Classic同步。 有关更多信息，请参阅同步的工作方式。

>[!CAUTION]
>
>从现有Dynamic Media Classic公司帐户导入资源可能需要很长时间才能在Experience Manager中显示。 确保在Dynamic Media Classic中指定了没有太多资源的文件夹。 例如，根文件夹通常包含太多资产。
>
>如果要测试集成，请将根文件夹仅指向子文件夹，而不是指向整个公司。

>[!NOTE]
>
>您可以有多个配置：一个云配置表示一家Dynamic Media Classic公司的一名用户。 如果要访问其他Dynamic Media Classic公司或用户，则必须创建多个配置。

**要为Dynamic Media Classic创建云配置：**

1. 选择Experience Manager图标并导航到&#x200B;**[!UICONTROL 部署]** > **[!UICONTROL 云服务]**，以便您可以访问Adobe Dynamic Media Classic。

1. 选择&#x200B;**[!UICONTROL 立即配置]**。

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. 在&#x200B;**[!UICONTROL Title]**&#x200B;字段和&#x200B;**[!UICONTROL Name]**&#x200B;字段中（可选），输入适当的信息。 选择&#x200B;**[!UICONTROL 创建]**。

   >[!NOTE]
   >
   >创建更多配置时，将显示&#x200B;**[!UICONTROL 父配置]**&#x200B;字段。
   >
   >请&#x200B;**不**&#x200B;更改父配置。 更改父配置可能会中断集成。

1. 输入Dynamic Media Classic帐户的电子邮件地址、密码和区域，然后选择&#x200B;**[!UICONTROL 连接到Dynamic Media Classic]**。 您已连接到Dynamic Media Classic服务器，并且对话框随即展开，其中包含更多选项。

1. 输入&#x200B;**[!UICONTROL 公司]**&#x200B;名称和&#x200B;**[!UICONTROL 根路径]**。 此信息是已发布的服务器名称以及您要指定的任何路径。 如果您不知道已发布的服务器名称，请在Dynamic Media Classic中转到&#x200B;**[!UICONTROL 设置>应用程序设置]**。

   >[!NOTE]
   >
   >Dynamic Media Classic根路径是Experience Manager连接到的Dynamic Media Classic文件夹。 可将其缩小到特定文件夹。

   >[!CAUTION]
   >
   >根据Dynamic Media Classic文件夹的大小，导入根文件夹可能需要较长时间。 此外，Dynamic Media Classic数据可能会超过Experience Manager存储空间。 确保您正在导入正确的文件夹。 导入太多数据可能会阻止系统。

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. 选择&#x200B;**[!UICONTROL 确定]**。 Experience Manager可保存您的配置。

>[!NOTE]
>
>如果您正在重新连接：
>
>* 在发布时重新连接到Dynamic Media Classic时，在发布或重新连接时重置密码不起作用（在创作实例上不是问题）。
>* 如果您修改了地区、公司名称等值，则必须重新连接到Dynamic Media Classic。 如果配置选项已被修改但未保存，则Experience Manager仍会错误地指示配置有效。 确保重新连接。
>

### 启用Adobe CQ Dynamic Media Classic Dam侦听器 {#enabling-the-adobe-cq-scene-dam-listener}

启用Adobe CQ Dynamic Media Classic Dam侦听器，默认情况下将禁用此项。

**要启用Adobe CQ Dynamic Media Classic Dam侦听器：**

1. 选择[!UICONTROL 工具]图标，然后导航到&#x200B;**[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。
1. 在Web控制台中，导航到&#x200B;**[!UICONTROL Adobe CQ Dynamic Media Classic Dam侦听器]**，并选择&#x200B;**[!UICONTROL 已启用]**&#x200B;复选框。

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. 选择&#x200B;**[!UICONTROL 保存]**。

### 向Dynamic Media Classic上传工作流程添加可配置超时 {#adding-configurable-timeout-to-scene-upload-workflow}

当Experience Manager实例配置为通过Dynamic Media Classic处理视频编码时，默认情况下，任何上传作业都有35分钟的超时。 要适应可能运行时间较长的视频编码作业，可以配置此设置。

1. 导航到&#x200B;**http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**。

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. 根据需要在&#x200B;**[!UICONTROL 活动作业超时]**&#x200B;字段中更改该数字。 可接受任何非负数，度量单位以秒为单位。 默认情况下，此数字设置为2100。

   >[!NOTE]
   >
   >最佳实践：大多数资产最多可在几分钟内摄取（例如，图像）。 但在某些情况下（例如较大的视频），为了适应较长的处理时间，会将超时值增加到7200秒（两个小时）。 否则，此Dynamic Media Classic上载作业在JCR (Java™内容存储库)元数据中被标记为&#x200B;**[!UICONTROL UploadFailed]**。

1. 选择&#x200B;**[!UICONTROL 保存]**。

### 从Experience Manager Assets自动上传 {#autouploading-from-aem-assets}

从Experience Manager 6.3.2开始，如果上传的数字资源位于CQ目标文件夹中，则对Experience Manager Assets进行配置，以便将这些资源更新到Dynamic Media Classic。

将资源添加到Experience Manager Assets后，该资源会自动上传并发布到Dynamic Media Classic。

>[!NOTE]
>
>从Experience Manager Assets自动上传到Dynamic Media Classic的最大文件大小为500 MB。

**从Experience Manager Assets自动上传：**

1. 选择Experience Manager图标并导航到&#x200B;**[!UICONTROL 部署]** > **[!UICONTROL 云服务]**。
1. 在Dynamic Media标题下的可用配置下，选择&#x200B;**[!UICONTROL dms7 (Dynamic Media]**)。
1. 选择&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡，选中&#x200B;**[!UICONTROL 启用自动上传]**&#x200B;复选框，然后选择&#x200B;**[!UICONTROL 确定]**。 配置DAM资源工作流以包括上传至Dynamic Media Classic。

   >[!NOTE]
   >
   >有关将处于未发布状态的资源推送到Dynamic Media Classic的信息，请参阅[配置推送到Dynamic Media Classic的资源状态（已发布/未发布）](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)。

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. 导航回Experience Manager欢迎页面，然后选择&#x200B;**[!UICONTROL 工作流]**。 双击&#x200B;**DAM更新资产**&#x200B;工作流，以将其打开。
1. 在Sidekick中，导航到&#x200B;**[!UICONTROL 工作流]**&#x200B;组件，然后选择&#x200B;**[!UICONTROL Dynamic Media Classic]**。 将&#x200B;**[!UICONTROL Dynamic Media Classic]**&#x200B;拖到工作流中，然后选择&#x200B;**[!UICONTROL 保存]**。 在target文件夹中添加到Experience Manager Assets的Assets会自动上传到Dynamic Media Classic。

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* 在自动化后添加资源时，如果它们未放置在CQ目标文件夹中，则不会上传到Dynamic Media Classic。
   >* Experience Manager在将所有元数据上传到XMP之前将其嵌入为Dynamic Media Classic，因此元数据节点上的所有属性在Dynamic Media Classic as XMP中均可用。

### 配置推送到Dynamic Media Classic的资源状态（已发布/未发布） {#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}

如果您将资产从Experience Manager Assets推送到Dynamic Media Classic，则可以自动发布它们（默认行为）或以未发布状态将它们推送到Dynamic Media Classic。

如果要在上线前在暂存环境中测试资产，则可能不希望立即在Dynamic Media Classic上发布资产。 您可以将Experience Manager与Dynamic Media Classic的安全测试环境一起使用，以未发布状态将资产直接从Assets推送到Dynamic Media Classic。

Dynamic Media Classic资源仍可通过安全预览使用。 只有在Experience Manager中发布资源后，Dynamic Media Classic资源才会正式上线。

如果要将资源推送到Dynamic Media Classic时立即发布资源，则无需配置任何选项。 此功能是默认行为。

但是，如果您不希望推送到Dynamic Media Classic的资源自动发布，本节将介绍如何配置Experience Manager和Dynamic Media Classic以执行此操作。

#### 将资源推送到Dynamic Media Classic的先决条件已取消发布 {#prerequisites-to-push-assets-to-scene-unpublished}

在将资源推送到Dynamic Media Classic而不发布它们之前，您必须设置以下设置：

1. [使用Admin Console创建支持案例](https://helpx.adobe.com/cn/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)。 在您的支持案例中，请求为您的Dynamic Media Classic帐户启用安全预览。
1. [为您的Dynamic Media Classic帐户设置安全预览](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html)。

这些步骤与在Dynamic Media Classic中创建任何安全测试设置时所遵循的步骤相同。

#### 推送处于未发布状态的资产的已知限制  {#known-limitations-for-pushing-assets-in-unpublished-state}

如果使用此功能，请注意以下限制：

* 不支持版本控制。
* 如果资产已在Experience Manager中发布并创建了后续版本，则会立即将新版本实时发布到生产环境。 激活时发布仅适用于资产的初始发布。

>[!NOTE]
>
>如果要立即发布资产，最佳实践是将&#x200B;**[!UICONTROL 启用安全预览]**&#x200B;保持设置为&#x200B;**[!UICONTROL 立即]**，并使用&#x200B;**[!UICONTROL 启用自动上传]**&#x200B;功能。

### 将推送到Dynamic Media Classic的资源状态设置为未发布 {#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>如果用户在Experience Manager中发布资产，则会自动将S7资产触发到生产/实时资产（资产不再处于安全预览/取消发布状态）。

**要将推送到Dynamic Media Classic的资源状态设置为未发布，请执行以下操作：**

1. 选择Experience Manager图标并导航到&#x200B;**[!UICONTROL 部署]** > **[!UICONTROL 云服务]**。
1. 选择&#x200B;**[!UICONTROL Dynamic Media Classic]**。
1. 在Dynamic Media Classic中选择您的配置。
1. 选择&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。
1. 在&#x200B;**[!UICONTROL 启用安全视图]**&#x200B;下拉菜单中，选择&#x200B;**[!UICONTROL 在AEM发布激活时]**&#x200B;以将资产推送到Dynamic Media Classic而不发布。 (默认情况下，此值设置为&#x200B;**[!UICONTROL 立即]**，其中立即发布Dynamic Media Classic资源。)

   有关在公开资源之前测试资源的更多信息，请参阅[Dynamic Media Classic文档](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html)。

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. 选择&#x200B;**[!UICONTROL 确定]**。

启用安全预览意味着您的资产将推送到未发布的安全预览服务器。

要查看是否已启用&#x200B;**[!UICONTROL 安全预览]**，请在Experience Manager的某个页面上导航到Dynamic Media Classic组件。 选择&#x200B;**[!UICONTROL 编辑]**。 资产的URL中列出了安全预览服务器。 在Experience Manager中发布后，文件引用中的服务器域将从预览URL更新为生产URL。

### 为WCM启用Dynamic Media Classic {#enabling-scene-for-wcm}

出于以下两个原因，需要为WCM启用Dynamic Media Classic：

* 它可启用通用视频配置文件的下拉列表以进行页面创作。 如果没有此列表，**[!UICONTROL 通用视频预设]**&#x200B;下拉列表将为空且无法设置。
* 如果数字资产不在目标文件夹中，且您在页面属性中为该页面启用了Dynamic Media Classic，则可以将资产上传到Dynamic Media Classic。 然后将资源拖放到Dynamic Media Classic组件上。 常规的继承规则适用（这意味着子页面从父页面继承配置）。

与其他配置一样，为WCM启用Dynamic Media Classic时，继承规则适用。 您可以在触控优化或经典用户界面中启用适用于WCM的Dynamic Media Classic 。

#### 在触控优化用户界面中启用适用于WCM的Dynamic Media Classic {#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}

1. 选择Experience Manager图标并导航到&#x200B;**[!UICONTROL 站点]**，然后导航到网站的根页面（非特定语言）。

1. 在工具栏中，选择[!UICONTROL 设置]图标，然后选择&#x200B;**[!UICONTROL 打开属性]**。

1. 选择&#x200B;**[!UICONTROL 云服务]**&#x200B;并选择&#x200B;**[!UICONTROL 添加配置]**&#x200B;并选择&#x200B;**[!UICONTROL Dynamic Media Classic]**。
1. 在&#x200B;**[!UICONTROL Adobe Dynamic Media Classic]**&#x200B;下拉列表中，选择所需的配置并选择&#x200B;**[!UICONTROL 确定]**。

   ![chlimage_1-303](assets/chlimage_1-303.png)

   来自该Dynamic Media Classic配置的视频预设可用于该页面和子页面上的Experience Manager以及Dynamic Media Classic视频组件。

#### 在Classic用户界面中启用适用于WCM的Dynamic Media Classic {#enabling-scene-for-wcm-in-the-classic-user-interface}

1. 在Experience Manager中，选择&#x200B;**[!UICONTROL 网站]**&#x200B;并导航到网站的根页面（非特定语言）。

1. 在Sidekick中，选择&#x200B;**[!UICONTROL 页面]**&#x200B;图标，然后选择&#x200B;**[!UICONTROL 页面属性]**。

1. 选择&#x200B;**[!UICONTROL 云服务]** > **[!UICONTROL 添加服务]** > **[!UICONTROL Dynamic Media Classic]**。
1. 在&#x200B;**[!UICONTROL Adobe Dynamic Media Classic]**&#x200B;下拉列表中，选择所需的配置并选择&#x200B;**[!UICONTROL 确定]**。

   来自该Dynamic Media Classic配置的视频预设可用于该页面和子页面上的Experience Manager以及Dynamic Media Classic视频组件。

### 配置默认配置 {#configuring-a-default-configuration}

如果您有多个Dynamic Media Classic配置，则可以指定其中一个配置作为Dynamic Media Classic内容浏览器的默认配置。

在给定时刻，只能将一个Dynamic Media Classic配置标记为默认。 默认配置是默认显示在Dynamic Media Classic内容浏览器中的公司资源。

**要配置默认配置：**

1. 选择Experience Manager图标并导航到&#x200B;**[!UICONTROL 部署]** > **[!UICONTROL 云服务]**。
1. 选择&#x200B;**[!UICONTROL Dynamic Media Classic]**。
1. 在Dynamic Media Classic中选择您的配置。
1. 要打开配置，请选择&#x200B;**[!UICONTROL 编辑]**。

1. 在&#x200B;**[!UICONTROL 常规]**&#x200B;选项卡中，选中&#x200B;**[!UICONTROL 默认配置]**&#x200B;复选框，使其成为Dynamic Media Classic内容浏览器中显示的默认公司和根路径。

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >如果只有一个配置，则选中&#x200B;**[!UICONTROL 默认配置]**&#x200B;复选框不会产生任何效果。

### 配置临时文件夹 {#configuring-the-ad-hoc-folder}

您可以根据需要配置一个文件夹，当资产不在CQ目标文件夹中时，该文件夹可在Dynamic Media Classic中上传资产。 请参阅从CQ目标文件夹外部发布资产。

**配置临时文件夹：**

1. 选择Experience Manager图标并导航到&#x200B;**[!UICONTROL 部署]** > **[!UICONTROL 云服务]**。
1. 选择&#x200B;**[!UICONTROL Dynamic Media Classic]**。
1. 在Dynamic Media Classic中选择您的配置。
1. 要打开配置，请选择&#x200B;**[!UICONTROL 编辑]**。

1. 选择&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。 在&#x200B;**[!UICONTROL 临时文件夹]**&#x200B;字段中，您可以修改&#x200B;**临时文件夹**。 默认情况下，它是&#x200B;**name_of_the_company/CQ5_adhoc**。

   ![chlimage_1-305](assets/chlimage_1-305.png)

### 配置通用视频预设 {#configuring-universal-presets}

要为视频组件配置通用视频预设，请参阅[视频](/help/assets/s7-video.md)。

## 启用基于MIME类型的Assets/Dynamic Media Classic上载作业参数支持 {#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

您可以启用通过同步Digital Asset Manager/Dynamic Media Classic资源触发的可配置Dynamic Media Classic上传作业参数。

具体来说，您可以在Experience Manager Web控制台配置面板的OSGi (Open Service Gateway Initiative)区域中，按MIME类型配置接受的文件格式。 然后，您可以自定义JCR (Java™内容存储库)中每个MIME类型使用的各个上载作业参数。

**要启用基于MIME类型的资源：**

1. 选择Experience Manager图标并导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。
1. 在“Adobe Experience Manager Web控制台配置”面板的&#x200B;**[!UICONTROL OSGi]**&#x200B;菜单中，选择&#x200B;**[!UICONTROL 配置]**。
1. 在“名称”列下，查找并选择&#x200B;**[!UICONTROL Adobe CQ Dynamic Media Classic Asset MIME类型服务]**&#x200B;以编辑配置。
1. 在MIME类型映射区域，选择任意加号(+)以添加MIME类型。

   查看[支持的MIME类型](/help/assets/assets-formats.md#supported-mime-types)。

1. 在文本字段中，键入新的MIME类型名称。

   例如，您应在`EPS=application/postscript`或`PSD=image/vnd.adobe.photoshop`中键入`<file_extension>=<mime_type>`。

1. 在配置窗口的右下角，选择&#x200B;**[!UICONTROL 保存]**。
1. 返回到Experience Manager，然后在左边栏中选择&#x200B;**[!UICONTROL CRXDE Lite]**。
1. 在CRXDE Lite页面的左边栏中，导航到`/etc/cloudservices/scene7/<environment>` （将`<environment>`替换为实际名称）。
1. 展开`<environment>` （将`<environment>`替换为实际名称）以显示`mimeTypes`节点。
1. 选择您刚刚添加的mimeType。

   例如，`mimeTypes > application_postscript`或`mimeTypes > image_vnd.adobe.photoshop`。

1. 在CRXDE Lite页面的右侧，选择&#x200B;**[!UICONTROL 属性]**&#x200B;选项卡。
1. 在&#x200B;**[!UICONTROL jobParam]**&#x200B;值字段中指定Dynamic Media Classic上载作业参数。

   例如，`psprocess="rasterize"&psresolution=120` 。

   有关您可以使用的更多上载作业参数，请参阅[Adobe Dynamic Media Classic Image Production System API](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-overview.html)。

   >[!NOTE]
   >
   >如果要上传PSD文件，并且希望将它们作为模板进行图层提取，请在&#x200B;**[!UICONTROL jobParam]**&#x200B;值字段中输入以下内容：
   >
   >`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`
   >
   >确保PSD文件具有“图层”。 如果它严格是一个图像或带有蒙版的图像，则它作为图像处理，因为没有要处理的图层。

1. 在CRXDE Lite页面的左上角，选择&#x200B;**[!UICONTROL 全部保存]**。

## Dynamic Media Classic与Experience Manager集成疑难解答 {#troubleshooting-scene-and-aem-integration}

如果您在将Experience Manager与Dynamic Media Classic集成时遇到问题，请参阅以下解决方案方案。

**如果将数字资产发布到Dynamic Media Classic失败：**

* 检查要上传的资源是否位于&#x200B;**[!UICONTROL CQ target]**&#x200B;文件夹中(您在Dynamic Media Classic云配置中指定此文件夹)。
* 如果不是，则必须在&#x200B;**[!UICONTROL 页面属性]**&#x200B;中为该页面配置云配置，以允许上载到&#x200B;**[!UICONTROL CQ临时]**&#x200B;文件夹。

* 检查日志以了解任何信息。

**如果您的视频预设未显示：**

* 请确保已通过&#x200B;**[!UICONTROL 页面属性]**&#x200B;配置该页面的云配置。 视频预设在Dynamic Media Classic视频组件中可用。

**如果您的视频资源不在Experience Manager中播放：**

* 确保您使用了正确的视频组件。 Dynamic Media Classic视频组件与基础视频组件不同。 查看[Foundation视频组件与Dynamic Media Classic视频组件](/help/assets/s7-video.md)。

**如果Experience Manager中的新资源或修改的资源未自动上传到Dynamic Media Classic：**

* 确保资产位于CQ目标文件夹中。 只有位于CQ目标文件夹中的资源才会自动更新(前提是您已将Experience Manager Assets配置为自动上传资源)。
* 确保您已将Cloud Services配置配置为启用自动上传，并且已更新和保存DAM资产工作流以包含Dynamic Media Classic上传。
* 将图像上传到Dynamic Media Classic目标文件夹的子文件夹时，请确保执行以下操作之一：

   * 确保所有资源的名称（无论位于何处）都是唯一的。 否则，主目标文件夹中的资产将被删除，并且仅保留子文件夹中的资产。
   * 在Dynamic Media Classic帐户的“设置”区域中更改Dynamic Media Classic覆盖资产的方式。 如果在子文件夹中使用同名的资源，请勿将Dynamic Media Classic设置为覆盖任何位置的资源。

**如果您删除的资源或文件夹未在Dynamic Media Classic和Experience Manager之间同步：**

* 在Experience Manager Assets中删除的Assets和文件夹仍显示在Dynamic Media Classic的同步文件夹中。 手动删除它们。

**如果视频上传失败：**

* 如果视频上传失败，并且您正在使用Experience Manager通过Dynamic Media Classic集成对视频进行编码，请参阅[将可配置的超时添加到Dynamic Media Classic上传工作流](#adding-configurable-timeout-to-scene-upload-workflow)。

>[!CAUTION]
>
>从现有Dynamic Media Classic公司帐户导入资源可能需要很长时间才能在Experience Manager中显示。 确保在Dynamic Media Classic中指定了没有太多资源的文件夹。 例如，根文件夹通常包含太多资产。
>
>如果要测试集成，请将根文件夹仅指向子文件夹，而不是整个公司。
