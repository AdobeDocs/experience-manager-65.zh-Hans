---
title: ' [!DNL Adobe Experience Manager] 6.5 发行说明'
description: 查找  [!DNL Adobe Experience Manager] 6.5 的版本信息、新增功能、安装操作方法和详细更改列表。
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: f018681e9202a934be2cfa8d426a32014c5ff66f
workflow-type: ht
source-wordcount: '6713'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager]6.5 最新服务包发行说明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section. -->

## 发行版本信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.23.0，适用于 GRANITE-61551 的热修复补丁<!-- UPDATE FOR EACH NEW RELEASE --> |
| 类型 | 服务包发行 |
| 日期 | 2025 年 9 月 9 日 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 下载 URL | [软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Fcq-6.5.0-hotfix-GRANITE-61551-SP23-1.2.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

<!-- OLD DOWNLOAD URL
(https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip) -->

## [!DNL Experience Manager] 6.5.23.0 的内容 {#what-is-included-in-aem-6523}

[!DNL Experience Manager] 6.5.23.0 包含新功能、客户重点要求的增强功能以及错误修复。还包括自 2019 年 4 月 6.5 首次发布以来推出的在性能、稳定性和安全性方面的改进。[在 [!DNL Experience Manager] 6.5 上安装此服务包](#install)。

<!-- UPDATE FOR EACH NEW RELEASE -->

## 主要功能和增强功能

<!--### Sites {#sites}

* A () -->

<!--
### [!DNL Assets]

* A ()
-->

### Forms {#forms-sp23}

本次发行中的主要功能和增强功能包括：

* [静态 PDF 中支持混合文本样式的可访问超链接](https://helpx.adobe.com/cn/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf)：包含混合文本样式的静态 PDF 超链接现已标记为单一可访问元素。此增强简化了标记树结构，改善了屏幕阅读器导航，并提升了无障碍合规性。

* [更新了支持平台矩阵](/help/forms/using/aem-forms-jee-supported-platforms.md)

  最新版本更新了支持的平台矩阵，确保与新技术的兼容性。

   * IBM® Content Manager 客户端 8.7

   * MongoDB 企业版 7.0

   * MySQL 8.4

   * Microsoft® SQL 服务器 2022

   * Microsoft® SQL 服务器 JDBC 驱动程序 12.8

   * Red Hat® Enterprise Linux® 9（内核 4.x，64 位）

* [强化了文件附件组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment)：作为一项安全措施，该组件现已阻止提交扩展名经过修改、试图绕过允许文件类型检查的文件。此类文件在提交过程中会被拦截，以确保仅接受有效文件类型。

* FORMS-20533、FORMS-20532：AEM Forms 现已将 Struts 版本从 2.5.33 升级至 6.x。此项支持是通过[热修复](/help/release-notes/aem-forms-hotfix.md)添加的，您可以[下载并安装](/help/release-notes/aem-forms-hotfix.md)该修补程序，以获得对最新 Struts 版本的支持。

* **LC-3922769**：部分 AEM Forms 功能现在需要 OpenSSL 3 才能正常运行。系统必须安装 OpenSSL 3，以及 `libcrypto.so.3` 和 `libssl.so.3` 库。由于安全更新仅适用于 3.0.14 及以上版本，且 SafeLogic 支持已于 2025 年 2 月终止，现已移除 BSAFE，转而采用 OpenSSL 3 满足安全合规要求。有关平台兼容性和详细要求方面的信息，请参阅 [AEM Forms on JEE 支持的平台](/help/forms/using/aem-forms-jee-supported-platforms.md)和[技术要求](/help/sites-deploying/technical-requirements.md)。


  **验证 OpenSSL 3 的安装：**

   * **基于 RHEL/CentOS/Fedora 的系统**：`rpm -qa | grep   openssl3`
   * **基于 Ubuntu/Debian 的系统**：`dpkg -l | grep openssl3`
   * **替代验证方式**：`ldd /path/to/XMLForm |   grep -E 'libcrypto.so.3|libssl.so.3'`（前提是库位于 LD_LIBRARY_PATH 中）





<!--* **Two-Factor authentication with SAML for AdminUI** 

  AdminUI in AEM Forms JEE now supports two-factor authentication using Security Assertion Markup Language (SAML) single sign-on (SSO), providing stronger security and a seamless login experience for administrators, similar to what is available in HTML Workspace. 

#### New GA features in AEM Forms {#ga-aem-forms-sp23}

* A ()

#### New Beta features in AEM Forms {#beta-aem-forms-sp23}
-->

## 服务包 23 中已修复的问题 {#fixed-issues}

<!-- 6.5.23.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-6523}

#### 辅助功能 {#sites-accessibility-6523}

* AEM 编辑器页面的画布区块现已全面支持键盘辅助功能。用户仅需使用键盘即可激活区块标题和编辑按钮，而无需依赖鼠标悬停。此更新确保符合 WCAG 2.1.1 要求，并提升了组件（如 Teaser、图像、轮播、版面、时间扭曲和注释模态框）的可用性。（SITES-25256）<!-- 6.5 LTS SP1 -->
* 修复了 AEM 页面编辑器中的一个辅助功能问题：在激活“用户画像”、“购物车”或“放弃”等按钮后，键盘焦点会意外重置到“人口统计”工具栏的起始位置。当前焦点仍位于已激活的按钮上，以支持一致的键盘导航和屏幕阅读器工作流。（SITES-25306）
* 修复了 AEM 页面编辑器中的严重辅助功能问题：在多个对话框和模态框（例如资产边栏或版面预览）的画布元素中，用户无法仅使用键盘进行操作。现在，所有交互式画布元素均支持仅使用键盘导航，确保符合 WCAG 2.1 成功准则 2.1.1 要求。（SITE-25256）
* 修复了 Sites 管理 UI 中的辅助功能问题：此前在“创建”弹出窗口中，交互式列表项使用了错误的 ARIA 角色。具有链接功能的元素被分配了 `role="listitem"` 而不是 `role="menuitem"`，这违反了 ARIA 设计模式，并导致屏幕阅读器识别混乱。更新后，所有列表组件均会遵循正确的语义角色，从而提升键盘操作和辅助技术支持的体验。（SITES-24493）
* 修复了页面标题和标记字段的无障碍标签关联问题。现在，AEM 界面在使用 JAWS 等屏幕阅读器时，能够正确关联“标题”和“页面标题”字段的无障碍标签。此项修复确保在页面创建、属性和移动工作流中正确朗读标签，从而改善 ADA 合规性。（SITES-27149）
* 修复了权限对话框中表格识别的辅助功能问题。AEM 中的权限表格现已使用正确的 ARIA 角色和属性，确保屏幕阅读器（如 JAWS）能够将其正确识别为表格。此修复提升了无障碍合规性，并确保用户能够获得准确的导航和内容提示。（SITES-27140）
* 修复了时间线中评论输入字段缺少可视化标签的问题。已为时间线部分下的“评论”输入字段补充可视化标签，以提升无障碍性。此更新确保屏幕阅读器能够准确播报字段标签。这种体验为所有用户改善了表单导航和提交体验，特别是为依赖辅助技术的用户带来便利。（SITES-26903）
* 修复了时间线评论中省略号按钮的键盘辅助功能问题。为时间线部分评论旁边的省略号（三个点）按钮启用了键盘导航功能。用户现在可以使用 Tab 键访问按钮并与之交互，改善了无障碍体验，方便依赖键盘进行导航的用户使用。（SITES-26891）
* 改进了 NVDA/Narrator 对选择对话框中搜索结果的公告。更新后的“打开选择”对话框在使用 NVDA 或 Narrator 等屏幕阅读器时，会播报是否找到搜索结果。此项改进可以帮助依赖辅助技术的用户在无需视觉确认的情况下理解搜索操作的结果。（SITES-26883）
* 修复了评论输入字段旁省略号图标的 ARIA 角色错误问题。现已将评论输入字段旁的省略号（三点）图标更新为正确的 ARIA 角色，确保屏幕阅读器能够准确识别该元素。此项改进提升了无障碍合规性，并优化了依赖于辅助技术的用户的使用体验。（SITES-26881）
* 修复了 Coral UI 组件中的无效 ARIA 属性问题。已更新 Coral UI 组件，确保所有 ARIA 属性均使用有效值，从而改善无障碍合规性。特别修复了此前错误分配的无效值（如 `aria-modal="dialog"`）。此项增强功能使屏幕阅读器能够正确解析对话框元素，从而提升依赖于辅助技术的用户的可访问性。（SITES-26873）
* 改进了“重排”场景下的图标可见性和工具提示。优化了“重排”行为，确保&#x200B;**下载**、**重新处理资产**&#x200B;和&#x200B;**签出**&#x200B;图标的工具提示能够正确显示。重点修复了当视口调整大小或更改浏览器缩放设置时，图标及其标签可能变得不可见的辅助功能问题。此项修复可以帮助视力低下的用户在“重排”过程中仍然能够看到图标，并会提供正确的图标说明。（SITES-26871）

#### 管理用户界面{#sites-adminui-6523}

修复了通用编辑器 URL 服务在缺少外部化器端点时出现异常的问题。通用编辑器 URL 服务现在能够在缺少 author、publish 或 local 外部化器端点的情况下正常处理，而不会抛出异常。即使部分外部化器配置不完整，管理员用户也能成功打开页面编辑器。（SITES-28877）<!-- LTS -->

#### 经典 UI{#sites-classicui-6523}

* 经典 UI 对话框中的问题：切换按钮后文本区域会被隐藏，且在后续点击中无法重新显示。此项修复确保在切换时文本区域能够正确重新显示，从而恢复预期行为，避免动态对话框工作流中断。（SITES-30230）
* 修复了升级到服务包 22 后经典 UI 图像资产查找器功能异常的问题。经典 UI 图像资产查找器现在能够正确处理包含空格或特殊字符的资产名称。此更新确保资产查找器能够正确编码文件名，防止搜索失败，使作者能够顺利定位并选择图像资产，而不会出现错误。（SITES-29151）

#### [!DNL Content Fragments]{#sites-contentfragments-6523}

* 修复了 `DeleteVariationIT.testUpdateBasic` 的验证测试失败问题。在运行服务包验证的过程中，`DeleteVariationIT.testUpdateBasic` 测试不再失败。此项修复纠正了 JSON 处理逻辑中的文本映射缺失问题，从而确保测试稳定性，避免不必要的测试中断。（SITES-28022）
* AEM 现已防止由图像资产中格式错误的 XMP 元数据导致的性能下降。包含无效或不合规 XMP 属性名称（例如带有数字区段或未限定结构）的资产，在处理过程中不再反复触发警告日志。系统会过滤掉存在问题的元数据，确保资产摄取和验证能够顺利完成且无错误。（SITES-30683）<!-- AEM 6.5 LTS SP1 -->


<!-- #### [!DNL Content Fragments] - Admin{#sites-admin-6523}

* A () -->


#### [!DNL Content Fragments] - 片段编辑器{#sites-fragments-editor-6523}

在某位作者已签出内容片段的情况下，其他作者仍然可以发布该片段，这与签出功能的预期行为不符。此项修复可防止在签出内容片段时，其他用户在创作界面中看到或使用发布按钮。（SITES-30578）<!-- LTS -->

#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6523}

修复了与内容片段架构相关的 GraphQL QueryValidationError。通过刷新 `cq-dam-cfm-graphql` 捆绑包，可以在使用内容片段引用时纠正架构验证错误。此项修复可确保 GraphQL 查询在部署软件包后能够正常运行，而无需手动重新对齐或重新发布架构。（SITES-27001）<!-- LTS -->


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6523}

* A () -->

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6523}

* A () -->


#### 组件控制台{#sites-component-console-6523}

改进了“组件实时使用情况”页面加载性能。优化了 AEM 中的“组件实时使用情况”页面，防止在滚动浏览大型数据集时出现空行。用户加载带有大量使用参考的组件时，现在可以连续查看数据，而不会出现不必要的空白或缺失条目。这种体验提升了页面导航体验、跟踪准确性，以及组件使用情况报告的管理效率。（SITES-26454）

#### 核心后端{#sites-core-backend-6523}

* 修复了因资产名称无效导致内容查找器资产列表失败的问题。内容查找器现在能够正确处理包含不可编码字符的资产名称。在页面编辑器中，遇到存在问题的资产名称时，资产列表不再失败或抛出异常。（SITES-28722）
* `SearchPathLimiter` 组件在每次调用时都以 ERROR 级别输出日志消息，从而导致生成过量日志条目的问题。该问题自服务包 17 开始出现，因极高的日志量引发性能问题。此次修复将日志级别降为 DEBUG，大幅减少了日志噪音，并提升了系统监控与诊断效率。（SITES-29835）
* 因 XMP 元数据格式不正确而在 `ValidationDataServlet` 中处理图像资产时触发错误的问题。此修复确保了对元数据的正确处理，并避免了对无效属性的重复解析。（SITE-30683）<!-- LTS -->


<!-- #### Core Components{#sites-core-components-6523}

* A () -->

<!-- #### Campaign integration{#sites-campaign-integration-6523}

* A () -->

<!-- #### Experience Fragments{#sites-experiencefragments-6523}

* A () -->

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6523}

* A () -->


#### 发布项{#sites-launches-6523}

* 修复了 12 月 25 日至 12 月 31 日之间启动日期显示错误的问题。发布项界面现在会正确显示 12 月 25 日至 12 月 31 日的年份。此项修复确保日期不再错误地显示为下一年，从而避免在营销活动规划和排期期间造成混淆。（SITES-28706）
* 修复了在升级至服务包 22 后，AEM 发布项模板损坏的问题。升级至服务包 22 后，AEM 发布项模板现在能够正常加载。此项修复更正了内部启动配置中的无效数据，使用户可以查看、编辑和创建发布项，不会再出现错误或字段缺失的情况。（SITES-28504）


<!-- #### Link Checker{#sites-link-checker-6523}

* A () -->

<!-- #### MSM - Live Copies{#sites-msm-live-copies-6523}

* A () -->


#### 页面编辑器{#sites-pageeditor-6523}

* 修复了在较低屏幕分辨率下 AssetPicker 的加载问题。当用户在较低分辨率（1728×1117 或更低）下滚动时，AssetPicker 现在能够正确加载资产。用户在滚动时不再遇到资产缺失的情况，从而改善了跨不同设备断点的资产管理体验。（SITES-28065）
* 修复了屏幕阅读器在页面锁定和解锁操作时未发出通知的问题。页面编辑器现在在用户点击锁定/解锁按钮时，会正确播报“信息：页面已被锁定/解锁”。此项修复提升了无障碍合规性，确保屏幕阅读器用户在页面编辑过程中能够收到动态更新。（SITES-27143）
* 改进了 AEM 创作环境中组件操作的键盘焦点行为。在 AEM 创作工具中增强了键盘导航功能，确保在执行“配置”、“删除”或“转化”等操作后，焦点能够留在新建或已选中的组件上。此前，焦点会跳转至页面顶部，造成无障碍合规性问题。此项更新改善了键盘和辅助技术用户的用户体验。它通过在编辑工作流中保持逻辑上的焦点推进来实现这一点。（SITES-26549）
* 改进了“创作”对话框中的制表键导航功能。通过允许用户在到达“描述”编辑框后继续使用制表键进行切换，增强了 AEM 创作对话框中的键盘导航功能。此前，焦点会被困在“描述”字段，若不使用特殊组合键则无法继续导航。此次更新确保用户仅使用制表键即可顺畅地在各字段间移动，从而提升了无障碍合规性和用户体验。（SITES-26524）
* 在 AEM 6.5 服务包 22 中引入了回归问题，该问题导致用户无法在“发布项”标题中输入空格。此次修复恢复了在“发布项”名称中使用空格的功能，使团队能够更灵活地定义和组织“发布项”名称，符合预期行为。（SITES-29414）
* 修复了在隐藏/取消隐藏操作后，布局容器内的组件调整大小的问题。页面编辑器现在会在隐藏和取消隐藏布局容器后正确计算列值。用户可以在不出现错误的情况下调整组件大小，并在调整过程中正确显示列布局。（SITES-28463）
* 修复了页面编辑器中内容树按钮位置错误的问题。页面编辑器现在会将内容树配置按钮正确定位在目标“Head Teaser”对话框下，而不会错误地放置在其他部分。此次修复更新了内容树对话框的 CSS，以将其定位从 `top:0` 改为 `bottom:0`，从而确保按钮位置正确。（SITES-28448）


<!-- #### Replication{#sites-replication-6523}

* A () -->


#### 富文本编辑器{#sites-rte-6523}

修复了在纯文本粘贴模式下，富文本编辑器中出现意外的 `<br>` 标记的问题。富文本编辑器在使用纯文本 `defaultPasteMode` 进行剪切和粘贴操作时，现在能够正确处理内容。此次修复避免了用户在 RTE 字段中进行剪切粘贴时插入意外的 `<br>` 标记，从而在内容编辑过程中确保格式整洁。（SITES-27780）

#### 通用编辑器 {#sites-universal-editor-6523}

* 当向 AEM 发送包含查询参数的多个请求时，login-token cookie 可能未能及时返回，从而造成登录失败。（SITES-30659）<!-- LTS -->
* 为确保与 SAML 处理程序的兼容性和支持，必须配置 `service.ranking` 属性，以便 `Query Token Auth` 处理程序在 `SAML Auth` 处理程序&#x200B;*之前*&#x200B;运行。（SITES-29684）

### [!DNL Assets]{#assets-6523}

* 在 [!DNL AEM] 本地部署版（6.5.22.0）导航页面中，选择![Assets](/help/assets/assets/Smock_Asset_18_N.svg)**[!UICONTROL Assets ]**后，进入**[!UICONTROL &#x200B;搜索 Adobe Stock ]**文件夹并选择一张 Stock 图片后，会出现以下问题：
   * 点击&#x200B;**[!UICONTROL 许可并保存]**&#x200B;时下拉菜单为空，所选 Stock 图像无法获得许可和保存。
   * 选择 Stock 图像或重新输入 Stock 页面 URL 时，会被重定向到 [!DNL AEM] 主页，导致无法访问 Adobe Stock 图像。（ASSETS-48687）
* 在 [!DNL AEM] 本地部署版（6.5.22.0）导航页面中，如果文件夹名称中包含 `/`，则在管理文件夹时会出现问题。（ASSETS-46740）
* 在 [!DNL AEM] 6.5 中，从![收藏集](/help/assets/assets/Smock_Collection_18_N.svg)**[!UICONTROL 收藏集&#x200B;]**视图进入资产详情页时，由于内存占用过高，页面无法加载。（ASSETS-46738）
* 修复了与 [!DNL InDesign] 的集成问题，因为 `Day CQ DAM Mime Type OSGI` 服务此前错误地将 [!DNL InDesign] 文件识别为 `x-adobe-indesign`，而非 `x-indesign`。（ASSETS-45953）
* [!DNL AEM 6.5.21] 中的会话泄漏问题追溯到开箱即用的&#x200B;**[!UICONTROL 定期发布到 Brand Portal]**&#x200B;工作流步骤。（ASSETS-44104）
* 在处理和发布图像时 [!DNL AEM] 中出现&#x200B;**[!UICONTROL 内存不足（OOM）]** 错误的问题。该问题是由在工作流中使用已弃用的方法引起的，例如 **[!DNL Dam Asset update]** 和 **[!DNL Dynamic Media: Reprocess assets]**。（ASSETS-43343）
* 在进行诸如更新标题等小幅修改后，在本地 Sites 实例中重新打开并保存 **[!DNL Connected Assets configuration]**。此时远程实例会丢失与本地实例的连接。因此，远程实例无法再与本地 Sites 实例建立通信。（ASSETS-44484）
* 在 [!DNL AEM 6.5.21] 中，当在列表视图中取消一次资产上传后再次执行上传时，[!DNL AEM] 会显示&#x200B;**[!UICONTROL 上传了 0 个资产，共 NaN 个资产]**&#x200B;错误。（ASSETS-44124）

#### [!DNL Dynamic Media]{#assets-dm-6523}

为资产新增了一个元数据属性（`jcr:content/metadata/dam:scene7SmartCropStatus`），用于标识智能裁剪失败的情况。此改进支持通过手动或自动化工作流对存在智能裁剪问题的资产进行高效的搜索、筛选和重新处理。（ASSETS-46237）

#### [!DNL Dynamic Media] - 混合模式 {#assets-dm-hybrid-6523}

##### Dynamic Media- 混合模式附加组件包（适用于 AEM 6.5.23 及更高版本）

从 AEM 6.5 服务包 23 开始，提供了一个适用于 Dynamic Media - 混合模式的新附加组件包。该软件包包含专门兼容 Dynamic Media - 混合运行模式的 `cq-scene7-imaging` 捆绑包。

**包含的关键修复**

修复了 Dynamic Media - 混合部署中的一个问题：即尽管复制成功且无错误，但 `/conf/global/settings/dam/dm/imageserver` 下的 `catalog.expiration` 参数更新未能在服务器或作者 URL 上反映出来。更新后确保 CRX/DE、服务器响应和公共传递 URL 之间的过期值保持一致。此改进提升了图像转化的缓存行为与可靠性。（ASSETS-44837）

**重要注意事项**

* 基础 AEM 6.5.23（及更高版本）安装中提供的 `cq-scene7-imaging` 捆绑包&#x200B;*不兼容* Dynamic Media - 混合运行模式。
* 仅安装服务包 23（及更高版本）*不会自动更新*&#x200B;已配置为 Dynamic Media - 混合模式（`-r dynamicmedia` 运行模式）的 AEM 实例中的现有 `cq-scene7-imaging` 捆绑包。

**何时安装混合模式附加组件包**

* 从 AEM 6.5.19 或更早版本直接升级至 AEM 6.5.23（及更高版本）时。
* 需要获取特定于 Dynamic Media - 混合模式功能的修复时。
* 从 AEM 6.5 GA（正式发布版）直接将新的 Dynamic Media - 混合模式实例部署至服务包 23（及更高版本）时。

**下载混合模式附加组件包**

混合模式附加组件包自 2025 年 5 月 22 日（星期四）起在 Adobe 软件分发公开发布，随 AEM 6.5.23 正式版一同推出。用户可在软件分发中搜索 **AEM 6.5 Dynamic Media 混合模式附加组件包**&#x200B;来找到该附加组件包。


### [!DNL Forms]{#forms-6523}

#### Forms Designer

* 在用户使用 exportDataAPI 导出基于 XFA 的 PDF 数据时，生成的 XML 与通过 Acrobat Reader 手动导出的 XML 数据存在差异。与 Acrobat Reader 生成的输出相比，部分字段的值在输出中缺失。（LC-3922791）

* 在 AEM Forms 6.5.22.0 中，使用工作台中的输出服务生成带标记的 PDF 时，在目录项表格的引用标记下会意外添加一个多余的标签标记。（LC-3922756）

* 当用户在 AEM Forms Designer 中将字段题注设置为底部或右对齐时，标记树仅包含题注而不包含对应的值，导致辅助功能标记不完整。（LC-3922619）

* 从 AEM Forms 6.5 服务包 6 升级至 AEM Forms 服务包 20 后，生成 PDF 中的 QR 代码变得无法识别。同时，QR 代码的替换文本在辅助功能测试中也未通过，影响了屏幕阅读器的兼容性。（LC-3922551）

* 在 AEM Forms 服务包 18 中，当用户在代理 UI 中渲染书信时，由于 FormService.render（）API 的问题，相关内容无法正确显示。（LC-3922461）

#### Forms

* 在 AEM Forms 中，如果在根面板上启用了“允许标题使用富文本”，则在嵌套面板上启用“从记录文档中排除标题”时，会错误地隐藏根面板的标题。此问题会在生成的记录文档中出现。（FORMS-19696）

* 在 AEM 6.5 中，系统会忽略通过 `aem:afProperties` 在 JSON 架构中分配的自定义 `sling:resourceType`。在渲染过程中，不会应用该自定义资源类型。（FORMS-19691）

* 当用户提交包含通过 URI 预填附件的自适应表单时，由于缺少二进制数据，表单提交会因 NullPointerException 而失败。（FORMS-19371）（FORMS-19486）

* 当用户在 AEM 6.5 Forms 的“表单与文档”部分上传 PDF 时，时间线功能会停止工作。（FORMS-19407）（FORMS-19234）

* 当用户在 AEM Forms 中使用开箱即用（OOTB）文件附件组件上传文件时，会检测到安全漏洞。该问题可能导致未经授权的实体拦截提交流程。（FORMS-19271）

* 当用户将 AEM Forms 中的开箱即用自适应表单配置为自动生成记录文档（DoR）时，Acrobat Reader 的“文档属性”中的“标题”字段未显示捕获的 DoR 标题。默认情况下，表单标题不会替换文件名显示。（FORMS-19263）

* 当用户在代理 UI 中打开交互式通信时，预填数据无法被完全清除；移除后，系统会自动再次填充相同数据。（FORMS-19151）

* 当用户在代理 UI 中预览日期字段时，日期会被意外更改。该问题是由于虚拟机的 UTC 设置与系统对日期的解读存在时区差异导致的。（FORMS-19115）

* 当用户提交表单时，文件附件可能会重复，导致同一文件多次上传。（FORMS-19045）（FORMS-19051）

* 在 AEM 6.5 文档安全中，将协调者添加到策略集时操作失败，该问题在生产环境和较低环境中均会出现。（FORMS-18603、FORMS-18212、FORMS-19697）

* 在 AEM Forms 服务包 22 中，当用户在桌面模式下点击空字段的 &quot;datepicker-calendar-icon&quot; 时，由于未定义 _$focusedDate 变量而报错，进而导致相关自定义脚本中断。（FORMS-18483）（FORMS-18268）

* 在 AEM Forms 服务包 19（6.5.19.0）中，当客户预览书信时，“大写金额”字段无法正确显示或更新数值，导致内容错位并缺少空格。（FORMS-18437、FORMS-17330、FORMS-18209、FORMS-18557、CTG-4150848、FORMS-19614、LC-3922004）

* 在 RHEL 上的 AEM Forms 6.5 SP19 中，当客户预览已保存的书信时，内容会出现错位、缺少空格，并显示如“x”等意外字符。（FORMS-18422）（FORMS-17641）

* 在 AEM Forms 中，当用户在不同选项卡之间切换时，无法响应对第一个选项卡中组件的选择操作。（FORMS-18345）

* 在 AEM Forms 6.5.21.0 中，当用户使用 WebToPDF 选项将 HTML 文件转化为 PDF 时，输出 PDF 中缺少页眉部分，包括元数据和标题标记。（FORMS-18223、FORMS-17835、FORMS-19642、FORMS-18224）

* 在 AEM JEE Process Manager SDK 中，当用户调用 retryAction（long actionOid）方法时，系统会错误地重试在 tb_action_instance 表中找到的第一个操作。即使提供了特定的操作 ID 或传入空值，仍会发生该工作流错误，导致产生非预期行为。（FORMS-18187）

* 在更新至 SP22 后，用户遇到问题：已保存草稿和提交功能均无法正常工作，且未显示任何错误消息。（FORMS-18069）

* 在 AEM 6.5.21.0 中，从基于 XSD 的基础组件迁移到核心组件时，无法在 JSON 架构中实现跨文件引用，从而影响自适应表单的迁移。（FORMS-18065）

* 当用户在代理 UI 中预览书信时，由于 IC 时间转化问题，日期字段会显示不正确的值。这些差异源于虚拟机环境与系统对时间的解读之间的时区差异（UTC 与本地时间）。（FORMS-17988）（FORMS-17248）

* 当用户在 AEM Forms 中使用 Notice IC 模板预览书信时，PDF 生成时间差异较大，即使在同一服务器上，生成时间也可能从 1.5 秒到 10 秒以上不等。这种不一致性会影响业务重要工作流。（FORMS-17951）

* 当用户在自适应表单中使用“数据源”选项将手写签名对象绑定到 XDP 时，更改无法保存。其原因在于持续存在纵横比验证错误，即使输入的值有效也是如此。（FORMS-17587）

* 当用户在文档片段中使用包含大量隐藏字段的特定 XDP 时，AEM 会创建将 `cm:optional` 属性设置为假的 CRX 节点，导致交互式通信 (IC) 提交失败。（FORMS-17538）

* 在 AEM Forms 6.5.19.0 中，当客户预览书信时，数字框字段在定义 Lead 和 Frac 位数限制的情况下无法正确处理负值。该问题是由于使用了 parseFloat 方法，它会将减号视为数字的一部分。（FORMS-17451）

* 在 AEM Forms 6.5 中，当用户预览书信时，Adobe.json 文件中使用了 “*” 通配符，这引发了对其用途及是否需要修改的担忧。（FORMS-17317）

* 当用户在 `Apply for a Fixed Rate Saver joint account` 上使用屏幕阅读器时，标题会被错误地播报为“`clickable`”，从而引发无障碍问题。（FORMS-17038）

* 当嵌入表单时，生成的 iframe 缺少标题属性，导致不符合无障碍合规要求。（FORMS-17010）

* 通过表单管理器 UI 下载表单时，总是包含相关依赖项，例如主题和片段。（FORMS-15811）

* 当用户在移动设备（iOS 和 Android™）上访问表单时，第一页上的“下一步”和“上一步”按钮处于禁用状态。然而，屏幕阅读器并未将其识别为禁用状态。（FORMS-15773）

* 当用户保存包含片段并启用了延迟加载的大型表单时，无法成功检索草稿，导致工作流中断。（FORMS-19890、FORMS-19808）

#### Forms JEE

* 当用户在 AEM Forms 中重新配置数据库时，由于存在硬编码参数，连接会失败。（FORMS-19568、FORMS-17621）

* 当用户通过部分即装即用方法在 AEM 6.5 中配置 MySQL 8.4 时，LiveCycle 配置管理器（LCM）无法识别所需的 MySQL 连接器驱动。这会导致数据库连接测试和设置失败。（FORMS-19442）

* 在 JEE 环境中，当用户在 JRE 11 上使用 JDBC 12.8.1 运行 LCM 时，因兼容性问题导致安装失败。（FORMS-19276）

* 在 AEM 内部部署中，当用户打开一个任务时，系统会执行 Workspace 启动操作轮廓，而不是 AssignedUserProfile。（FORMS-19065）

* 当用户在 AEM JEE 流程管理器中使用 retryAction（long actionOid）方法时，会出现非预期行为。（FORMS-18357）（FORMS-18187）

* 在 AEM Forms 6.5.21.0 中，PDFG 转化失败，并出现以下错误：（FORMS-16851）（FORMS-14613）

#### 表单验证码 {#forms-captcha-6523}

* 通过将提交错误代码更新为 400，在自适应表单中改进了 reCAPTCHA 警报机制：此外，优化了日志警报功能，以区分超时、过期和机器人检测失败，从而提升故障排查的准确性和系统的可观测性。（FORMS-19240）
* 修复了 `ReCaptchaConfigurationServiceImpl` 中未关闭的 `ResourceResolver` 实例，以防止潜在的资源泄漏，并在使用 AEM Forms 内的 reCAPTCHA 集成时提升系统稳定性。（FORMS-19242）
* 改进了 AEM Forms 的 CAPTCHA 配置处理逻辑，确保当 `/conf/global` 文件夹中存在多个配置项时，每个表单均能绑定到正确的配置。此项修复避免了在未明确选择配置容器时，意外使用不正确的 CAPTCHA 设置的问题。（FORMS-19239）

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

* 修复了 Coral 警报横幅的问题：在升级至服务包 21 后，文本颜色显示为白色而非黑色。该项修复可确保应用正确的样式，以维持警报消息在界面中的对比度和可读性。（NPR-42359）
* 在智能标记配置中新增对 OAuth 集成的支持，以配合 JWT（JSON Web 令牌）的弃用。此项改进可确保智能标记功能在采用更新后的身份验证方式后仍可正常运行。（NPR-42296）

#### Apache Felix {#foundation-apachefelix-6523}

修复了在 CRX 中将私钥文件上传到二进制类型属性字段时出现的 NullPointerException 问题，恢复了自服务包 16 起提供的兼容性。该项修复可确保 AEM Managed Services 中的密钥文件上传工作流能够安全执行，而不会引发服务器错误或中断证书续订流程。（CQ-4359178）


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

* 解决了 Apache Sling 脚本服务之间的 OSGi 依赖循环问题，该问题在升级至服务包 21 后会导致 HTML 页面加载延迟或失败。通过更新内部服务引用，消除了涉及 `SightlyScriptingEngineFactory` 及相关组件的循环依赖，从而提升了脚本引擎的可靠性和启动行为。（GRANITE-56808）
* 更新后的 JS 使用 Apache Sling 中的脚本，使其仅按需加载，而非在启动时提前加载，从而消除了线程争用问题，降低了发布服务器在高负载下无响应的风险。此次更改通过防止脚本因过早解析而导致的资源锁定问题，提高了高流量场景下的服务器稳定性和响应速度。（GRANITE-56611）
* 修复了在 AEM 全方位搜索中输入字段占位符错误显示为标签的问题，该问题会引起视觉混淆。该项修复确保占位符在筛选字段中正确渲染，从而保持一致且无障碍的表单体验。（GRANITE-51791）
* 解决了在内容片段模型编辑器中选择超过 30 个带多字段引用的内容片段模型（Content Fragment Model，简称 “CFM”）时触发的服务器错误。增强了筛选建议组件以支持 POST 操作。此功能能够在内容片段创建过程中妥善处理大型引用集，并改善高容量模型配置下的稳定性。（GRANITE-57164）
* 修复了内容片段模型中的一个问题：在复选框附近点击时，会意外切换其状态。更新后的样式会将点击激活功能严格限制在复选框元素本身，以防止用户意外操作，从而提升表单的可用性和无障碍性。（GRANITE-52384）


<!--
#### Integrations{#foundation-integrations-6523}

* A () -->


#### Jetty{#foundation-jetty-6523}

修复了一个问题：在 AEM 客户使用带自定义主机标头的 Dispatcher SSL 配置时，SNI 验证阻止了通过 HTTPS 的 API 调用。此次更新在 Jetty 配置中引入了一个选项，可禁用 SNI 验证，从而兼容某些无法使用 `mod_proxy` 的反向代理设置。（NPR-42614）


<!--
#### Localization{#foundation-localization-6523}

* A () -->

<!--
#### Oak {#foundation-oak-6523}

* A () -->


#### 平台{#foundation-platform-6523}

* 修复了标记合并行为不一致的问题，确保无论标记是内联创建还是通过标准标记创建方式生成的，合并后的标记值都能在资产中正确显示。此修复可防止 `EN:title` 字段中的残留值覆盖合并后的标记的显示。（CQ-4358812）
* 修复了在标记编辑对话框内标记值中 &amp; 字符被重复编码的问题。该修复避免在每次保存时附加额外的 “&amp;” 实体，确保标记值在多次编辑后保持简洁一致，并防止在创作内容中出现显示方面的错误。（CQ-4359048）
* 修复了在 WebSphere® 环境下运行 AEM 6.5 时，提交自适应表单后阻止发送电子邮件的 `ClassCastException` 错误。此修复通过确保 `com.sun.mail.handlers.text_plain` 与 `java.activation.DataContentHandler` 之间的兼容性，满足 WebSphere® 环境所需的邮件处理程序配置，从而支持电子邮件的成功传输。（NPR-42500）
* 改进了包管理器的错误处理机制：当安装失败且错误响应为空时，AEM 现在会显示明确的错误信息。该修复可防止出现静默失败的情况，并加快了包部署过程中的调试。（NPR-42375）

<!--
#### Security{#foundation-security-6523}

* A -->

<!--
#### Sling{#foundation-sling-6523}

* A () -->


#### 翻译{#foundation-translation-6523}

修复了在使用&#x200B;**更新语言副本**&#x200B;的工作流中更新内容片段时触发的 NullPointerException（NPE）问题。此修复确保在编辑与翻译引用相关的内容时，工作流不会进入失败状态或卡在运行状态。（NPR-42115）

#### 用户界面{#foundation-ui-6523}

为 Coral UI 对话框中的按钮（如&#x200B;**完成**&#x200B;和&#x200B;**取消**）补充了缺失的 `title` 属性，以提升无障碍性并支持自动化验证。该修复确保按钮在标记渲染过程中保持预期属性，避免基于 Selenium 的 UI 测试失败。（NPR-42412）

#### WCM{#foundation-wcm-6523}

修复了在服务包 19 或更高版本环境中使用&#x200B;**更新语言副本**&#x200B;时，页面无法添加到翻译任务中的问题。该修复确保翻译工作流能够按预期执行，实现语言副本之间的页面正确传输，而无需人工干预。（CQ-4357929）

#### 工作流{#foundation-workflow-6523}

修复了 `EmailNotificationServiceProcessor` 中的一个问题：在热修复部署后，`getSegmentId` 方法返回 `null`，导致工作流处理过程中电子邮件触发失败。该修复通过确保处理器能够正确检索所需的 `SegmentInfo` 值，恢复了正确的区段 ID 解析逻辑，从而支持 AEM 实例中的电子邮件通知工作流。（CQ-4359755）


## 安装 [!DNL Experience Manager] 6.5.23.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.23.0 需要依赖 [!DNL Experience Manager] 6.5。详细说明请参阅[升级文档](/help/sites-deploying/upgrade.md)。<!-- UPDATE FOR EACH NEW RELEASE -->
* 服务包可通过 Adobe [软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip)下载。
* 在使用 MongoDB 且包含多个实例的部署中，请在其中一个作者实例上使用包管理器安装 [!DNL Experience Manager] 6.5.23.0。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe 不建议移除或卸载 [!DNL Experience Manager] 6.5.23.0 包。因此，在安装该包之前，您应创建 `crx-repository` 的备份，以便在需要时进行回滚。<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### 在 [!DNL Experience Manager] 6.5 上安装服务包{#install-service-pack}

1. 如果实例处于更新模式（即由早期版本升级而来），请在安装前先重启该实例。如果实例已长时间运行，Adobe 建议先重启。

1. 在安装之前，请为您的 [!DNL Experience Manager] 实例创建快照或执行一次全新的备份。

1. 从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip)下载服务包。<!-- UPDATE FOR EACH NEW RELEASE -->

1. 打开包管理器，然后选择&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传该包。如需了解更多信息，请参阅[包管理器](/help/sites-administering/package-manager.md)。

1. 选择该包，然后选择&#x200B;**[!UICONTROL 安装]**。

1. 要更新 S3 连接器，请在安装服务包后停止实例，用安装文件夹中提供的新二进制文件替换现有连接器，然后重新启动实例。请参阅 [Amazon S3 数据存储](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>在安装服务包过程中，包管理器 UI 中的对话框有时会意外退出。Adobe 建议您在访问部署之前，先等待错误日志趋于稳定。在确认安装成功之前，请先等待与卸载更新捆绑包相关的特定日志出现。通常，该问题会在 [!DNL Safari] 浏览器中出现，但也可能会在其他浏览器中间歇出现。

**自动安装**

您可以使用以下两种方法来安装 [!DNL Experience Manager] 6.5.23.0。<!-- UPDATE FOR EACH NEW RELEASE -->

* 当服务器在线时，将包放入 `../crx-quickstart/install` 文件夹中。该包会自动安装。
* 使用[包管理器的 HTTP API](/help/sites-administering/package-manager.md#package-share)。请使用 `cmd=install&recursive=true` 以便安装嵌套的包。

>[!NOTE]
>
>Experience Manager 6.5.23.0 不支持 Bootstrap 安装。<!-- UPDATE FOR EACH NEW RELEASE -->

**验证安装**

要了解与此版本兼容的已经过认证的平台，请参阅[技术要求](/help/sites-deploying/technical-requirements.md)。

1. 在[!UICONTROL 已安装的产品]下，产品信息页面（`/system/console/productinfo`）会显示更新后的版本字符串 `Adobe Experience Manager (6.5.23.0)`。<!-- UPDATE FOR EACH NEW RELEASE -->

1. 在 OSGi 控制台中，所有 OSGi 捆绑包均应处于&#x200B;**[!UICONTROL 活跃]**&#x200B;或&#x200B;**[!UICONTROL 片段]**&#x200B;状态（使用网页控制台：`/system/console/bundles`）。

1. OSGi 捆绑包 `org.apache.jackrabbit.oak-core` 的版本应为 1.22.20 或更高版本（使用网页控制台：`/system/console/bundles`）。<!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### 安装 [!DNL Experience Manager] Forms 的服务包{#install-aem-forms-add-on-package}

如需了解在 Experience Manager Forms 上安装服务包的操作说明，请参阅 [Experience Manager Forms 服务包安装说明](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)。

>[!NOTE]
>
>在 [AEM 6.5 快速入门](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/implementing/deploying/deploying/deploy)中谈及的自适应表单功能旨在仅作探索和评估用途。由于自适应表单功能需要适当的许可，因此必须获得 AEM Forms 的有效许可证才能作生产用途。

### 为 Experience Manager 内容片段安装 GraphQL 索引包{#install-aem-graphql-index-add-on-package}

使用 GraphQL 的客户必须安装[带有 GraphQL 索引包 1.1.1 的 Experience Manager 内容片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip)。

这样做可根据实际使用的功能添加所需的索引定义。

如果未安装该包，可能会导致 GraphQL 查询变慢或失败。

>[!NOTE]
>
>每个实例只需安装一次该包；无需在每次安装服务包时重新安装。

### UberJar{#uber-jar}

适用于 [!DNL Experience Manager] 6.5.23.0 的 UberJar 可在 [Maven Central 存储库](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.22/)获取。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

要在 Maven 项目中使用 UberJar，请参阅[如何使用 UberJar](/help/sites-developing/ht-projects-maven.md)，并在项目 POM 中包含以下依赖项：<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

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
>UberJar 和其他相关工件现已发布在 Maven Central 存储库，而非 Adobe 公共 Maven 存储库（`repo.adobe.com`）。主 UberJar 文件已重命名为 `uber-jar-<version>.jar`。因此，在 `dependency` 标记中不再包含以 `apis` 为值的 `classifier`。



## 已弃用和已移除的功能{#removed-deprecated-features}

请参阅[已弃用和已移除的功能](/help/release-notes/deprecated-removed-features.md/)，以获取 AEM 6.5 中所有已弃用或已移除功能的详细列表。

### SPA 编辑器 {#spa-editor}

从 AEM 6.5.23 版本开始，[SPA 编辑器](/help/sites-developing/spa-overview.md)已在新项目中弃用。对于现有项目，SPA 编辑器仍受支持，但不建议在新项目中使用。

现在管理 AEM 中的 Headless 内容时首选以下编辑器：

* [Universal Editor ](/help/sites-developing/universal-editor/introduction.md)，用于可视化编辑。
* [内容片段编辑器](/help/sites-developing/universal-editor/introduction.md)，用于以基于表单的方法编辑。

## 已知问题{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* **AEM 6.5.21-6.5.23 和 AEM 6.5 LTS GA 中的 JSP 脚本包问题**
AEM 6.5.21、6.5.22、6.5.23 和 AEM 6.5 LTS GA 随附的 `org.apache.sling.scripting.jsp:2.6.0` 捆绑包存在已知问题。此问题经常在 AEM 实例处理许多并发请求而导致高负载的情况下发生。

  当出现此问题时，错误日志中可能会出现以下异常之一，并会引用 `org.apache.sling.scripting.jsp:2.6.0`：

   * `java.io.IOException: classFile.delete() failed`
   * `java.io.IOException: tmpFile.renameTo(classFile) failed`
   * `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
   * `java.io.FileNotFoundException`

  出现该错误后，唯一的恢复方法是重启 AEM 实例。

  请联系 Adobe 客户支持，并引用本发行说明以获取解决方案。

* **与 Oak 相关**
自服务包 13 起及更高版本中，开始出现以下错误日志，从而影响持久化缓存：

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

   1. 从 `crx-quickstart/repository/` 中删除以下两个文件夹

      * `cache`
      * `diff-cache`

   1. 安装服务包，或重新启动 Experience Manager as a Cloud Service。
新的 `cache` 和 `diff-cache` 文件夹会自动创建，并且不会再在 `error.log` 中遇到与 `mvstore` 相关的异常。

* 请将可能使用了自定义 API 名称的 GraphQL 查询更新为使用内容模型的默认名称。

* GraphQL 查询可能会使用 `damAssetLucene` 索引，而不是 `fragments` 索引。此操作可能导致 GraphQL 查询失败或运行时间过长。

  要解决该问题，必须在 `/indexRules/dam:Asset/properties` 下配置 `damAssetLucene`，以添加以下两个属性：

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

  在修改索引定义后，需要重新索引（`reindex` = `true`）。

  完成以上步骤后，GraphQL 查询的性能应会提升。

* 在尝试移动、删除或发布内容片段、网站或页面时，获取内容片段引用时会出现问题。后台查询失败。也就是说，该功能无法正常工作。
为确保该功能正常运行，必须将以下属性添加到索引定义节点 `/oak:index/damAssetLucene`（无需重新索引）：

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* 如果您在 Java™ 11 上将 [!DNL Experience Manager] 实例从 6.5.0 – 6.5.4 升级到最新的服务包，可能会在 `error.log` 文件中看到 `RRD4JReporter` 异常。要停止这些异常，请重新启动 [!DNL Experience Manager] 实例。<!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 用户可以在 [!DNL Assets] 的层级中重命名文件夹，并将嵌套文件夹发布到 [!DNL Brand Portal]。但是，在 [!DNL Brand Portal] 中，文件夹标题不会更新，直到重新发布根文件夹。

* 在安装 [!DNL Experience Manager] 6.5.x.x 期间，可能会显示以下错误和警告消息：
   * 当在 [!DNL Experience Manager] 中使用 Target Standard API（IMS 身份验证）配置 Adobe Target 集成时，将体验片段导出到 Target 会导致创建错误的产品建议类型。在 Target 中，系统不会创建类型为“Experience Fragment”/来源为“Adobe Experience Manager”的产品建议，而是会创建多个类型为“HTML”/来源为“Adobe Target Classic”的产品建议。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：未在 `granite/operations/maintenance` 找到维护窗口。
   * 当在自适应表单中使用 SUM、MAX 和 MIN 等聚合函数时，服务器端验证失败（CQ-4274424）。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：未在 `granite/operations/maintenance` 找到维护窗口。
   * 通过 Shoppable Banner 查看器预览资产时，Dynamic Media 交互式图像中的热点不可见。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]`：等待完成取消注册的注册变更时超时。

* 从 AEM 6.5.15 开始，由 ```org.apache.servicemix.bundles.rhino``` 捆绑包提供的 Rhino JavaScript 引擎引入了新的提升行为。使用严格模式（```use strict;```）的脚本必须声明正确的变量。否则脚本将无法运行，并会抛出运行时错误。

* 通过官方更新包安装与标记相关的开箱即用内容时，`/content/cq:tags` 节点的语言属性会被重置为默认值。此操作适用于服务包、安全服务包、扩展功能包、累积功能包、补丁等。因此，在安装之前必须从属性中手动添加该项。

### AEM Sites 已知问题 {#known-issues-aem-sites-6523}

内容片段预览在处理大型片段树时因 DoS 防护而失败。请参阅[关于默认 GraphQL 查询执行器配置选项的知识库文章](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-kcs/kbarticles/ka-23945)（SITES-17934）

### AEM Forms 已知问题 {#known-issues-aem-forms-6523}

>[!NOTE]
>
> 对于尚未发布热修复补丁的问题，请勿升级至服务包 6.5.23.0，否则可能导致意外错误。仅在所需的热修复补丁发布后再升级至服务包 6.5.23.0。

#### 可通过热修复补丁解决的问题 {#aem-forms-issues-with-hotfixes}

以下问题已提供可下载并安装的热修复补丁：您可以通过[下载并安装热修复补丁](/help/release-notes/aem-forms-hotfix.md)来解决这些问题：

* **FORMS-20203**：当用户将 Struts 框架从 2.5.x 版本升级到 6.x 版本时，AEM Forms 中的策略 UI 无法显示所有配置，例如添加水印的选项。

* **FORMS-20360**：升级到 AEM Forms 服务包 6.5.23.0 后，ImageToPDF 转化服务失败并报错。
  ```17:15:44,468 ERROR [com.adobe.pdfg.GeneratePDFImpl] (default task-49) ALC-PDG-001-000-ALC-PDG-011-028-Error occurred while converting the input image file to PDF. com/adobe/internal/pdftoolkit/core/encryption/EncryptionImp```

* **FORMS-20478**：尝试将 7/8 类型的 TIFF 文件转化为 PDF 时，转化流程失败并出现以下错误：“ALC-PDG-001-000-Image2Pdf 转化失败，原因：com/sun/image/codec/jpeg/JPEGCodec” 以及 “ALC-PDG-016-003-在 PDF 后处理过程中发生了未知/意外错误”。系统会尝试使用 TM ImageIO TIFF 解码器重试，但最终仍无法完成任务。

* **FORMS-14521**：如果用户尝试使用已保存的 XML 数据预览草稿信件，某些特定信件会卡在 `Loading` 状态。

* AEM Forms 现已将表单组件中的 Struts 版本从 2.5.33 升级至 6.x。此次升级补充了 SP23 中未包含的 Struts 更新。相关支持已通过[热修复补丁](/help/release-notes/aem-forms-hotfix.md)提供，您可以下载并安装该热修复补丁，以支持 Struts 的最新版本。

#### 其他已知问题 {#aem-forms-other-known-issues}

* 在安装 AEM Forms JEE 服务包 21（6.5.21.0）后，如果您在 `<AEM_Forms_Installation>/lib/caching/lib` 文件夹下发现 Geode jar 的重复条目 `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)`（FORMS-14926），请执行以下步骤以解决该问题：

   1. 如果定位器正在运行，请先停止定位器。
   2. 停止 AEM 服务器。
   3. 进入 `<AEM_Forms_Installation>/lib/caching/lib`。
   4. 移除所有 Geode 补丁文件，仅保留 `geode-*-1.15.1.2.jar`。确认仅存在 `version 1.15.1.2` 的 Geode jar。
   5. 以管理员模式打开命令提示符。
   6. 使用 `geode-*-1.15.1.2.jar` 文件安装 Geode 补丁。

* 当用户从 AEM 6.5 Forms 服务包 18 或 19 升级到服务包 20 或 21 时，会遇到 JSP 编译错误。该错误会导致无法打开或创建自适应表单。它也会影响其他 AEM 界面。这些界面包括页面编辑器、AEM Forms UI、工作流编辑器和系统概览 UI。（FORMS-15256）

  如果遇到此类问题，请执行以下步骤进行解决：
   1. 进入 CRXDE 中的目录 `/libs/fd/aemforms/install/`。
   2. 删除名为 `com.adobe.granite.ui.commons-5.10.26.jar` 的捆绑包。
   3. 重新启动 AEM 服务器。

* 在交互式通信代理 UI 的打印预览中，货币符号（如美元符号 $）在各字段值中的显示不一致。对于不超过 999 的数值会显示符号，但对于 1000 及以上的数值则缺少符号。（FORMS-16557）
* 在交互式通信中，对嵌套布局片段的 XDP 所做的任何修改都不会反映在 IC 编辑器中。（FORMS-16575）
* 在交互式通信代理 UI 的打印预览中，部分计算值未正确显示。（FORMS-16603）
* 在“打印预览”中查看信件时，内容发生变化。具体表现为：部分空格消失，某些字母被替换为 `x`。（FORMS-15681）
* **FORMS-15428**：更新至带有 Forms 附加组件的 AEM Forms 服务包 20（6.5.20.0）后，依赖基于凭据的身份验证的旧版 Adobe Analytics Cloud 服务的配置将停止工作。此问题会导致分析规则无法正确执行。

* 当用户配置 WebLogic 14c 实例时，在 JBoss® 上运行的 JEE 环境中的 AEM Forms 服务包 21（6.5.21.0）内，PDFG 服务因涉及 SLF4J 库的类加载器出现冲突而失败。错误显示如下（CQDOC-22178）：

  ```java
  Caused by: java.lang.LinkageError: loader constraint violation: when resolving method "org.slf4j.impl.StaticLoggerBinder.getLoggerFactory()Lorg/slf4j/ILoggerFactory;"
  the class loader org.ungoverned.moduleloader.ModuleClassLoader @404a2f79 (instance of org.ungoverned.moduleloader.ModuleClassLoader, child of 'deployment.adobe-livecycle-jboss.ear'
  @7e313f80 org.jboss.modules.ModuleClassLoader) of the current class, org/slf4j/LoggerFactory, and the class loader 'org.slf4j.impl@1.1.0.Final-redhat-00001' @506ab52
  (instance of org.jboss.modules.ModuleClassLoader, child of 'app' jdk.internal.loader.ClassLoaders$AppClassLoader) for the method's defining class, org/slf4j/impl/StaticLoggerBinder,
  have different Class objects for the type org/slf4j/ILoggerFactory used in the signature.
  ```

* Forms-21378：启用服务器端验证（SSV）时，表单提交可能失败。如果遇到此问题，请联系 Adobe 支持部门寻求帮助。



## 包含的 OSGi 捆绑包和内容包{#osgi-bundles-and-content-packages-included}

以下文本文档列出了此 [!DNL Experience Manager] 6.5 服务包版本中包含的 OSGi 捆绑包和内容包：

* [Experience Manager 6.5.23.0](/help/release-notes/assets/65230-bundles.txt) 中包含的 OSGi 捆绑包列表 <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.23.0](/help/release-notes/assets/65230-packages.txt) 中包含的内容包列表 <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限网站{#restricted-sites}

这些网站仅对客户开放。如果您已是客户并需要访问权限，请联系您的 Adobe 客户经理。

* [在 licensing.adobe.com 下载产品](https://licensing.adobe.com/)
* [联系 Adobe 客户支持部门](https://experienceleague.adobe.com/zh-hans/docs/customer-one/using/home)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 产品页面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 文档](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65)
>* [订阅 Adobe 产品更新早知道](https://www.adobe.com/cn/subscription/priority-product-update.html)
