---
title: ' [!DNL Adobe Experience Manager] 6.5 发行说明'
description: 查找 [!DNL Adobe Experience Manager] 6.5 的版本信息、新增功能、安装操作方法和详细更改列表。
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: cc10229ca767a803fe0b24b1b4b47111e6c88cdd
workflow-type: tm+mt
source-wordcount: '7111'
ht-degree: 24%

---

# [!DNL Adobe Experience Manager]6.5 最新服务包发行说明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!--
DO NOT DELETE THIS HIDDEN NOTE!      DO NOT DELETE THIS HIDDEN NOTE!
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section.
-->

## 发行版信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.25.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 类型 | 服务包发行 |
| 日期 | 2026年5月21日<!-- UPDATE FOR EACH NEW RELEASE --> |
| 下载 URL | [软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

<!--
OLD DOWNLOAD URL
(https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip)
-->

## [!DNL Experience Manager] 6.5.25.0 的内容 {#what-is-included-in-aem-6525}

[!DNL Experience Manager] 6.5.25.0 包含新功能、客户重点要求的增强功能以及错误修复。 还包括自 2019 年 4 月 6.5 首次发布以来推出的在性能、稳定性和安全性方面的改进。 [在 [!DNL Experience Manager] 6.5 上安装此服务包](#install)。

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- ## Key features and enhancements -->


## 修复了Service Pack 25中的问题 {#fixed-issues}

<!-- 6.5.25.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->


### [!DNL Sites]{#sites-6525}

#### 辅助功能 {#sites-accessibility-6525}

* 现在，“站点”列表视图中的表格行拖放控件可用于键盘导航。 屏幕阅读器和键盘用户可以在操作期间重新排序行并接收反馈。 (SITES-24946)

* 现在，编辑布局工具栏以有意义的屏幕阅读器序列显示较小的屏幕标签和平板电脑标签。 用户用相关的标尺度量听到标签，而不是听见它们乱序。 (SITES-25291)
* 现在，当从注释模式打开样本弹出窗口模式时，可以正确管理焦点。 焦点从模式标题开始，而不是直接移动到选定的样本按钮。 (SITES-25275)
* Teaser模式现在提供了一种使用键盘移动对话框的可访问方式。 用户不再需要鼠标在页面上重新定位该模式窗口。 (SITES-25226)
* 卡片视图通过删除不必要的ARIA网格行为而提高了可访问性。 屏幕阅读器用户会收到更清晰的卡信息，并且不会收到与可视布局不匹配的网格导航控件。 (SITES-24933)
* 现在，重复悬停操作后，删除模式中的工具提示会一致显示。 用户可以移开指针并返回到图标以再次阅读工具提示。 (SITES-24778)
* 现在，用户从站点主页打开左边栏后，该边栏会按预期顺序获得焦点。 键盘和屏幕阅读器用户可以从配置按钮移动到边栏内容，而无需跳过扩展区域。 (SITES-24754)
* 现在，焦点管理在轮播模式对话框中可始终如一地工作。 键盘和屏幕阅读器用户可以从模式标题开始，并在关闭对话框后返回到原始控件。 (SITES-24716)
* 现在，链接选择对话框将焦点返回到用户关闭对话框后打开该对话框的控件。 关闭对话框后，键盘和屏幕阅读器用户不再丢失其位置。 (SITES-24707)
* 当作者打开或关闭对话框时，“图像”模式不再将焦点移动到第一个选项卡或主页面里程碑。 焦点首先移动到对话框标题，然后返回到打开对话框的控件。 (SITES-24693)
* 现在，当模式对话框打开时，引用边栏可正确管理焦点。 键盘和屏幕阅读器用户将保留在对话框中，直到他们关闭该对话框，然后继续导航而不会丢失上下文。 (SITES-24683)
* 当作者打开或关闭超链接路径选择模式时，该模式不再将焦点移动到错误的字段或控件。 焦点从模式标题开始，并返回到打开该模式的按钮。 (SITES-24672)
* 当作者打开或关闭页面时，Teaser模式不再将焦点移动到该页面的第一个选项卡或顶部。 现在，焦点遵循预期的对话框流程，并减少不必要的屏幕阅读器公告。 (SITES-24522)

* 页面编辑器锁定按钮现在可提供更精确的屏幕阅读器反馈。 屏幕阅读器会使用标题属性（可用时），从而减少使用辅助技术的作者的详细公告。 (SITES-41431)
* 键盘导航现在会跳过隐藏的内容。 用户可以浏览可见的界面元素，而无需将焦点移动到他们无法看到的内容。 (SITES-41430)
* 现在，用户关闭叠加后，键盘焦点会返回到触发元素。 页面编辑器不再将焦点发送回叠加，这会改进键盘用户的导航。 (SITES-40819)
* 现在，当用户使用键盘导航工具栏项目时，页面编辑器工具栏会显示标签，例如工具提示。 当焦点从一个项目移动到另一个项目时，用户可以了解每个工具栏操作。 (SITES-40751)
* 将鼠标悬停在组件浏览器项目上时，不再从活动的文本组件中删除焦点。 作者可以编辑文本而不会中断，键盘焦点始终可预测。 (SITES-35370)
* 屏幕阅读器现在可以更清楚地宣布搜索模式排序方向按钮。 按钮标签不再重复相同的方向，它更好地描述了切换行为。 (SITES-25534)
* 现在，搜索模式会在“更改文件或文件夹”列表框中显示选定选项的可视指示器。 用户可以识别当前的痕迹导航选项，而无需仅依赖焦点。 (SITES-25532)
* 搜索模式现在提高了排序依据标签的对比度。 该文本符合辅助功能要求，并提高了视力缺佳用户的可读性。 (SITES-25531)
* 设备选择按钮现在会在“编辑布局”工具栏中显示正确的当前状态信息。 屏幕阅读器用户可以识别活动设备，而不会听到误导性的切换状态。 (SITES-25524)
* 现在，当焦点离开收件箱菜单时，键盘和屏幕阅读器导航会关闭该菜单。 用户可避免出现当焦点移动到其他位置时菜单保持打开状态的混乱状态。 (SITES-25518)
* 现在，当焦点离开帮助菜单时，键盘和屏幕阅读器导航会关闭该菜单。 当菜单保持打开状态时，焦点不再移动到菜单之外的内容。 (SITES-25517)
* 内容片段主页现在为侧栏选项卡提供可访问的一致标签。 当用户导航选项卡控件时，NVDA会正确公告选项卡标签。 (SITES-25509)
* “页面信息”菜单中的重点选项现在符合最低对比度要求。 改进的对比度可帮助视力缺佳的用户识别活动菜单项。 (SITES-25321)
* 键盘导航现在会跳过折叠的人口统计工具栏中的隐藏控件。 焦点位于可见的交互式元素上，这改进了布局预览中的导航顺序。 (SITES-25304)
* 现在，旋转设备按钮在编辑布局工具栏中提供更清晰的屏幕阅读器反馈。 屏幕阅读器会朗读当前方向以及对其进行更改的操作。 (SITES-25292)
* 编辑布局工具栏现在为桌面按钮显示一个清除选定状态。 Desktop选项与其他设备按钮匹配，使活动视图更容易识别。 (SITES-25290)
* 现在，编辑布局工具栏将为标尺区域添加标签，以供使用辅助技术。 屏幕阅读器用户在版面编辑期间不再遇到未标记的测量值。 (SITES-25287)
* 编辑布局工具栏现在以未勾选状态显示完整的iPhone 8 Plus按钮标签。 当按钮周围有足够的空间时，标签不再截断。 (SITES-25284)
* 所报告的问题描述了“编辑布局”工具栏中的焦点指示器，该指示器似乎涵盖了多个设备控件。 当焦点大纲包含相邻按钮时，键盘用户可能会失去对活动控件的跟踪，这引起了人们的关注。 该问题按计划运行。 (SITES-25283)
* 所报告的问题描述了在每个按钮标签之前声明注释的注释模式按钮。 人们关注的是不清晰的屏幕阅读器输出，用于诸如注释、色板和删除等操作。 (SITES-25277)
* 注释按钮文本现在在注释模式中使用足够的对比度。 此更新提高了视力缺佳用户的可读性，并支持WCAG对比度要求。 (SITES-25267)
* 现在，当用户筛选插入新组件列表时，屏幕阅读器会收到状态更新。 该模式会公告结果更改，以便用户了解列表在他们键入时发生了更改。 (SITES-25251)
* 记录的问题描述了注释模态标题缺少标题语义。 关注焦点集中在屏幕阅读器导航和了解模态结构的能力上。 (SITES-25248)
* 页面编辑器侧边栏中的标题级别现在遵循更清晰的内容层次结构。 左边栏部分不再显示为辅助技术的主页标题。 (SITES-25222)
* 现在，Assets左边栏中的“编辑”按钮具有更大的触控目标。 具有移动性需求的用户可以更轻松地激活按钮，并避开附近的控制。 (SITES-25221)
* Assets左边栏现在用于标识何时使用“编辑”按钮打开新的浏览器选项卡。 用户可以预料到导航更改，而不是意外丢失上下文。 (SITES-25220)
* 现在，当用户应用增加的文本间距时，组件标题可正确显示。 侧边栏保留可读标签并支持WCAG文本间距要求。 (SITES-25219)
* 现在，侧边栏组件中的过滤器字段会显示一个可访问的正确名称。 此更新可帮助屏幕阅读器用户识别字段，而无需依赖占位符文本。 (SITES-25212)
* 所报告的问题描述了注释模式中的不逻辑焦点序列。 据报告，键盘用户缺少注释工具栏，除非他们在激活模式后使用Shift+Tab。 (SITES-24996)
* 编辑器画布公开其顶栏标题作为标题。 屏幕阅读器可以通过正确的结构朗读标题，这可以提高导航和页面理解能力。 (SITES-24993)
* 辅助功能报告指出，用户切换视图时显示的加载状态消息的对比度不足。 关注点集中在视力低下或色盲用户的可读性上。 (SITES-24991)
* 辅助功能报表注意到卡片链接包含非描述性文本。 重点在于帮助屏幕阅读器用户了解每个链接目标而无需额外的上下文。 (SITES-24975)
* 站点列表视图现在显示对比度更强的Live Copy文本。 这项更新提高了视力缺佳作者以及在明亮屏幕条件下工作的用户的可读性。 (SITES-24956)
* 现在，键盘导航可在用户展开模拟器菜单后将焦点移到该菜单中。 此行为可帮助屏幕阅读器和键盘用户按预期顺序访问菜单选项。 (SITES-24954)
* 站点列表视图现在提高了表格行中拖放按钮的可见性。 当作者对内容重新排序时，可以更轻松地识别控件。 (SITES-24951)
* 当图像链接和标题链接共享同一目标时，信息卡不再将它们公开为单独的链接。 该更新降低了屏幕阅读器的详细程度并提高了导航效率。 (SITES-24947)
* 标题菜单按钮现在使用更准确的辅助功能属性。 屏幕阅读器将按钮朗读为可扩展控件，而不是对话框打开控件。 (SITES-24742)
* 收件箱现在使用语义列表标记来标记相关链接。 屏幕阅读器用户可以更轻松地了解收件箱链接的数量和分组。 (SITES-24730)
* 标题按钮标签现在可避免使用冗长的易访问名称。 屏幕阅读器用户可获得更清晰的公告，图标文本中不重复角色信息。 (SITES-24715)
* CSV报表按钮现在可以更清楚地提供有关新选项卡行为的反馈。 用户可以了解选择按钮会在激活之前打开新的浏览器选项卡。 (SITES-24704)
* 模式对话框现在为标题控件使用更准确的辅助功能标记。 “帮助”和“切换全屏”按钮仍然是交互式控件，不再显示为屏幕阅读器的标题。 (SITES-24696)
* 过滤器边栏标志现在使用不同的标签来标识其用途。 屏幕阅读器用户可以更自信地导航具有多个相似地标的页面。 (SITES-24686)
* 引用边栏消息现在为依赖足够文本对比度的用户提供更好的可读性。 报告的问题涉及选择和多选消息，这些消息在背景中显得太浅。 (SITES-24666)
* 现在，搜索模式为“删除位置”和“关闭”按钮提供了更大的接触目标。 此更改可帮助手颤抖、痉挛或视力缺佳的用户激活预期的控制。 (SITES-24530)
* 报告了Adobe Experience Manager标题链接使用不正确的ARIA属性。 测试确认该链接控制可扩展内容，因此现有的访问状态仍然适用。 (SITES-24528)
* 在“组件”列表中，“署名”按钮的焦点指示器不再显示为截断。 可见的大纲可帮助键盘用户跟踪他们在编辑器中的位置。 (SITES-24503)
* 一个报告的问题描述了“组件”面板中信息工具提示图标缺少替换文本。 问题没有重现，但审查确认，信息图标必须公开一个清晰易用的名称。 (SITES-24500)
* 页面编辑器不再公开具有相同标签的多个区域标志。 现在，每个地标都有一个唯一的可访问名称，因此屏幕阅读器用户可以识别当前区域。 (SITES-24497)
* 更改文件或文件夹控件现在将控件标签与其状态信息分开。 屏幕阅读器用户在导航标题控件时听到名称更短、更清晰。 (SITES-24496)
* 内容片段管理员表中的交互式控件现在支持标准键盘导航。 键盘用户可以跳转到按钮和链接，而不是仅通过箭头键导航来发现它们。 (SITES-24285)
* 站点管理员UI现在为屏幕阅读器正确处理装饰性地球图标。 这些图标使用空的替换文本，因此用户只能听到有意义的界面内容。 (SITES-3057)

#### 管理用户界面{#sites-adminui-6525}

站点控制台现在正确显示保存的&#x200B;**列表视图**&#x200B;列设置。 当作者重新打开“设置”对话框时，选定的列保持选中状态，并且活动的列计数保持准确状态。 (SITES-38576)

#### 经典 UI{#sites-classicui-6525}

经典UI文本组件对话框现在将富文本编辑器(RTE)内容显示为格式化的文本，而不是原始HTML。 作者无需切换到Source模式或手动删除标记，即可编辑现有文本。 (SITES-38709)

#### 组件控制台{#sites-component-console-6525}

* 用户现在可以使用本地化或多字节字符搜索组件控制台。 控制台还会显示本地化的&#x200B;**Remove**&#x200B;标签，而不是未翻译的英文字符串。 (SITES-39747)
* “组件属性”页面现在将本地化工具>组件>组件属性中的字符串。 用户不再在本地化的创作界面中看到未翻译的英语标签。 (SITES-39745)

#### [!DNL Content Fragments]{#sites-contentfragments-6525}

现在，当用户选择或更改筛选器时，Assets Search会正确响应。 过滤的结果集将按预期更新，从而恢复Assets控制台中的可靠搜索细化。 (SITES-38686)

#### [!DNL Content Fragments] - 管理{#sites-admin-6525}

* Assets列表视图现在为锁定的内容片段显示本地化的由工具提示签出。 此修复可改进作者查看工作流行时的本地化一致性。 (SITES-42531)

* AEM现在在内容片段下载对话框中本地化主标签。 此修复使下载工作流在非英语区域设置中保持一致。 (SITES-42534)
* 现在，当作者从Assets计划内容片段发布时，AEM会翻译`Later`状态标签。 此修复可保持本地化界面中“已发布”列的一致性。 (SITES-42532)
* 现在，当作者在标题字段中输入无效字符时，内容片段创建会显示本地化的验证消息。 该对话框不再显示未本地化的“提供的名称无效”字符串。 (SITES-19796)
* 编辑内容片段页面现在为标记和收藏集使用本地化的标签。 作者会看到翻译后的字段名称，而不是未本地化的英文字符串。 (SITES-977)

#### [!DNL Content Fragments] - 片段编辑器{#sites-fragments-editor-6525}

* 现在，当作者从收藏集中删除内容时，内容片段编辑器中的关联内容会显示正确的本地化字符串。 该对话框不再将内容名称替换为未定义。 (SITES-33675)
* 内容片段编辑器现在为没有配置占位符的选项卡显示翻译的常规标签。 本地化的界面不再在该编辑器区域显示未翻译的英语字符串。 (SITES-30715)
* 内容片段编辑器中的内容引用选取器现在为允许的资产类型显示本地化标签。 本地化的界面不再为支持的资源类别显示英语类型的名称。 (SITES-29699)

#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6525}

* 当DAM文件名包含空格或非ASCII字符时，GraphQL JSON响应现在包括来自内容片段富文本字段的嵌入图像引用。 此修复可帮助应用程序渲染引用的图像，而无需作者重命名资产。 (SITES-42191)
* GraphQL对内容片段的响应现在可以更可靠地处理持久查询。 更新可纠正重复的缓存标头，改进编码的变量处理，并对缺少内容或失败的查询返回更清晰的响应。 (SITES-40159)
* GraphQL持久查询现在运行，日志中没有不必要的错误和警告消息。 AEM可正确处理编码的变量，因此成功的查询将不再产生误导性的`PersistedQueryServlet`条目。 (SITES-39354)

* “编辑GraphQL端点”对话框现在会本地化其界面字符串。 用户不会再看到从本地化界面中的配置消息中获取未翻译的GraphQL架构。 (SITES-34018)

#### [!DNL Content Fragments] - GraphQL 查询编辑器{#sites-graphql-query-editor-6525}

当选定的配置浏览器名称包含CJK或西里尔字母字符时，用户现在可以打开GraphQL查询编辑器。 编辑器显示端点的持久查询而不是显示错误。 (SITES-31616)

#### [!DNL Content Fragments] — 模型和模型编辑器{#sites-models-model-editor-6525}

* 现在，当选定的值需要有效的模型类型时，用户在内容片段模型编辑器中会看到本地化的验证消息。 编辑器不再在本地化界面中显示未翻译的英语消息。 (SITES-41117)
* 内容片段模型过滤器面板现在本地化其状态和标题字符串。 用户不再看到未翻译的标签，例如模型标题、状态、草稿、启用和禁用。 (SITES-30863)

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6525} -->

#### ContextHub{#sites-contexthub-6525}

ContextHub现在加载时不会出现JavaScript错误，从而中断个性化。 Teaser和其他个性化体验可以在受影响的页面上正确呈现。 (SITES-38430)

<!-- #### Core Backend{#sites-core-backend-6525} -->

#### 核心组件{#sites-core-components-6525}

* 当请求定位到缺少的DAM资源时，AEM不再生成重复的ThumbnailServlet错误。 Servlet在重定向后停止处理，这会阻止NullPointerException条目泛洪错误日志。 (SITES-41238)
* 在作者重新打开组件对话框时，AEM不再将可选对话框字段标记为必填。 该对话框使验证始终专注于实际需要输入的字段，从而防止出现误导性的选项卡级错误。 (SITES-40449)

* AEM包含多个支持的安全修复，可加强Sites和相关云服务组件。 这些修复减少了跨站点脚本风险，并跨受影响的创作路径改进了请求处理。 (SITES-38314)
* 图像v3组件配置对话框现在可在页面编辑器中本地化字符串。 作者在本地化界面中配置图像组件时，不会再看到未翻译的标签。 (SITES-38726)

<!-- #### Campaign integration{#sites-campaign-integration-6525} -->

<!-- #### ContentHub {#sites-contenthub-6525} -->

#### 人行横道 {#sites-crosswalk-6525}

* 安装后，交叉通路不再需要单独的软件包和配置设置。 AEM包括开箱即用包中的所需包、内容包、系统用户、服务用户映射和功能切换。 (SITES-41417)
* 现在，人行横道工作流可以使用AEM 6.5中所需的cq-wcm-core支持。 作者可以使用“创建模板”和“打开通用编辑器”操作，而无需进行单独的核心捆绑包更新。 (SITES-37666)

#### 体验片段{#sites-experiencefragments-6525}

现在，当作者创建体验片段变体并滚动浏览前40个结果时，AEM会加载正确的模板。 模板选取器在分页期间保留选定的体验片段路径。 (SITES-41531)

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6525} -->

#### 发布项{#sites-launches-6525}

* 站点时间线现在对AEM在提升启动项之前创建版本时显示的消息进行本地化。 用户不再在本地化界面中看到未翻译的英语字符串。 (SITES-39157)
* 对于没有模板或Live Copy继承而创建的启动项，启动项列表现在会显示正确的说明。 用户不再看到误导性的“已覆盖”模板标签。 (SITES-34229)

<!-- #### Link Checker{#sites-link-checker-6525} -->

#### 本地化{#sites-localization-6525}

* 体验片段中的文本组件属性现在使用本地化标签。 格式菜单不再显示段落、标题、引号或预设格式文本选项的非本地化字符串。 (SITES-15091)

* 模板状态文本现在在&#x200B;**工具** > **常规** > **模板**&#x200B;中正确对齐。 更新、启用和发布状态标签显示在一条水平线上。 (SITES-36797)
* “移动页面”对话框现在显示完整的“选择日期和时间”标签。 标签不再截断本地化界面，例如法语。 (SITES-36795)
* 模板编辑器中的Assets部分现在显示已翻译的标记标签。 在模板配置期间，本地化的创作界面呈现一致的标签。 (SITES-33770)
* 现在，页面策略描述可在模板编辑器中正确呈现。 用户可以阅读“样式”选项卡中的默认CSS类完整指南，而不会截断文本。 (SITES-29724)
* 现在，当作者尝试将组件拖动到已删除的模板上时，模板编辑器会显示一个本地化的错误。 消息不再显示为未翻译的“处理时”字符串。 (SITES-19313)
* Teaser配置窗口中的“Target”标签现在显示本地化文本。 “超链接”部分不再以非英语区域设置显示英语字符串。 (SITES-18622)
* 页面编辑器中的“启动工作流”对话框现在显示本地化的工作流操作标签。 作者不会再看到工作流选项（如批准、发布、请求和取消发布操作）的英文字符串。 (SITES-18103)
* 现在，“分隔符”编辑面板中的“父项”下拉菜单会显示本地化字符串，且不会截断。 作者可以在配置组件时查看完整标签。 (SITES-17480)
* 页面编辑器现在在容器组件样式菜单中显示“完整宽度”和“固定宽度”的本地化标签。 使用受支持的区域设置的作者不会再看到这些字符串的英文版本。 (SITES-17478)
* 现在，作者可以在“模板”控制台的导航属性区域中阅读完整的工具提示。 UI在模板编辑期间保持工具提示对齐并防止文本截断。 (SITES-15480)
* 现在，作者可以在“引用”侧面板中阅读完整的“Forms &amp; Documents Using Template”标签。 模板控制台不再为支持的区域设置切断字符串。 (SITES-13167)
* 引用视图现在为刷新错误消息使用本地化的文本。 当AEM无法更新引用列表时，作者会看到已翻译消息。 (SITES-13102)
* 表单验证现在标识包含无效时间值的字段。 时间扭曲模式会显示更清晰的错误消息，以便作者可以更正受影响的小时或分钟字段。 (SITES-10980)
* “模板”控制台现在在“选择图像”对话框中显示本地化的Assets标签。 当作者从模板属性中浏览资产时，标签正确显示。 (SITES-8113)

#### MSM - 实时副本{#sites-msm-live-copies-6525}

* Live Copy概述现在可以在“关系状态”视图中本地化日期格式。 L **Live Copy Source上次修改时间**、**Live Copy上次修改时间**&#x200B;和&#x200B;**上次转出时间**&#x200B;字段显示的日期与用户的区域设置相匹配。 (SITES-40756)
* MSM现在会记录修改时推送事件的更多详细信息。 添加的事件信息可帮助团队跟踪转出活动并确定意外页面更改的来源。 (SITES-38029)

#### 页面编辑器{#sites-pageeditor-6525}

* 现在，作者可以创建包含大写字母或空格的标记，并在保存第一个“页面属性”期间应用这些标记。 AEM会创建标记，并在相同的操作中将正确的值写入页面元数据。 (SITES-42550)

* 作者现在可以在名称包含撇号的DAM文件夹中创建内容片段。 AEM可正确处理编码的文件夹路径，并且在创建过程中不再触发NullPointerException。 (SITES-38653)

* AEM现在支持在页面编辑器中对配置的内容片段组件执行复制和粘贴操作。 组件会保留其内容片段引用，以便作者可以复制内容而无需手动重新创作。 (SITES-41586)
* 页面编辑器现在在组件对话框中正确显示第一字段描述工具提示。 较长的描述仍然可见，因此作者可以在工具提示顶部查看字段说明而不会丢失文本。 (SITES-39937)
* 现在，当作者通过HTTP使用AEM时，可以打开富文本编辑器链接对话框。 此修复程序可恢复对不使用HTTPS的内部部署环境的链接编辑。 (SITES-39467)

<!-- #### Replication{#sites-replication-6525} -->

<!-- #### Rich Text Editor{#sites-rte-6525} -->

#### 通用编辑器 {#sites-universal-editor-6525}

* 默认情况下，通用编辑器不再在预览模式下打开。 AEM将用户发送到生产通用编辑器环境，除非他们明确请求预览行为。 (SITES-37193)
* Universal Editor现在以预览模式打开，用于AEM开发、快速开发和暂存环境。 “打开”命令对非生产实例使用正确的预览行为。 (SITES-33839)

### [!DNL Assets] {#assets-6525}

* 我的共享客户端库现在可在将共享资产标题数据添加到页面标记之前安全地处理该数据。 生成的共享页面不再通过人工处理的资源元数据向用户显示脚本注入。 (ASSETS-60898)

* Adobe Stock授权现在可在Assets用户界面中正确运行。 AEM加载股票资产配置文件和权利数据后，“许可证”按钮不再保持禁用状态。 (ASSETS-62610)
* 现成可用的资产到期通知现在可以正确处理接近到期的日期。 当剩余时间达到配置的阈值时，会运行提醒电子邮件，而不是在八天过期后跳过资产。 (ASSETS-57857)

* AEM Assets现在可在用户选择保存的搜索后恢复键盘导航。 利用界面，用户无需刷新或重新启动Assets视图，即可从下拉列表中离开。 (ASSETS-52061)

* 现在，管理员视图下载工作流可正确保留ZIP文件名。 下载ZIP资源不再生成具有双重.zip扩展名的文件名。 (ASSETS-62207)
* Assets引用工作流现在可以正确处理文件名中的空格。 当所选文件名包含一个或多个空格时，相关资源更新不再失败。 (ASSETS-56418)

#### [!DNL Dynamic Media]{#assets-dm-6525}

现在，“字幕”和“音频轨道”下拉菜单将阿拉伯语显示为Dynamic Media支持的语言。 此更新允许用户添加阿拉伯语字幕轨道，而无需自定义变通办法。 (ASSETS-61771)

### [!DNL Forms]{#forms-6525}

>[!NOTE]
>
>[!DNL Experience Manager] Forms中的修补程序在计划的[!DNL Experience Manager] Service Pack发行日期后一周通过单独的附加组件包交付。 在本例中，此附加组件包计划于2026年5月28日星期四发布。 此外，此部分还添加了Forms修复和增强功能的列表。



<!-- ALL THE FORMS BUG FIXES LISTED BELOW GO WITH AEM 6.5.25 FORMS MAY 28 2026 RELEASE!! UNHIDE THEM!! -->




<!-- #### Forms Designer {#forms-designer-6525} -->

<!-- 
* The Output API now handles dynamic form content consistently when PDF generation uses client rendering. Generated PDFs retain scripted description text across affected sections instead of leaving some fields blank. (LC-3928858)
* Document of Record generation now handles repeated panel pagination correctly when parent and child panels use the same "Place Top of Next Page" configuration. Authors no longer lose child panel data during the first repeated panel instance in generated output documents. (LC-3923274)
* Long multiline text fields in PDF preview now flow correctly across pages. The generated PDF no longer duplicates page content or drops hidden text during printing. (LC-3924324)
* Fillable PDFs now reset accessibility data when users clear form fields. Screen readers announce the cleared state correctly instead of reading old field values that no longer appear in the form. (LC-3923872)
* The Accessibility Checker now handles Nepali text correctly during PDF validation. Users can check Nepali-language documents without false accessibility errors tied to character encoding. (LC-3922988) 
-->

<!-- #### XMLFM {#forms-xmlfm-6525} -->

<!-- 
* Generated PDFs now include proper tags for supported form fields that use borders in the template. Screen readers can identify numeric fields, date fields, text fields, and checkboxes more reliably. (LC-3923534)
* Document of Record output now applies the correct tag structure to supported fields that include borders in the template. Numeric, date, text, and checkbox fields remain accessible in the generated PDF. (LC-3923265)
-->

<!-- #### XTG {#forms-xtg-6525} -->

<!-- 
* Forms output now merges XML data correctly when generatePDFOutputBatch generates PDFs in batch mode. The batch process no longer creates documents with blank or missing merged fields. (LC-3924192) 
* Document of Record output now includes nested child panels in the first occurrence of a repeatable panel. Forms that use Top of Next Page pagination no longer drop child panel data from the generated output. (LC-3923923)
* Custom bullet characters in XDP templates now map correctly for accessible PDF output. PAC validation no longer reports that text object characters cannot map to Unicode. (LC-3923079) 
-->


### 基础 {#foundation-6525}

#### Apache Felix {#foundation-apachefelix-6525}

现在，启动程序正确连接CredentialsSupport服务以进行基于Felix的身份验证。 这可防止在AEM启动期间发生可能影响令牌身份验证的依赖项错误。 (GRANITE-63186)

<!-- #### Campaign{#foundation-campaign-6525} -->

<!-- #### Cloud Services{#foundation-cloudservices-6525} -->

<!-- #### Communities {#foundation-communities-6525} -->

<!-- #### Content distribution{#foundation-content-distribution-6525} -->

#### CRX {#foundation-crx-6525}

升级AEM 6.5后，JSP文件编辑现在可在CRXDE Lite中按预期工作。 CodeMirror编辑器会加载文件内容，而不是将JSP选项卡留空。 (GRANITE-64333)

<!-- #### Granite{#foundation-granite-6525} -->

<!-- #### Integrations{#foundation-integrations-6525} -->

<!-- #### Jetty{#foundation-jetty-6525} -->

#### 本地化{#foundation-localization-6525}

* 现在，安全>信任存储区中的证书上传对话框会显示本地化的数据格式标签。 用户添加证书时，不再看到未本地化的英文标签。 (NPR-43412)

* 现在，“创建KeyStore”对话框将“取消”按钮与其他对话框按钮对齐。 按钮布局保持一致且不再偏离对齐方式。 (NPR-43291)
* **安全** > A **Adobe IMS配置**&#x200B;中的“检查”对话框现在显示本地化的确认文本。 检查和删除消息不再显示为未本地化的英文字符串。 (NPR-43289)
* 现在，本地化的UI标签在受影响的对话框和Keystore选项卡中正确显示。 Aria标签值使用翻译的字符串，并且密码字段标签显示时不会截断。 (NPR-43285)
* 创建新用户工作流现在显示无效字符的本地化验证错误。 用户会收到一个清晰的已翻译消息，而不是未本地化的IllegalArgumentException字符串。 (GRANITE-52920)

<!-- #### Oak {#foundation-oak-6525} -->

#### 平台{#foundation-platform-6525}

* “显示标记引用”按钮现在可显示选定标记的引用数量。 此更新可帮助用户了解标记的使用情况，而无需额外的导航。 (CQ-4355509)
* 现在，标记中的“移动”对话框可正确放置验证消息。 当用户提交必填字段为空的对话框时，错误文本不再包含搜索路径图标。 (CQ-4353009)

#### 安全性{#foundation-security-6525}

AEM现在会列入允许列表其他包含客户端密钥的关键字。 当受支持的集成使用这些客户端密钥命名模式时，配置创建不再失败。 (GRANITE-66495)

<!-- #### Sling{#foundation-sling-6525} -->

<!-- #### SPA editor {#foundation-spa-editor-6525} -->

#### 翻译{#foundation-translation-6525}

升级后，翻译项目状态计数现在可正确更新。 作者可以审查草稿、正在处理和完整值，而无需依赖早期Service Pack行为中的过时元数据。 (NPR-43418)

#### 用户界面{#foundation-ui-6525}

* 手动输入的站点控制台URL现在可以解析为预期的页面或文件夹路径。 内容层次结构在刷新后保持不变，不再回退到基本URL。 (NPR-43688)
* AEM 6.5 LTS SP1实例升级到LTS SP2后，CRX包管理器测试套件不再失败。 现在，缩略图列表servlet测试可按预期完成。 (NPR-43534)

* 现在，每次刷新浏览器后，站点控制台内容树都会始终加载。 内容存在时，作者不会再看到空白左边栏或“没有项目”消息。 (NPR-43442)

<!-- #### WCM{#foundation-wcm-6525} -->

#### 工作流{#foundation-workflow-6525}

* 工作流模型编辑器现在可以正确验证租户特定的工作流模型路径。 在租户级别/conf路径下存储工作流模型的客户可以编辑这些模型，而无需将其移动到全局配置路径。 (GRANITE-65376)

* 工作流模型编辑器现在在路径验证期间标准化Windows文件路径。 作者可以在Windows服务器上编辑工作流模型，而不会出现阻止模型更新的访问错误。 (GRANITE-63692)
* 任务创建现在包括对截止日期的服务器端验证。 用户无法创建截止日期早于开始日期的任务，这样可使收件箱任务数据保持一致。 (CQ-4362253)
* 命名空间创建现在可以正确处理本地化的文本。 用户可以在标题字段中输入非拉丁字符，并在没有验证错误的情况下创建命名空间。 (CQ-4355587)

## 安装 [!DNL Experience Manager] 6.5.25.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.25.0需要[!DNL Experience Manager] 6.5。 有关详细说明，请参阅[升级文档](/help/sites-deploying/upgrade.md)。<!-- UPDATE FOR EACH NEW RELEASE -->
* 服务包可通过 Adobe [软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip)下载。
* 在使用 MongoDB 且包含多个实例的部署中，请在其中一个作者实例上使用包管理器安装 [!DNL Experience Manager] 6.5.25.0。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe 不建议移除或卸载 [!DNL Experience Manager] 6.5.25.0 包。 因此，在安装该包之前，您应创建 `crx-repository` 的备份，以便在需要时进行回滚。<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### 在 [!DNL Experience Manager] 6.5 上安装服务包{#install-service-pack}

1. 如果实例处于更新模式（即由早期版本升级而来），请在安装前先重启该实例。 如果实例已长时间运行，Adobe 建议先重启。

1. 在安装之前，请为您的 [!DNL Experience Manager] 实例创建快照或执行一次全新的备份。

1. 从[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip)下载Service Pack。<!-- UPDATE FOR EACH NEW RELEASE -->

1. 打开包管理器，然后选择&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传该包。 如需了解更多信息，请参阅[包管理器](/help/sites-administering/package-manager.md)。

1. 选择该包，然后选择&#x200B;**[!UICONTROL 安装]**。

1. 要更新 S3 连接器，请在安装服务包后停止实例，用安装文件夹中提供的新二进制文件替换现有连接器，然后重新启动实例。 请参阅 [Amazon S3 数据存储](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>在安装服务包过程中，包管理器 UI 中的对话框有时会意外退出。 Adobe 建议您在访问部署之前，先等待错误日志趋于稳定。 在确认安装成功之前，请先等待与卸载更新捆绑包相关的特定日志出现。 通常，该问题会在 [!DNL Safari] 浏览器中出现，但也可能会在其他浏览器中间歇出现。

**自动安装**

您可以使用以下两种方法来安装 [!DNL Experience Manager] 6.5.25.0。<!-- UPDATE FOR EACH NEW RELEASE -->

* 当服务器在线时，将包放入 `../crx-quickstart/install` 文件夹中。 该包会自动安装。
* 使用[包管理器的 HTTP API](/help/sites-administering/package-manager.md#package-share)。 请使用 `cmd=install&recursive=true` 以便安装嵌套的包。

>[!NOTE]
>
>Experience Manager 6.5.25.0 不支持 Bootstrap 安装。<!-- UPDATE FOR EACH NEW RELEASE -->

**验证安装**

要了解与此版本兼容的已经过认证的平台，请参阅[技术要求](/help/sites-deploying/technical-requirements.md)。

1. 在[!UICONTROL 已安装的产品]下，产品信息页面（`/system/console/productinfo`）会显示更新后的版本字符串 `Adobe Experience Manager (6.5.25.0)`。<!-- UPDATE FOR EACH NEW RELEASE -->

1. 在 OSGi 控制台中，所有 OSGi 捆绑包均应处于&#x200B;**[!UICONTROL 活跃]**&#x200B;或&#x200B;**[!UICONTROL 片段]**&#x200B;状态（使用网页控制台：`/system/console/bundles`）。

1. OSGi 捆绑包 `org.apache.jackrabbit.oak-core` 的版本应为 1.22.20 或更高版本（使用网页控制台：`/system/console/bundles`）。<!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### 安装 [!DNL Experience Manager] Forms 的服务包{#install-aem-forms-add-on-package}

如需了解在 Experience Manager Forms 上安装服务包的操作说明，请参阅 [Experience Manager Forms 服务包安装说明](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)。

>[!NOTE]
>
>在 [AEM 6.5 快速入门](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/implementing/deploying/deploying/deploy)中谈及的自适应表单功能旨在仅作探索和评估用途。 由于自适应表单功能需要适当的许可，因此必须获得 AEM Forms 的有效许可证才能作生产用途。

### 为 Experience Manager 内容片段安装 GraphQL 索引包{#install-aem-graphql-index-add-on-package}

使用 GraphQL 的客户必须安装[带有 GraphQL 索引包 1.1.1 的 Experience Manager 内容片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip)。

这样做可根据实际使用的功能添加所需的索引定义。

如果未安装该包，可能会导致 GraphQL 查询变慢或失败。

>[!NOTE]
>
>每个实例只需安装一次该包；无需在每次安装服务包时重新安装。

### UberJar{#uber-jar}

适用于 [!DNL Experience Manager] 6.5.25.0 的 UberJar 可在 [Maven Central 存储库](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.25/)获取。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

要在 Maven 项目中使用 UberJar，请参阅[如何使用 UberJar](/help/sites-developing/ht-projects-maven.md)，并在项目 POM 中包含以下依赖项：<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.25</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar 和其他相关工件现已发布在 Maven Central 存储库，而非 Adobe 公共 Maven 存储库（`repo.adobe.com`）。 主 UberJar 文件已重命名为 `uber-jar-<version>.jar`。 因此，在 `dependency` 标记中不再包含以 `apis` 为值的 `classifier`。



## 已弃用和已移除的功能{#removed-deprecated-features}

请参阅[已弃用和已移除的功能](/help/release-notes/deprecated-removed-features.md)，以获取 AEM 6.5 中所有已弃用或已移除功能的详细列表。

### AEM Assets REST API 中的内容片段支持 {#cf-support-assets-rest-api}

AEM 6.5 LTS SP2 为内容片段和模型管理提供了现代化的 OpenAPI，因此 AEM Assets REST API 中的旧版内容片段支持端点已弃用。

Adobe打算在生命周期结束公告之前保持这些旧端点可用。 Adobe 不计划为已弃用的端点提供进一步的增强功能。

### SPA 编辑器 {#spa-editor}

[从AEM 6.5版本6.5.25开始的新项目已弃用SPA编辑器](/help/sites-developing/spa-overview.md)。 SPA编辑器仍受现有项目的支持，但不应用于新项目。

现在管理 AEM 中的 Headless 内容时首选以下编辑器：

* [Universal Editor &#x200B;](/help/sites-developing/universal-editor/introduction.md)，用于可视化编辑。
* [内容片段编辑器](/help/sites-developing/universal-editor/introduction.md)，用于以基于表单的方法编辑。

## 已知问题{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

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

   1. 从 `crx-quickstart/repository/` 中删除以下两个文件夹

      * `cache`
      * `diff-cache`

   1. 安装服务包，或重新启动 Experience Manager as a Cloud Service。
新的 `cache` 和 `diff-cache` 文件夹会自动创建，并且不会再在 `error.log` 中遇到与 `mvstore` 相关的异常。

* 请将可能使用了自定义 API 名称的 GraphQL 查询更新为使用内容模型的默认名称。

* GraphQL 查询可能会使用 `damAssetLucene` 索引，而不是 `fragments` 索引。 此操作可能导致 GraphQL 查询失败或运行时间过长。

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

* 在尝试移动、删除或发布内容片段、网站或页面时，获取内容片段引用时会出现问题。 后台查询失败；功能无法正常工作。
为确保该功能正常运行，必须将以下属性添加到索引定义节点 `/oak:index/damAssetLucene`（无需重新索引）：

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* 如果您在 Java™ 11 上将 [!DNL Experience Manager] 实例从 6.5.0 – 6.5.4 升级到最新的服务包，可能会在 `error.log` 文件中看到 `RRD4JReporter` 异常。 要停止这些异常，请重新启动 [!DNL Experience Manager] 实例。<!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 用户可以在 [!DNL Assets] 的层级中重命名文件夹，并将嵌套文件夹发布到 [!DNL Brand Portal]。 但是，在 [!DNL Brand Portal] 中，文件夹标题不会更新，直到重新发布根文件夹。

* 在安装 [!DNL Experience Manager] 6.5.x.x 期间，可能会显示以下错误和警告消息：
   * 当在 [!DNL Experience Manager] 中使用 Target Standard API（IMS 身份验证）配置 Adobe Target 集成时，将体验片段导出到 Target 会导致创建错误的产品建议类型。 在 Target 中，系统不会创建类型为“Experience Fragment”/来源为“Adobe Experience Manager”的产品建议，而是会创建多个类型为“HTML”/来源为“Adobe Target Classic”的产品建议。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：未在 `granite/operations/maintenance` 找到维护窗口。
   * 当在自适应表单中使用 SUM、MAX 和 MIN 等聚合函数时，服务器端验证失败（CQ-4274424）。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：未在 `granite/operations/maintenance` 找到维护窗口。
   * 通过 Shoppable Banner 查看器预览资产时，Dynamic Media 交互式图像中的热点不可见。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]`：等待完成取消注册的注册变更时超时。

* 从 AEM 6.5.15 开始，由 ```org.apache.servicemix.bundles.rhino``` 捆绑包提供的 Rhino JavaScript 引擎引入了新的提升行为。 使用严格模式（```use strict;```）的脚本必须声明正确的变量。 否则脚本将无法运行，并会抛出运行时错误。

* 通过官方更新包安装与标记相关的开箱即用内容时，`/content/cq:tags` 节点的语言属性会被重置为默认值。 此操作适用于服务包、安全服务包、扩展功能包、累积功能包、补丁等。 因此，在安装之前必须从属性中手动添加该项。

### AEM Sites 已知问题 {#known-issues-aem-sites-6525}

内容片段预览在处理大型片段树时因 DoS 防护而失败。 请参阅[关于默认 GraphQL 查询执行器配置选项的知识库文章](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-kcs/kbarticles/ka-23945)（SITES-17934）

### AEM Forms 已知问题 {#known-issues-aem-forms-6525}

* **FORMS-14521**&#x200B;如果用户尝试预览包含保存的XML数据的草稿书信，则会陷入某些特定书信的`Loading`状态。
* **FORMS-16603**&#x200B;在交互式通信代理UI的打印预览中，某些计算值未正确显示。
* **FORMS-15681**&#x200B;在“打印预览”中查看信件时，内容已更改；某些空格消失，某些信件已替换为`x`。
* **FORMS-15428**&#x200B;使用Forms加载项更新到AEM Forms Service Pack 20 (6.5.20.0)后，依赖使用基于凭据的身份验证的旧版Adobe Analytics Cloud Service的配置停止工作。 此问题会导致分析规则无法正确执行。
* **FORMS-16557**&#x200B;在交互式通信代理UI的打印预览中，所有字段值的货币符号（如美元符号$）显示不一致。 对于不超过 999 的数值会显示符号，但对于 1000 及以上的数值则缺少符号。
* **FORMS-16575**&#x200B;交互式通信中对嵌套布局片段XDP所做的任何修改都不会反映在IC编辑器中。
* **FORMS-21378**&#x200B;启用服务器端验证(SSV)时，表单提交可能会失败。 如果遇到此问题，请联系 Adobe 支持部门寻求帮助。
* **FORMS-23722**&#x200B;如果将包含使用`bindref`的&#x200B;**文件附件**&#x200B;字段的表单提交到AEM工作流，且步骤为&#x200B;**分配任务**，则不会显示附件。 因此，当任务从“收件箱”中打开时，它们不会显示。 文件将正确地保存到存储库，但分配任务步骤UI无法显示附件。
* 当自适应表单嵌入到站点页面中时，**FORMS-23802**&#x200B;自定义函数无法在预览或发布中加载。 当&#x200B;**aem-forms-core-component**&#x200B;库版本低于1.1.76时，会发生此问题。 您可能会在日志中看到错误，例如`InvalidFormContainerException: No form container found`。 要解决此问题，请[下载并安装适用于AEM Forms SP24 (AddOn 6.0.1454)的修补程序](/help/release-notes/aem-forms-hotfix.md)。

#### 可用修补程序的已知问题 {#aem-forms-issues-with-hotfixes}

<!--
>[!NOTE]
>
>Avoid upgrading to Service Pack 6.5.25.0 for issues without an available hotfix. It may lead to unexpected errors. Upgrade to Service Pack 6.5.25.0 only after the required hotfixes are released.
-->

以下问题已提供可下载并安装的热修复补丁： 您可以通过[下载并安装热修复补丁](/help/release-notes/aem-forms-hotfix.md)来解决这些问题：

* **FORMS-23881**&#x200B;在使用6.5.23.0完整安装程序设置的AEM Forms JEE部署中，当调用中提供了自定义XCI文件时，输出服务无法处理请求。 要解决此问题，请从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)门户安装最新的AEM 6.5.25.0 Forms Service Pack。
* **FORMS-23789**（仅限JEE上的AEM Forms）：用户在JEE SP24上的AEM Forms中遇到Log4j问题，导致企业客户的日志记录和监视出现中断。 要解决此问题，请在JEE Service Pack 6.5.25.0上[下载并安装适用于AEM Forms的修补程序](/help/release-notes/aem-forms-hotfix.md)。
* **FORMS-23802**&#x200B;当表单位于具有旧版aem-forms-core-component (&lt;1.1.76)的站点页面中时，在预览或发布中无法加载自定义函数。 要解决此问题，请安装适用于SP24的[AEM Forms附加组件修补程序6.0.1454](/help/release-notes/aem-forms-hotfix.md)。
* **FORMS-23789**（仅限JEE上的AEM Forms）：用户在JEE SP24上的AEM Forms中遇到Log4j问题，导致企业客户的日志记录和监视出现中断。 要解决此问题，请在JEE Service Pack 6.5.25.0上[下载并安装适用于AEM Forms的修补程序](/help/release-notes/aem-forms-hotfix.md)。
* **FORMS-23802**&#x200B;当表单位于具有旧版aem-forms-core-component (&lt;1.1.76)的站点页面中时，在预览或发布中无法加载自定义函数。 要解决此问题，请安装适用于SP24的[AEM Forms附加组件修补程序6.0.1454](/help/release-notes/aem-forms-hotfix.md)。
* AEM Forms 现已将表单组件中的 Struts 版本从 2.5.33 升级至 6.x。 此升级提供了以前未包含在SP24中的Struts更改。 相关支持已通过[热修复补丁](/help/release-notes/aem-forms-hotfix.md)提供，您可以下载并安装该热修复补丁，以支持 Struts 的最新版本。
* **FORMS-14926**&#x200B;安装AEM Forms JEE Service Pack 21 (6.5.21.0)后，如果在`<AEM_Forms_Installation>/lib/caching/lib`文件夹下找到Geode jars `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)`的重复条目，请执行以下步骤，以解决该问题：

   1. 如果定位器正在运行，请先停止定位器。
   2. 停止 AEM 服务器。
   3. 进入 `<AEM_Forms_Installation>/lib/caching/lib`。
   4. 移除所有 Geode 补丁文件，仅保留 `geode-*-1.15.1.2.jar`。 确认仅存在 `version 1.15.1.2` 的 Geode jar。
   5. 以管理员模式打开命令提示符。
   6. 使用 `geode-*-1.15.1.2.jar` 文件安装 Geode 补丁。

* **FORMS-15256**&#x200B;用户从AEM 6.5 Forms Service Pack 18或19升级到Service Pack 20或21时，遇到JSP编译错误。 该错误会导致无法打开或创建自适应表单。 它也会影响其他 AEM 界面。 这些界面包括页面编辑器、AEM Forms UI、工作流编辑器和系统概览 UI。

  如果遇到此类问题，请执行以下步骤进行解决：
   1. 进入 CRXDE 中的目录 `/libs/fd/aemforms/install/`。
   2. 删除名为 `com.adobe.granite.ui.commons-5.10.26.jar` 的捆绑包。
   3. 重新启动 AEM 服务器。

* **FORMS-23703**&#x200B;如果未使用默认值配置`contains`规则时，自适应表单的服务器端验证失败。 您可以安装最新版本的[AEM Forms 6.5.25.0 Service Pack](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#aem-65-forms-releases)以修复此问题。
* **GRANITE-63681**&#x200B;表单数据模型连接器可能无法通过身份验证，因为默认情况下不允许使用所需的关键字和正则表达式模式。 要解决此问题，请从[链接](/help/release-notes/aem-forms-hotfix.md)下载并安装修补程序。
* **FORMS-23979** HTML-PDF转换(PDFG)可能会遇到间歇性超时。 随后发布了适用于SP24的较新版本的Forms加载项，其中包括此修补程序。 如果您遇到此问题，请将您的环境更新到6.5.25.0[&#128279;](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#aem-65-forms-releases)的最新发布的Forms加载项。
* **FORMS-23717**&#x200B;升级到&#x200B;**AEM Forms6.5.25.0**&#x200B;后，`server.log`和`error.log`可能会泛洪为重复的警告消息，例如&#x200B;*安全解析器工厂创建失败*&#x200B;或&#x200B;*不支持安全属性……*。 日志可能会以每秒&#x200B;**5到10行**（每小时数百兆字节）的速度增长，这会填充磁盘并阻止生产转出。

要减少日志卷，请在应用程序服务器配置中或通过JVM参数`-Dlogging.level.com.adobe.util.XMLSecurityUtil=ERROR`将`com.adobe.util.XMLSecurityUtil`的日志记录级别设置为`ERROR`。 此功能仅隐藏消息，不会修复根本原因。

* **FORMS-23875**&#x200B;在表单数据模型搜索中，即使不存在相关实体，也会在UI中显示HTML标记。 要解决此问题，请从[链接](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bb-expressionmanager-pkg-10.0.48.zip)下载并安装修补程序。

## 已包含的 OSGi 捆绑包和内容包{#osgi-bundles-and-content-packages-included}

以下文本文档列出了此 [!DNL Experience Manager] 6.5 服务包版本中包含的 OSGi 捆绑包和内容包：

* [Experience Manager 6.5.25.0 中包含的 OSGi 捆绑包列表](/help/release-notes/assets/65250-bundles.txt)
<!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.25.0 中包含的内容包列表](/help/release-notes/assets/65250-packages.txt)
<!-- UPDATE FOR EACH NEW RELEASE -->

## 受限网站{#restricted-sites}

这些网站仅对客户开放。 如果您已是客户并需要访问权限，请联系您的 Adobe 客户经理。

* [从 licensing.adobe.com 下载产品](https://licensing.adobe.com/)
* [联系 Adobe 客户支持部门](https://experienceleague.adobe.com/zh-hans/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience#)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 产品页面](https://business.adobe.com/cn/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 文档](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65)
>* [订阅 Adobe 产品更新早知道](https://www.adobe.com/cn/subscription/priority-product-update.html)

