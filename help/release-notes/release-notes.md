---
title: ' [!DNL Adobe Experience Manager] 6.5的发行说明'
description: 查找 [!DNL Adobe Experience Manager] 6.5的版本信息、新增功能、安装操作说明和详细更改列表。
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 80482da847b86c91963dbb0d37375e370a503588
workflow-type: tm+mt
source-wordcount: '6643'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack发行说明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section. -->

## 发行版信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本号 | 6.5.23.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 类型 | Service Pack版本 |
| 日期 | 2025年5月22日星期四<!-- UPDATE FOR EACH NEW RELEASE --> |
| 下载 URL | [软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## [!DNL Experience Manager] 6.5.23.0中包括的内容 {#what-is-included-in-aem-6523}

[!DNL Experience Manager] 6.5.23.0包括新增功能、客户请求的关键增强功能和错误修复。 其中还包括自2019年4月6.5首次发布以来在性能、稳定性和安全性方面做出的改进。 在[ 6.5上](#install)安装此Service Pack[!DNL Experience Manager]。

<!-- UPDATE FOR EACH NEW RELEASE -->

## 主要功能和增强功能

<!--### Sites {#sites}

* A () -->

<!--
### [!DNL Assets]

* A ()
-->

### Forms {#forms-sp23}

此版本中的主要功能和增强功能包括：

* [静态PDF中具有混合文本样式的辅助超链接](https://helpx.adobe.com/cn/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf)：静态PDF中包含混合文本样式的超链接现在被标记为单个辅助元素。 此增强功能简化了标记树结构，改进了屏幕阅读器导航，并支持更好的辅助功能合规性。

* [已更新支持的平台矩阵](/help/forms/using/aem-forms-jee-supported-platforms.md)

  最新版本引入了受支持平台矩阵的更新，确保与新技术兼容。

   * IBM® Content Manager客户端8.7

   * MongoDB Enterprise 7.0

   * MySQL 8.4

   * Microsoft® SQL Server 2022

   * Microsoft® SQL Server JDBC驱动程序12.8

   * Red Hat® Enterprise Linux® 9（内核4.x，64位） 

* [强化的文件附件组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment)：作为安全措施，该组件现在阻止提交具有修改扩展名的文件，这些文件尝试绕过允许的文件类型检查。 在提交期间将阻止此类文件，以确保仅接受有效的文件类型。

* Forms-20533：AEM Forms现在包含用于forms组件的Struts版本从2.5.33升级到6.x。 这提供了以前未包含在SP23中的Struts更改。 通过[修补程序](/help/release-notes/aem-forms-hotfix.md)添加支持，您可以[下载并安装](/help/release-notes/aem-forms-hotfix.md)以添加对最新版本Struts的支持。

* Forms-20532：AEM Forms现在包含用于输出组件的Struts版本从2.5.33升级到6.x。 这提供了以前未包含在SP23中的Struts更改。 通过[修补程序](/help/release-notes/aem-forms-hotfix.md)添加支持，您可以[下载并安装](/help/release-notes/aem-forms-hotfix.md)以添加对最新版本Struts的支持。

<!--* **Two-Factor authentication with SAML for AdminUI** 

  AdminUI in AEM Forms JEE now supports two-factor authentication using Security Assertion Markup Language (SAML) single sign-on (SSO), providing stronger security and a seamless login experience for administrators, similar to what is available in HTML Workspace. 

#### New GA features in AEM Forms {#ga-aem-forms-sp23}

* A ()

#### New Beta features in AEM Forms {#beta-aem-forms-sp23}
-->

## 修复了Service Pack 23中的问题 {#fixed-issues}

<!-- 6.5.23.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-6523}

#### 辅助功能 {#sites-accessibility-6523}

* AEM编辑器页面中的画布部分现在支持完全的键盘辅助功能。 用户只需使用键盘即可激活节标题和编辑按钮，而无需依赖鼠标悬停。 此更新确保符合WCAG 2.1.1并提高跨组件（例如Teaser、图像、轮播、布局、时间扭曲和注释模式）的可用性。 (SITES-25256) <!-- 6.5 LTS SP1 -->
* 修复了AEM页面编辑器中的辅助功能问题：在激活“角色”、“购物车”或“已放弃”等按钮后，键盘焦点意外地重置为人口统计工具栏的起始位置。 现在，焦点仍然在激活的按钮上，以支持一致的键盘导航和屏幕阅读器工作流。 (SITES-25306)
* 修复了AEM页面编辑器中的关键辅助功能问题，该问题导致无法仅使用键盘操作多个对话框和模式（例如，资产边栏或布局预览）中的画布元素。 现在，所有交互式画布元素都支持仅键盘导航，确保符合WCAG 2.1成功标准2.1.1 (SITE-25256)
* 修复了站点管理员UI中的辅助功能问题，该问题导致创建弹出窗口中的交互式列表项使用不正确的ARIA角色。 行为类似于链接的元素被分配了`role="listitem"`而不是`role="menuitem"`，这违反了ARIA设计模式并混淆了屏幕阅读器。 更新确保所有列表组件遵循正确的语义角色，以改进键盘和辅助技术支持。 (SITES-24493)
* 修复了页面标题和标记字段的辅助功能标签关联问题。 在使用JAWS等屏幕阅读器时，AEM界面现在可以正确地将辅助功能标签与“标题”和“页面标题”字段相关联。 此修复确保正确读取标签，并提高了页面创建、属性和移动工作流中的ADA合规性。 (SITES-27149)
* 修复了“权限”对话框中表标识存在的辅助功能问题。 AEM中的权限表现在使用正确的ARIA角色和属性，以确保屏幕阅读器（如JAWS）将其正确标识为表。 此修复程序提高了辅助功能合规性，并确保用户能够收到准确的导航和内容公告。 (SITES-27140)
* 修复了时间轴中注释输入字段缺少可视标签的问题。 修复了时间线部分下“评论”输入字段缺少可视标签的问题，从而提高辅助功能。 此更新确保屏幕阅读器可以准确地朗读字段标签。 此体验可增强所有用户（尤其是依赖辅助技术的个人）的表单导航和提交。 (SITES-26903)
* 修复了时间轴注释中省略号按钮的键盘辅助功能。 为时间线部分下的注释旁边的省略号（三个点）按钮启用键盘导航。 用户现在可以使用Tab键访问按钮并与之交互，从而提高依赖仅键盘导航的用户的可访问性。 (SITES-26891)
* 改进了在选择对话框中针对搜索结果的NVDA/讲述人公告。 更新了“打开选择”对话框，以宣布在使用屏幕阅读器（如NVDA或“讲述人”）时是否找到搜索结果。 这项改进可帮助依赖辅助技术的用户了解其搜索操作的结果，而无需视觉确认。 (SITES-26883)
* 更正了评论输入字段旁边的省略号图标的ARIA角色。 更新了评论输入字段旁边的省略号（三个点）图标以使用正确的ARIA角色，确保屏幕阅读器可以准确识别元素。 这项改进增强了辅助功能的合规性，改善了依赖辅助技术的用户的体验。 (SITES-26881)
* 更正了Coral UI组件中的无效ARIA属性。 更新了Coral UI组件以确保所有ARIA属性都使用有效值，从而提高辅助功能合规性。 特别是，解决了错误分配`aria-modal="dialog"`等无效值的情况。 此增强功能使屏幕阅读器能够正确解释对话框元素，从而提高依赖辅助技术的用户的辅助功能。 (SITES-26873)
* 改进了重排方案中图标的可见性和工具提示。 增强了重排行为，以确保为&#x200B;**下载**、**重新处理资源**&#x200B;和&#x200B;**签出**&#x200B;图标正确显示工具提示。 重点关注在调整视区大小或更改浏览器缩放设置时，图标及其标签会变得不可见的辅助功能问题。 此修复程序通过维持可见性并在重排期间提供适当的图标描述，为视力缺佳的用户提供支持。 (SITES-26871)

#### 管理员用户界面{#sites-adminui-6523}

修复了通用编辑器URL服务异常，其中缺少外部化器端点。 Universal Editor URL服务现在可处理缺失的作者、发布或本地外部化器端点，而不会引发异常。 即使某些外部化器配置不完整，管理员用户也可以成功打开页面编辑器。 (SITES-28877) <!-- LTS -->

#### 经典 UI{#sites-classicui-6523}

* 经典UI对话框中的问题，其中切换按钮会隐藏文本区域，并且在后续单击时无法再次显示。 此修复可确保在切换时文本区域正确重新显示，恢复预期行为并防止动态对话框工作流中断。 (SITES-30230)
* 修复了Service Pack 22升级后经典UI图像资产查找器功能中断的问题。 经典UI图像资产查找器现在可以正确处理包含空格或特殊字符的资产名称。 此更新可确保资产查找器正确编码文件名，防止搜索失败，并允许作者查找并选择图像资产，而不会出现错误。 (SITES-29151)

#### [!DNL Content Fragments]{#sites-contentfragments-6523}

* 修复了`DeleteVariationIT.testUpdateBasic`的验证测试失败。 `DeleteVariationIT.testUpdateBasic`测试在Service Pack验证运行时不再失败。 该修复更正了JSON处理逻辑中缺少文本映射的问题，从而确保测试稳定性并避免不必要的测试中断。 (SITES-28022)
* AEM现在可以防止图像资源中XMP元数据的格式错误导致性能下降。 包含无效或不合规的Assets XMP属性名称（例如具有数值区段或不合格结构的属性名称）在处理期间不再触发重复的警告日志。 系统会过滤掉有问题的元数据，以确保资产摄取和验证已完成，并且没有错误。 (SITES-30683) <!-- AEM 6.5 LTS SP1 -->


<!-- #### [!DNL Content Fragments] - Admin{#sites-admin-6523}

* A () -->


#### [!DNL Content Fragments] — 片段编辑器{#sites-fragments-editor-6523}

其他作者仍可以发布内容片段，即使其他作者签出了它们，这违反了签出功能的预期行为。 此修复可防止其他用户查看或使用签出内容片段时在创作界面中的发布按钮。 (SITES-30578) <!-- LTS -->

#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6523}

修复了内容片段架构的GraphQL QueryValidationError问题。 刷新`cq-dam-cfm-graphql`包可更正使用内容片段引用时的架构验证错误。 此修复可确保GraphQL查询正常运行，而无需在部署包后手动重新调整或重新发布架构。 (SITES-27001) <!-- LTS -->


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6523}

* A () -->

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6523}

* A () -->


#### 组件控制台{#sites-component-console-6523}

改进了“组件实时使用情况”页面加载功能。 优化AEM中的“组件实时使用情况”页面，以防止在滚动大型数据集时显示空行。 现在，用户加载具有大量使用引用的组件时，可能会遇到连续数据加载的情况，且没有不必要的间隔或空条目。 此体验提高了跨组件使用报告的页面导航、跟踪准确性和管理效率。 (SITES-26454)

#### 核心后端{#sites-core-backend-6523}

* 修复了因资产名称无效而导致内容查找器资产列表失败的问题。 内容查找器现在可以正确处理包含不可编码字符的资源名称。 遇到名称有问题的资产时，页面编辑器中的资产列表不再失败或引发异常。 (SITES-28722)
* `SearchPathLimiter`组件通过每次调用在ERROR级别打印消息而生成过多日志条目的问题。 这种行为开始于Service Pack 17之后，并且由于日志量极高而导致性能问题。 此修复程序将日志级别降级为DEBUG，从而显着降低日志噪音并提高系统监控和诊断效率。 (SITES-29835)
* 处理`ValidationDataServlet`中的图像资源时，XMP元数据的格式不正确触发了错误。 此修复可确保合规的元数据处理，并避免冗余解析无效属性。 (SITE-30683) <!-- LTS -->


<!-- #### Core Components{#sites-core-components-6523}

* A () -->

<!-- #### Campaign integration{#sites-campaign-integration-6523}

* A () -->

<!-- #### Experience Fragments{#sites-experiencefragments-6523}

* A () -->

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6523}

* A () -->


#### 启动项{#sites-launches-6523}

* 修复了12月25日至12月31日之间不正确的启动日期显示问题。 启动项UI现在显示12月25日至12月31日之间的日期，其中包含正确的年份。 此修复可确保日期不再错误地显示下一年，从而避免在营销活动规划和计划期间造成混淆。 (SITES-28706)
* 修复了Service Pack 22升级后损坏的AEM Launch模板。 现在，在升级Service Pack 22后，可以正确加载AEM Launch模板。 此修复程序可更正内部启动配置中的无效数据，从而允许用户查看、编辑和创建启动项，而不会出现错误或缺少字段的情况。 (SITES-28504)


<!-- #### Link Checker{#sites-link-checker-6523}

* A () -->

<!-- #### MSM - Live Copies{#sites-msm-live-copies-6523}

* A () -->


#### 页面编辑器{#sites-pageeditor-6523}

* 修复了屏幕分辨率较低时加载AssetPicker的问题。 现在，当用户以较低屏幕分辨率(1728×1117或更低)滚动时，AssetPicker可正确加载资产。 用户在滚动时不再遇到缺少资产的情况，这改进了跨不同设备断点的资产管理。 (SITES-28065)
* 修复了页面锁定和解锁操作缺少屏幕阅读器公告的问题。 现在，当用户激活“锁定/解锁”按钮时，页面编辑器会正确宣布“信息：页面已被锁定/解锁”消息。 此修复提高了辅助功能合规性，并确保屏幕阅读器用户在页面编辑期间接收动态更新。 (SITES-27143)
* 改进了AEM创作中组件操作的键盘焦点行为。 AEM创作工具中增强的键盘导航功能，可确保在“配置”、“删除”或“转换”等操作完成后，焦点仍位于新创建或选定的组件上。 以前，焦点转移到页面顶部，导致出现辅助功能合规性问题。 此更新改善了键盘和辅助技术用户的用户体验。 它通过在编辑工作流中保持逻辑焦点进度来实现这一点。 (SITES-26549)
* 改进了“作者”对话框中的选项卡导航。 通过允许用户在到达“描述”编辑框后继续往前按Tab键，增强了“AEM创作”对话框中的键盘导航功能。 以前，描述字段中的焦点陷印会阻止进一步的导航，而无需使用特殊的组合键。 此更新确保用户仅使用Tab键即可无缝地在各个字段之间移动，从而改进了辅助功能合规性和用户体验。 (SITES-26524)
* AEM 6.5 Service Pack 22中引入了一个回归，该回归阻止用户在Launch标题中包含空格。 此修复恢复了使用空格的能力，使团队能够根据预期行为更灵活地定义和组织Launch名称。 (SITES-29414)
* 修复了在隐藏/取消隐藏操作后布局容器中组件的大小调整问题。 现在，在隐藏和取消隐藏布局容器后，页面编辑器可正确计算列值。 用户可以调整组件大小而不会出错，并且在调整大小操作期间列可以正确显示。 (SITES-28463)
* 修复了页面编辑器中的“内容树”按钮放置错误。 页面编辑器现在可以在预期的“Head Teaser”对话框下正确放置内容树配置按钮，而不是错误的部分。 该修复更新了“内容树”对话框的CSS以使用`top:0`而不是`bottom:0`，从而确保按钮放置正确。 (SITES-28448)


<!-- #### Replication{#sites-replication-6523}

* A () -->


#### 富文本编辑器{#sites-rte-6523}

使用纯文本粘贴模式修复富文本编辑器中的意外`<br>`标记。 使用纯文本`defaultPasteMode`时，富文本编辑器现在可以正确处理剪切和粘贴操作。 此修复可防止在用户在RTE字段中剪切和粘贴文本时插入意外的`<br>`标记，从而确保在内容编辑期间可干净地设置格式。 (SITES-27780)

#### Universal Editor {#sites-universal-editor-6523}

* 在将包含查询参数的多个请求发送到AEM时，可能无法及时返回登录令牌Cookie，这可能会导致登录失败。 (SITES-30659) <!-- LTS -->
* 要确保与SAML处理程序兼容和支持，您必须配置`service.ranking`属性，以便`Query Token Auth`处理程序在&#x200B;**&#x200B;处理程序之前`SAML Auth`运行。 (SITES-29684)

### [!DNL Assets]{#assets-6523}

* 选择[!DNL AEM]Assets6.5.22.0Assets![、导航到](/help/assets/assets/Smock_Asset_18_N.svg)**[!UICONTROL 搜索Adobe Stock ]**文件夹并选择库存图像后，**[!UICONTROL &#x200B;内部部署(]**)导航页面上出现以下问题：
   * 无法许可所选库存图像并将其保存为单击&#x200B;**[!UICONTROL 许可并保存]**&#x200B;将显示一个空下拉列表。
   * 选择Stock图像或重新输入库存页面URL将重定向到[!DNL AEM]主页，阻止访问Adobe Stock图像。 (ASSETS-48687)
* 如果在`/`内部部署([!DNL AEM])导航页面上的文件夹名称包含6.5.22.0，则管理文件夹时出现问题。 (ASSETS-46740)
* 在[!DNL AEM] 6.5上，由于内存使用率较高，资产详细信息页面无法从![收藏集](/help/assets/assets/Smock_Collection_18_N.svg)**[!UICONTROL 收藏集&#x200B;]**视图加载。 (ASSETS-46738)
* 将[!DNL InDesign]作为`Day CQ DAM Mime Type OSGI`服务的集成问题错误地将[!DNL InDesign]文件识别为`x-adobe-indesign`而不是`x-indesign`。 (ASSETS-45953)
* [!DNL AEM 6.5.21]会话泄露跟踪到现成的&#x200B;**[!UICONTROL 计划发布到Brand Portal]**&#x200B;工作流步骤。 (ASSETS-44104)
* 处理和发布图像时，**[!UICONTROL 中显示]**&#x200B;内存不足(OOM)[!DNL AEM]错误。 此问题是由工作流中已弃用的方法造成的，例如&#x200B;**[!DNL Dam Asset update]**&#x200B;和&#x200B;**[!DNL Dynamic Media: Reprocess assets]**。 (ASSETS-43343)
* 进行细微更改后（例如更新标题），您将在本地Sites实例上重新打开并重新保存&#x200B;**[!DNL Connected Assets configuration]**。 然后，远程实例会断开与本地实例的连接。 因此，它无法与本地Sites实例建立通信。 (ASSETS-44484)
* 在[!DNL AEM 6.5.21]中，取消列表视图中的资产上传并执行第二次上传时，[!DNL AEM]显示已上传&#x200B;**[!UICONTROL 0个NaN资产]**&#x200B;错误。 (ASSETS-44124)

#### [!DNL Dynamic Media]{#assets-dm-6523}

向资源添加了元数据属性(`jcr:content/metadata/dam:scene7SmartCropStatus`)，用于标识失败的智能裁剪层代。 通过手动或自动工作流，支持高效地搜索、筛选和重新处理存在智能裁剪问题的资源。 (ASSETS-46237)

#### [!DNL Dynamic Media] — 混合模式 {#assets-dm-hybrid-6523}

##### Dynamic Media — 混合附加组件包(AEM 6.5.23及更高版本)

从AEM 6.5 Service Pack 23开始，提供了适用于Dynamic Media — 混合模式的新附加组件包。 此包中包含与Dynamic Media — 混合运行模式特别兼容的`cq-scene7-imaging`捆绑包。

**包含密钥修复**

修复了Dynamic Media — 混合部署中的一个问题：尽管复制成功且没有错误，但`catalog.expiration`下对`/conf/global/settings/dam/dm/imageserver`参数的更新未反映在服务器或创作URL上。 此更新可确保CRX/DE、服务器响应和公共交付URL之间的过期值保持一致。 反过来，它改进了缓存行为以及映像转换的可靠性。 (ASSETS-44837)

**重要注意事项**

* 基本AEM 6.5.23（及更高版本）安装中的`cq-scene7-imaging`捆绑包&#x200B;*与Dynamic Media — 混合运行模式不兼容*。
* 仅安装Service Pack 23（及更高版本）不会&#x200B;*自动更新为Dynamic Media — 混合（*&#x200B;运行模式）配置的AEM实例上的`cq-scene7-imaging`现有`-r dynamicmedia`捆绑包。

**何时安装混合附加组件包**

* 从AEM 6.5.19或更低版本直接升级到AEM 6.5.23（及更高版本）时。
* 当需要特定于Dynamic Media — 混合功能的修复时。
* 直接从AEM 6.5 GA（正式发布）部署新的Dynamic Media — 混合实例到Service Pack 23（及更高版本）时。

**下载混合附加组件包**

从2025年5月22日星期四开始，混合附加组件包在Adobe Software Distribution上公开发布，正式版本为AEM 6.5.23。通过在Software Distribution中搜索&#x200B;**AEM 6.5 Dynamic Media混合加载项包**，用户可以找到它。


### [!DNL Forms]{#forms-6523}

#### 表单设计器

* 当用户使用exportDataAPI导出基于XFA的PDF的数据时，生成的XML与使用Acrobat Reader手动导出的XML数据相比，显示差异。 与Acrobat Reader生成的输出相比，输出中缺少某些字段的值。 (LC-3922791)

* 在AEM Forms 6.5.22.0中，在Workbench中使用“输出服务”生成带标记的PDF时，会在目录项的引用标记下添加一个意外的标签标记。 (LC-3922756)

* 当用户在AEM Forms Designer中对齐字段字幕且对其底部或右侧对齐时，标记树仅包含字幕而不包含相应的值，从而导致辅助功能标记不完整。 (LC-3922619)

* 从AEM Forms 6.5 Service Pack 6升级到AEM Forms Service Pack 20时，生成的PDF中的二维码变得不可读。 二维码的替换文本也无法通过辅助功能测试，从而影响屏幕阅读器兼容性。 (LC-3922551)

* 当用户在AEM Forms Service Pack 18上的代理UI中渲染信件时，由于FormService.render() API，内容无法正确显示。 (LC-3922461)

#### Forms

* 在AEM Forms中，在根面板上启用“允许标题使用富文本”会导致嵌套面板上的“从记录文档排除标题”错误地隐藏根面板的标题。 它会在生成的记录文档中进行此操作。 (FORMS-19696)

* 在AEM 6.5上的JSON架构中，系统忽略通过`sling:resourceType`分配的自定义`aem:afProperties`。在渲染期间忽略自定义资源类型。 (FORMS-19691)

* 当用户使用URI提交带有预填充附件的自适应表单时，由于缺少二进制数据，表单提交失败并出现NullPointerException。 (FORMS-19371) (FORMS-19486)

* 当用户在PDF 6.5 Forms的“Forms和文档”部分下上传AEM时，时间轴功能停止运行。 (FORMS-19407)(FORMS-19234)

* 当用户使用AEM Forms中的现成(OOTB)文件附件组件上传文件时，会识别安全漏洞。 这个问题可能导致未经授权的实体拦截提交流程。 (FORMS-19271)

* 当用户在AEM Forms中配置现成的自适应表单以自动生成记录文档(DoR)时，Acrobat Reader文档属性中的“标题”字段不显示捕获的DoR标题。 默认情况下，表单标题不会代替文件名出现。 (FORMS-19263)

* 当用户在Agent UI中打开交互式通信时，无法完全擦除预填充的数据；移除后，它将自动使用相同的数据重新填充。 (FORMS-19151)

* 当用户在Agent UI中预览日期字段时，日期意外变化。 出现此问题的原因是VM的UTC设置与系统对日期的解释之间存在时区差异。 (FORMS-19115)

* 当用户提交表单时，文件附件可能会重复，从而导致同一文件被多次上传。 (FORMS-19045)(FORMS-19051)

* 在AEM 6.5 Document Security中将协调员添加到策略集在生产环境和较低环境中均失败。 (FORMS-18603、FORMS-18212、FORMS-19697)

* 当用户在AEM Forms Service Pack 22中单击桌面模式下字段为空的“datepicker-calendar-icon”时，由于未定义的_$focusedDate变量将发生错误，并中断关联的自定义脚本。 (FORMS-18483)(FORMS-18268)

* 在AEM Forms Service Pack 19 (6.5.19.0)上，当客户预览信件时，“字内金额”字段无法正确显示或更新数字值，导致对齐错误和内容中缺少空格。 (FORMS-18437、FORMS-17330、FORMS-18209、FORMS-18557、CTG-4150848、FORMS-19614、LC-3922004)

* 当客户在RHEL上预览在AEM Forms 6.5 SP19中保存的书信时，内容无法对齐，缺少空格，并出现意外字符，如“x”。 (FORMS-18422)(FORMS-17641)

* 当用户在AEM Forms中的选项卡之间导航时，在第一个选项卡上选择组件会变得无响应。 (FORMS-18345)

* 在AEM Forms 6.5.21.0中，当用户使用WebToPDF选项将HTML文件转换为PDF时，输出PDF缺少标题部分，包括元数据和标题标记。 (FORMS-18223、FORMS-17835、FORMS-19642、FORMS-18224)

* 在AEM JEE Process Manager SDK中，当用户调用retryAction(long actionOid)方法时，系统会错误地重试tb_action_instance表中找到的第一个操作。 即使提供了特定的操作ID或ID为空，也会发生此工作流，从而导致意外行为。 (FORMS-18187)

* 更新到SP22后，用户遇到问题，即保存的草稿和提交功能失败，但未显示任何错误消息。 (FORMS-18069)

* 在AEM 6.5.21.0中，从基于XSD的基础组件转换为核心组件会阻止在JSON架构中实施跨文件引用，从而影响自适应Forms迁移。 (FORMS-18065)

* 当用户在代理UI中预览信件时，由于IC时间转换问题，日期字段显示不正确的值。 这些差异源于VM环境与系统对时间的解释（UTC与本地时间）之间的时区差异。 (FORMS-17988) (FORMS-17248)

* 当用户在AEM Forms中使用通知IC模板预览信件时，PDF的生成时间存在显着差异，从1.5秒到超过10秒不等，即使是在同一服务器上。 这种不一致性会影响业务关键型工作流。 (FORMS-17951)

* 当用户使用“数据源”选项将自适应表单中的涂写签名对象绑定到XDP时，无法保存更改。 原因在于，即使使用有效值，仍存在长宽比验证错误。 (FORMS-17587)

* 当用户使用具有用于文档片段的许多隐藏字段的特定XDP时，AEM会在`cm:optional`属性设置为false的情况下创建CRX节点，这会导致交互式通信(IC)提交失败。 (FORMS-17538)

* 在AEM Forms 6.5.19.0上，当客户预览信件时，如果定义了商机和帧的数字限制，则数字框字段无法正确处理负值。 此问题因使用parseFloat而发生，它将减号视为数字的一部分。 (FORMS-17451)

* 在AEM Forms 6.5上，当预览信件时，注意到Adobe.json文件中使用了“*”通配符，令人担心其用途和潜在的修改。 (FORMS-17317)

* 当用户在`Apply for a Fixed Rate Saver joint account`上使用屏幕阅读器时，标题被错误地宣布为`clickable`，导致可访问性问题。 (FORMS-17038)

* 嵌入表单时，生成的iframe缺少title属性，从而导致出现辅助功能合规性问题。 (FORMS-17010)

* 使用Forms Manager UI下载表单时，始终包含关联的依赖项，例如主题和片段。 (FORMS-15811)

* 当用户访问移动设备上的表单(iOS和Android™)时，第一页上的“下一个”和“上一个”按钮被禁用。 但是，屏幕阅读器不会将其标识为已禁用。 (FORMS-15773)

* 当用户保存启用了片段和延迟加载的大型表单时，无法检索草稿，并中断工作流。 (FORMS-19890和FORMS-19808)

#### FORMS JEE

* 当用户在AEM Forms中重新配置数据库时，由于硬编码的参数，连接失败。 (FORMS-19568和FORMS-17621)

* 当用户使用partial turnkey方法使用MySQL 8.4设置AEM 6.5时，LiveCycle Configuration Manager (LCM)无法识别所需的MySQL连接器驱动程序。 这会导致数据库连接测试和设置失败。 (FORMS-19442)

* 当用户在JEE环境中的JRE 11上运行带有JDBC 12.8.1的LCM时，由于不兼容问题，设置失败。 (FORMS-19276)

* 当用户在AEM内部部署中打开任务时，系统会执行Workspace启动操作配置文件，而不是AssignedUserProfile。 (FORMS-19065)

* 当用户在AEM JEE进程管理器中使用retryAction(long actionOid)方法时，会发生意外行为。 (FORMS-18357)(FORMS-18187)

* 在AEM Forms 6.5.21.0上，PDFG转换失败并出现以下错误：(FORMS-16851)(FORMS-14613)

#### Forms验证码 {#forms-captcha-6523}

* 通过将提交错误代码更新为400，改进了自适应Forms中的reCAPTCHA警报。 此外，改进了日志警报以区分超时、过期和机器人检测故障，从而提高故障排除的准确性和系统可观察性。 (FORMS-19240)
* 在AEM Forms中使用reCAPTCHA集成时，在`ResourceResolver`中关闭了一个未关闭的`ReCaptchaConfigurationServiceImpl`实例，以防止潜在的资源泄漏并提高系统稳定性。 (FORMS-19242)
* 通过确保`/conf/global`文件夹中存在多个条目时每个表单绑定正确的配置，改进了AEM Forms的验证码配置处理。 如果未明确选择配置容器，则防止意外使用错误的验证码设置。 (FORMS-19239)

<!--
#### XMLFM {#forms-xmlfm-6523}

* A () -->

<!--
#### [!DNL Adaptive Forms] {#adaptive-forms-6523}

* A () -->

<!--
#### [!DNL Forms Designer] {#forms-designer-6523}

* A () -->


### 基础 {#foundation-6523}

* 修复了Coral警报横幅中的一个问题：在升级到Service Pack 21后，文本颜色显示为白色而非黑色。 确保应用正确的样式，以保持界面中警报消息的正确对比度和可读性。 (NPR-42359)
* 在智能标记配置中添加了对OAuth集成的支持，以便与弃用JWT（JSON Web令牌）保持一致。 使用更新的身份验证方法确保智能标记功能的持续功能。 (NPR-42296)

#### Apache Felix {#foundation-apachefelix-6523}

修复了将私钥文件上传到CRX中的二进制类型属性字段时发生的NullPointerException，从而恢复通过Service Pack 16存在的兼容性。 在AEM Managed Services中启用安全密钥文件上传工作流，而不会出现服务器错误或证书续订过程中断。 (CQ-4359178)


<!--
#### Campaign{#foundation-campaign-6523}

* A () -->

<!--
#### Cloud Services{#foundation-cloudservices-6523}

* A () -->

<!--
#### Communities {#foundation-communities-6523}

* A () -->

<!--
#### Content distribution{#foundation-content-distribution-6523}

* A () -->

<!--
#### CRX {#foundation-crx-6523}

* A () -->


#### Granite{#foundation-granite-6523}

* 解决了在升级到Service Pack 21后加载HTML页面时，Apache Sling脚本服务之间导致延迟或失败的OSGi依赖项循环。 更新了内部服务引用，以消除涉及`SightlyScriptingEngineFactory`和相关组件的循环依赖关系，从而提高脚本引擎的可靠性和启动行为。 (GRANITE-56808)
* 更新了JS Use Scripts in Apache Sling to only-demand而不是在启动时急切地加载，从而消除了线程争用并降低发布服务器在加载下无响应的风险。 此更改通过防止早期脚本解析导致的资源锁定，提高了高流量情况下的服务器稳定性和响应时间。 (GRANITE-56611)
* 更正了AEM Omnisearch中的一个问题：输入字段的占位符错误地显示为标签，从而导致视觉混乱。 确保跨过滤器字段正确呈现占位符，保持一致和可访问的表单行为。 (GRANITE-51791)
* 解决了在内容片段模型编辑器中选择超过30个具有多字段引用的CFM（内容片段模型）时触发的服务器错误。 增强了过滤器建议组件以支持POST操作。 此功能允许在内容片段创建期间正确处理大型引用集，并改善高容量模型配置的稳定性。 (GRANITE-57164)
* 解决了CFM中单击靠近复选框无意间切换其状态的问题。 更新了样式，以严格限制对复选框元素的点击激活，防止意外用户交互，并提高表单可用性和可访问性。 (GRANITE-52384)


<!--
#### Integrations{#foundation-integrations-6523}

* A () -->


#### Jetty{#foundation-jetty-6523}

解决了SNI验证阻止使用具有自定义主机标头的Dispatcher SSL配置的AEM客户通过HTTPS进行API调用的问题。 引入了一个选项，该选项可作为Jetty配置的一部分禁用SNI验证，从而启用与特定反向代理设置（其中`mod_proxy`不可行）的兼容性。 (NPR-42614)


<!--
#### Localization{#foundation-localization-6523}

* A () -->

<!--
#### Oak {#foundation-oak-6523}

* A () -->


#### Platform{#foundation-platform-6523}

* 通过确保合并的标记值始终在资产中正确显示，修复了标记合并行为不一致的问题，无论标记是内联创建还是通过标准标记创建方法创建。 防止`EN:title`字段中的残值覆盖合并的标记显示。 (CQ-4358812)
* 修复了“标记编辑”对话框中标记值中的&amp;字符的重复编码问题。 防止在每次保存时附加额外的“&amp;”实体，确保标记值在编辑过程中保持干净和一致，并避免创作内容中出现显示错误。 (CQ-4359048)
* 解决了阻止在WebSphere®上运行的AEM 6.5中自适应表单提交时发送电子邮件的`ClassCastException`错误。 此修复程序通过确保`com.sun.mail.handlers.text_plain`和`java.activation.DataContentHandler`之间的兼容性，并与WebSphere®环境预期的邮件处理程序配置保持一致，从而成功传输电子邮件。 (NPR-42500)
* 通过确保AEM在安装失败且错误响应为空时显示一条明确消息，改进了包管理器中的错误处理。 此修复可防止静默式故障，并有助于在包部署期间更快地调试。 (NPR-42375)

<!--
#### Security{#foundation-security-6523}

* A -->

<!--
#### Sling{#foundation-sling-6523}

* A () -->


#### 翻译{#foundation-translation-6523}

修复了在使用&#x200B;**更新语言副本**&#x200B;更新工作流中的内容片段时触发的NullPointerException (NPE)问题。 此修复可确保在编辑与翻译引用关联的内容时，工作流不会进入失败状态或停滞在运行状态。 (NPR-42115)

#### 用户界面{#foundation-ui-6523}

将缺少的`title`属性添加到组件编辑对话框中的Coral UI对话框按钮，如&#x200B;**完成**&#x200B;和&#x200B;**取消**，以改善辅助功能并启用自动验证。 确保按钮在标记呈现过程中保留预期属性，防止在基于Selenium的UI测试中失败。 (NPR-42412)

#### WCM{#foundation-wcm-6523}

修复了在具有Service Pack 19或更高版本的环境中使用&#x200B;**更新语言副本**&#x200B;时，阻止将页面添加到翻译作业的问题。 确保翻译工作流按预期进行，从而实现语言副本之间的正确页面传输，而无需手动干预。 (CQ-4357929)

#### 工作流{#foundation-workflow-6523}

解决了`EmailNotificationServiceProcessor`中的一个问题：在修补程序部署后，`getSegmentId`方法返回`null`，导致电子邮件触发器在工作流处理期间失败。 通过确保处理器检索所需的`SegmentInfo`值来支持跨AEM实例的电子邮件通知工作流，还原正确的区段ID解析逻辑。 (CQ-4359755)


## 安装[!DNL Experience Manager] 6.5.23.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.23.0需要[!DNL Experience Manager] 6.5。有关详细说明，请参阅[升级文档](/help/sites-deploying/upgrade.md)。<!-- UPDATE FOR EACH NEW RELEASE -->
* 可在Adobe [软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip)上下载Service Pack。
* 在具有MongoDB和多个实例的部署中，使用包管理器在其中一个创作实例上安装[!DNL Experience Manager] 6.5.23.0。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe不建议您删除或卸载[!DNL Experience Manager] 6.5.23.0包。 因此，在安装该包之前，您应该创建`crx-repository`的备份，以防必须回滚。<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### 在[!DNL Experience Manager] 6.5上安装服务包{#install-service-pack}

1. 如果实例处于更新模式（从早期版本更新实例时），请在安装之前重新启动该实例。 如果实例的当前正常运行时间较长，Adobe建议重新启动。

1. 安装之前，请为[!DNL Experience Manager]实例拍摄快照或进行全新备份。

1. 从[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip)下载Service Sack。<!-- UPDATE FOR EACH NEW RELEASE -->

1. 打开包管理器，然后选择&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。 若要了解更多信息，请参阅[包管理器](/help/sites-administering/package-manager.md)。

1. 选择包，然后选择&#x200B;**[!UICONTROL 安装]**。

1. 要更新S3连接器，请在安装Service Pack后停止实例，使用安装文件夹中提供的新的二进制文件替换现有连接器，然后重新启动实例。 请参阅[Amazon S3数据存储](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>在安装Service Pack期间，包管理器UI上的对话框有时会退出。 Adobe建议您在访问部署之前等待错误日志稳定下来。 等待与卸载更新程序捆绑包相关的特定日志，然后确定安装成功。 通常，此问题发生在[!DNL Safari]浏览器中，但可能会间歇性地发生在任何浏览器中。

**自动安装**

可以使用两种不同的方法来安装[!DNL Experience Manager] 6.5.23.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* 当服务器联机时，将包放入`../crx-quickstart/install`文件夹中。 软件包会自动安装。
* 使用包管理器[中的](/help/sites-administering/package-manager.md#package-share)HTTP API。 使用`cmd=install&recursive=true`安装嵌套包。

>[!NOTE]
>
>Experience Manager 6.5.23.0不支持Bootstrap安装。<!-- UPDATE FOR EACH NEW RELEASE -->

**验证安装**

要了解经认证可与此版本配合使用的平台，请参阅[技术要求](/help/sites-deploying/technical-requirements.md)。

1. 产品信息页面(`/system/console/productinfo`)在`Adobe Experience Manager (6.5.23.0)`已安装的产品[!UICONTROL 下显示更新的版本字符串]。<!-- UPDATE FOR EACH NEW RELEASE -->

1. 在OSGi控制台中，所有OSGi包均为&#x200B;**[!UICONTROL 活动]**&#x200B;或&#x200B;**[!UICONTROL 片段]**（使用Web控制台： `/system/console/bundles`）。

1. OSGi捆绑包`org.apache.jackrabbit.oak-core`的版本为1.22.20或更高版本（使用Web控制台： `/system/console/bundles`）。<!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### 安装[!DNL Experience Manager] Forms的Service Pack{#install-aem-forms-add-on-package}

有关在Experience Manager Forms上安装Service Pack的说明，请参阅[Experience Manager Forms Service Pack安装说明](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)。

>[!NOTE]
>
>在 [AEM 6.5 快速入门](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/implementing/deploying/deploying/deploy)中谈及的自适应表单功能旨在仅作探索和评估用途。由于自适应表单功能需要适当的许可，因此必须获得 AEM Forms 的有效许可证才能作生产用途。

### 安装适用于Experience Manager内容片段的GraphQL索引包{#install-aem-graphql-index-add-on-package}

使用GraphQL的客户必须安装[Experience Manager内容片段和GraphQL索引包1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip)。

这样，您就可以根据实际使用的功能添加所需的索引定义。

无法安装此包可能会导致GraphQL查询缓慢或失败。

>[!NOTE]
>
>每个实例仅安装此包一次；无需随每个Service Pack一起重新安装。

### UberJar{#uber-jar}

[!DNL Experience Manager] 6.5.23.0的UberJar在[Maven中央存储库](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.22/)中可用。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

要在Maven项目中使用UberJar，请参阅[如何使用UberJar](/help/sites-developing/ht-projects-maven.md)，并在项目POM中包含以下依赖项： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.23</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar和其他相关工件可在Maven中央存储库上使用，而不是Adobe公共Maven存储库(`repo.adobe.com`)。 主UberJar文件已重命名为`uber-jar-<version>.jar`。 因此，`classifier`标记中没有`apis`，值为`dependency`。



## 已弃用和已删除的功能{#removed-deprecated-features}

有关AEM 6.5已弃用或删除的所有功能的详细列表，请参阅[已弃用和已删除的功能](/help/release-notes/deprecated-removed-features.md/)。

### SPA 编辑器 {#spa-editor}

[从AEM 6.5版本6.5.23开始的新项目已弃用SPA编辑器](/help/sites-developing/spa-overview.md)。SPA编辑器仍受现有项目的支持，但不应用于新项目。

现在管理 AEM 中的 Headless 内容时首选以下编辑器：

* [通用编辑器](/help/sites-developing/universal-editor/introduction.md)，用于可视化编辑。
* [内容片段编辑器](/help/sites-developing/universal-editor/introduction.md)，用于以基于表单的方法编辑。

## 已知问题{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* **AEM 6.5.21-6.5.23和AEM 6.5 LTS GA中的JSP脚本包问题**
AEM 6.5.21、6.5.22、6.5.23和AEM 6.5 LTS GA随`org.apache.sling.scripting.jsp:2.6.0`捆绑包一起提供，其中包含已知问题。 当AEM实例处理许多并发请求时，高负载下通常会出现问题。

  出现此问题时，错误日志中可能会出现以下异常之一，并伴有对`org.apache.sling.scripting.jsp:2.6.0`的引用：

   * `java.io.IOException: classFile.delete() failed`
   * `java.io.IOException: tmpFile.renameTo(classFile) failed`
   * `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
   * `java.io.FileNotFoundException`

  出现此错误时，唯一的恢复方法是重新启动AEM实例。

  请联系Adobe客户支持并参考此发行说明以获得解决方案。

* **与Oak相关**
在Service Pack 13及更高版本中，已开始出现以下错误日志，这会影响持久性缓存：

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  或者

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  要解决此异常，请执行以下操作：

   1. 从`crx-quickstart/repository/`中删除以下两个文件夹

      * `cache`
      * `diff-cache`

   1. 安装Service Pack，或重新启动Experience Manager as a Cloud Service。
`cache`和`diff-cache`的新文件夹是自动创建的，您在`mvstore`中不再遇到与`error.log`相关的异常。

* 更新可能已为内容模型使用自定义API名称的GraphQL查询，以改用内容模型的默认名称。

* GraphQL查询可以使用`damAssetLucene`索引而不是`fragments`索引。 此操作可能会导致GraphQL查询失败或需要很长时间才能运行。

  若要更正此问题，必须将`damAssetLucene`配置为在`/indexRules/dam:Asset/properties`下包含以下两个属性：

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  更改索引定义后，需要重新索引(`reindex` = `true`)。

  执行这些步骤后，GraphQL查询的执行速度应该会更快。

* 尝试移动、删除或发布内容片段、站点或页面时，在获取内容片段引用时出现问题。 后台查询失败。 也就是说，功能无法正常工作。
为确保操作正确，必须将以下属性添加到索引定义节点`/oak:index/damAssetLucene`（不需要重新索引）：

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* 如果您将[!DNL Experience Manager]实例从6.5.0 - 6.5.4升级到Java™ 11上的最新Service Pack，则会在`RRD4JReporter`文件中看到`error.log`异常。 若要停止异常，请重新启动[!DNL Experience Manager]的实例。<!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 用户可以在[!DNL Assets]中重命名层次结构中的文件夹，并将嵌套文件夹发布到[!DNL Brand Portal]。 但是，在重新发布根文件夹之前，[!DNL Brand Portal]中的文件夹标题不会更新。

* 安装[!DNL Experience Manager] 6.5.x.x期间可能会显示以下错误和警告消息：
   * “当使用Adobe Target API（IMS身份验证）在[!DNL Experience Manager]中配置Target Standard集成时，将体验片段导出到Target会导致创建错误的选件类型。 Target将创建多个类型为“HTML”/源“Adobe Experience Manager”的选件，而不是类型为“体验片段”/源“Adobe Target Classic”。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在`granite/operations/maintenance`处未找到维护时段。
   * 当使用集合函数(如SUM、MAX和MIN)时，自适应表单服务器端验证失败(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` ：在`granite/operations/maintenance`处未找到维护时段。
   * 通过可购物横幅查看器预览资产时，Dynamic Media交互式图像中的热点不可见。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` ：等待注册更改完成取消注册时超时。

* 从AEM 6.5.15开始，```org.apache.servicemix.bundles.rhino```捆绑包提供的Rhino JavaScript Engine具有新的提升行为。 使用严格模式(```use strict;```)的脚本必须声明其正确的变量。 否则，它们将不会运行，并最终引发运行时错误。

* 通过官方更新包安装与标记相关的现成内容会将`/content/cq:tags`节点的languages属性重置为默认值。 此操作适用于Service Pack、Security Service Pack、Extended Feature Pack、Cumulative Feature Pack、修补程序等。 因此，在安装之前，必须从属性中添加它。

### AEM Sites的已知问题 {#known-issues-aem-sites-6523}

内容片段 — 预览由于大型片段树的DoS保护而失败。 请参阅关于默认GraphQL查询执行器配置选项[的](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-kcs/kbarticles/ka-23945)KB文章(SITES-17934)

### AEM Forms的已知问题 {#known-issues-aem-forms-6523}

>[!NOTE]
>
> 对于没有可用修补程序的问题，请勿升级到Service Pack 6.5.23.0，因为这可能会导致意外错误。 只有在发布了所需的修补程序之后，才能升级到Service Pack 6.5.23.0。

* 当用户将Struts从AEM Service Pack 2.5.x升级到AEM Forms Service Pack 6.x时，策略UI无法显示所有配置，例如添加水印的选项。 您可以[下载并安装修补程序](/help/release-notes/aem-forms-hotfix.md)以解决问题。  (FORMS-20203)
* 升级到AEM Forms Service Pack 6.5.23.0后，ImageToPDF转换服务失败，并出现错误(FORMS-20360)：
  ```17:15:44,468 ERROR [com.adobe.pdfg.GeneratePDFImpl] (default task-49) ALC-PDG-001-000-ALC-PDG-011-028-Error occurred while converting the input image file to PDF. com/adobe/internal/pdftoolkit/core/encryption/EncryptionImp```您可以[下载并安装修补程序](/help/release-notes/aem-forms-hotfix.md)以解决问题。

* 安装AEM Forms JEE Service Pack 21 (6.5.21.0)后，如果在`(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)`文件夹下找到Geode Jar `<AEM_Forms_Installation>/lib/caching/lib`的重复条目(FORMS-14926)，请执行以下步骤，以解决该问题：

   1. 如果定位器正在运行，请停止它们。
   2. 停止AEM服务器。
   3. 转到`<AEM_Forms_Installation>/lib/caching/lib`。
   4. 删除除`geode-*-1.15.1.2.jar`之外的所有Geode修补程序文件。 确认仅存在具有`version 1.15.1.2`的Geode jar。
   5. 在管理员模式下打开命令提示符。
   6. 使用`geode-*-1.15.1.2.jar`文件安装Geode修补程序。

* 如果用户尝试预览包含保存的XML数据的草稿信件，则对于某些特定信件，它会陷入`Loading`状态。 要下载并安装修补程序，请参阅[Adobe Experience Manager Forms修补程序](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)文章。 (FORMS-14521)
* 用户从AEM 6.5 Forms Service Pack 18或19升级到Service Pack 20或21时，遇到JSP编译错误。 此错误会阻止他们打开或创建自适应表单。 它还导致其他AEM界面出现问题。 这些界面包括页面编辑器、AEM Forms UI、工作流编辑器和系统概述UI。 (FORMS-15256)

  如果您遇到此类问题，请执行以下步骤来解决此问题：
   1. 导航到CRXDE中的目录`/libs/fd/aemforms/install/`。
   2. 删除名为`com.adobe.granite.ui.commons-5.10.26.jar`的包。
   3. 重新启动AEM服务器。

* 使用Forms加载项更新到AEM Forms Service Pack 20 (6.5.20.0)后，依赖使用基于凭据的身份验证的旧版Adobe Analytics Cloud Service的配置停止工作。 此问题会导致Analytics规则无法正确执行。 要下载并安装修补程序，请参阅[Adobe Experience Manager Forms修补程序](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)文章。 (FORMS-15428)
* 在交互式通信代理UI的打印预览中，所有字段值的货币符号（如美元符号$）显示方式不一致。 对于最多999的值，它出现，但对于1000及更高版本的值则缺失。 (FORMS-16557)
* 交互式通信中对嵌套布局片段XDP所做的任何修改都不会反映在IC编辑器中。 (FORMS-16575)
* 在交互式通信代理UI的打印预览中，某些计算值无法正确显示。 (FORMS-16603)
* 在打印预览中查看信件时，内容会更改。 即，某些空格消失，某些字母被替换为`x`。 (FORMS-15681)
* 当用户配置WebLogic 14c实例时，由于涉及SLF4J库的类加载程序冲突，因此AEM Forms Service Pack 21 (6.5.21.0)中JEE上在JBoss®上运行的PDFG服务失败。 错误显示如下(CQDOC-22178)：

  ```java
  Caused by: java.lang.LinkageError: loader constraint violation: when resolving method "org.slf4j.impl.StaticLoggerBinder.getLoggerFactory()Lorg/slf4j/ILoggerFactory;"
  the class loader org.ungoverned.moduleloader.ModuleClassLoader @404a2f79 (instance of org.ungoverned.moduleloader.ModuleClassLoader, child of 'deployment.adobe-livecycle-jboss.ear'
  @7e313f80 org.jboss.modules.ModuleClassLoader) of the current class, org/slf4j/LoggerFactory, and the class loader 'org.slf4j.impl@1.1.0.Final-redhat-00001' @506ab52
  (instance of org.jboss.modules.ModuleClassLoader, child of 'app' jdk.internal.loader.ClassLoaders$AppClassLoader) for the method's defining class, org/slf4j/impl/StaticLoggerBinder,
  have different Class objects for the type org/slf4j/ILoggerFactory used in the signature.
  ```

* Forms-20478：尝试将类型7/8 TIFF文件转换为PDF时，转换过程失败，并出现以下错误：“ALC-PDG-001-000-Image2Pdf转换失败，原因是：com/sun/image/codec/jpeg/JPEGCodec”和“ALC-PDG-016-003-PDF后处理期间发生未知/意外错误。” 系统尝试使用TM ImageIO TIFF解码器重试，但最终无法完成作业。 您可以[下载并安装修补程序](/help/release-notes/aem-forms-hotfix.md)以修复此问题。


## 包含的OSGi包和内容包{#osgi-bundles-and-content-packages-included}

以下文本文档列出了此[!DNL Experience Manager] 6.5 Service Pack版本中包含的OSGi包和内容包：

* [Experience Manager中包含的OSGi包列表6.5.23.0](/help/release-notes/assets/65230-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager中包含的内容包列表6.5.23.0](/help/release-notes/assets/65230-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的网站{#restricted-sites}

这些网站仅供客户使用。 如果您是客户并且需要访问权限，请联系您的Adobe客户经理。

* [产品下载位于licensing.adobe.com](https://licensing.adobe.com/)
* [联系Adobe客户支持](https://experienceleague.adobe.com/en/docs/customer-one/using/home)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 产品页](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5文档](https://experienceleague.adobe.com/en/docs/experience-manager-65)
>* [订阅Adobe优先产品更新](https://www.adobe.com/cn/subscription/priority-product-update.html)
