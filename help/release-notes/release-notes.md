---
title: '[!DNL Adobe Experience Manager] 6.5的发行说明'
description: 查找 [!DNL Adobe Experience Manager] 6.5 的版本信息、新增功能、安装操作方法和详细更改列表。
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
contentOwner: Rick Brough
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: ed762d86-a04b-452b-a08f-86359bb8ff27
    internal-label: Configuration and operations
subfeature_v2:
  - id: c21ccc2b-e0c8-4853-bf41-f12259ed93f8
    internal-label: Release information
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: d777049ff8873ab60b286ec268fd544dc61fb038
workflow-type: tm+mt
source-wordcount: '7172'
ht-degree: 16%
---
# [!DNL Adobe Experience Manager]6.5 最新服务包发行说明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!--
DO NOT DELETE THIS HIDDEN NOTE!      DO NOT DELETE THIS HIDDEN NOTE!
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section.
-->

## 发行摘要 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.26.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 类型 | 服务包发行 |
| 日期 | 2026年11月12日<!-- UPDATE FOR EACH NEW RELEASE --> |
| 下载 URL | [软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.26.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |


<!-- REWRITE AI GENERATED SUMMARY OF NOTES BELOW FOR EACH NEW SERVICE PACK RELEASE -->

Experience Manager 6.5.26.0包括新增功能、客户请求的关键增强功能和错误修复。 此外，还包括基于2019年4月以来推出的6.5基础的辅助功能、本地化、性能、稳定性和安全性改进。

Service Pack 26的主要功能亮点包括：

* 安全。 两个关键修复修复了元数据编辑器中的服务器端模板插入漏洞和Coral UI Servlet中的跨站点脚本(XSS)违规问题。
* C2PA合规性。 Assets现在检测C2PA凭据并签署更新资产工作流生成的演绎版。 签名在每个实例中本地运行，不支持专用或客户拥有的签名基础架构。
* 辅助功能。 超过25个修复可帮助页面编辑器和站点控制台满足WCAG对比度、键盘和屏幕阅读器要求。
* 本地化。 数十种修复程序可以翻译字符串，并更正站点、Assets、安全和运营中的布局问题。
* 可靠性。 修复了经典UI中的发布实例上GraphQL锁争用、MSM转出、富文本编辑器工具栏操作以及页面激活问题。
* Analytics。 Launch集成在Analytics 1.4于2026年8月31日终止使用之前使用Adobe Analytics 2.0 API。


<!-- UPDATE FOR EACH NEW RELEASE -->

## 修复了Service Pack 26中的问题、增强功能和改进 {#fixed-issues}

<!-- 6.5.25.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->


### [!DNL Sites]{#sites-6526}

#### 辅助功能 {#sites-accessibility-6526}

* 作者仅可使用键盘添加、移动和删除组件。 拖放交互需要一个指针，因此未通过WCAG 2.1.1键盘标准。 现在，编辑器将插入组件弹出菜单、剪切并粘贴和删除作为键盘可操作的等效项。 (SITES-25359)

* 作者现在可以在文本组件内联菜单中看到活动的格式(“T”)按钮。 在作者应用粗体或斜体格式后，按钮图标在深灰色背景中保持深色，并缺少WCAG 2.1 AA最低对比度4.5:1。 更新后的CSS使图标变亮，图标将恢复早期Service Pack提供的对比度。 (SITES-51864)

* 现在，当您从“图像”下拉列表中选择“段落”后，页面编辑器中的“Assets”选项卡会在“选择组件”下拉菜单中显示一个翻译的字符串。 以前，字符串“OTHER”显示为英文，因为本地化资源缺少它。 更新的词典在所有区域设置中提供翻译。 (SITES-24525)




* 页面编辑器中的ContextHub iframe现在具有描述性标题属性。 以前，`contexthub-ui-iframe`元素没有标题，因此屏幕阅读器用户在焦点移至它时无法识别它。 标题现在显示在每个编辑器页面和视图中，包括画布、侧边栏和布局预览。 (SITES-24650)
* 站点控制台过滤器边栏中的过滤器按钮未在保存的搜索和选择搜索目录字段上方添加可见标签。 审核报告指出，焦点离开按钮、按下某个键或单击该按钮时会显示标签。 测试无法重现行为，因此无需进行更改。 (SITES-24706)
* 站点控制台应用程序导航中的链接现在更加清晰地脱颖而出。 链接文本符合4.5:1的对比度，但字体粗细和较小尺寸使链接难以查看。 较大的字体粗细和大小使有视觉障碍的用户更容易阅读文本。 (SITES-24723)
* 屏幕阅读器不再在“用户首选项”模式中的工具提示内容之前宣告“空白”。 以前，信息图标使用`role="tooltip"`和`aria-labelledby`引用，因此NVDA先读取空标签。 该图标现在使用`role="button"`和`aria-label`个“信息”，并且更改适用于共享该模式的Coral表单组件。 (SITES-24732)
* 现在，删除模式中的删除按钮符合WCAG 1.4.3的对比度要求4.5:1。 以前，作者选择项目并单击操作工具栏中的“删除”后，红色背景上的白色文本的比率为3.9:1。 较深的按钮颜色使具有视觉障碍的作者能够阅读标签。 (SITES-24772)
* 站点控制台引用边栏中的引用标题现在使用标题元素而不是`div`。 以前，屏幕阅读器无法朗读文本作为标题，因此用户无法按标题导航。 标题也出现在初始“参照”视图的顶部。 (SITES-24967)
* 站点控制台过滤器边栏中折叠按钮的焦点指示器现在符合WCAG 1.4.11的3:1对比度要求。 以前，蓝色指示器在背景中显示的是2.3:1的比率，这使得键盘用户很难找到标记折叠按钮。 更新后的颜色为键盘用户提供了清晰的焦点提示。 (SITES-24986)
* 站点控制台过滤器边栏中单选按钮的焦点指示器现在符合WCAG 1.4.11的3:1对比度要求。 以前，淡蓝色指示器在背景中的比率为1.7:1。 键盘用户现在可以在修改日期折叠面板中跟踪其位置。 (SITES-24987)
* 页面编辑器侧边栏中路径和标记字段旁边的“选择”按钮不再使用复选框图标。 以前，该图标建议进行切换，但激活按钮会打开一个包含树目录的模式窗口。 现在，“选择”按钮可正确传达其功能，同样适用于Image和Teaser模式。 (SITES-25210)
* 屏幕阅读器现在跳过页面编辑器侧边栏中资产的缩略图图像。 以前，每个图像都带有与可见资源名称重复的替换文本，因此用户会听到两次相同的文本。 空`alt`属性将图像标记为装饰性并将名称保留在卡片标题中。 (SITES-25213)
* 屏幕阅读器将侧边栏“组件”列表识别为列表。 审核报告这些项目为不相关的元素，但测试确认标记使用列表元素和列表项目。 无需更改代码。 (SITES-25214)
* 页面编辑器侧边栏中组件的信息图标更大，更易于查看。 以前，这些图标使用大约12像素的超小尺寸，视觉障碍的用户很难看到这些尺寸。 图标现在使用中等大小。(SITES-25217)
* 注释模式中样本按钮上的焦点指示器现在从按钮中脱颖而出。 以前，指示器与样本颜色相匹配。 这使得键盘用户难以查看哪个按钮具有焦点。 偏移可以使指示器与背景有足够的对比度，并使其保持清晰可见。 (SITES-25253)
* 时间扭曲模式中的“日期”字段不再包含`aria-haspopup="dialog"`。 以前，屏幕阅读器会宣布该字段会打开一个对话框，即使它没有打开。 删除属性可为屏幕阅读器用户提供准确的信息。 (SITES-25263)
* “人口统计”工具栏中的文本标签（如“推荐”）现在符合WCAG 1.4.3的4.5:1对比度要求。 以前，在预览模式下，深灰色背景中的灰色文本的比例为2.8:1。 较深或较浅的文本（取决于背景）使每个标签都可读。 (SITES-25307)
* “人口统计”工具栏中Commerce、角色和设备按钮上的焦点指示器现在符合WCAG 1.4.11的3:1对比度要求。 以前，指示器显示与工具栏背景的比率为1.9:1。 键盘用户现在可以跟踪其位置。 (SITES-25308)
* 现在，作者在“人口统计”工具栏文本字段中键入的文本符合WCAG 1.4.3的对比度要求4.5:1。 以前，灰色背景上的白色文本在字段中的比例为2.9:1，例如预览模式下的用户档案下拉列表`displayName`字段。 更新后的颜色使有视觉障碍的作者能够读取键入的值。 (SITES-25318)
* 屏幕阅读器现在会在焦点进入Teaser、图像和轮播对话框中的复选框时阅读描述工具提示。 以前，文本与复选框缺乏程序化关联，因此用户无法听到指令。 `aria-describedby`属性现在将每个复选框链接到其描述。 (SITES-25364)
* 屏幕阅读器现在会朗读在富文本编辑器中活动的段落格式按钮。 以前，从列表中选择一个选项不会为辅助型技术指明当前的选择。 活动按钮现在带有`aria-current="true"`，而活动超链接目标选项带有`aria-selected="true"`。 (SITES-25367)
* 现在，站点控制台列表视图的表标题中的排序按钮符合WCAG 1.4.11的3:1对比度要求。 以前，浅灰色图标与标题背景的比例为1.5:1。 较深的图标颜色使按钮对有视觉障碍的作者可见。 (SITES-25372)
* 当焦点移至过滤器字段时，页面编辑器侧边栏中的Assets选项卡不再重新加载。 以前，跳转到空字段会触发重新加载，并且屏幕阅读器每次都会宣布加载消息。 现在，只有在更改筛选器值并按Enter键后，选项卡才会重新加载。 (SITES-25377)
* 注释模式中选择的样本图标现在符合WCAG 1.4.11对比度要求3:1。 以前，白色复选标记显示与黄色、橙色和绿色色板的比例仅为1.58:1。 更新的图标为具有视觉障碍的作者提供了明确的指示器。 (SITES-25523)
* 页面编辑器侧面板中的“组件”列表不再使用键盘焦点。 键盘用户使用内容窗口中的控件选择和移动组件，因此侧面板列表重复了此功能。 组件过滤器下的注释会通知键盘用户从何处查找控件。 (SITES-40752)


#### 管理用户界面{#sites-adminui-6526}


#### 经典 UI{#sites-classicui-6526}

* 作者可以在经典UI站点控制台(`siteadmin.html`)中再次激活页面。 以前，“激活页面”按钮会无限期地显示“正在加载”旋转图标，并且永远不会触发复制，因为失败的跟踪脚本会停止点击处理程序。 现在，点击处理程序可在没有错误的情况下运行并完成激活。 (SITES-52165)
* 印度尼西亚语代码现在在语言副本属性中显示为ID。 以前，引用边栏为印度尼西亚语言根下的页面显示旧版代码IN 。 cq-wcm-core捆绑包更新可更正该值，因此代码符合ISO标准。 (SITES-4491)

<!--
#### Component Console{#sites-component-console-6526}



#### [!DNL Content Fragments]{#sites-contentfragments-6526}



#### [!DNL Content Fragments] - Admin{#sites-admin-6526}
-->


#### [!DNL Content Fragments] — 片段编辑器{#sites-fragments-editor-6526}

* 对于内容片段编辑器中的每个多字段引用，会立即显示编辑内容片段按钮。 以前，按钮会一直保持隐藏状态，直到作者保存父片段，并且在打开路径浏览器后没有任何反应。 编辑器现在在首次渲染时构建操作列表，因此作者无需额外步骤即可打开引用的片段。 (SITES-43733)

* 在“创建内容片段”对话框占位符中，中文、日语和韩语字符不再以斜体显示。 以前，斜体样式应用于&#x200B;**Assets** > **文件**&#x200B;下的CJK字符，这会使文本难以阅读。 更新的样式跳过了CJK语言的斜体。 (SITES-43548)
* 在Granite UI更新后，内容片段编辑器正确验证字段。 最近的Granite UI更改导致回归，因此编辑器客户端库不再与新的验证行为匹配。 经过调整的库和测试可解决不匹配。 (SITES-46650)


#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6526}

* 对内容片段的GraphQL查询现在可以通过OpenAPI Assets识别对Dynamic Media的RemoteRef引用。 以前，当AEM 6.5站点使用AEM as a Cloud Service Assets时，查询失败并出现“持久查询验证错误”，并且未返回任何资产数据。 响应现在包括存储库ID和资产ID，因此客户端可以构建投放URL。 (SITES-48507)

* 在GraphQL流量较大时，发布实例保持响应状态。 `GraphQLServiceImpl`中的锁定争用延迟了架构方法上的请求处理线程，这会减慢请求并需要重新启动。 改进的同步可解决性能限制并维护站点和移动应用程序的可用性。 (SITES-48699)

* 重新加载页面后，“GraphQL端点”页面上的消息仍保持本地化状态。 以前，当您创建和删除端点时，“未找到端点”消息会以您的语言显示，但在重新加载后会还原为英语。 页面现在会在每次访问时加载翻译的字符串。 (SITES-43586)


<!--
#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6526}
-->


#### [!DNL Content Fragments] — 模型和模型编辑器{#sites-models-model-editor-6526}

* 当配置名称包含本地化字符（如“espanol テスト”）时，内容片段模型的缩略图显示在&#x200B;**工具** > **常规** > **内容片段模型**&#x200B;中。 以前，上传的缩略图不会显示，因为字符在路径中导致错误。 更新的处理可正确编码名称。 (SITES-39242)

* 内容片段模型编辑器画布上的字段标签字符串现在以用户的语言显示。 以前，在作者将组件拖到画布上后，标签仍为英文，并且仅在他们保存并重新打开模型后才会翻译。 现在，标签会立即翻译，与“属性”面板匹配。 (SITES-45383)


<!--
#### [!DNL Content Fragments] - REST API{#sites-restapi-6526}

#### ContextHub{#sites-contexthub-6526}
-->


#### 核心后端{#sites-core-backend-6526}

* 现在，通过开启关闭时间计划的页面激活仅在需要时运行。 `OnOffTriggerProcessor`以前经常触发复制和缓存失效，这强制作者手动重新发布内容。 反向移植的修复消除了不必要的处理，并恢复可靠的计划发布。 (SITES-48483)

* 文件上传适用于多字段内下一代资产管理的远程资产。 以前，当作者为多字段中的字段选择远程资产时，上传失败。 核心组件更新将恢复上传流程，因此字段可接受资产。 (SITES-44266)


#### 核心组件{#sites-core-components-6526}

* 远程资产选取器将每个多字段项目的图像分开。 以前，在一个多字段项目中选择图像会将其应用于所有其他项目，并且远程资产引用不会保存。 现在，每个项目都有其自己的选择，在保存对话框后，参照将持续存在。 (SITES-42376)

* 此版本包括对Commerce、核心组件、基础组件（旧版）、启动项和MSM Live Copies的后台修复。 修复了安全漏洞、跨站点脚本(XSS)违规、文件上传行为和Live Copy行为。 这些后端端口使AEM 6.5和AEM 6.5 LTS与之前在AEM as a Cloud Service中提供的修复一致。 (SITES-43738)


<!--
#### Campaign integration{#sites-campaign-integration-6526}

#### ContentHub {#sites-contenthub-6526}

#### Crosswalk {#sites-crosswalk-6526}

#### Experience Fragments{#sites-experiencefragments-6526}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-6526}
-->


#### Headless — 管理员 {#sites-headless-admin-6526}

增强：Headless管理员中的“预览”视图现在将选定的变量路径传递到预览组件。 此更改确保具有多个变体的内容片段的预览从正确的变体加载内容。 `draftFragmentIds`数组包含变量参数。 (SITES-42714)


#### 发布项{#sites-launches-6526}

* 提升启动项的时间线条目现在以用户的语言显示。 以前，字符串“Created version of”和“before promoting launch”在作者提升启动项并在Sites中打开站点时间线后保留英文。 更新的资源在所有区域设置中提供翻译。 (SITES-13389)
* 启动项过滤器面板中的选择Launch Source占位符路径会完整显示。 以前，在法语、意大利语和葡萄牙语等本地化界面中，文本被切断，因为它不适合该字段。 更新的布局显示完整的占位符。 (SITES-42792)
* 工具>站点>启动项中的“实时日期”列不再显示德语、法语、西班牙语、意大利语、巴西葡萄牙语和繁体中文语言环境的上午或下午。 以前，该列使用12小时制，这与这些区域设置不匹配。 列现在显示24小时格式。 (SITES-43178)


<!--
#### Link Checker{#sites-link-checker-6526}
-->


#### 本地化{#sites-localization-6526}

* 现在，**工具** > **操作**&#x200B;下的运行状况报告页面上的字符串将以用户的语言显示。 以前，资源搜索路径、维护、复制队列、日志错误、活动包和请求性能消息仍使用英文。 更新的i18n资源提供了翻译，而回退文件可使字符串保持可用。 (NPR-44279)

* 错误消息“选中“手动添加”选项时忽略“JSON路径”的设置”现在以用户的语言显示在&#x200B;**工具** > **Assets** > **元数据架构**&#x200B;控制台中。 以前，在作者添加下拉元素、选择通过JSON路径添加并切换为手动添加后，消息保持英语。 更新的资源提供翻译。 (ASSETS-31575)
* **Assets** > **管理**&#x200B;标记中的“提升”字符串现在以用户的语言显示。 以前，当您选择“提升”后将鼠标悬停在智能标记上时，字符串仍为英文。 更新的资源在所有区域设置中提供翻译。 (ASSETS-36070)
* 添加按钮标签不再与&#x200B;**文件夹属性** > **资产贡献**&#x200B;中的按钮重叠。 以前，在创建具有“资产贡献”设置的文件夹后，文本与德语、意大利语和巴西葡萄牙语界面中的按钮冲突。 更新的样式为翻译时间较长的标签提供了足够的空间。 (ASSETS-36746)
* Assets列表视图中的列标题现在在日语界面中水平显示。 以前，标题垂直显示在&#x200B;**Assets** > **文件**&#x200B;下的列表视图中，以及内容片段编辑器的卡片视图中。 更新的`cq-dam-content`包更正文本方向。(ASSETS-43105)
* Assets列视图中的发布状态“已计划为以后使用”现在将以用户的语言显示。 以前，在作者选择资产、选择&#x200B;**管理发布**、选择&#x200B;**稍后**&#x200B;选项、添加日期并发布后，字符串仍为英文。 更新的`cq-dam-content`包在所有区域设置中提供翻译。 (ASSETS-43307)
* **智能标记配置**&#x200B;选项卡中的字符串现在以完整形式显示法语和巴西葡萄牙语。 以前，单击&#x200B;**工具** > **云服务** > **智能标记**&#x200B;下的&#x200B;**创建**&#x200B;后，文本被截断。 要在没有工具提示的情况下阅读文本，请使用可提供充足空间的CSS更新。 (ASSETS-68045)
* Assets管理员搜索边栏中的“多路径值属性谓词”字符串现在以用户的语言显示。 以前，当管理员在&#x200B;**工具** > **常规** > **搜索**&#x200B;表单下编辑搜索表单并将谓词拖到该表单上时，字符串仍为英文。 更新的`cq-dam-content`包提供了翻译。(CQ-4336103)
* “项目”视图中的Aria标签现在以用户的语言显示。 以前，每个项目拼贴上的“操作”按钮没有可访问的名称，并且“配置拼贴”操作在本地化同级标签时使用硬编码英语标签。 更新的拼贴脚本为这两个操作提供了一个本地化的标签。 (CQ-4352359)
* 现在，名称中包含中文、日文或韩文字符的智能收藏集可正确保存。 以前，当名称包含CJK字符时，从&#x200B;**Assets** > **文件** > **筛选器**&#x200B;中保存收藏集失败，原因是“保存搜索失败 — 无效请求，不允许存在重复的收藏集”。 重复检查现在比较收藏集标题而不是节点名称，因此具有不同CJK标题的收藏集不再冲突。 (GRANITE-62592)
* **安全** > **用户** > **创建**&#x200B;中的国家/地区下拉列表现在会按用户语言的字母顺序对名称进行排序。 以前，该列表在显示本地化名称时会按英语顺序对名称进行排序，因此国家/地区在日语等语言环境中会出现混乱。 更新的`com.adobe.granite.security.content`包使用区域设置感知规则排序。 (GRANITE-67789)
* **工具** > **操作** > **维护**&#x200B;中的审核日志维护任务的免责声明现在以用户的语言显示。 以前，在用户单击“Weekly Maintenance”（每周维护）窗口中的免责声明图标后，有关审核日志清除和合规性要求的警告仍为英文。 更新的资源在所有区域设置中提供翻译。 (NPR-44189)
* **安全** > **权限** > **审核视图**&#x200B;中的权限名称现在以用户的语言显示。 以前，由于缺少翻译，这些名称以英文显示。 更新的`com.adobe.granite.platform.i18n`包提供它们。 (NPR-44477)
* **安全** > **Adobe IMS配置**&#x200B;中的“检查运行状况”对话框现在以用户的语言显示。 以前，该对话框在本地化界面中显示英语字符串，因为缺少翻译。 更新的`com.adobe.granite.platform.i18n`包提供它们。 (NPR-44479)
* 在&#x200B;**工具** > **操作** > **诊断**&#x200B;下的用户同步诊断工具中的字符串现在以用户的语言显示。 以前，该工具在本地化界面中显示英语文本。 更新的`com.adobe.granite.platform.i18n`包提供翻译。 (NPR-44481)
* 配置流现在以用户的语言显示用户友好的错误消息。 以前，AEM配置页面中的故障会产生技术文本或未翻译文本。 更新的`com.adobe.granite.ui.content`包处理错误并提供本地化的消息。 (NPR-44840)
* 更改&#x200B;**安全性** > **组**&#x200B;中已删除组的属性时显示的错误消息现在以用户的语言显示。 以前，本地化界面的消息仍为英文。 更新的`com.adobe.granite.security.content`包提供翻译。 (NPR-44841)
* 错误消息“将更改保存到组时发生错误！” 现在在&#x200B;**安全** > **组** > **编辑组**&#x200B;控制台中以用户的语言显示。 以前，对于本地化的界面，消息以英语保留。 更新的`com.adobe.granite.security.content`包提供翻译。 (NPR-44842)
* 中文、日文和韩文字符不再以斜体显示在收件箱图标错误消息中。 以前，斜体样式会扭曲字符并使文本更难以阅读。 更新的`com.adobe.granite.ui.coralui3`包将删除这些语言的样式。 (NPR-44843)
* **操作** > **监控**&#x200B;中的数字现在遵循用户的区域设置格式。 以前，无论界面语言如何，页面都会以固定格式显示数字。 更新的`com.adobe.granite.monitoring.dashboard`包应用正确的分隔符和格式。 (NPR-44844)
* “Explain查询”选项卡现在显示“Query Builder Debugger工具”。 用户语言的链接。 以前，在本地化的界面中缺少链接文本，因为字符串未外部化。 更新的`com.adobe.granite.monitoring.dashboard`包将还原它。 (NPR-44845)
* Query Builder Debugger工具对话框中的文本现在以用户的语言显示在Explain Query选项卡上。 以前，由于多个字符串没有外部化，因此它们一直保留在英语中。 更新的`cq-platform-content`包提供翻译。 (NPR-44846)
* “一致性检查结果”页面中的文本现在以用户的语言显示。 以前，英语会显示多个字符串，因为它们未外部化。 更新的`com.adobe.granite.operations.ui.core`包提供翻译。 (NPR-44847)
* 监视图表现在以用户的语言显示月和周标签。 以前，标签使用英文硬编码，因此图表忽略了界面区域设置。 更新的`com.adobe.granite.monitoring.dashboard`包将字符串外部化，现在将显示翻译。 (NPR-44848)
* **安全** > **用户** > **创建**&#x200B;中的国家/地区下拉列表现在可以正确排序条目。 以前，某些语言的本地化国家/地区名称出现的顺序错误。 更新的`com.adobe.granite.security.content`包应用区域设置感知排序。 (NPR-44942)
* 按钮组件对话框中的工具提示现在以用户的语言显示。 以前，按钮文本、链接、图标、HTML ID和`aria-label`字段的信息文本仍为英文，即使本地化服务中存在这些字符串。 更新的字典在所有支持的区域设置中提供翻译。 (SITES-7579)
* 内容片段列表组件的“属性”部分中的工具提示现在以用户的语言显示。 以前，内容片段模型、标记、最大项数、父路径、排序顺序和排序依据字段的信息文本仍使用英文。 更新的字典为所有支持的区域设置提供翻译。 (SITES-14969)
* 模板编辑器中核心组件的帮助链接现在指向本地化的文档页面。 以前，在组件配置对话框中选择帮助会打开英语页面，而不管界面语言如何。 更新后的URL现在会将用户路由到与其区域设置相对应的页面。 (SITES-15058)
* 内容片段对话框中的信息工具提示现在以用户的语言显示。 以前，“单个文本元素”和“多个元素”模式以及“内容片段”路径的工具提示文本保留为英文。 更新的字典为所有区域设置提供翻译。 (SITES-17333)
* 模板编辑器组件策略编辑器中的错误消息现在以用户的语言显示。 以前，当作者编辑组件策略或创建新组件策略时，消息“资源{}不可修改”和“无法创建位于的节点”仍为英文。 更新的资源为所有支持的区域设置提供翻译。 (SITES-17475)
* 现在，当您从“图像”下拉列表中选择“段落”后，页面编辑器中的“Assets”选项卡会在“选择组件”下拉菜单中显示一个翻译的字符串。 以前，字符串“OTHER”显示为英文，因为本地化资源缺少它。 更新的词典在所有区域设置中提供翻译。 (SITES-21481)
* 页面编辑器配置组件对话框中的信息工具提示不再显示额外的换行符。 以前，PDF Viewer和进度条等组件的工具提示会笨拙地包裹在多个区域设置中。 工具提示现在可以正确换行，并且单词连字符按预期工作。 (SITES-38567)
* 工具提示“退出文本编辑器并按Esc键”现在以用户的语言显示在文本组件配置对话框中。 以前，字符串以英语显示，因为本地化资源缺少它。 工具提示现在翻译为所有区域设置。 (SITES-43186)
* 模板编辑器中的STRUCTURE标签现在以用户的语言显示。 以前，由于本地化资源中缺少字符串，因此在作者打开自适应表单模板时，标签仍为英文。 标签现在翻译为所有区域设置。 (SITES-43599)


#### MSM - 实时副本{#sites-msm-live-copies-6526}

* 升级后，“MSM转出”对话框会再次加载Live Copy列表。 以前，`AsyncOperationServlet.doGet`中的`NullPointerException`在旋转图标上停止了对话框，因此作者无法选择目标区域设置或开始转出。 更新的`com.adobe.granite.jobs.async`包处理缺少的作业数据并完成请求。 (SITES-43116)
* 再次从Blueprint页面上的可编辑工具栏转出。 工具栏操作失败，因为`MSM.Rollout`客户端库未加载，出现“无法读取未定义的属性（读取“doRollout”）”。 更新页面现在会加载库，因此转出作业将开始并对活动副本进行更改。 (SITES-46052)

* 批量停用Blueprint页面及其子页面时，不再发送重复的转出事件。 在一个请求中停用父页面及其子页面时，复制系统发出五个事件，而不是三个事件，并且每个子页面转出两次。 转出管理器中的重复数据删除现在每页提交一个转出，因此活动副本不会接收冗余包。 (SITES-44988)


#### 页面编辑器{#sites-pageeditor-6526}

* 滚动列表后，选定的样式在“页面编辑器样式选择”对话框中保持高亮显示。 以前，选中某个样式时会高亮显示该样式，但在单击滚动条时，该高亮会消失。 此回归开始于SP22之后，此时对话框将保持所选状态可见。 (SITES-30874)

* 当父组件和子组件定义不同的响应式断点时，作者可以在布局模式下编辑页面。 getResponsiveCssClasses函数以前在省略了cq:responsive/电话宽度的组件上因出现TypeError而失败。 函数现在回退到可用值，并继续渲染。 (SITES-46681)
* 现在，对于具有多个图像放置目标的组件，自定义裁切比可在混合内联编辑模式下加载。 以前，图像编辑器为所有放置目标初始化一个通用ipeConfig，因此编辑器只显示默认比率，并忽略每个目标的aspectRatios。 编辑器现在会读取选定放置目标的配置，并且裁切会同时应用于内联视图和全屏视图。 (SITES-45771)
* 在富文本编辑器中按Backspace键不会为文本添加额外的内联样式。 一位客户报告说，删除粗体文本后的换行符后，将style=&quot;font-size： 0.8125rem； background-color： transparent；&quot;添加到粗体标记中。 在最新的Service Pack上测试无法重现行为，因此无需更改。 (SITES-15883)


<!--
#### Replication{#sites-replication-6526}
-->


#### 富文本编辑器{#sites-rte-6526}

* 富文本编辑器工具栏按钮在响应式视图和布局模式下工作。 以前，单击按钮时会高亮显示这些按钮，但选定内容保持不变，并且不会打开任何对话框。 更新后的编辑器脚本将应用格式，并与“编辑”模式下的行为相匹配。 (SITES-44233)
* 作者可以在文本组件中添加货币和商标符号，而不会丢失它们。 “特殊字符”插件插入符号，但这些符号在编辑器和发布的输出中都显示为空白。 更正后的处理将按照输入的格式呈现每个符号。 (SITES-46532)
* 富文本编辑器工具栏中的全屏图标再次展开该编辑器。 以前，单击核心文本组件中的图标不会执行任何操作，并且编辑器会保持其内联大小。 现在，作者可以在内联和对话框编辑中为长格式内容使用集中的工作区。 (SITES-46396)


#### 站点管理员UI{#sites-admin-ui-6526}

将资产还原到早期版本现在会刷新其卡片缩略图。 时间轴客户端库中的URL编码更改导致路径不匹配，因此信息卡查找失败，缩略图仍然过时。 匹配编码路径和原始路径将恢复刷新。 (SITES-46590)

<!--
#### Universal editor {#sites-universal-editor-6526}
-->

#### 工作流扩展 {#sites-workflow-extensions-6526}

查看有效负载现在为管理发布启动多个页面的工作流打开Touch UI包编辑器。 以前，该操作会打开已弃用的经典UI包编辑器，即使作者在触屏UI中启动了该工作流也是如此。 作者现在无需离开触屏UI即可检查有效负载。 (SITES-40928)


### [!DNL Assets] {#assets-6526}

* 增强：AEM Assets 6.5支持创作AI内容符合“内容来源与真实性联盟”(C2PA)要求。 更新资产工作流可检测C2PA凭据、提取元数据并签名工作流重新生成的演绎版。 签名在每个AEM实例中本地运行，因此客户不需要专用的签名基础设施。 (ASSETS-75868)

* 文档增强：新的公共文档介绍了如何在保持C2PA合规性的同时自定义资产处理管道。 本文档介绍如何在呈现步骤之前定位检测C2PA凭据步骤，以及如何在每个AEM实例中本地运行签名。 本文档还说明了专用或客户拥有的签名基础架构的限制。 (ASSETS-76100)
* 现在，当您将鼠标悬停在AEM 6.5 SP26环境中的帮助下拉列表链接上时，shell标题中的帮助下拉列表保持打开状态。 以前，当指针进入列表时，下拉菜单关闭，因此作者无法单击文档、社区或支持链接。 更新的`com.adobe.granite.ui.content`包推迟了焦点检查，因此菜单仅在焦点真正离开时关闭。 (ASSETS-65676)

<!--
#### [!DNL Dynamic Media]{#assets-dm-6526}
-->

### [!DNL Forms]{#forms-6526}

* 新功能：支持富文本中的列表上的辅助功能标记。 以前，仅当模板遵循特定结构时，辅助功能标记树中才会显示列表标记。 该请求作为提供该功能的相关票证的副本关闭。 (LC-3923202)


<!--
#### Forms JEE {#forms-jee-6526}

#### Forms Designer {#forms-designer-6526}
-->


### 基础 {#foundation-6526}

* **安全** > **用户** > **创建**&#x200B;用户对话框中的“国家/地区”字符串现在以用户的语言显示。 以前，本地化界面的标签仍为英文。 更新的`com.adobe.granite.security.content`包提供翻译。 (NPR-43882)
* 现在，当您将鼠标悬停在AEM 6.5 SP26环境中的帮助下拉列表链接上时，shell标头中的帮助下拉列表会保持打开状态。 以前，当指针进入列表时，下拉菜单关闭，因此作者无法单击文档、社区或支持链接。 更新的`com.adobe.granite.ui.content`包推迟了焦点检查，因此菜单仅在焦点真正离开时关闭。 (NPR-44686)
* 改进： `HtmlLibraryManagerImpl`查询现在包含节点类型标记，以便查询始终使用预期的索引。 当服务找不到客户端库时，也会记录错误，从而提醒管理员存在此问题。 更新会颠覆Service Pack中的`com.adobe.granite.clientlibs`包版本。 (NPR-44698)


<!--
#### Apache Felix {#foundation-apachefelix-6526}
-->


#### 身份验证 {#foundation-authentication-6526}

现在，用户编辑器中的保存并关闭会返回到当前搜索的搜索结果。 以前，在作者在Omnisearch中搜索第二个用户、编辑属性并单击保存并关闭后，页面会打开第一个用户的属性。 更新的UserProperties.js脚本可恢复预期的导航。 (NPR-44774)

<!--
#### Campaign{#foundation-campaign-6526}

#### Cloud Services{#foundation-cloudservices-6526}

#### Communities {#foundation-communities-6526}

#### Content distribution{#foundation-content-distribution-6526}

#### Adobe CRX {#foundation-crx-6526}
-->


#### Granite{#foundation-granite-6526}

* Assets Omnisearch筛选器中的“内容片段模型”占位符现在显示为空。 以前，在转到Assets、单击过滤器或搜索图标，并展开内容片段模型字段后，文本会被截断。 更新后的样式为占位符提供了足够的空间。 (GRANITE-54387)
* 现在，将指针移到外壳标题的链接上时，该标题中的帮助下拉列表将保持打开状态。 以前，当指针进入“文档”、“社区”和“支持”链接的列表时，下拉菜单就会关闭，导致链接无法通过鼠标访问。 焦点处理程序现在将其检查延迟到下一个动画帧，因此悬停不再计为焦点离开菜单。 (GRANITE-70978)

<!--
#### Jetty{#foundation-jetty-6526}
-->

#### Launch集成{#foundation-launch-integrations-6526}

改进： Adobe Analytics与Adobe Experience Manager Launch的集成使用Analytics 2.0 API。 Analytics 1.4 API于2026年8月31日到达其生命周期结束日期。 迁移过程中，报表和Launch集成会在迁移日期之后继续工作。 （CQ-4365074和CQ-4365080）

<!--
#### Localization{#foundation-localization-6526}

#### Oak {#foundation-oak-6526}
-->

#### 平台{#foundation-platform-6526}

* AEM登录页面页脚中的帮助链接现在会打开一个工作页面。 以前，该链接指向的marketing.adobe.com URL不再存在。 页脚配置现在使用[Adobe Experience Manager文档](https://experienceleague.adobe.com/en/docs/experience-manager) URL。 (NPR-44388)
* 增强：AEM发送电子邮件时，某个客户请求使用Microsoft Graph API作为SMTP的替代方案。 该票证已解析为重复，因为另一个票证已实施图形API流。 带OAuth 2.0的SMTP仍然适用于需要离开SMTP基本身份验证的客户。 (GRANITE-57478)

* 在&#x200B;**工具** > **常规** > **配置**&#x200B;浏览器中，“有效权限”对话框中的字符串现在正确对齐。 以前，在您选择文件夹、单击“属性”并单击“有效权限”后，系统会显示一个乱排的字符串。 更新后的布局规则可恢复对齐方式。 (CQ-4359166)


#### 项目 {#foundation-projects-6526}

现在，选择i18n词典对话框中的“选择根目录”字符串已完整显示。 以前，在创建翻译项目并添加i18n词典后，会在多个本地化的界面中截断文本。 更新的`cq-projects-translation-content`包为字符串提供了足够的空间。 (CQ-4355405)

<!--
#### Security{#foundation-security-6526}

#### Sling{#foundation-sling-6526}

#### SPA editor {#foundation-spa-editor-6526}
-->


#### 翻译{#foundation-translation-6526}

列表组件的样式选项现在以用户的语言显示。 以前，在作者将List组件添加到体验片段后，诸如块和网格之类的字符串在“样式”菜单中保留为英文。 更新后的资源可提供翻译，包括朝鲜语、简体中文和繁体中文界面。 (CQ-4349666)

<!--
#### User interface{#foundation-ui-6526}

#### WCM{#foundation-wcm-6526}
-->

#### 工作流{#foundation-workflow-6526}

改进：触屏UI页面编辑器现在呈现内容树，并支持在工作流包页面上编辑资源定义组件。 以前，**管理发布** > **稍后发布**&#x200B;创建的`/etc/workflow/packages/`下的页面在左侧面板中未显示内容树，作者无法编辑资源定义组件。 审批者现在可以在触屏UI中检查工作流有效负载中的页面和资产，这与经典UI行为相匹配。 (GRANITE-65620)

## 安装 [!DNL Experience Manager] 6.5.26.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.26.0需要[!DNL Experience Manager] 6.5。 有关详细说明，请参阅[升级文档](/help/sites-deploying/upgrade.md)。<!-- UPDATE FOR EACH NEW RELEASE -->
* 服务包可通过 Adobe [软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.26.0.zip)下载。
* 在使用 MongoDB 且包含多个实例的部署中，请在其中一个作者实例上使用包管理器安装 [!DNL Experience Manager] 6.5.26.0。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe建议您不要删除或卸载[!DNL Experience Manager] 6.5.26.0包。 若要根据需要进行回滚，请在安装包之前创建`crx-repository`的备份。<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### 在 [!DNL Experience Manager] 6.5 上安装服务包{#install-service-pack}

1. 如果实例处于更新模式（即由早期版本升级而来），请在安装前先重启该实例。 如果实例已长时间运行，Adobe 建议先重启。

1. 在安装之前，请为您的 [!DNL Experience Manager] 实例创建快照或执行一次全新的备份。

1. 从[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.26.0.zip)下载Service Pack。<!-- UPDATE FOR EACH NEW RELEASE -->

1. 打开包管理器，然后选择&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传该包。 有关详细信息，请参阅[包管理器](/help/sites-administering/package-manager.md)。

1. 选择该包，然后选择&#x200B;**[!UICONTROL 安装]**。

1. 要更新 S3 连接器，请在安装服务包后停止实例，用安装文件夹中提供的新二进制文件替换现有连接器，然后重新启动实例。 请参阅 [Amazon S3 数据存储](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>在安装服务包过程中，包管理器 UI 中的对话框有时会意外退出。 Adobe建议您等待错误日志停止更改后再访问部署。 等待与卸载更新程序捆绑包相关的特定日志，然后确认安装成功。 此问题发生在[!DNL Safari]浏览器中，但有时也发生在任何浏览器中。

**自动安装**

您可以使用以下两种方法来安装 [!DNL Experience Manager] 6.5.26.0。<!-- UPDATE FOR EACH NEW RELEASE -->

* 当服务器在线时，将包放入 `../crx-quickstart/install` 文件夹中。 该包会自动安装。
* 使用[包管理器的 HTTP API](/help/sites-administering/package-manager.md#package-share)。 请使用 `cmd=install&recursive=true` 以便安装嵌套的包。

>[!NOTE]
>
>Experience Manager 6.5.26.0 不支持 Bootstrap 安装。<!-- UPDATE FOR EACH NEW RELEASE -->

**验证安装**

对于经认证可与此版本配合使用的平台，请参阅[技术要求](/help/sites-deploying/technical-requirements.md)。

1. 在[!UICONTROL 已安装的产品]下，产品信息页面（`/system/console/productinfo`）会显示更新后的版本字符串 `Adobe Experience Manager (6.5.26.0)`。<!-- UPDATE FOR EACH NEW RELEASE -->

1. 在 OSGi 控制台中，所有 OSGi 捆绑包均应处于&#x200B;**[!UICONTROL 活跃]**&#x200B;或&#x200B;**[!UICONTROL 片段]**&#x200B;状态（使用网页控制台：`/system/console/bundles`）。

1. OSGi 捆绑包 `org.apache.jackrabbit.oak-core` 的版本应为 1.22.20 或更高版本（使用网页控制台：`/system/console/bundles`）。<!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### 安装 [!DNL Experience Manager] Forms 的服务包{#install-aem-forms-add-on-package}

如需了解在 Experience Manager Forms 上安装服务包的操作说明，请参阅 [Experience Manager Forms 服务包安装说明](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)。

>[!NOTE]
>
>在 [AEM 6.5 快速入门](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/implementing/deploying/deploying/deploy)中谈及的自适应表单功能旨在仅作探索和评估用途。 由于自适应表单功能需要适当的许可，因此必须获得 AEM Forms 的有效许可证才能作生产用途。

### 为 Experience Manager 内容片段安装 GraphQL 索引包{#install-aem-graphql-index-add-on-package}

使用 GraphQL 的客户必须安装[带有 GraphQL 索引包 1.1.1 的 Experience Manager 内容片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip)。

这使您可以根据使用的功能添加所需的索引定义。

无法安装此包会导致GraphQL查询变慢或失败。

>[!NOTE]
>
>每个实例只需安装一次该包；无需在每次安装服务包时重新安装。

### UberJar{#uber-jar}

适用于 [!DNL Experience Manager] 6.5.26.0 的 UberJar 可在 [Maven Central 存储库](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.26/)获取。<!-- CHECK FOR UPDATE EACH NEW RELEASE FROM MADHULIKA SINGH -->

要在 Maven 项目中使用 UberJar，请参阅[如何使用 UberJar](/help/sites-developing/ht-projects-maven.md)，并在项目 POM 中包含以下依赖项：<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.26</version>
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

* [Universal Editor ](/help/sites-developing/universal-editor/introduction.md)，用于可视化编辑。
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
     `cache`和`diff-cache`的新文件夹是自动创建的，您在`error.log`中不再遇到与`mvstore`相关的异常。

* 更新使用内容模型的自定义API名称的GraphQL查询，以改用内容模型的默认名称。

* GraphQL查询使用`damAssetLucene`索引而不是`fragments`索引。 此操作导致GraphQL查询失败或需要很长时间才能运行。

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

  执行这些步骤后，GraphQL查询的执行速度得到了改进。

* 在尝试移动、删除或发布内容片段、网站或页面时，获取内容片段引用时会出现问题。 后台查询失败；功能无法正常工作。
为确保该功能正常运行，必须将以下属性添加到索引定义节点 `/oak:index/damAssetLucene`（无需重新索引）：

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* 如果您在 Java™ 11 上将 [!DNL Experience Manager] 实例从 6.5.0 – 6.5.4 升级到最新的服务包，可能会在 `error.log` 文件中看到 `RRD4JReporter` 异常。 要停止这些异常，请重新启动 [!DNL Experience Manager] 实例。<!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 用户可以重命名[!DNL Assets]中的文件夹并将嵌套文件夹发布到[!DNL Brand Portal]。 但是，在 [!DNL Brand Portal] 中，文件夹标题不会更新，直到重新发布根文件夹。

* 安装[!DNL Experience Manager] 6.5.x.x期间出现以下错误和警告消息：
  * 当在 [!DNL Experience Manager] 中使用 Target Standard API（IMS 身份验证）配置 Adobe Target 集成时，将体验片段导出到 Target 会导致创建错误的产品建议类型。 在 Target 中，系统不会创建类型为“体验片段”/来源为“Adobe Experience Manager”的产品建议，而是会创建多个类型为“HTML”/来源为“Adobe Target Classic”的产品建议。
  * `com.adobe.granite.maintenance.impl.TaskScheduler`：未在 `granite/operations/maintenance` 找到维护窗口。
  * 当在自适应表单中使用 SUM、MAX 和 MIN 等聚合函数时，服务器端验证失败（CQ-4274424）。
  * `com.adobe.granite.maintenance.impl.TaskScheduler`：未在 `granite/operations/maintenance` 找到维护窗口。
  * 通过 Shoppable Banner 查看器预览资产时，Dynamic Media 交互式图像中的交互热点不可见。
  * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]`：等待完成取消注册的注册变更时超时。

* 从 AEM 6.5.15 开始，由 `org.apache.servicemix.bundles.rhino` 捆绑包提供的 Rhino JavaScript 引擎引入了新的提升行为。 使用严格模式（`use strict;`）的脚本必须声明正确的变量。 否则脚本将无法运行，并会抛出运行时错误。

* 通过官方更新包安装与标记相关的标准内容会将`/content/cq:tags`节点的languages属性重置为默认值。 此操作适用于服务包、安全服务包、扩展功能包、累积功能包、补丁等。 因此，在安装之前，必须将其添加到属性。

### AEM Sites 已知问题 {#known-issues-aem-sites-6526}

<!--
* Known issue with a hotfix available for AEM Foundation {#known-issue-foundation-hotfix-6526}

  After you upgrade from an earlier service pack to Experience Manager 6.5.26.0, the OSGi version ordering for CRXDE Lite can prevent Experience Manager from selecting the intended bundle. An earlier service pack contains a higher CRXDE Lite version than the artifact that Service Pack 26 includes (`com.adobe.granite.crxde-lite-1.1.44-CQ651-B00024`).
  
  To resolve this issue, download and install the hotfix [cq-6.5.26-hotfix-GRANITE-76725.zip](https://artifactory.corp.adobe.com/ui/native/maven-aem-release-local/com/adobe/cq/hotfix/cq-6.5.26-hotfix-GRANITE-76725/1.0/cq-6.5.26-hotfix-GRANITE-76725.zip). The hotfix updates CRXDE Lite to `com.adobe.granite.crxde-lite-1.1.44-CQ651-B0026`, and it contains a version change only, with no code or functional changes. (GRANITE-76725)
-->

* 内容片段预览在处理大型片段树时因 DoS 防护而失败。 请参阅[关于默认 GraphQL 查询执行器配置选项的知识库文章](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-kcs/kbarticles/ka-23945)（SITES-17934）

### AEM Forms 已知问题 {#known-issues-aem-forms-6526}

* 将包含使用`bindref`的&#x200B;**文件附件**&#x200B;字段的表单提交给具有&#x200B;**分配任务**&#x200B;步骤的AEM Workflow时，附件未显示。 因此，当任务从“收件箱”中打开时，它们不会显示。 文件将正确地保存到存储库，但分配任务步骤UI无法显示附件。 (FORMS-23722)

* 将经过数字签名的PDF附加到AEM Forms JEE Workspace中的任务后，上传状态将持续停滞或出现“文件无效”错误而失败。 因此，无法将较大的已签名PDF附件添加到任务中。 此问题已在更高版本中修复。 有关该版本的修补程序，请与Adobe支持部门联系。 (FORMS-28517)

#### 可用修补程序的已知问题 {#aem-forms-issues-with-hotfixes}

以下问题已提供可下载并安装的热修复补丁： 您可以通过[下载并安装热修复补丁](/help/release-notes/aem-forms-hotfix.md)来解决这些问题：

* 安装AEM Forms JEE Service Pack 21 (6.5.21.0)后，如果在`<AEM_Forms_Installation>/lib/caching/lib`文件夹下找到Geode Jar `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)`的重复条目，请执行以下步骤，以解决问题(FORMS-14926)：

  1. 如果定位器正在运行，请先停止定位器。
  1. 停止 AEM 服务器。
  1. 进入 `<AEM_Forms_Installation>/lib/caching/lib`。
  1. 移除所有 Geode 补丁文件，仅保留 `geode-*-1.15.1.2.jar`。 确认仅存在 `version 1.15.1.2` 的 Geode jar。
  1. 在管理模式下打开命令提示符。
  1. 使用 `geode-*-1.15.1.2.jar` 文件安装 Geode 补丁。

## 已包含的 OSGi 捆绑包和内容包{#osgi-bundles-and-content-packages-included}

以下zip文件包含文本文档，其中列出了此[!DNL Experience Manager] 6.5 Service Pack版本中包含的OSGi包和内容包：

* [Experience Manager中包含的OSGi包列表6.5.26.0](/help/release-notes/assets/65260-bundles.zip)
<!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager中包含的内容包列表6.5.26.0](/help/release-notes/assets/65260-packages.zip)
<!-- UPDATE FOR EACH NEW RELEASE -->

## 受限网站{#restricted-sites}

这些网站仅对客户开放。 如果您已是客户并需要访问权限，请联系您的 Adobe 客户经理。

* [从 licensing.adobe.com 下载产品](https://licensing.adobe.com/)
* [联系 Adobe 客户支持部门](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience#)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 产品页面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 文档](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65)
>* [订阅 Adobe 产品更新早知道](https://www.adobe.com/cn/subscription/priority-product-update.html)




