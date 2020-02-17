---
title: 与Dynamic Media Classic集成(Scene7)
seo-title: 与Dynamic Media Classic集成(Scene7)
description: 了解如何将AEM与Dynamic Media Classic集成。
seo-description: 了解如何将AEM与Dynamic Media Classic集成。
uuid: b014d643-1cc1-47f3-a79c-7f6f9e45637a
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: f55e68c3-3309-4400-bef9-fd3afa6e2b5f
translation-type: tm+mt
source-git-commit: e9c64d214456eed8e0adb29edd60c2350b852a67

---


# 与Dynamic Media Classic集成(Scene7){#integrating-with-dynamic-media-classic-scene}

[Adobe Dynamic Media Classic](https://help.adobe.com/en_US/scene7/using/WS26AB0D9A-F51C-464e-88C8-580A5A82F810.html) 是一款托管解决方案，用于管理、增强、发布富媒体资产并将富媒体资产交付到Web、移动设备、电子邮件以及连接Internet的显示屏和印刷品。

要使用Dynamic Media Classic，您需要配置云配置，以便Dynamic Media Classic和AEM资产能够相互交互。 本文档介绍如何配置AEM和Dynamic Media Classic。

有关在页面上使用所有Dynamic Media Classic组件和处理视频的信息，请参 [阅使用Dynamic Media Classic](../assets/scene7.md)。

>[!NOTE]
>
>* Dynamic Media Classic的DHTML查看器平台于2014年1月31日正式终止。 有关详细信息，请参 [阅DHTML查看器生命周期结束常见问题解答](../sites-administering/dhtml-viewer-endoflifefaqs.md)。
>* 在配置Dynamic Media Classic以与AEM结合使用之前，请参 [阅将Dynamic Media Classic与AEM集成的最佳实践](#best-practices-for-integrating-scene-with-aem) 。
>* 如果您使用的是带有自定义代理配置的Dynamic Media Classic，则需要配置两个HTTP客户端代理配置，因为AEM的某些功能使用3.x API，而其他功能使用4.x API。 3.x配置了http://localhost:4502/system/console/configMgr/com.day.commons.httpclient [](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) ,4.x配置了 [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)。
>



## AEM/Dynamic Media Classic集成与Dynamic Media {#aem-scene-integration-versus-dynamic-media}

AEM用户可以选择使用两种解决方案来处理Dynamic Media:将其AEM实例与Dynamic Media Classic集成，或使用已集成到AEM的Dynamic media解决方案。

使用以下标准确定要选择的解决方案：

* 如果您是现有 **Dynamic** Media Classic客户，其富媒体资产位于Dynamic Media Classic中，用于发布和交付，但您希望将这些资产与站点(WCM)创作和／或AEM资产集成以进行管理，则请使用本文档中描述的 [AEM/Dynamic Media Classic点对点集成](#aem-scene-point-to-point-integration) 。

* 如果您是具有 **富媒体交付需求的** AEM新客户，请选择 [Dynamic Media选项](#aem-dynamic-media)。 如果您没有现有的S7帐户，并且该系统中存储了许多资源，则此选项最有意义。

* 在某些情况下，您可能希望同时使用这两种解决方案。 双 [用方案描述了这种方案](/help/sites-administering/scene7.md#dual-use-scenario) 。

### AEM/Dynamic Media Classic点对点集成 {#aem-scene-point-to-point-integration}

在此解决方案中处理资产时，您需要执行下列操作之一：

* 将资产直接上传到Dynamic Media Classic，然后通过Dynamic Media Classic内容浏览器访 **问** ，以进行页面创作或
* 上传到AEM资产，然后启用自动发布到Dynamic Media Classic;您可以通过Assets **内容浏览器** （用于页面创作）访问

您用于此集成的组件位于设计模式 **的Dynamic Media Classic** 组件 [区域。](/help/sites-authoring/author-environment-tools.md#page-modes)

### AEM Dynamic Media {#aem-dynamic-media}

AEM Dynamic media是直接在AEM平台内统一Dynamic Media Classic功能。

在此解决方案中处理资产时，您需要遵循以下工作流：

1. 将单个图像和视频资产直接上传到AEM。
1. 在AEM中直接对视频进行编码。
1. 直接在AEM中构建基于图像的集。
1. 如果适用，可向图像或视频添加交互性。

您用于Dynamic Media的组件位于“设计”模 **[!UICONTROL 式的Dynamic Media]** 组件 [区域中](/help/sites-authoring/author-environment-tools.md#page-modes)。 其中包括：

* **[!UICONTROL Dynamic Media]** - **[!UICONTROL Dynamic Media组件是智能的]** ，具体取决于您添加的是图像还是视频，您有各种选项。 该组件支持图像预设、基于图像的查看器（例如图像集、旋转集、混合媒体集）和视频。此外，查看器是响应式的 - 其屏幕大小可根据设备屏幕大小自动进行更改。所有查看器都是 HTML5 查看器。

* **[!UICONTROL 交互式媒体]** -交互式媒体组 **** 件适用于在热点或图像映射等资源上具有交互性的资源，如传送横幅、交互式图像和交互式视频。 此组件是智能的——根据您添加的是图像还是视频，您有各种选项。 此外，查看器是响应式的 - 其屏幕大小可根据设备屏幕大小自动进行更改。所有查看器都是 HTML5 查看器。

### 两用场景 {#dual-use-scenario}

开箱即用，您可以同时使用AEM的Dynamic Media和Dynamic Media Classic集成功能。 下表介绍了在打开和关闭某些区域时的使用案例。

要同时使用Dynamic media和Dynamic Media Classic，请执行以下操作：

1. 在云 [服务中配置Dynamic Media](#creating-a-cloud-configuration-for-scene) Classic。
1. 按照您的用例中特有的说明操作：

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
    <td><strong>成像／视频</strong></td>
    <td><strong>动态媒体组件</strong></td>
    <td><strong>S7内容浏览器和组件</strong></td>
    <td><strong>从资产自动上传到S7</strong></td>
    </tr>
    <tr>
    <td>站点和Dynamic Media新功能</td>
    <td>将资产上传到AEM，然后使用AEM Dynamic media组件在站点页面上创作资产</td>
    <td><p>开启</p> <p>（请参阅第3步）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">开启</a></td>
    <td>关闭</td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>零售行业，对站点和动态媒体不熟悉</td>
    <td>将非产品资产上传到AEM以便进行管理和交付。 将产品资产上传到Dynamic Media Classic，然后在AEM和组件中使用Dynamic Media Classic内容浏览器在站点上创作产品详细信息页面。</td>
    <td><p>开启</p> <p>（请参阅第3步）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">开启</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>资产和Dynamic Media的新功能</td>
    <td>将资产上传到AEM资产，然后使用Dynamic media中发布的URL/嵌入代码</td>
    <td><p>开启</p> <p>（请参阅第3步）</p> </td>
    <td>关闭</td>
    <td>关闭</td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>动态媒体和模板的新增功能</td>
    <td>使用Dynamic Media进行成像和视频处理。 在Dynamic Media Classic中创作图像模板，并使用Dynamic Media Classic内容查找器在“站点”页面中包含模板。</td>
    <td><p>开启</p> <p>（请参阅第3步）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">开启</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>现有的Dynamic Media Classic客户，不熟悉站点</td>
    <td>将资产上传到Dynamic Media Classic，然后使用AEM Dynamic Media Classic内容浏览器在站点页面上搜索和创作资产</td>
    <td>关闭</td>
    <td>关闭</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>现有Dynamic Media Classic客户，不熟悉站点和资产</td>
    <td>将资产上传到DAM并自动发布到Dynamic Media Classic以便交付。 使用AEM Dynamic Media Classic内容浏览器在站点页面上搜索和创作资产。</td>
    <td>关闭</td>
    <td>关闭</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">开启</a></p> <p>（请参阅第4步）</p> </td>
    </tr>
    <tr>
    <td>现有Dynamic Media Classic客户和新资产</td>
    <td><p>将资产上传到AEM，然后使用Dynamic media生成要下载／共享的演绎版。 自动将AEM资产发布到Dynamic Media Classic以进行交付。</p> <p><strong></strong> 重要说明：在AEM中生成的重复处理和再现将不会同步到Dynamic Media Classic</p> </td>
    <td><p>开启</p> <p>（请参阅第3步）</p> </td>
    <td>关闭</td>
    <td>关闭</td>
    <td><p><a href="#configuringautouploadingfromaemassets">开启</a></p> <p>（请参阅第4步）</p> </td>
    </tr>
    </tbody>
    </table>

1. (可选；请参阅用例表)-设置 [Dynamic Media云配置](/help/assets/config-dynamic.md) , [并启用Dynamic Media服务器](/help/assets/config-dynamic.md)。
1. (可选；请参阅用例表)-如果您选择启用从资产自动上传到Dynamic Media Classic，则需要添加以下内容：

   1. 设置自动上传到Dynamic Media Classic。
   1. 在Dam更新 **资产工作流结束时** ，在所有Dynamic media工作流步骤之后添加Dynamic Media Classic ****** 上传步骤( `https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`
   1. （可选）按 [https://&lt;server>:&lt;port>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl中的MIME类型限制Dynamic Media Classic资产上传](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl)。 此列表中未包含的资产MIME类型将不会上传到Dynamic Media Classic服务器。
   1. （可选）在Dynamic Media Classic配置中设置视频。 您可以同时为Dynamic media和Dynamic Media Classic启用视频编码。 动态演绎版用于在AEM实例中本地预览和回放，而Dynamic Media Classic视频演绎版则生成并存储在Dynamic Media Classic服务器上。 在为Dynamic media和Dynamic Media Classic设置视频编码服务时，将视频处理配置文 [件应用到](/help/assets/video-profiles.md) Dynamic Media Classic资产文件夹。
   1. （可选）在 [Dynamic Media Classic中配置安全预览](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)。

#### 限制 {#limitations}

启用Dynamic Media Classic和Dynamic Media后，有以下限制：

* 无法通过选择资产并将其拖动到AEM页面上的Dynamic Media Classic组件，手动上传到Dynamic Media Classic。
* 即使在资产中编辑资产时，AEM-Dynamic Media Classic已同步的资产会自动更新为Dynamic Media Classic，回滚操作也不会触发新的上传，因此，Dynamic Media Classic在回滚后不会立即获得最新版本。 解决方法是在回滚完成后再次编辑。
* 如果您需要将Dynamic media用于一个用例，将Dynamic Media Classic集成用于另一个用例，以便Dynamic Media资产不与Dynamic Media Classic系统交互，那么请勿将Dynamic Media Classic配置应用到Dynamic media文件夹，或将Dynamic Media配置（处理配置文件）应用到DynamicMedia Classic文件夹。

## 将Dynamic Media Classic与AEM集成的最佳实践 {#best-practices-for-integrating-scene-with-aem}

将Dynamic Media Classic与AEM集成时，需要在以下方面遵循一些重要的最佳实践：

* 测试推动集成
* 对于某些情况，建议直接从Dynamic Media Classic上传资产

请参 [阅已知限制](#known-limitations-and-design-implications)。

### 测试推动集成 {#test-driving-your-integration}

Adobe建议您通过让根文件夹仅指向子文件夹而非整个公司来测试集成。

>[!CAUTION]
>
>从现有Dynamic Media Classic公司帐户导入资产可能需要很长时间才能在AEM中显示。 请确保在Dynamic Media Classic中指定的文件夹没有太多的资产（例如，根文件夹通常拥有的资产过多，并且可能会导致系统崩溃）。

### 从AEM资产上传资产与从Dynamic Media Classic上传资产 {#uploading-assets-from-aem-assets-versus-from-scene}

您可以通过使用资产（数字资产管理）功能，或通过Dynamic Media Classic内容浏览器直接在AEM中访问Dynamic Media Classic来上传资产。 您选择哪个选项取决于以下因素：

* AEM资产尚不支持的Dynamic Media Classic资产类型必须通过Dynamic Media Classic内容浏览器（例如，图像模板）直接从Dynamic Media Classic添加到AEM网站。
* 对于AEM资产和Dynamic Media Classic都支持的资产类型，确定如何上传资产类型取决于以下各项：

   * 当前资产所在的位置，以及
   * 在公用存储库中管理它们的重要性

如果资产已在Dynamic Media Classic中，并且在公用存储库中管理资产并不重要，则仅将资产导出到AEM资产以将其同步回Dynamic Media Classic进行交付将是不必要的往返操作。 否则，最好将资产保留在单个存储库中并仅同步到Dynamic Media Classic以便交付。

## 配置Dynamic Media Classic集成 {#configuring-scene-integration}

您可以配置AEM以将资产上传到Dynamic Media Classic。 可以从CQ目标文件夹中的资产从AEM上传（自动或手动）到Dynamic Media Classic公司帐户。

>[!NOTE]
>
>Adobe建议您仅使用指定的目标文件夹来导入Dynamic Media Classic资产。 位于目标文件夹之外的数字资产只能用于启用了Dynamic Media Classic配置的页面上的Dynamic Media Classic组件。 此外，它们还位于Dynamic Media Classic中的临时文件夹中。 临时文件夹未与AEM同步（但资产可在Dynamic Media Classic内容浏览器中显示）。

要配置Dynamic Media Classic以与AEM集成，您需要完成以下步骤：

1. [定义云配置](#creating-a-cloud-configuration-for-scene) -定义Dynamic Media Classic文件夹与Assets文件夹之间的映射。 即使您只希望单向（AEM资产到Dynamic Media Classic）同步，您也需要完成此步骤。
1. [启用 **Adobe CQ s7dam Dam监听器&#x200B;**](#enabling-the-adobe-cq-scene-dam-listener)-在[!UICONTROL OSGi控制台中完成]。
1. 如果您希望AEM资产自动上传到Dynamic Media Classic，您需要打开此选项，然后将Dynamic Media Classic添加到DAM更新资产工作流。 您还可以手动上传资产。
1. 将Dynamic Media Classic组件添加到Sidekick。 这允许用户在其AEM页面上使用Dynamic Media Classic组件。
1. [将配置映射到AEM](#enabling-scene-for-wcm) —— 此步骤是查看在Dynamic Media Classic中创建的任何视频预设所必需的。 如果您需要将资产从CQ目标文件夹外部发布到Dynamic Media Classic，则需要执行此操作。

本节介绍如何执行所有这些步骤，并列出重要限制。

### Dynamic Media Classic与AEM资产之间的同步工作方式 {#how-synchronization-between-scene-and-aem-assets-works}

在设置AEM资产和Dynamic Media Classic同步时，请务必了解以下内容：

#### 从AEM资产上传到Dynamic Media Classic {#uploading-to-scene-from-aem-assets}

* AEM中有一个指定的同步文件夹，用于Dynamic Media Classic上传。
* 如果数字资产放在指定的同步文件夹中，则上传到Dynamic Media Classic的内容可以自动完成。
* AEM中的文件夹和子文件夹结构将复制到Dynamic Media Classic中。

>[!NOTE]
>
>AEM会先将所有元数据嵌入XMP，然后再将其上传到Dynamic Media Classic，因此，在Dynamic Media Classic中，元数据节点上的所有属性都可以作为XMP使用。

#### 已知限制和设计含义 {#known-limitations-and-design-implications}

在AEM资产和Dynamic Media Classic之间进行同步后，当前存在以下限制／设计含义：

<table>
 <tbody>
  <tr>
   <td><strong>限制／设计含义</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>一个指定的同步（目标）文件夹</td>
   <td>在AEM中，对于Dynamic Media Classic上传，每个公司只能有一个指定的文件夹。 如果需要在Dynamic Media Classic中访问多个公司帐户，可以创建多个配置。</td>
  </tr>
  <tr>
   <td>文件夹结构</td>
   <td>如果删除的是与资产同步的文件夹，则所有Dynamic Media Classic远程资产都将被删除，但该文件夹仍会保留。</td>
  </tr>
  <tr>
   <td>临时文件夹</td>
   <td>在WCM中手动上传到Dynamic Media Classic的目标文件夹之外的资产将自动放置在Dynamic Media Classic上的单独的临时文件夹中。 您可以在AEM的云配置中配置此项。</td>
  </tr>
  <tr>
   <td>混合媒体</td>
   <td>混合媒体集显示在AEM中，但AEM中不支持它们。</td>
  </tr>
  <tr>
   <td>PDF</td>
   <td>从Dynamic Media Classic中的eCatalog生成的PDF将导入到CQ目标文件夹中。</td>
  </tr>
  <tr>
   <td>UI刷新</td>
   <td>在AEM和Dynamic Media Classic之间同步时，请务必刷新用户界面以查看更改。 </td>
  </tr>
  <tr>
   <td>视频缩略图</td>
   <td>如果将视频上传到AEM资产以通过Dynamic Media Classic进行编码，则视频缩略图和编码视频在AEM资产中可能需要一些时间才能可用，具体取决于视频处理时间。</td>
  </tr>
  <tr>
   <td>目标子文件夹</td>
   <td><p>如果您在目标文件夹中使用子文件夹，请确保对每个资产使用唯一的名称（无论位置如何），或者配置Dynamic Media Classic（在设置区域），以不覆盖任何位置的资产。</p> <p>否则，上传到Dynamic Media Classic目标子文件夹的同名资产会被上传，但目标文件夹中同名的资产会被删除。 </p> </td>
  </tr>
 </tbody>
</table>

### 配置Dynamic Media Classic服务器 {#configuring-scene-servers}

如果您在代理后运行AEM或具有特殊的防火墙设置，则可能需要显式启用不同区域的主机。 服务器在内容中进行管 `/etc/cloudservices/scene7/endpoints` 理，并可以根据需要自定义。 点按一个URL，然后根据需要编辑以更改该URL。 在AEM的早期版本中，这些值是硬编码的。

如果导航到， `/etc/cloudservices/scene7/endpoints.html`您会看到列出的服务器（并可以通过单击URL编辑它们）:

![chlimage_1-296](assets/chlimage_1-296.png)

### 为Dynamic Media Classic创建云配置 {#creating-a-cloud-configuration-for-scene}

云配置定义Dynamic Media Classic文件夹与AEM Assets文件夹之间的映射。 它需要配置以将AEM资产与Dynamic Media Classic同步。 有关详细信息，请参阅同步的工作方式。

>[!CAUTION]
>
>从现有Dynamic Media Classic公司帐户导入资产可能需要很长时间才能在AEM中显示。 确保在Dynamic Media Classic中指定的文件夹没有太多的资产（例如，根文件夹通常拥有太多的资产）。
>
>如果要测试集成，您可能希望根文件夹仅指向子文件夹，而不是指向整个公司。

>[!NOTE]
>
>您可以有多个配置：一个云配置表示Dynamic Media Classic公司的一个用户。 如果要访问其他Dynamic Media Classic公司或用户，您需要创建多个配置。

要将AEM配置为能够将资产发布到Dynamic Media Classic，请执行以下操作：

1. 点按AEM图标，然后导航到 **[!UICONTROL 部署>云服务]** ，以访问Adobe Dynamic Media Classic。

1. 点按 **[!UICONTROL 立即配置]**。

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. 在“标 **[!UICONTROL 题]** ”字段中，或者在“名称”字 **[!UICONTROL 段中]** ，输入相应的信息。 点按&#x200B;**[!UICONTROL 创建]**。

   >[!NOTE]
   >
   >创建其他配置时，将显 **[!UICONTROL 示父配置]** 字段。
   >
   >请 **勿更** 改父配置。 更改父配置可能会中断集成。

1. 输入Dynamic Media Classic帐户的电子邮件地址、密码和区域，然后点 **[!UICONTROL 按连接到Dynamic Media Classic]**。 您已连接到Dynamic Media Classic服务器，该对话框会展开，并显示更多选项。

1. 输入公 **[!UICONTROL 司名称和]** 根路径 **** (这是已发布的服务器名称以及要指定的任何路径；如果您不知道已发布的服务器名称，请在Dynamic Media Classic中，转到“设置”>“应 **[!UICONTROL 用程序设置]**”。)

   >[!NOTE]
   >
   >Dynamic Media Classic根路径是AEM连接到的Dynamic Media Classic文件夹。 可缩小到特定文件夹。

   >[!CAUTION]
   >
   >根据Dynamic Media Classic文件夹的大小，导入根文件夹可能需要很长时间。 此外，Dynamic Media Classic数据可能超过AEM存储。 确保导入的文件夹正确无误。 导入过多数据可能会停止系统。

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. 单击&#x200B;**[!UICONTROL 确定]**。AEM会保存您的配置。

>[!NOTE]
>
>如果要重新连接：
>
>* 在发布时重新连接到Dynamic Media Classic时，您可能需要在发布时重置密码，否则重新连接将无法工作。 这不是创作实例上的问题。
>* 如果您修改了区域、公司名称等值，则必须重新连接到Dynamic Media Classic。 如果配置选项已修改但未保存，AEM仍会错误地指示配置有效。 务必重新连接。
>



### 启用Adobe CQ Dynamic Media Classic Dam监听器 {#enabling-the-adobe-cq-scene-dam-listener}

必须启用Adobe CQ Dynamic Media Classic Dam监听器，该监听器在默认情况下处于禁用状态。

要启用它，请执行以下操作：

1. 点按工 [!UICONTROL 具图标] ，然后导航到操 **[!UICONTROL 作> web控制台]**。 Web控制台将打开。
1. 导航到 **[!UICONTROL Adobe CQ Dynamic Media Classic Dam监听器]** ，然后选中“已 **[!UICONTROL 启用]** ”复选框。

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. 点按&#x200B;**[!UICONTROL 保存]**。

### 向Dynamic Media Classic上传工作流添加可配置超时 {#adding-configurable-timeout-to-scene-upload-workflow}

将AEM实例配置为通过Dynamic Media Classic(Scene7)处理视频编码时，默认情况下，任何上传作业都有35分钟超时。 要适应运行时间可能较长的视频编码作业，可以配置以下设置：

1. 导航到 **http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**。

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. 在“活动作业超时”字段中根 **[!UICONTROL 据需要更改数字]** 。 以秒为单位接受任何非负数。 默认情况下，此值设置为2100。

   >[!NOTE]
   >
   >最佳实践：大多数资源最多只需几分钟即可摄取（例如，图像）。 但在某些情况下（例如，更大的视频），超时值应该增加到7200秒（2小时）以适应较长的处理时间。 否则，此Dynamic Media Classic上传作业在JCR元数据中 **[!UICONTROL 标记为]** UploadFailed。

1. 点按&#x200B;**[!UICONTROL 保存]**。

### 从AEM资产进行自动部署 {#autouploading-from-aem-assets}

从AEM 6.3.2开始，AEM资产现已为您配置，这样，如果资产位于CQ目标文件夹中，您上传到数字资产管理器的任何数字资产都将自动更新至Dynamic Media Classic。

将资产添加到AEM资产后，该资产会自动上传并发布到Dynamic Media Classic。

>[!NOTE]
>
>从AEM资产自动上传到Dynamic Media Classic的最大文件大小为500 MB。

要从AEM资产配置自动部署，请执行以下操作：

1. 点按AEM图标并导航到 **[!UICONTROL 部署>云服务]** ，然后在Dynamic media标题下的可用配置下，点按 **[!UICONTROL dms7(Dynamic Media]**)
1. 点按高级 **[!UICONTROL 选项卡]** ，选中启用 **[!UICONTROL 自动上传复选框]** ，然后点按 **[!UICONTROL 确定]**。 您现在需要配置DAM资产工作流，以包括上传到Dynamic Media Classic。

   >[!NOTE]
   >
   >有关 [](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene) 将资产推送到未发布状态Dynamic Media Classic的信息，请参阅配置推送到Dynamic Media Classic的资产的状态（已发布／未发布）。

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. 导航回AEM欢迎页面，然后点按工 **[!UICONTROL 作流]**。 双击 **DAM更新资产工作流** ，以将其打开。
1. 在Sidekick中，导航到工作流 **[!UICONTROL 组件]** ，然后选择 **[!UICONTROL Dynamic Media Classic]**。 将 **[!UICONTROL Dynamic Media Classic拖动到工作流]** ，然后点按 **[!UICONTROL 保存]**。 添加到目标文件夹中AEM资产的资产将自动上传到Dynamic Media Classic。

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* 在自动添加资产时，如果资产未放在CQ目标文件夹中，则不会将其上传到Dynamic Media Classic。
   >* AEM会先将所有元数据嵌入XMP，然后再将其上传到Dynamic Media Classic，因此，在Dynamic Media Classic中，元数据节点上的所有属性都可以作为XMP使用。


### 配置推送到Dynamic Media Classic的资产的状态（已发布／未发布） {#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}

如果要将资产从AEM资产推送到Dynamic Media Classic，您可以自动发布资产（默认行为），或将资产推送到处于未发布状态的Dynamic Media Classic。

如果要在上线前在分阶段环境中测试资产，则可能不希望立即在Dynamic Media Classic上发布资产。 您可以将AEM与Dynamic Media Classic的安全测试环境结合使用，将资产直接从资产推送到处于未发布状态的Dynamic Media Classic中。

Dynamic Media Classic资源通过安全预览保持可用。 仅当在AEM中发布资产时，Dynamic Media Classic资产才会在生产中实时发布。

如果要在将资产推送到Dynamic Media Classic时立即发布资产，则无需配置任何选项。 这是默认行为。

但是，如果您不希望将资产推送到Dynamic Media Classic以自动发布，本节将介绍如何配置AEM和Dynamic Media Classic以实现此操作。

#### 将资产推送到未发布的Dynamic Media Classic的先决条件 {#prerequisites-to-push-assets-to-scene-unpublished}

在不发布资产的情况下将资产推送到Dynamic Media Classic之前，必须设置以下内容：

1. 联系Dynamic Media Classic客户关怀(s7support@adobe.com)，为您的Dynamic Media Classic帐户启用安全预览。
1. 按照说明为 [您的Dynamic Media Classic帐户设置安全预览。](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html)

这些步骤与在Dynamic Media Classic中创建任何安全测试设置的步骤相同。

>[!NOTE]
>
>如果您的安装环境是Unix 64位操作系统，请参阅 [https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html) ，了解需要设置的其他配置选项。

#### 将资产推入未发布状态的已知限制 {#known-limitations-for-pushing-assets-in-unpublished-state}

如果您使用此功能，请注意以下限制：

* 不支持版本控制。
* 如果资产已在AEM中发布，且随后版本已创建，则新版本将立即实时发布到生产。 激活后发布仅与资产的初始发布配合使用。

>[!NOTE]
>
>如果要立即发布资产，最佳做法是将“启用安全预 **[!UICONTROL 览]** ”设置为“立即 **[!UICONTROL 启用”]** ，然后使用“启 **[!UICONTROL 用自动上传]** ”功能。

### 将推送到Dynamic Media Classic的资产状态设置为未发布 {#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>如果用户在AEM中发布资产，则会自动将S7资产触发到生产／实时资产（资产将不再处于安全预览／取消发布状态）。

要将推送到Dynamic Media Classic的资产状态设置为未发布，请执行以下操作：

1. 点按AEM图标，然后导航到 **[!UICONTROL 部署>云服务]**，点按 **[!UICONTROL Dynamic Media Classic]**，然后在Dynamic Media Classic中选择配置。
1. 点按&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。在“启 **[!UICONTROL 用安全视图]** ”下拉菜单中，选择“在AEM **[!UICONTROL 发布激活时]** ”，将资产推送到Dynamic Media Classic而不发布。 (默认情况下，此值设置为“立即” ****，此时Dynamic Media Classic资产会立即发布。)

   有关在 [公开资产之前测试资产的更多信息](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html) ，请参阅Dynamic Media Classic文档。

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. 点按 **[!UICONTROL 确定]**。

启用安全视图意味着您的资产将被推送到未发布的安全预览服务器。

您可以通过导航到AEM中页面上的Dynamic Media Classic组件并点按编辑来选中此 **[!UICONTROL 选项]**。 资产的URL中将列出安全预览服务器。 在AEM中发布后，文件引用中的服务器域将从预览URL更新到生产URL。

### 为WCM启用Dynamic Media Classic {#enabling-scene-for-wcm}

需要为WCM启用Dynamic Media Classic，原因有二：

* 启用用于页面创作的通用视频配置文件的下拉列表。 如果没有此选项， **[!UICONTROL “通用视频预设]** ”下拉框将为空，并且无法设置。
* 如果数字资产不在目标文件夹中，则您可以在页面属性中为该页面启用Dynamic Media Classic，然后将资产拖放到Dynamic Media Classic组件上，即可将资产上传到Dynamic Media Classic。 正常继承规则适用（这意味着子页面将从父页面继承配置）。

在为WCM启用Dynamic Media Classic时，请注意，与其他配置一样，继承规则也适用。 您可以在触屏优化或经典用户界面中为WCM启用Dynamic Media Classic。

#### 在触屏优化用户界面中为WCM启用Dynamic Media Classic {#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}

要在触屏优化UI中为WCM启用Dynamic Media Classic，请执行以下操作：

1. 点按AEM图标，然后导航到 **[!UICONTROL 站点]** ，然后导航到网站的根页面（不是特定于语言的页面）。

1. 在工具栏中，选择设 [!UICONTROL 置图标] ，然后点 **[!UICONTROL 按打开属性]**。

1. 点按 **[!UICONTROL 云服务]** ，点按 **[!UICONTROL 添加配置]** ，然后选择 **[!UICONTROL Dynamic Media Classic]**。
1. 在 **[!UICONTROL Adobe Dynamic Media Classic下拉列表中]** ，选择所需的配置并点按 **[!UICONTROL 确定]**。

   ![chlimage_1-303](assets/chlimage_1-303.png)

   根据Dynamic Media Classic的配置提供的视频预设可在AEM中与该页面和子页面上的Dynamic Media Classic视频组件一起使用。

#### 在经典用户界面中为WCM启用Dynamic Media Classic {#enabling-scene-for-wcm-in-the-classic-user-interface}

要在经典UI中为WCM启用Dynamic Media Classic，请执行以下操作：

1. 在AEM中，点 **[!UICONTROL 按网站]** ，然后导航到网站的根页面（不是特定于语言的页面）。

1. In the sidekick, tap the **[!UICONTROL Page]** icon and tap **[!UICONTROL Page Properties]**.

1. 点按 **[!UICONTROL 云服务>添加服务> Dynamic Media Classic]**。
1. 在 **[!UICONTROL Adobe Dynamic Media Classic下拉列表中]** ，选择所需的配置并点按 **[!UICONTROL 确定]**。

   根据Dynamic Media Classic的配置提供的视频预设可在AEM中与该页面和子页面上的Dynamic Media Classic视频组件一起使用。

### 配置默认配置 {#configuring-a-default-configuration}

如果您有多个Dynamic Media Classic配置，则可将其中一个配置指定为Dynamic Media Classic内容浏览器的默认配置。

在给定时刻，只能将一个Dynamic Media Classic配置标记为默认配置。 默认配置是默认在Dynamic Media Classic内容浏览器中显示的公司资产。

配置默认配置：

1. 点按AEM图标，然后导航到 **[!UICONTROL 部署>云服务]**，点按 **[!UICONTROL Dynamic Media Classic]**，然后在Dynamic Media Classic中选择配置。
1. 点按 **[!UICONTROL 编辑]** ，以打开配置。

1. 在“常 **[!UICONTROL 规]** ”选项卡中，选中“默认配置 **** ”复选框，使其成为Dynamic Media Classic内容浏览器中显示的默认公司和根路径。

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >如果只有一个配置，则选中“默认配 **[!UICONTROL 置]** ”复选框不起作用。

### 配置临时文件夹 {#configuring-the-ad-hoc-folder}

当资产未位于CQ目标文件夹中时，您可以配置资产上传到Dynamic Media Classic中的文件夹。 请参阅从CQ目标文件夹外部发布资产。

配置临时文件夹：

1. 点按AEM图标，然后导航到 **[!UICONTROL 部署>云服务]**，点按 **[!UICONTROL Dynamic Media Classic]**，然后在Dynamic Media Classic中选择配置。
1. 点按 **[!UICONTROL 编辑]** ，以打开配置。

1. 点按&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。在临时 **[!UICONTROL 文件夹字段中]** ，您可以修改临 **时文件夹** 。 默认情况下，它 **是name_of_the_company/CQ5_adhoc**。

   ![chlimage_1-305](assets/chlimage_1-305.png)

### 配置通用预设 {#configuring-universal-presets}

要为视频组件配置通用预设，请参阅 [视频](/help/assets/s7-video.md)。

## 启用基于MIME类型的资产/Dynamic Media Classic上传作业参数支持 {#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

您可以启用通过同步Digital Asset Manager/Dynamic Media Classic资产触发的可配置Dynamic Media Classic上传作业参数。

具体而言，您可以在AEM Web Console“配置”面板的OSGi（Open Service gateway活动）区域按MIME类型配置接受的文件格式。 然后，您可以自定义单个上传作业参数，这些参数用于JCR（Java内容存储库）中的每个MIME类型。

**要启用基于MIME类型的资产，请执行以下操作：**

1. 点按AEM图标，然后导航到工 **[!UICONTROL 具>操作> Web Console]**。
1. 在Adobe Experience Manager web控制台的“配置”面板的“ **[!UICONTROL OSGi”菜单中]** ，点按 **[!UICONTROL 配置]**。
1. 在“名称”列下，查找并点 **[!UICONTROL 按Adobe CQ Dynamic Media Classic资产MIME类型服务]** ，以编辑配置。
1. 在“Mime类型映射”区域中，点按任何加号(+)以添加MIME类型。

   请参 [阅支持的MIME类型](/help/assets/assets-formats.md#supported-mime-types)。

1. 在文本字段中，键入新的MIME类型名称。

   例如，您应键入 `<file_extension>=<mime_type>` as in `EPS=application/postscript` OR `PSD=image/vnd.adobe.photoshop`。

1. 在配置窗口的右下角，点按保 **[!UICONTROL 存]**。
1. 返回AEM，在左边栏中点按CRXDE Lite。
1. 在CRXDE lite页面的左边栏中，导航到( `/etc/cloudservices/scene7/<environment>` 替 `<environment>` 代实际名称)。
1. 展开 `<environment>` (替 `<environment>` 换实际名称)以显示节 `mimeTypes` 点。
1. 点按刚添加的mimeType。

   例如， `mimeTypes > application_postscript` OR `mimeTypes > image_vnd.adobe.photoshop`。

1. 在CRXDE lite页面的右侧，点按属性选 **[!UICONTROL 项卡]** 。
1. 在jobParam值字段中指定Dynamic Media Classic上传作 **[!UICONTROL 业参数]** 。

   For example, `psprocess="rasterize"&psresolution=120` .

   有关可 [使用的其他上传作业参数，请参阅Adobe Dynamic Media Classic Image Production System API](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/) 。

   >[!NOTE]
   >
   >如果要上传PSD文件，并且要将它们作为带有图层提取的模板进行处理，请在 **[!UICONTROL jobParam值字段中输入]** :
   >
   >`process=MaintainLayers&createTemplate=true`
   >
   >确保PSD文件具有“图层”。如果它只是一幅图像或带有遮罩的图像，则它将作为图像处理，因为没有要处理的图层。

1. 在CRXDE lite页面的左上角，点按全 **[!UICONTROL 部保存]**。

## Dynamic Media Classic和AEM集成疑难解答 {#troubleshooting-scene-and-aem-integration}

如果您在将AEM与Dynamic Media Classic集成时遇到问题，请参阅以下解决方案。

**如果您的数字资产发布到Dynamic Media Classic失败：**

* 检查您尝试上传的资产是否位于 **[!UICONTROL CQ目标文件夹中]** （您可以在Dynamic Media Classic云配置中指定此文件夹）。
* 否则，您需要在该页面的页面属性中配置云配 **[!UICONTROL 置]** ，以允许上传到 **[!UICONTROL CQ临时文件夹]** 。

* 检查日志中的任何信息。

**如果视频预设未显示：**

* 请确保您已通过页面属性配置了该页面 **[!UICONTROL 的云配置]**。 视频预设在Dynamic Media Classic视频组件中可用。

**如果您的视频资产不在AEM中播放：**

* 确保您使用了正确的视频组件。 Dynamic Media Classic视频组件与基础视频组件不同。 请参 [阅基础视频组件与动态媒体经典视频组件](/help/assets/s7-video.md)。

**如果AEM中的新资产或已修改资产没有自动上传到Dynamic Media Classic:**

* 确保资产位于CQ目标文件夹中。 只有CQ目标文件夹中的资产才会自动更新（前提是您已将AEM资产配置为自动上传资产）。
* 确保您已将云服务配置配置为启用自动上传，并且您已更新并保存DAM资产工作流以包括Dynamic Media Classic上传。
* 将图像上传到Dynamic Media Classic目标文件夹的子文件夹时，请确保执行以下操作之一：

   * 确保所有资产的名称（不管位置如何）都是唯一的。 否则，将删除主目标文件夹中的资产，并且只保留子文件夹中的资产。
   * 更改Dynamic Media Classic帐户在“设置”区域覆盖资产的方式。 如果您在子文件夹中使用同名的资产，则不要将Dynamic Media Classic设置为覆盖资产，而不管该资产位于何处。

**如果已删除的资产或文件夹未在Dynamic Media Classic和AEM之间同步：**

* 在AEM资产中删除的资产和文件夹仍会显示在Dynamic Media Classic的同步文件夹中。 您必须手动删除它们。

**如果视频上传失败**

* 如果视频上传失败，并且您正在使用AEM通过Dynamic Media Classic集成对视频进行编码，请参阅向Dynamic Media Classic上传工作流 [添加可配置的超时](#adding-configurable-timeout-to-scene-upload-workflow)。

>[!CAUTION]
>
>从现有Dynamic Media Classic公司帐户导入资产可能需要很长时间才能在AEM中显示。 确保在Dynamic Media Classic中指定的文件夹没有太多的资产（例如，根文件夹通常拥有太多的资产）。
>
>如果要测试集成，您可能希望根文件夹仅指向子文件夹，而不是指向整个公司。

