---
title: ' [!DNL Adobe Experience Manager] 6.5 发行说明'
description: 查找  [!DNL Adobe Experience Manager] 6.5 的版本信息、新增功能、安装操作方法和详细更改列表。
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: f2c92b990a5c09cbcf532e0800e264620d98af77
workflow-type: tm+mt
source-wordcount: '10136'
ht-degree: 20%

---

# [!DNL Adobe Experience Manager]6.5 最新服务包发行说明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!--
DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section.
-->

## 发行版信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.24.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 类型 | 服务包发行 |
| 日期 | 2025年11月26日<!-- UPDATE FOR EACH NEW RELEASE --> |
| 下载 URL | [软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.24.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

<!--
OLD DOWNLOAD URL
(https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip)
-->

## [!DNL Experience Manager] 6.5.24.0 的内容 {#what-is-included-in-aem-6524}

[!DNL Experience Manager] 6.5.24.0 包含新功能、客户重点要求的增强功能以及错误修复。 还包括自 2019 年 4 月 6.5 首次发布以来推出的在性能、稳定性和安全性方面的改进。 [在 [!DNL Experience Manager] 6.5 上安装此服务包](#install)。

<!-- UPDATE FOR EACH NEW RELEASE -->


## 主要功能和增强功能

### Forms

* **支持传递自定义XCI：**&#x200B;添加了对在命令行应用程序xmlformcmd的参数中传递自定义XCI的支持。 此功能允许用户指定用于测试的自定义XCI文件，增强测试过程的灵活性和控制力。 （LC-3923248）


## 服务包 24 中已修复的问题 {#fixed-issues}

<!-- 6.5.24.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Assets] {#assets-sp24}

* 更新到版本6.5.23.0后，在卡片视图中按修改日期对文件夹排序，导致难以为内部部署查找最近修改的资源。 (Assets-56946)
* 在调度程序执行期间会生成重复的警告日志条目。 (Assets-52554)
* 标题排序在列表视图中不起作用。 (Assets-50716)
* 即使单击取消按钮，“收藏集属性”窗口也不会关闭。 (Assets-48504)

* 尝试在AEM 6.5.22中为资源添加注释时出现&#x200B;*无效URL*&#x200B;错误。 （NPR-42684）
* 执行相关或取消相关操作后，Assets元数据编辑器表单不会重新初始化。 (Assets-52207)
* 当资产从远程DAM重新同步到本地站点时，资产的发布状态错误地更新为`Not published`。 （Assets-48958）
* 从SP23升级到6.5 LTS版本时遇到问题。 (Assets-50541)

### [!DNL Sites]{#sites-6524}

#### 辅助功能 {#sites-accessibility-6524}

* **切换显示格式**&#x200B;对话框现在支持全键盘操作。 焦点不再跳过&#x200B;**查看设置**&#x200B;按钮，标准键(`Tab`、`Enter`、`Space`)始终工作。 （SITES-24306）
* 键盘用户无需鼠标即可删除已发布的状态标记。 焦点位于每个标记上，激活可与`Enter`/`Space`和Backspace/Delete配合使用。 标记控件的行为现在类似于按钮，可改善屏幕阅读器的反馈并符合WCAG 2.1.1键盘要求。 （SITES-24491）
* 筛选器边栏在狭窄视区响应式重排。 选择控件和结果以400%缩放保留在视区中，从而消除水平滚动和内容截断。 （SITES-24708）
* AEM恢复对ContextHub“重置”、“角色”和“设备”按钮的完全键盘访问权限。 Tab键和箭头键可访问每个控件，显示可见的焦点指示器，并使用`Enter`或`Space`激活操作。 屏幕阅读器会朗读清晰的标签。 （SITES-24939）
* 日期输入和选取器在320像素处保持完全可见。 时间扭曲模式使用响应式大小调整，因此控件不再在最小视区上剪切或消失。 （SITES-24962）
* 引用边栏现在支持400%浏览器缩放，且不会失去对其内容的访问权限。 边栏使用响应式大小调整而不是固定的宽度，因此在1280×1024时，项目保持可见和可选择。 （SITES-24972）
* 筛选器边栏现在以400%缩放工作。 边栏会使用相对单位调整大小，并且不再阻止或隐藏过滤器控件。 用户可以查看和选择每个过滤器选项，而无需水平滚动或剪切点击目标。 （SITES-24981）
* 键盘用户可以在Teaser模式中操作格式菜单。 按&#x200B;**列表**&#x200B;或&#x200B;**段落格式**&#x200B;上的`Enter`或`Space`可打开弹出窗口、箭头键导航选项，而`Enter`可应用选择。 `Escape`关闭菜单并将焦点恢复到触发控件，生成一致的工具栏工作流。 （SITES-25235）
* 现在，“色板”拾色器弹出窗口位于视区内，即320像素。 弹出框显示所有颜色行并支持滚动，因此作者可以在小屏幕上选择任何色板。 （SITES-25274）
* 人口统计工具栏下拉菜单现在完全可以使用键盘。 打开菜单会将焦点移动到第一个选项，使用箭头键导航列表，然后关闭Esc/Tab或前进而不将焦点转储到工具栏。 交互项使用正确的语义，以便NVDA和其他阅读器正确声明选项。 （SITES-25310）
* 在“内容”树中添加组件的方式与在AEM 6.5 SP24上设计的一样。 错误初始错误来自本地设置中缺少作者权限，而不是AEM。 具有编辑权限的作者可以通过键盘或鼠标激活按钮并添加组件。 （SITES-25312）
* “人口统计”工具栏中的键盘和屏幕阅读器访问现在可以可靠地工作。 使用NVDA的作者可以使用箭头遍历&#x200B;**Commerce**、**角色**&#x200B;和88，观察清晰的焦点反馈，并了解哪个选项卡处于活动状态。 （SITES-25326）

* 现在，**跳至内容**&#x200B;链接将键盘焦点移至主内容标题。 焦点在唯一标识的目标上保持可见，因此屏幕阅读器会朗读正确的部分。 此更改符合WCAG 2.4.1和2.4.3。 （SITES-24061）
* 使用&#x200B;**全选**&#x200B;后，站点主页树中的键盘导航遵循逻辑顺序。 焦点从&#x200B;**全选**&#x200B;移动到下一个控件（左边栏打开），而不是跳回页面开头。 （SITES-24307）
* 站点编辑器中的区域标题和编辑控件对键盘焦点及激活作出响应。 键盘用户将显示与以前仅在悬停鼠标时显示的相同标题和操作。 （SITES-24479）
* 站点编辑器中的按钮显示描述性名称，而不是通用或缺少的标签。 辅助型技术会宣布正确的操作，从而提高清晰度并减少误击。 （SITES-24480）
* 在站点视图刷新时，屏幕阅读器会收到口语`Loading`消息。 更新会添加一个专用的状态实时区域，并以编程方式将消息写入其中，这样无需移动焦点即可确认进度。 （SITES-24481）
* Assets侧边栏现在包含一个清除&#x200B;**关闭**&#x200B;控件，并将焦点返回到切换按钮。 键盘和屏幕阅读器用户会立即关闭面板，而不是通过Tab键浏览每个控件。 此更改可减少击键次数，并匹配预期的面板行为。 （SITES-24489）
* 站点页面编辑器中的ARIA选项卡列表包含一个描述性名称。 屏幕阅读器现在将控件识别为选项卡列表并阅读正确的标签，使用户能够找到正确的选项卡集并在它们之间可靠地移动。 （SITES-24492）
* 编辑器侧边栏中的搜索现在会向屏幕阅读器公告结果。 当用户键入时，实时状态消息会报告匹配和更新的数量，而不会移动焦点。 键盘用户会立即发现结果。 （SITES-24506）
* 列表视图中的行选择可改进辅助技术用户。 复选框会显示从行Title派生的有意义的名称，因此公告会保持简短并正确描述操作。 （SITES-24514）
* 更正了列表视图辅助功能名称。 该表从非交互元素中删除`aria-label`，并将标签分配给可操作链接或按钮。 屏幕阅读器用户现在可以在整个列中听到准确、不重复的标签。 （SITES-24515）
* 使用高缩放期间，粘性标头停止遮蔽Teaser模式对话框。 在200%和400%缩放的情况下，内容保持可读性和可用性，具有垂直流量且没有剪切部分。 （SITES-24523）
* 在搜索字段中键入不再触发第一次结果的提前公告或意外激活。 体验现在会用结果计数公告简明的状态消息，而焦点仍保留在字段中，直到用户导航到列表。 （SITES-24658）
* 文本编辑器的超链接对话框中的替换文本字段现在会显示一个程序化标签。 屏幕阅读器将朗读该字段的`Alternative text`，并专注于正确命名的控件。 此修复改进了键盘和语音用户的导航。 （SITES-24675）
* 在引用边栏中添加了实时状态消息，以便辅助型技术立即宣布更改。 选择多个项目会触发有关引用可用性的明确消息，以防止静默状态更改并减少重复操作。 （SITES-24678）
* “图像”对话框现在通过ARIA实时区域宣布其加载状态。 屏幕阅读器在旋转图标出现时收听`Loading, please wait`消息。 此外，内容完成时可进行更新，以便用户了解他们何时可以交互。 （SITES-24697）
* 链接选择对话框现在会显示一个可公告搜索结果的实时区域。 屏幕阅读器在每次搜索后都能听到`results updated`状态，而无需移动焦点，因此用户可获得清晰的确认信息，确认搜索已完成。 （SITES-24700）
* 现在，“链接选择”对话框会以320像素重排。 所有字段和操作都保持可见且可用，并且不再显示水平滚动条。 （SITES-24709）
* 现在，“链接选择”对话框对屏幕上的文本和每个树项目上的辅助功能名称使用相同的标签。 屏幕阅读器在使用箭头键移动时朗读每个项目，包括最后一个级别，从而消除静默节点和错误名称。 （SITES-24710）
* 更改筛选器现在将其状态报告为展开或折叠。 该按钮与筛选器面板同步切换`aria-expanded`，并公开一个清除的名称(`Change filters`)，从而删除令人困惑的`filter?`公告。 屏幕阅读器用户可以预测激活控制的结果。 （SITES-24713）
* 模态标头不再包含宽度为320像素的内容。 标题会从其粘性状态中释放，并且对话框正文会滚动，因此所有字段和操作按钮都保持可见和可用。 键盘用户可以访问每个控件而不会失去焦点。 （SITES-24718）
* 应用程序导航链接现在会公开正确的链接语义。 屏幕阅读器将每个项目作为链接而不是列表项目进行通知，这改进了键盘导航和语音控制。 列表容器保留列表语义，而链接保留可聚焦的目标。 （SITES-24719）
* 筛选器更改时，结果状态现在会向屏幕阅读器公告。 NVDA同时读取`X of Y results`计数和`no results`消息。 分页状态使用就地更新的实时区域，因此用户无需移动焦点即可听到确认。 （SITES-24720）
* “轮播”对话框中的旋转按钮现在向屏幕阅读器宣布一个简洁的名称。 控件不再重复组标签和输入标签，这减少了NVDA用户的详细程度和混淆。 （SITES-24725）
* 帮助菜单搜索列表显示正确的语义。 容器会显示一个列表，每个结果都保留一个没有冲突角色的链接。 NVDA和JAWS可准确宣布链接，并且导航保持一致。 （SITES-24729）
* Adobe修复了“用户首选项”中的颜色样本弹出窗口，因此NVDA会公告焦点中的样本，而不是之前选择的样本。 键盘用户在浏览列表时听到准确的颜色名称，并且可以确认正确的选择。 （SITES-24739）
* NVDA现在会读取Tree目录中的完整说明。 详细信息面板会将多行文本公开为一个值，并将其链接到字段标签。 键盘用户在通过只读字段按Tab键时听到完整的文本。 （SITES-24780）
* 树目录现在会宣布“修改日期”。 NVDA读取焦点移至“已修改”列中的日期。 网格将每个日期与项目名称绑定，以便用户能够听到文件及其上次更新。 （SITES-24782）
* 预览模式现在遵循用户文本间距首选项。 画布反映所有预览内容中的字母、单词和行高变化。 当间距增大时，文本不再保持固定或剪辑。 键盘和视力缺佳的用户读取内容时不会出现布局中断。 （SITES-24936）
* AEM在Assets编辑器页面上更正选项卡顺序。 Tab键现在从标题控件移至联系人中心按钮，最后以清晰的顺序移至画布工具。 屏幕阅读器遵循相同的顺序，这消除了混淆并加快了键盘导航。 （SITES-24937）
* AEM会在“卡片操作”菜单栏中添加一个程序化名称。 屏幕阅读器可正确朗读控件，语音用户可按名称定向控件。 键盘导航和焦点保持不变。 （SITES-24938）
* 卡片视图菜单采用增加的文本间距。 “更多操作”项目会增大，且不再截断标签，包括“快速发布”。 提高字母、单词或行距的用户保留完整的标签和键盘访问权限。 （SITES-24941）
* 已从辅助功能树中删除隐藏站点主页表的`presentation`角色。 该表再次正确读取。 NVDA和JAWS在行和列导航期间检测表、识别标题并声明标题关系。 （SITES-24942）
* 在列表视图中排序反馈是明确且一致的。 排序后，标头通过`aria-sort`公开顺序。 它会宣布更改，而未排序的标题将不再声明状态，从而帮助屏幕阅读器用户跟踪哪个列控制排序。 （SITES-24943）
* 编辑布局标题不再显示不工作的&#x200B;**编辑**&#x200B;按钮。 该控件现在充当静态状态标签并退出Tab键顺序，因此键盘用户不会浪费击键。 使用&#x200B;**选择其他模式**&#x200B;以更改模式，并清除屏幕阅读器反馈。 （SITES-24950）
* 默认情况下，模拟器工具栏会显示完整的设备名称。 标签在加载时不再截断，因此用户无需猜测即可读取和选择设备。 文本在缩放级别和窄宽度之间均匀缩放。 （SITES-24952）
* 模拟器工具栏适合小型视区。 设备为320像素，无需剪辑即可列出并控制显示，因此用户可以选择Galaxy S7和更新的型号。 布局可缩放和换行，以避免即使在400%缩放时水平滚动。 （SITES-24953）
* 屏幕阅读器在模拟器中朗读选定的设备及其测量。 NVDA停止读取标尺流；设备按钮使用附加的工具提示文本描述，从而减少噪音并引导导航。 （SITES-24955）
* 过滤器栏现在将每个选定的标记视为操作按钮。 Clear accessible names and focus handling improve announcements and keyboard control. （SITES-24980）
* Status updates in the Sites Admin filter view announce to screen readers. When users switch Card/List while items load, NVDA now speaks the `Please wait` message through a live region. This guidance prevents extra clicks and confusion. （SITES-24992）
* Keyboard focus now moves in a logical order when users expand the left rail. Focus shifts directly from the left rail button to the expanded content, eliminating the need to backtrack or skip elements. This change improves accessibility for screen reader and keyboard users. （SITES-24998）
* Screen reader feedback for the **Edit** button now matches the control. Activating the button announces the Edit action rather than a preview message, which improves clarity and reduces input errors for non-mouse users. （SITES-25208）
* The confirm action in the Teaser dialog box announces correctly to screen readers. The control reports `Confirm` not the icon description, giving keyboard and screen-reader users clear guidance. （SITES-25223）
* The Help button now exposes a clear accessible name. Screen readers announce `Help` instead of a verbose icon description. Users understand the action and can find assistance faster. （SITES-25224）
* The Timewarp modal displays a clear focus ring on the **`Set Date`** and **Exit Timewarp** links. Users who tab see exactly where the focus lands and avoid unintended actions. The ring maintains at least 3:1 contrast against the background. （SITES-25232）
* Screen readers now announce the Annotate and Close Annotate controls accurately in the Annotation toolbar. NVDA no longer says `Preview button pressed,` which misled authors and suggested the wrong action. The announcement matches the button pressed and keeps the workflow clear. （SITES-25234）
* Keyboard navigation in the annotation toolbar behaves consistently. Focus no longer jumps to Exit when opening the mode and instead moves to the starting control for adding annotations. Users navigate the controls in sequence without reverse tabbing. （SITES-25241）
* Small-screen viewing works as expected in the Teaser modal. The dialog box no longer creates a horizontal scroll bar at 320 px, and the toolbar stays accessible without panning sideways. 此更新可帮助缩放页面的弱视用户。 （SITES-25242）
* 小屏幕查看功能在图像模式中按预期工作。 该对话框不再创建320像素的水平滚动条，并且图像工具保持可访问状态而不会侧移。 此更新改进了缩放页面的弱视用户的导航。 （SITES-25244）
* 搜索模式采用用户文本间距设置。 提高行高、段落间距、字母间距或字间距不再截断文本或与树重叠。 内容在WCAG 1.4.12值处重新流动并保持完全可读。 （SITES-25245）
* 现在，搜索模式可适应小屏幕，而不会与树目录（320像素）重叠。 内容在对话框中重排，仅保持垂直滚动，并保持控件可见。 此修复提高了可读性和键盘导航能力，并与WCAG Reflow保持一致。 （SITES-25246）
* 轮播模式溢出不再强制以手机大小的宽度进行水平滚动。 该组件可适应320像素，保持垂直流量，并保持控件处于可见状态。 这项更改改进了创作过程中的可读性和键盘访问权限。 （SITES-25254）
* 注释工作流不再失去焦点。 模式将初始焦点置于有意义的标题上，防止焦点跳出对话框，并在关闭对话框后将焦点恢复到触发条件。 屏幕阅读器输出保持简洁和相关。 （SITES-25257）
* **删除注释**&#x200B;对话框现在可以正确处理键盘焦点。 打开该对话框会将焦点移动到屏幕阅读器上下文的标题，关闭该对话框会将焦点发送回启动该对话框的&#x200B;**删除注释**&#x200B;按钮。 用户不再登陆不相关的控件或模式窗口。 （SITES-25258）
* 时间扭曲日期选取器现在可正确管理焦点。 按`Esc`将焦点返回到&#x200B;**日期选取器**&#x200B;按钮，选择日期会将焦点移动到链接的输入字段。 键盘和屏幕阅读器用户可保留上下文，并且不会落在模式窗口中。 （SITES-25264）
* 屏幕阅读器会朗读&#x200B;**注释**&#x200B;和&#x200B;**关闭注释**&#x200B;按钮的正确操作。 NVDA不再显示`Preview button pressed`；它会朗读按钮名称，以便用户了解注释模式何时开始或结束。 （SITES-25268）
* 注释模式现在显示清除&#x200B;**提交**&#x200B;操作。 作者可以添加注释并使用钢笔图标按钮提交它，也可以使用`Esc`关闭模式窗口，而无需猜测流量。 （SITES-25269）
* 注释条目包括显式操作按钮。 该对话框显示&#x200B;**提交**&#x200B;以保存注释，显示&#x200B;**取消**&#x200B;以关闭注释，键盘可通过辅助技术访问和通知。 作者无需再依赖单击对话框外部或仅按`Esc`即可完成。 （SITES-25281）
* 注释模式现在使键盘焦点位于叠加图及其工具栏上。 当作者按Tab键时，叠加后面的页面不再受到关注，因此用户保持定向并且无需跳转到底层内容即可导航注释。 （SITES-25282）
* 编辑布局中的设备选择器可按预期工作。 如果两个设备选项的宽度相似（例如，Galaxy 7旁边的iPhone 8 Plus），则选定按钮会显示工具提示以显示完整标签，而两个按钮均保持可见和可访问。 （SITES-25285）
* 在200%缩放时，编辑布局不再超出页面。 工具栏会完全呈现并在需要时显示水平滚动，从而恢复对弱视用户以前隐藏的控件的访问。 （SITES-25288）
* 布局预览中的选项卡顺序现在从主工具栏直接移动到人口统计工具栏。 键盘和屏幕阅读器用户可以按可预测的顺序遍历控件，而不是跳转到辅助工具栏。 此更改与WCAG 2.4.3的焦点顺序一致。 （SITES-25305）
* 将页面缩放为200%不再隐藏“人口统计”工具栏的一部分。 工具栏部分管理溢出，并在其自己的区域提供滚动，使每个控件在高放大率下可见且可操作。 （SITES-25309）
* “人口统计”工具栏中的文本输入现在会公开适当的可访问名称。 每个字段都包含一个带有程序化标签的唯一ID，因此屏幕阅读器会朗读字段的用途，用户可以按标签导航。 可见标签位于控件附近，以改善弱视可读性。 （SITES-25316）
* 现在，编辑按钮在辅助工具栏中向屏幕阅读器宣布正确的操作。 激活它可读取`Edit`而不是不相关的`Preview button pressed,`，这样可在键盘导航期间消除混淆。 （SITES-25320）
* 人口统计工具栏购物车滑块现在会显示一个适当的可访问名称。 屏幕阅读器将朗读`Cart total`，语音输入工具可以按名称定位控件，从而改善对WCAG 4.1.2（名称、角色、值）的合规性。 （SITES-25322）
* 现在，当作者使用箭头键更改值时，人口统计工具栏滑块会保持焦点。 焦点不再跳转到“购物车”按钮，因此键盘用户不断调整值，屏幕阅读器会朗读每次更改。 （SITES-25324）
* 搜索Assets时现在可干净地重排320像素（缩放约400%）。 The modal keeps headings, fields, and actions readable and non-overlapping, so authors can search without horizontal scrolling. （SITES-25330）
* The Assets panel in the editor follows a logical focus sequence. Keyboard users tab across each thumbnail and can access the panel exit controls. The change removes skips and improves compliance with WCAG 2.4.3. （SITES-25360）
* AEM updates the **Lists** and **Paragraphs** buttons in the Teaser modal&#39;s rich text editor to expose their expanded and collapsed state. The buttons now toggle `aria-expanded` and announce the state change to screen readers. Authors get clear feedback and avoid guessing before opening or closing the format menus. （SITES-25365）
* AEM announces the loading state in the Teaser modal. The modal now exposes a live status message while content loads, so NVDA and JAWS speak `Loading, please wait.` Authors should receive clear feedback and avoid interacting with the dialog box before it is ready. （SITES-25366）
* Improves status messaging in the Asset tab of the Link selection dialog box. When an error occurs, the component injects a readable status update and keeps keyboard focus stable, letting NVDA/JAWS inform users right away. （SITES-25368）
* Corrected UI behavior in the Note panel for very narrow viewports. At 320 px, the title and Add control previously collided; the toolbar now reflows and preserves clear separation between elements. Authors can operate the controls without loss of information or function. （SITES-25376）
* Fixed a lingering error state in the **Teaser** dialog box&#39;s **Links &amp; Actions** tab. After authors enable **Call to Action** and correct blank or invalid fields, the tab clears its error styling and icon and removes `aria-invalid`. Screen readers no longer announce an error once the fields validate. （SITES-25527）
* Error handling in Sites Admin forms now meets accessibility expectations. When validation fails, the page shows the error immediately, shifts focus to a usable message target, and exposes the text to screen readers such as JAWS. （SITES-27138）
* Creating a folder in Sites now shows a clear confirmation toast. JAWS announces the message through the live region, so authors receive immediate, accessible feedback after the action. （SITES-27141）
* Fixed an accessibility gap where images in authoring dialog boxes rendered without alt text. The dialog box now provides descriptive alt text where needed and empty alt for purely visual elements, restoring compliant behavior for JAWS and other screen readers. （SITES-27153）
* Improved error handling in authoring dialog boxes. When a configuration error occurs, the UI shows explicit text and triggers a screen-reader announcement by way of an alert region. Authors receive immediate feedback and can correct the problem without losing context. （SITES-27155）
* Fixed a Reflow accessibility defect in Sites Admin. At 400% browser zoom, the toolbar and grid controls overlapped and pushed key actions off-screen, which blocked keyboard navigation and screen-reader use. The layout now reflows correctly so the search, filter, and action buttons remain visible and operable at 400% zoom. （SITES-27238）
* Corrected low contrast in the lock status message shown in the page Lock/Unlock workflow. The message now meets a 4.5:1 ratio, improving readability and ADA compliance for authors. （SITES-27270）
* Added accessible names to the checkmark icons in the **Effective Permissions** dialog box. JAWS now announces the icons and their meaning, improving keyboard navigation and ADA compliance. （SITES-27272）
* Hidden header navigation accepted focus and confused both sighted and screen-reader users. The update disables focus on collapsed controls and exposes only visible items. Navigation stays predictable and meets WCAG 2.4.3. （SITES-35224）

* Fixed the folder thumbnail icons in Sites Admin to behave as decorative images. The update removes the image role and applies empty alt text, so assistive technology ignores the icons and reads only meaningful labels. （SITES-2852）
* Adobe increased the color contrast for the References text in the Sites home page. The text now meets WCAG 2.1 AA with a ratio of at least 4.5:1 and reads clearly on light themes and bright screens. （SITES-24755）
* The References rail landmark now announces its name to screen readers. The region exposes a unique `aria-label` (`References rail`), which improves landmark navigation and distinguishes it from other regions. （SITES-24973）
* The Description RTE blocked forward Tab navigation and broke dialog flow. The fix restores standard keyboard movement. Authors continue past the field with a single Tab and keep the selection order predictable. （SITES-35228）
* Authoring controls lacked accessible names and exposed raw icon text, which confused JAWS. The fix adds explicit ARIA labels and standard roles. Announcements sound correct and align with accessibility expectations. （SITES-35227）
* The Categories drop-down list lacked a specific label, so JAWS spoke a generic `images button menu.` The update names the control `Categories` and defines its role. Screen-reader users hear an accurate label and understand the available choices. （SITES-35226）
* “属性”对话框显示一个数据网格，屏幕阅读器被视为纯文本。 JAWS和NVDA错过了焦点，并且无法宣告行和列。 此修复添加真正的表语义和ARIA角色。 屏幕阅读器现在可以识别表格并正确跟踪焦点。 （SITES-35225）
* 内容片段文本编辑器加载了截断的操作栏。 图标被剪切，溢出菜单变得不可访问。 更新修复了布局，以便完整工具栏保持可见和可访问。 （SITES-33005）
* 基本选项卡表单字段无法显示有用的错误文本。 该表单现在显示清楚的内联消息，并将它们链接到屏幕阅读器字段。 键盘和辅助技术用户将立即获得有关固定输入的指导。 （SITES-32480）
* 自定义组件中使用的多字段显示了未标记的图标按钮和一致的选项卡顺序。 JAWS/NVDA仅宣布`button`或跳过阻止键盘操作的控件。 该更新提供了添加、删除和移动的描述性名称，规范了制表位，并宣布了列表更新以满足ADA的期望。 （SITES-30660）
* “快速发布”现在会返回一个明确的成功通知。 对话框关闭，随后将显示一个祝酒词确认操作，屏幕阅读器将朗读该消息，这样作者就不会错过结果。 （SITES-26912）
* 无需更改。 Adobe审核了搜索图标与附近文本重叠的说法。 标头包含客户添加的标签；vanilla AEM仅呈现图标。 干净的实例以100%缩放显示正确的布局，因此错误已关闭为超出范围。 （SITES-26910）
* 创建页面主题不再隐藏焦点状态。 在键盘导航期间，水生样式和沙漠样式在&#x200B;**基本**&#x200B;选项卡和相邻选项卡上呈现一致的高亮。 此更改恢复了视力缺佳的用户的可预测、可感知的焦点反馈。 （SITES-26907）



#### 管理员用户界面{#sites-adminui-6524}

在&#x200B;**目录系统Blueprint**&#x200B;网格中，屏幕阅读器用户未收到导航帮助。 JAWS只是宣布了牢房的位置，然后就安静下来了。 此版本添加了辅助指南和角色，使JAWS能够读取列表上下文、选定项和所需的箭头/空格控件。 （SITES-30661）

#### 经典 UI{#sites-classicui-6524}

经典UI复选框丢失了标签并显示空白选项。 Dialog boxes also displayed encoded HTML such as `<br>`. The update restores checkbox labels and decodes markup, so dialog boxes read correctly. （SITES-31822）

<!--
#### [!DNL Content Fragments]{#sites-contentfragments-6524}
-->

#### [!DNL Content Fragments] - 管理{#sites-admin-6524}

Parentheses in a Content Fragment name caused the References panel to misreport usage. Authors saw 0 even when other fragments referenced it. The fix corrects the path parsing for `(` and `)` and surfaces the proper non-zero count and entries. （SITES-35078）


#### [!DNL Content Fragments] - 片段编辑器{#sites-fragments-editor-6524}

* Unpublish failed for Content Fragments whose DAM path contained parentheses. The Manage Publication wizard rewrote `(` and `)`, and broke the asset path. The fix preserves the characters and resolves the correct item, so the unpublish action completes. （SITES-35077）
* Editing a Content Fragment and going back to the Assets list hid the fragment or the whole folder. The list failed to refresh after closing the editor. The fix now refreshes the list reliably and keeps the edited fragment visible without a hard reload. （SITES-35374）

* Content Fragment Editor failed to open the Polaris Asset Selector because required IMS scopes were removed. The fix restores the minimal scopes and re-establishes the Delivery connection. Asset browsing and selection work again, without HTTP 500 errors. （SITES-35837）

#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6524}

After each deployment, valid GraphQL queries started returning `GraphQL_QueryValidationError`. The endpoint kept a stale schema until teams flushed caches or restarted. The fix refreshes the GraphQL schema and persisted-query registry during deployment, restoring normal responses immediately. （SITES-34301）

<!--
#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6524}


#### [!DNL Content Fragments] - REST API{#sites-restapi-6524}


#### Component Console{#sites-component-console-6524}


#### Core Backend{#sites-core-backend-6524}


#### Core Components{#sites-core-components-6524}


#### Campaign integration{#sites-campaign-integration-6524}
-->


#### ContentHub {#sites-contenthub-6524}

ContextHub no longer injects a second jQuery copy on publish pages. The segment-engine client library drops the cq.shared dependency that pulled jQuery 1.12.4, so sites load one consistent jQuery and front-end code works reliably. （SITES-30404）

#### 体验片段{#sites-experiencefragments-6524}

* Experience Fragments now localize the warning shown when no Adobe Target configuration exists. The message displays in the author&#39;s locale instead of English, so export and activation steps read correctly for global teams. （SITES-11868）
* Publishing an Experience Fragment variation now shows a localized error message when no cloud service attaches to the variation. The message appears in the UI in the user&#39;s language instead of an English-only string. （SITES-20293）
* Exporting an Experience Fragment to Target crashed with `Attempt to modify attribute at illegal index: -1`. Web vitals instrumentation conflicted with the exporter and corrupted attribute handling. The fix hardens attribute processing and removes that conflict. Exports succeed and the fragment renders in Target. （SITES-31891）

* Experience Fragment properties now localize the **References** tab. Labels and column headings such as `Page,` `Page path,` and `Variation title` show in the author&#39;s language. This change removes English-only strings and keeps the properties view consistent for global teams. （SITES-11203）
* The **Variations** > **Create workflow** now shows complete translation text. The dialog box handles long locale strings by wrapping and sizing content correctly, eliminating clipped or cut-off labels. （SITES-19304）
* Experience Fragment properties now localize the Social Media status labels. Authors see status values such as Posted and Not Posted in their selected language across all locales. This change removes English-only strings that caused confusion during review. （SITES-20014）

<!--
#### Foundation Components (Legacy){#sites-foundation-components-legacy-6524}
-->

#### 发布项{#sites-launches-6524}

* Deleting a very large Launch froze the repository. The job queued too many removals and starved other requests. The fix now batches delete and yields between chunks, so cleanup completes while the system stays responsive. （SITES-32004）

* Launch Configuration > Properties shows working Company and Property drop-downs. **Save** and **Close** honors completed fields, and the Title validation no longer triggers errors on Company or Property. （CQ-4359853）
* Required checks in IMS Configuration run on update, not only on creation. Empty values in fields like Client ID or Client Secret display an error and halt the save until a valid value is entered, preventing reuse of the prior value. （CQ-4359938）
* Launch creation shows translated validation and error strings. English-only messages for creation failures and missing source pages no longer appear. Authors see clear, locale-correct feedback during Launch setup. （SITES-13085）
* Launch promotion updates page properties `jcr:title`, `jcr:description`, and `cq:redirectTarget` on the source page. The change removes property exclusions in MSM rollout config and workflow logic. Campaigns, translations, and SEO keep consistent titles, descriptions, and redirects. （SITES-34509）
* The Launch action ignored scope and included pages that shared the same parent as the target section. The update enforces subtree boundaries and promotes only the chosen page and its descendants. 不相关的页面会保留其现有内容。 （SITES-34344）
* 修复了在创作处停止并跳过发布层的嵌套启动项自动提升。 子启动项的自动促销会将更新页面发布到配置的发布者，并按照计划完成完整启动。 （SITES-30420）

<!--
#### Link Checker{#sites-link-checker-6524}
-->

#### MSM - Live Copy{#sites-msm-live-copies-6524}

* 文件夹级别的转出无法在该文件夹下创建体验片段的活动副本。 单个转出有效，从而中断了批量工作流。 此更改使文件夹转出与页面行为保持一致，并在子树中传播关系和引用。 （SITES-35161）
* 删除Live Copy中的组件后，**启用继承**&#x200B;因JavaScript错误而中断，组件在第二次尝试之前一直丢失。 该更新修复了已删除后重新加载以携带正确的参数，并替换了过时的警报调用。 对话框会干净地打开，并且继承会在第一次尝试时恢复。 （SITES-31387）
* 转出向导接受了&#x200B;**稍后**，但没有日期。 作者已推进并创建转出，但没有计划。 更新强制进行日期选择并显示一个清晰的提示。 **Continue**&#x200B;操作在日期存在之前保持禁用状态。 （SITES-31374）


#### 页面编辑器{#sites-pageeditor-6524}

* 在具有Personalization容器的页面上打开内容树时，返回空面板和控制台空引用错误。 作者无法选取或配置组件。 更新将删除错误并重新启用树和组件交互。 （SITES-34336）
* AEM 6.5 SP23中断了页面编辑器中的模式切换。 单击&#x200B;**布局**、**开发人员**&#x200B;或&#x200B;**定位**&#x200B;导致编辑器卡在&#x200B;**编辑**&#x200B;模式下，并引发控制台`TypeError`。 更新将恢复工具栏模式更改并清除错误。 （SITES-34536）
* 当作者在长容器中添加组件时，页面编辑器会从插入点跳离。 更新调谐覆盖定时和滚动处理。 视图保持其位置，新组件保持可见状态并准备好进行配置。 （SITES-32621）
* 自定义标记标签在页面编辑器中失败，且UI始终显示`Tags.`。谓词现在先计算`fieldLabel`，再计算`labelText`秒，然后应用默认值。 作者可以看到他们设置的标签。 （SITES-32278）
* 取消站点中的“位置”筛选器会使OmniSearch图标未对齐，并与占位符文本重叠。 图标变得不可点击。 修复程序会重新对齐图标并恢复点击区域，因此鼠标和键盘都会触发搜索。 （SITES-30946）
* 选择“开发人员”将使页面处于不良状态，并阻止在该页面上创作。 面板消失且UI停止响应。 更新将修复模式切换逻辑和缓存处理，保持页面可编辑并立即显示开发人员数据。 （SITES-30922）
* 在&#x200B;**插入新组件**&#x200B;中单击&#x200B;**清除**&#x200B;未删除搜索查询，并将列表过滤为单个项（折叠）。 此修复会重置查询并刷新列表。 所有允许的组件都会再次显示。 （SITES-30921）

<!--
#### Replication{#sites-replication-6524}
-->

#### 富文本编辑器{#sites-rte-6524}

* 在全屏模式下，当不存在错误时，富文本编辑器会将拼写检查结果隐藏在对话框后面。 更新将结果面板放在前面，并保持消息和建议可见。 作者无需离开全屏即可查看和接受更正。 （SITES-32366）
* 富文本编辑器图像现在遵循所选对齐方式。 作者在“图像”对话框中设置“左”、“中”或“右”，编辑器在输出中始终应用该选择。 此更改还会稳定“替换文本”对话框，因此替换文本和对齐将保存并在重新编辑时保留。 （SITES-30634）

#### 通用编辑器 {#sites-universal-editor-6524}

配置查询令牌身份验证处理程序会使用户感到困惑，因为标签与字段不匹配。 UI从路径中提取文本并显示错误的名称。 此修复恢复了服务排名和查询令牌选项的清晰、准确的标签。 （SITES-31305）


### [!DNL Assets]{#assets-6524}


#### [!DNL Dynamic Media]{#assets-dm-6524}

* 现在，视频的&#x200B;**选择缩略图**&#x200B;选项在AEM Assets - Dynamic Media中可正常使用。 单击将打开对话框，并允许从Assets中选择缩略图，从而消除之前的死键行为并消除仅提取视频帧的限制。 (Assets-58926)


### [!DNL Forms]{#forms-6524}

<!--
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, December 4, 2025. In addition, a list of Forms fixes and enhancements is added to this section.
-->

#### Forms Designer

* 用户在特定测试用例中遇到无法单击超链接的问题，这会影响他们在应用程序中导航和验证链接的能力。 （LC-3923505）
* 用户在使用非拉丁语言的AEM Forms Designer 6.5.23生成的PDF中遇到可访问性问题。 路径标记未放置在工件容器中，导致PAC和屏幕阅读器检查失败。 （LC-3923295）
* 在使用输出服务从6.5.21版修补到6.5.23版后，用户在“可移植文档格式”(PDF)文本框中遇到断开的超链接问题。 （LC-3923290）
* 用户遇到记录文档(DoR)表单的辅助功能问题。 当输入字段为空时，屏幕阅读器仅读取字段标题，而不读取值，这使得残障用户难以有效地浏览表单。 （LC-3923234）
* 用户在DoR PDF forms中遇到辅助功能问题，其中NVDA错误地宣布了复选框、单选按钮和文本字段的`unavailable`。 该消息经常被重复，给屏幕阅读器用户造成混淆。 （LC-3923201）
* 用户在添加新字段时遇到XDP中的制表符订单差异。 现有选项卡顺序意外更改，影响表单导航。 （LC-3923183和LC-3922630）
* 用户遇到了HTML渲染问题。 使用`docReady`事件时，它未在HTML中正确触发，从而导致脚本无法按预期执行。 （LC-3923118）
* 用户遇到了PDF渲染脚本在AEM Forms Cloud生产环境中不起作用的问题。 (LC-3923082 )
* 用户遇到表单中浮动字段的问题。 使用不同的数据文件时，浮动字段在一个文件中正确呈现，但在另一个文件中无法正确呈现，尽管与字段无关的细微差别。 （LC-3923056）
* 在具有多个主页面的XDP（XML数据包）中，仅选择英语内容时，用户遇到空白西班牙语主页面。 （LC-3923009）
* 用户在AEM Designer中发现了过时的版权年份信息。 此错误出现在启动时的弹出框、`About`分区和`Legal Notices`分区中，显示`2003-2024`而不是“2003-2025”。 （LC-3923005）
* 用户在AEM Forms Designer中使用分页时遇到空白的PDF页面。 为WireAdviceHeader选择`Top of the Next Page/Top of Page`时出现问题，这会中断数据迭代的布局。 （LC-3922997和LC-3922830）
* 用户遇到了一个问题：可扩展标记语言(XML)架构定义(XSD)的文件摘要值未保留在AEM Forms Designer的64位版本中。 （LC-3922924）
* 用户在AEM Designer 6.5.19中遇到不稳定的超链接格式，其中文本框内的超链接错误地采用了周围文本的样式，例如第一个字符的格式。 （LC-3922376）
* 用户在使用HTML OSGI v6.5.22在Mac上通过移动渲染来渲染AEM Forms表单时遇到问题。 （LC-3923058）
* 用户在使用Designer 6.5.23创建并与PAC 2024分析的XDP模板中使用边界或后台字段时，遇到了“可移植文档格式(PDF)文件中的路径对象未标记”错误。 （LC-3923013）
* 用户在接收消息`path object not tagged.`时，遇到可移植应用程序组件(PAC)中标题`Dati Richiedente`的背景颜色错误(LC-3922912)
* 用户遇到了一个问题，特定模板将目标字体替换为精简字体。 （LC-3922330）

#### 自适应表单

* 用户遇到规则编辑器中缺少选项的问题。 当作者编写有关数字输入的规则时，查询、UTM和浏览器详细信息选项不可用。 （FORMS-21660）
* 用户在与OdataResponse交互时由于空指针异常而遇到应用程序崩溃的情况。 （FORMS-20344）
* 用户在创建规则以显示面板并将焦点置于面板内部的元素时遇到问题。 在可见性更新之前执行setFocus规则，会导致焦点操作失败。 （FORMS-19563）
* 用户在AEM Forms Author中遇到组件选择问题。 在编辑模式下在选项卡之间导航时，某些容器变为不可选，从而妨碍轻松识别和交互。 （FORMS-18525）
* 用户尝试在AEM 6.5.22中为资源添加注释时遇到`Invalid URL`错误。 （NPR-42684）

### 基础 {#foundation-6524}


#### Apache Felix {#foundation-apachefelix-6524}

更新了Felix Web控制台包以包含FELIX-6747。 此修补程序更正了以前在OSGi Web控制台中中断页面渲染和身份验证的响应处理。 控制台始终加载，不再在日志中抛出IllegalStateException条目。 （NPR-42730）

<!--
#### Campaign{#foundation-campaign-6524}

#### Cloud Services{#foundation-cloudservices-6524}

#### Communities {#foundation-communities-6524}

#### Content distribution{#foundation-content-distribution-6524}

#### CRX {#foundation-crx-6524}
-->

#### Granite{#foundation-granite-6524}

* 原始字符串或仅英文字符串不再出现在&#x200B;**删除访问控制**&#x200B;对话框中。 该对话框跨支持的语言显示完全本地化的内容，以实现一致的辅助功能。 （GRANITE-48479）
* “帮助”图标现在会显示辅助型技术的简要标签。 JAWS读取`Help button`并且不再添加多余的`menu`措辞。 此更新使控件符合WCAG 4.1.2，并简化了键盘和屏幕阅读器的使用。 （GRANITE-55360）
* 消除OSGi服务中的依赖性循环后，恢复HTL脚本引擎工厂。 环境启动干净，HTL渲染可在创作pod之间工作，管理员不再遇到启动失败或缺少脚本服务。 （GRANITE-58276）

* 标题搜索框不再叠加占位符文本上的放大镜图标。 占位符以适当的填充显示，并且在所有浏览器中保持完全可读。 （GRANITE-54391）
* 作者在自动完成字段中看到可读标签，而在对话框中看到原始值。 该实施使值保存在JCR中，并提高了动态提供选项的单选和多选配置的清晰度。 （GRANITE-57615）
* 当htmlLibraryManager.debug设置为true时，编辑模式将保持运行状态。 此更改将恢复正确的clientlib解析和加载，从而使开发人员能够在创作期间使用HTML Library Manager的调试工具。 （GRANITE-58002）
* 复制代理编辑页面在经典UI中不再引发JavaScript错误。 此时将打开页面，显示所有选项卡，并在没有控制台错误的情况下保存代理设置。 （GRANITE-58302）
* Corrected the health-status aggregation in System Overview. The view now updates after individual checks run and displays the right counts. Operators see `OK` when Security and Maintenance checks pass, instead of an incorrect `2 errors` banner. （GRANITE-61482）
* Stopped `CodeUpgradeTasks` from running during AEM 6.5 LTS (Long Term Support) upgrades. The upgrade now proceeds without task-triggered repository changes or reconfigurations. This fix reduces upgrade risk and prevents avoidable downtime. （GRANITE-61486）
* In authoring dialog boxes, required fields now show a single, accurate validation error. The message uses the field&#39;s own label when present, and falls back to a generic prompt when no label exists. Duplicate and mismatched messages across fields no longer appear. （GRANITE-59531）
* The page creation wizard dialog box now re-validates required fields on every interaction, including tab changes and multifield edits. The **Create** button stays disabled until authors complete all required inputs, and the wizard shows inline errors for missing values. （GRANITE-58826）

#### 集成{#foundation-integrations-6524}

Publishing AEM Target activities no longer fails when authors set start and end dates. The integration sends standards-compliant timestamps that include the time zone, so Target processes the activity payload and completes the sync as expected. （CQ-4360733）

<!--
#### Jetty{#foundation-jetty-6524}
-->

#### 本地化{#foundation-localization-6524}

* Localization in zh-CN removes an ambiguous phrase in the reference-gathering status shown during asset operations such as Move. The UI now displays `正在获取对 [[0]] 项的引用`, providing accurate meaning and consistent terminology. （CQ-4354648）
* Creating a smart collection no longer translates saved-search keywords on refresh. Authors who enter English terms see that those same terms are retained and the collection continues to return consistent results. （NPR-43158）
* Fixed truncated tooltip text in the Image panel. The `Display caption as pop-up` description renders completely in all supported locales, improving guidance for non-English authors. （SITES-10490）
* Sites Admin Column view truncated localized labels in French and Spanish. `End Time` and `Off Time` appeared truncated and showed no tooltip. Adobe corrected the translations and restored the tooltip on hover, so labels read in full. （SITES-31318）
* The **Move** dialog box in Sites showed raw i18n keys instead of readable labels. Items such as `Referencing pages,` `Created on,` `Created by,` and `Path` looked garbled. The fix hooks the dialog box to the correct dictionaries and supplies translations, with an English fallback. （SITES-30881）

<!--
#### Oak {#foundation-oak-6524}
-->

#### 平台{#foundation-platform-6524}

* 验证错误现在显示清晰的描述性文本，而不是仅显示一个图标。 屏幕阅读器在消息出现时自动朗读，因此用户无需导航到图标即可了解错误情况。 （CQ-4359152）


* 光标离开控件后，导航栏中的悬停标签不再保留在屏幕上。 UI会在模糊或鼠标移出后立即隐藏这些工具提示，从而防止出现视觉杂乱和误点击。 （CQ-4360030）
* 在Sites中，工具栏操作可停止在重复单击时创建第二个弹出窗口。 第二次单击将关闭现有弹出窗口，并且只保留一个实例可见，从而消除重叠和干扰。 （CQ-4360038）
* 过时的2024年版权文本不再显示。 登录页面和&#x200B;**帮助** > **关于AEM**&#x200B;弹出窗口显示2025，AEM以编程方式读取年份以避免手动编辑。 （CQ-4360042）
* 单击AEM标题栏中的工具提示时，将不再触发基础操作。 弹出窗口仅在用户单击实际按钮时打开，以防止在与工具提示文本交互时意外出现对话框。 （CQ-4360105）
* 年份滚动不再保留过时的版权文本。 登录屏幕和&#x200B;**帮助** > **关于AEM**&#x200B;对话框从系统时钟派生年份，并在每次UI加载时渲染最新值。 （CQ-4360173）
* 标题栏弹出窗口现在可正确切换。 单击同一操作（例如，**搜索**&#x200B;或&#x200B;**筛选器**）将关闭打开的弹出窗口，而不是打开另一个叠加图。 此更改可防止栈叠弹出窗口，并将焦点返回到标题控件。 （NPR-42891）
* 项目和收件箱日历视图将正确呈现。 切换视图不会再清空页面；日历将加载并显示计划项目。 （NPR-42968）

<!--
#### Security{#foundation-security-6524}
-->

#### Sling{#foundation-sling-6524}

* 修复了`org.apache.sling.scripting.jsp:2.6.0`包中出现的意外JSP编译错误。 （SLING-12442）
* 该平台将核心Sling引擎从2.16.2升级到2.16.6。 较新的引擎加强了输入验证，并在负载下稳定了请求处理。 （NPR-43105）

#### SPA编辑器 {#foundation-spa-editor-6524}

启用Sling主Servlet **检查Content-Type**&#x200B;覆盖操作会中断AEM 6.5 SP21/22中的`.model.json`导出。 由于导出程序翻转了类型中间链，请求返回了HTML或错误。 该修复从一开始就使用正确的类型发出JSON，因此`.model.json`适用于创作和发布环境。 （SITES-32634）


#### 翻译{#foundation-translation-6524}

* 为翻译项目状态添加了重新索引操作。 当状态视图不同步时，管理员可以重建后备索引，从而恢复结果并消除Oak遍历警告。 页面加载速度更快，且会显示当前作业状态。 （NPR-42699）
* 修复了XLIFF导入报告成功但JSON词典文件未更改的回归。 现在，导入的目标是正确的i18n路径并保留翻译，因此无需手动编辑即可完成本地化往返测试。 （NPR-42989）


* 翻译规则XML现在按配置工作。 翻译框架遵循异常规则，并在作业创建期间正确应用于`include`和`exclude`模式。 翻译请求不再发送排除的内容。 （NPR-42761）



#### 用户界面{#foundation-ui-6524}

* 修复了禁用“Adobe Stock许可证”对话框中的输入的UI回归。 该对话框现在行为正常，接受必填字段中的文本，并从“资产详细信息”视图中完成Stock资产许可流程。 （NPR-42748）

* 修复了创作环境中的组可见性。 “组”控制台不再在大约41个结果处停止，并返回每个用户的完整成员资格集。 此修复程序在累积修复后可恢复一致行为，并保持当前的安全强化。 （NPR-42749）


<!--
#### WCM{#foundation-wcm-6524}



#### Workflow{#foundation-workflow-6524}
-->




## 安装 [!DNL Experience Manager] 6.5.24.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.24.0需要[!DNL Experience Manager] 6.5。 有关详细说明，请参阅[升级文档](/help/sites-deploying/upgrade.md)。<!-- UPDATE FOR EACH NEW RELEASE -->
* 服务包可通过 Adobe [软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.24.0.zip)下载。
* 在使用 MongoDB 且包含多个实例的部署中，请在其中一个作者实例上使用包管理器安装 [!DNL Experience Manager] 6.5.24.0。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe 不建议移除或卸载 [!DNL Experience Manager] 6.5.24.0 包。 因此，在安装该包之前，您应创建 `crx-repository` 的备份，以便在需要时进行回滚。<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### 在 [!DNL Experience Manager] 6.5 上安装服务包{#install-service-pack}

1. 如果实例处于更新模式（即由早期版本升级而来），请在安装前先重启该实例。 如果实例已长时间运行，Adobe 建议先重启。

1. 在安装之前，请为您的 [!DNL Experience Manager] 实例创建快照或执行一次全新的备份。

1. 从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.24.0.zip)下载服务包。<!-- UPDATE FOR EACH NEW RELEASE -->

1. 打开包管理器，然后选择&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传该包。 如需了解更多信息，请参阅[包管理器](/help/sites-administering/package-manager.md)。

1. 选择该包，然后选择&#x200B;**[!UICONTROL 安装]**。

1. 要更新 S3 连接器，请在安装服务包后停止实例，用安装文件夹中提供的新二进制文件替换现有连接器，然后重新启动实例。 请参阅 [Amazon S3 数据存储](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>在安装服务包过程中，包管理器 UI 中的对话框有时会意外退出。 Adobe 建议您在访问部署之前，先等待错误日志趋于稳定。 在确认安装成功之前，请先等待与卸载更新捆绑包相关的特定日志出现。 通常，该问题会在 [!DNL Safari] 浏览器中出现，但也可能会在其他浏览器中间歇出现。

**自动安装**

您可以使用以下两种方法来安装 [!DNL Experience Manager] 6.5.24.0。<!-- UPDATE FOR EACH NEW RELEASE -->

* 当服务器在线时，将包放入 `../crx-quickstart/install` 文件夹中。 该包会自动安装。
* 使用[包管理器的 HTTP API](/help/sites-administering/package-manager.md#package-share)。 请使用 `cmd=install&recursive=true` 以便安装嵌套的包。

>[!NOTE]
>
>Experience Manager 6.5.24.0 不支持 Bootstrap 安装。<!-- UPDATE FOR EACH NEW RELEASE -->

**验证安装**

要了解与此版本兼容的已经过认证的平台，请参阅[技术要求](/help/sites-deploying/technical-requirements.md)。

1. 在[!UICONTROL 已安装的产品]下，产品信息页面（`/system/console/productinfo`）会显示更新后的版本字符串 `Adobe Experience Manager (6.5.24.0)`。<!-- UPDATE FOR EACH NEW RELEASE -->

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

适用于 [!DNL Experience Manager] 6.5.24.0 的 UberJar 可在 [Maven Central 存储库](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.24/)获取。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

要在 Maven 项目中使用 UberJar，请参阅[如何使用 UberJar](/help/sites-developing/ht-projects-maven.md)，并在项目 POM 中包含以下依赖项：<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.24</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar 和其他相关工件现已发布在 Maven Central 存储库，而非 Adobe 公共 Maven 存储库（`repo.adobe.com`）。 主 UberJar 文件已重命名为 `uber-jar-<version>.jar`。 因此，在 `dependency` 标记中不再包含以 `apis` 为值的 `classifier`。



## 已弃用和已移除的功能{#removed-deprecated-features}

请参阅[已弃用和已移除的功能](/help/release-notes/deprecated-removed-features.md)，以获取 AEM 6.5 中所有已弃用或已移除功能的详细列表。

### AEM Assets REST API中的内容片段支持 {#cf-support-assets-rest-api}

AEM 6.5 LTS SP2为内容片段和模型管理提供了现代化的OpenAPI，因此现已弃用AEM Assets REST API中的旧版内容片段支持端点。

Adobe打算在生命周期结束公告之前保持这些旧端点可用。 Adobe不计划为已弃用的端点提供进一步的增强功能。

### SPA 编辑器 {#spa-editor}

[从AEM 6.5版本6.5.24开始的新项目已弃用SPA编辑器](/help/sites-developing/spa-overview.md)。 SPA编辑器仍受现有项目的支持，但不应用于新项目。

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

* 在尝试移动、删除或发布内容片段、网站或页面时，获取内容片段引用时会出现问题。 后台查询失败。 也就是说，该功能无法正常工作。
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

### AEM Sites 已知问题 {#known-issues-aem-sites-6524}

内容片段预览在处理大型片段树时因 DoS 防护而失败。 请参阅[关于默认 GraphQL 查询执行器配置选项的知识库文章](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-kcs/kbarticles/ka-23945)（SITES-17934）

### AEM Forms 已知问题 {#known-issues-aem-forms-6524}

* **FORMS-14521**&#x200B;如果用户尝试预览包含保存的XML数据的草稿书信，则会陷入某些特定书信的`Loading`状态。
* **FORMS-16603**&#x200B;在交互式通信代理UI的打印预览中，某些计算值未正确显示。
* **FORMS-15681**&#x200B;在打印预览中查看信件时，内容已更改。 具体表现为：部分空格消失，某些字母被替换为 `x`。
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
>Avoid upgrading to Service Pack 6.5.24.0 for issues without an available hotfix. It may lead to unexpected errors. Upgrade to Service Pack 6.5.24.0 only after the required hotfixes are released.
-->

以下问题已提供可下载并安装的热修复补丁： 您可以通过[下载并安装热修复补丁](/help/release-notes/aem-forms-hotfix.md)来解决这些问题：

* **FORMS-23881**&#x200B;在使用6.5.23.0完整安装程序设置的AEM Forms JEE部署中，当调用中提供了自定义XCI文件时，输出服务无法处理请求。 要解决此问题，请从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)门户安装最新的AEM 6.5.24.0 Forms Service Pack。

* **FORMS-23789**（仅限JEE上的AEM Forms）：用户在JEE SP24上的AEM Forms中遇到Log4j问题，导致企业客户的日志记录和监视出现中断。 要解决此问题，请在JEE Service Pack 6.5.24.0上[下载并安装适用于AEM Forms的修补程序](/help/release-notes/aem-forms-hotfix.md)。

* **FORMS-23802**&#x200B;当表单位于具有旧版aem-forms-core-component (&lt;1.1.76)的站点页面中时，在预览或发布中无法加载自定义函数。 要解决此问题，请安装适用于SP24的[AEM Forms附加组件修补程序6.0.1454](/help/release-notes/aem-forms-hotfix.md)。

* **FORMS-23789**（仅限JEE上的AEM Forms）：用户在JEE SP24上的AEM Forms中遇到Log4j问题，导致企业客户的日志记录和监视出现中断。 要解决此问题，请在JEE Service Pack 6.5.24.0上[下载并安装适用于AEM Forms的修补程序](/help/release-notes/aem-forms-hotfix.md)。

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

* **FORMS-23703**&#x200B;如果未使用默认值配置`contains`规则时，自适应表单的服务器端验证失败。 您可以安装最新版本的[AEM Forms 6.5.24.0 Service Pack](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#aem-65-forms-releases)以修复此问题。

* **GRANITE-63681**&#x200B;表单数据模型连接器可能无法通过身份验证，因为默认情况下不允许使用所需的关键字和正则表达式模式。 要解决此问题，请从[链接](/help/release-notes/aem-forms-hotfix.md)下载并安装修补程序。

  <!--
  To resolve the issue, add the following via the Configuration Manager (`/system/console/configmgr`):

  * **Keywords:** `fdm-client-secret`, `oauth-client-secret`
  * **Regex:** `^\[/conf/[^/]+(/[^/]+)?/settings/dam/cfm/models/[^,\]]+(?:,/conf/[^/]+(/[^/]+)?/settings/dam/cfm/models/[^,\]]+)*\]$`

    >[!VIDEO](https://video.tv.adobe.com/v/3479697)
  -->

* **FORMS-23979** HTML-PDF转换(PDFG)可能会遇到间歇性超时。 随后发布了适用于SP24的较新版本的Forms加载项，其中包括此修补程序。 如果您遇到此问题，请将您的环境更新到6.5.24.0[&#128279;](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#aem-65-forms-releases)的最新发布的Forms加载项。

* **FORMS-23717**&#x200B;升级到&#x200B;**AEM Forms6.5.24.0**&#x200B;后，`server.log`和`error.log`可能会泛洪为重复的警告消息，例如&#x200B;*安全解析器工厂创建失败*&#x200B;或&#x200B;*不支持安全属性……*。 日志可能会以每秒&#x200B;**5到10行**（每小时数百兆字节）的速度增长，这会填充磁盘并阻止生产转出。

要减少日志卷，请在应用程序服务器配置中或通过JVM参数`-Dlogging.level.com.adobe.util.XMLSecurityUtil=ERROR`将`com.adobe.util.XMLSecurityUtil`的日志记录级别设置为`ERROR`。 此功能仅隐藏消息，不会修复根本原因。

* **FORMS-23875**&#x200B;在表单数据模型搜索中，即使不存在相关实体，也会在UI中显示HTML标记。 要解决此问题，请从[链接](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bb-expressionmanager-pkg-10.0.48.zip)下载并安装修补程序。

## 已包含的 OSGi 捆绑包和内容包{#osgi-bundles-and-content-packages-included}

以下文本文档列出了此 [!DNL Experience Manager] 6.5 服务包版本中包含的 OSGi 捆绑包和内容包：

* [Experience Manager 6.5.24.0 中包含的 OSGi 捆绑包列表](/help/release-notes/assets/65240-bundles.txt)
<!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.24.0 中包含的内容包列表](/help/release-notes/assets/65240-packages.txt)
<!-- UPDATE FOR EACH NEW RELEASE -->

## 受限网站{#restricted-sites}

这些网站仅对客户开放。 如果您已是客户并需要访问权限，请联系您的 Adobe 客户经理。

* [产品下载地址：licensing.adobe.com](https://licensing.adobe.com/)
* [联系 Adobe 客户支持部门](https://experienceleague.adobe.com/zh-hans/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience#)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 产品页面](https://business.adobe.com/cn/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 文档](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65)
>* [订阅 Adobe 产品更新早知道](https://www.adobe.com/cn/subscription/priority-product-update.html)

