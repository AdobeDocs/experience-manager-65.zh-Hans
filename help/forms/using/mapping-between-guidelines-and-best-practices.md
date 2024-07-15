---
title: 在Forms Designer中创建表单的准则和最佳辅助功能实践
description: 在Forms Designer中开发表单时辅助功能的最佳实践和准则。
feature: Adaptive Forms, Forms Designer
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 38fb132f0eb5b710745db11e7ddf59efc0f0ae95
workflow-type: tm+mt
source-wordcount: '3366'
ht-degree: 1%

---

# 准则与最佳实践之间的映射

以下部分将第508节和WCAG准则映射到本指南中描述的最佳实践。

## § 1194.21准则说明和最佳实践

### 第508节§1194.21：软件应用程序和操作系统

| § 1194.21准则 | 准则描述 | 合规性所需的LiveCycleDesigner最佳实践 | 注释 |
|-----------|-----------------------|-----------------------------------------------------------|-------|
| (a) | 当软件设计为运行在带有键盘的系统上时，产品功能应该通过键盘来执行，其中功能本身或执行功能的结果可以通过文本来辨识。 | <li> 2.7确保可使用键盘访问表单控件 </li><li> 2.6确保读取和制表符顺序正确</li> | |
| (b) | 对于已确定为辅助功能的其他产品，如果其辅助功能是按照行业标准开发和记录的，则应用程序不得中断或禁用这些功能的激活功能。 对于标识为辅助功能的任何操作系统，如果操作系统的制造商已记录用于这些辅助功能的应用程序编程接口，并且可供产品开发人员使用，则应用程序也不应中断或禁用这些操作系统的激活功能。 | 没有特定于Designer的LiveCycle技术 — 该指南由Adobe Reader处理，以供PDF forms使用。 | |
| (c) | 当输入焦点改变时，应当提供当前焦点在交互式界面元素之间移动的良好定义的屏幕指示。 焦点应以编程方式公开，以便辅助型技术可以跟踪焦点并关注更改。 | 2.3选择正确的控件为确保以编程和直观的方式显示焦点，请始终使用标准控件。 | |
| (d) | 辅助技术应提供有关用户界面元素的充分信息，包括元素的身份、操作和状态。 当图像表示项目群元素时，由图像传递的信息还必须以文本形式提供。 | <ul><li>2.1保持表单简单易用</li> <li>2.1.1避免移动、闪烁或闪烁内容</li> <li>2.2配置表单属性以生成辅助功能信息</li> <li>2.5为表单控件提供适当的标签</li></ul> | |
| (e) | 当使用位图图像来标识控件、状态指示器或其他编程元素时，分配给这些图像的含义在应用程序的整个性能中应保持一致。 | <ul><li>2.4为图像提供等效文本</li><li> 2.5为表单控件提供适当的标签此标准仅适用于您在表单上的多个位置使用同一图像的情况。 不建议使用基于图像的自定义控件。 请仅使用由LiveCycleDesigner提供的标准控件。 如果您在控件中使用了图像，请始终确保图像使用的一致性。</li> | |
| (f) | 文字信息应通过操作系统功能提供以显示文字。 应提供的最少信息是文本内容、文本输入插入符号位置和文本属性。 | 2.3选择正确的控件避免使用图像传递文本信息。 应始终使用标准控件，而不是使用自定义输入组件（该组件可能无法向操作系统正确显示文本属性）。 | |
| (g) | 应用程序不得覆盖用户选择的对比度和颜色选择以及其他单独的显示属性。 | 没有LiveCycleDesigner特定的技术 | 在可能的情况下，使用基本默认系统颜色。 |
| (h) | 当显示动画时，信息应可在至少一个非动画演示模式下根据用户的选择显示。 | 2.1保持表单简单且易于使用避免在表单中使用动画，或者提供将动画替换为静态图像的单独版本。 | |
| (i) | 颜色编码不得用作传达信息、指示行动、提示回应或区分视觉元素的唯一手段。 | 2.8负责任地使用颜色 | |
| (j) | 当产品允许使用者调整颜色和对比度设置时，应提供能够产生一系列对比度水平的多种颜色选择。 | 不适用 | 此功能通常由Adobe Reader提供，而不是由表单开发人员提供。 |
| (k) | 软件不得使用闪烁或闪烁的文本、对象或闪光或闪烁频率大于2 Hz且小于55 Hz的其他元素。 | 2.1.1避免移动、闪烁或闪烁内容 | |
| (l) | 使用电子表单时，表单应允许使用辅助技术的人访问填写和提交表单所需的信息、字段元素和功能，包括所有指示和提示。 | 2.5为表单控件提供适当的标签 | |

### 第508款§11942：网基内联网和因特网信息及应用

| §11942准则 | 准则描述 | 合规性所需的LiveCycleDesigner最佳实践 | 注释 |
|-----------|-----------------------|-----------------------------------------------------------|-------|
| (a) | 应提供每个非文本元素的等效文本（例如，通过“alt”、“longdesc”或在元素内容中）。 | 2.4为图像提供等效文本 | |
| (b) | 任何多媒体演示的等效替代方案应与演示同步。 | 2.12确保所有多媒体内容均可访问 | |
| (c) | 网页的设计应使所有通过颜色传递的信息也能无颜色地提供，例如从上下文或标记中提供。 | 2.8负责任地使用颜色 | |
| (d) | 文档应经过组织，以便可读，而无需关联的样式表。 | 不适用 | |
| (e) | 应为服务器端图像映射的每个活动区域提供冗余文本链接。 | 不适用 | |
| (f) | 应提供客户端图像映射而不是服务器端图像映射，除非区域不能用可用几何形状定义。 | 不适用 | |
| (g) | 应为数据表标识行和列标题。 | 2.9提供表格的标题单元格 | |
| (h) | 对于具有两个或多个行或列标题逻辑级别的数据表，应使用标记将数据单元格与标题单元格相关联。 | 2.9提供表格的标题单元格 | |
| (i) | 框架标题应为便于框架识别和导航的文本。 | 不适用 | |
| (j) | 应设计页以防止在频率大于2 Hz且小于55 Hz时导致屏幕闪烁。 | 2.1保持表单简单易用 | |
| (k) | 如果无法以任何其他方式实现遵从，则应提供具有同等信息或功能的纯文本页面，以使网站遵守本部分的规定。 当主页面发生更改时，纯文本页面的内容将进行更新。 | 不适用 | |
| (l) | 当页面使用脚本语言显示内容或创建界面元素时，脚本提供的信息应使用辅助技术可读取的功能文本进行标识。 | 2.11避免中断脚本编写 | |
| (m) | 当网页要求在客户端系统上存在小程序、插件或其他应用程序来解释页面内容时，该页面必须提供一个指向符合§1194.21(a)到(l)的插件或小程序的链接。 | 不适用 | 链接到PDF forms的网页应提供指向Adobe Reader的链接。 |
| (n) | 当电子表单设计为在线完成时，该表单应允许使用辅助技术的人访问完成和提交表单所需的信息、字段元素和功能，包括所有指示和提示。 | 2.5为表单控件提供适当的标签 | |
| (o) | 应提供一种允许用户跳过重复导航链接的方法。 | 2.10提供可导航表单结构 | |
| (p) | 当需要定时响应时，应向用户发出警报，并给予足够的时间以指示需要更多时间。 | 2.11避免中断脚本编写 | |

### WCAG 1.0优先级1检查点

| 检查点 | 检查点说明 | 合规性所需的LiveCycleDesigner最佳实践 | 注释 |
|------------|------------------------|-----------------------------------------------------------|-------|
| [1.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-text-equivalent) | 为每个非文本元素提供等效的文本（例如，通过“alt”、“longdesc”或在元素内容中）。 这包括：图像、文本的图形表示（包括符号）、图像映射区、动画(例如动画GIF)、小程序和程序化对象、ASCII艺术、框架、脚本、用作列表项目符号的图像、分隔符、图形按钮、声音（无论是否经过用户交互播放）、独立音频文件、视频的音频轨道和视频。 | <ul><li>2.4为图像提供等效文本</li> <li>2.12确保所有多媒体内容均可访问</li> | |
| [1.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-redundant-server-links) | 为服务器端图像映射的每个活动区域提供冗余文本链接。 | 不适用 | |
| [1.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-auditory-descriptions) | 在用户代理能够自动朗读视觉轨迹的等效文本之前，提供对多媒体呈现的视觉轨迹的重要信息的听觉描述。 | 2.12确保所有多媒体内容均可访问 | |
| [1.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-synchronize-equivalents) | 对于任何基于时间的多媒体呈现（例如，电影或动画），将等效的替代方案（例如，视觉轨迹的字幕或听觉描述）与呈现同步。 | 2.12确保所有多媒体内容均可访问 | |
| [2.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-color-convey) | 确保通过颜色传递的所有信息也无颜色可用，例如从上下文或标记中可用。 | 2.8负责任地使用颜色 | |
| [4.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-identify-changes) | 清楚地标识文档文本的自然语言和任何等效文本（例如字幕）的更改。 | 2.13确定语文的改动 | |
| [5.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-headers) | 对于数据表，请标识行和列标题。 | 2.9提供表格的标题单元格 | |
| [5.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-structure) | 对于具有两个或多个行或列标题逻辑级别的数据表，请使用标记将数据单元格与标题单元格相关联。 | 2.9提供表格的标题单元格 | |
| [6.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-order-style-sheets) | 组织文档，以便不使用样式表读取文档。 例如，在呈现不带关联样式表的HTML文档时，仍必须能够读取该文档。 | 不适用 | |
| [6.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-dynamic-source) | 确保在动态内容发生更改时更新动态内容的等效内容。 | 2.11避免中断脚本编写 | |
| [ 6.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-scripts) | 在关闭或不支持脚本、小程序或其他编程对象时，确保页面可用。 如果无法执行此操作，请在可访问的替代页面上提供等效信息。 | 2.11避免中断脚本编写 | |
| [7.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-flicker) | 在用户代理允许用户控制闪烁之前，请避免导致屏幕闪烁。 | 2.1保持表单简单易用 | |
| [9.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-client-side-maps) | 提供客户端图像映射，而不是服务器端图像映射，除非区域不能使用可用的几何形状进行定义。 | 不适用 | |
| [11.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-alt-pages) | 如果经过最大努力，您无法创建可访问的页面，并提供指向使用W3C技术的替代页面的链接，该页面可供访问，具有等效的信息（或功能），并且与不可访问（原始）页面的更新频率相同。 | 不适用 | |
| [12.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-frame-titles) | 为每一帧添加标题，以便于帧识别和导航。 | 不适用 | |
| [14.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-simple-and-straightforward) | 使用适用于站点内容的最清晰、最简单的语言。 | 2.1保持表单简单易用 | |

### WCAG 1.0优先级2检查点

| 优先级2检查点 | 检查点说明 | 合规性所需的LiveCycle最佳实践 | 注释 |
|------------|------------------------|-------------------------------------------------|-------|
| [2.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-color-contrast) | 当有人看到颜色有缺陷的人或在黑白屏幕上查看时，请确保前景色和背景色组合提供足够的对比度。 [图像的优先级2，文本的优先级3]。 | 2.8负责任地使用颜色 | |
| [3.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-use-markup) | 当存在合适的标记语言时，使用标记而不是图像来传递信息。 | <ul><li>2.1保持表单简单易用</li><li> 2.1.1避免移动、闪烁或闪烁内容</li> <li>2.2配置表单属性以生成辅助功能信息始终使用实际文本而不是文本的图像。</li> | |
| [3.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-identify-grammar) | 创建验证已发布的正式语法的文档。 | | PDF forms必须匹配已发布的PDF规范，才能在Adobe Reader中渲染。 |
| [3.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-style-sheets) | 使用样式表控制布局和演示。 | 不适用 | |
| [3.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-relative-units) | 在标记语言属性值和样式表属性值中使用相对单位而不是绝对单位。 | 不适用 | |
| [3.5](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-logical-headings) | 使用页眉元素来传达文档结构，并根据规范使用它们。 | 2.10提供可导航表单结构 | |
| [3.6](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-list-structure) | 正确标记列表和列表项。 | 2.10.3标记列表使用“列表”和“列表项”角色将基于列表的内容标记为列表。 | |
| [3.7](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-quotes) | 标明报价单。 请勿将引号用于格式效果，如缩进。 | 不适用 | |
| [5.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-table-for-layout) | 请勿将表用于布局，除非将表线性化后有意义。 否则，如果表没有意义，请提供替代等效项（可以是线性化版本）。 | 无特定的LiveCycle技术 | 没有理由在LiveCycle表单中使用表格进行布局。 相反，请使用布局面板来定位网格模式中的表单字段。 仅在利用表特定功能（如表标题）时使用表。 |
| [5.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-layout) | 如果表格用于布局，请勿将任何结构标记用于视觉格式设置。 | 无特定的LiveCycle技术 | |
| [ 6.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-keyboard-operable-scripts) | 对于脚本和小程序，请确保事件处理程序独立于输入设备。 | 2.7确保可使用键盘访问表单控件 | |
| [ 6.5](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-fallback-page) | 确保动态内容可访问，或者提供替代演示文稿或页面。 | 2.11避免中断脚本编写 | |
| [7.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-blinking) | 在用户代理允许用户控制闪烁之前，请避免导致内容闪烁（即，定期更改演示文稿，例如打开和关闭）。 | 2.1保持表单简单易用 | |
| [7.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-movement) | 在用户代理允许用户冻结移动内容之前，请避免在页面中移动。 | 2.1保持表单简单易用 | |
| [7.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-no-periodic-refresh) | 在用户代理提供停止刷新的功能之前，请勿定期创建自动刷新页面。 | 不适用 | |
| [7.5](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-no-auto-forward) | 在用户代理提供停止自动重定向功能之前，请勿使用标记自动重定向页面。 而是将服务器配置为执行重定向。 | 不适用 | |
| [8.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-directly-accessible) | 使编程元素（如脚本和小程序）可直接访问或与辅助技术兼容[优先级1（如果功能重要且不在其他位置显示），否则优先级2.] | 2.11避免中断脚本编写 | |
| [9.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-keyboard-operable) | 确保任何具有自己界面的元素均能够以独立于设备的方式操作。 | 2.7确保可使用键盘访问表单控件 | |
| [9.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-device-independent-events) | 对于脚本，请指定逻辑事件处理程序，而不是依赖于设备的事件处理程序。 | 2.7确保可使用键盘访问表单控件 | |
| [10.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-pop-ups) | 在用户代理允许用户关闭衍生窗口之前，请勿导致出现弹出窗口或其他窗口，也不要在未通知用户的情况下更改当前窗口。 | 2.11避免中断脚本编写 | |
| [10.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-unassociated-labels) | 在用户代理支持标签和表单控件之间的显式关联之前，对于具有隐式关联标签的所有表单控件，请确保标签正确放置。 | 2.5为表单控件提供适当的标签 | |
| [11.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-latest-w3c-specs) | 在有W3C技术并且适合某项任务时使用，并在支持时使用最新版本。 | 不适用 | |
| [11.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-deprecated) | 避免W3C技术的已弃用功能。 | 不适用 | |
| [12.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-frame-longdesc) | 描述帧的用途以及帧如何相互关联（如果单独使用帧标题无法明显实现此目的）。 | 不适用 | |
| [12.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-group-information) | 将大信息块划分成更易于管理的组，以使其更加自然和恰当。 | 2.10提供可导航表单结构 | |
| [12.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-associate-labels) | 将标签与其控件显式关联。 | 2.5为表单控件提供适当的标签 | |
| [13.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-meaningful-links) | 清楚地标识每个链接的目标。 | 2.5为表单控件2.5.6提供链接文本提供适当的标签 | |
| [13.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-use-metadata) | 提供元数据以将语义信息添加到页面和站点。 | 不适用 | |
| [13.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-site-description) | 提供有关网站总体布局的信息（例如，网站地图或目录）。 | 2.10提供可导航表单结构 | |
| [13.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-clear-nav-mechanism) | 以一致的方式使用导航机制。 | 2.10提供可导航表单结构 | 使用母版页创建一致的导航内容。 |

### WCAG 2.0成功标准

| 优先级1 G 2检查点 | 合规性所需的LiveCycle最佳实践 | 注释 |
| --- | --- | --- |
| 1.1 [替换文本](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv.html) | | |
| 1.1.1 [非文本内容](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv-all.html) | 2.4为图像提供等效文本 | |
| | 2.5为表单控件提供适当的标签 | |
| 1.2 [基于时间的媒体](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv.html) | | |
| 1.2.1 [纯音频和纯视频（预先录制）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-av-only-alt.html) | 2.12确保所有音频和视频内容均可访问 | |
| 1.2.2 [字幕（预先录制）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-captions.html) | 2.12确保所有音频和视频内容均可访问 | |
| 1.2.3 [音频描述或替代媒体（预先录制）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc.html) | 2.12确保所有音频和视频内容均可访问 | |
| 1.2.4 [字幕（实时）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-real-time-captions.html) | 2.12确保所有音频和视频内容均可访问 | |
| 1.2.5 [音频描述（预先录制）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc-only.html) | 2.12确保所有音频和视频内容均可访问 | |
| 1.2.6 [手语（预先录制）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-sign.html) | 2.12确保所有音频和视频内容均可访问 | |
| 1.2.7 [扩展音频描述（预先录制）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-extended-ad.html) | 2.12确保所有音频和视频内容均可访问 | |
| 1.2.8 [替代媒体（预先录制）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-text-doc.html) | 2.12确保所有音频和视频内容均可访问 | |
| 1.2.9 [纯音频（正式启用）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-live-audio-only.html) | 2.12确保所有音频和视频内容均可访问 | |
| 1.3 [可适应](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation.html) | | |
| 1.3.1 [信息和关系](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-programmatic.html) | 2.9提供表格的标题单元格 | |
| 1.3.2 [有意义的顺序](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-sequence.html) | 2.6确保读取和制表符顺序正确 | |
| | 2.10提供可导航表单结构 | |
| 1.3.3 [感官特性](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-understanding.html) | 2.8负责任地使用颜色 | |
| 1.4 [可区分](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast.html) | | |
| 1.4.1 [使用颜色](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-without-color.html) | 2.8负责任地使用颜色 | |
| 1.4.2 [音频控制](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-dis-audio.html) | 无特定的LiveCycle技术 | |
| 1.4.3 [对比度（最小）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html) | 2.8负责任地使用颜色 | |
| 1.4.4 [调整文本大小](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-scale.html) | 无特定的LiveCycle技术 | |
| 1.4.5 [文本的图像](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-presentation.html) | 无特定的LiveCycle技术 | |
| 1.4.6 [对比度（增强）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast7.html) | 2.8负责任地使用颜色 | |
| 1.4.7 [低背景音频或无背景音频](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-noaudio.html) | 无特定的LiveCycle技术 | |
| 1.4.9 [文本的图像（无异常）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-images.html) | 无特定的LiveCycle技术 | |
| 2.1 [无障碍键盘](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation.html) | | |
| 2.1.1 [键盘](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-keyboard-operable.html) | 2.6确保读取和制表符顺序正确 | |
| | 2.7确保可使用键盘访问表单控件 | |
| 2.1.2 [无键盘陷阱](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-trapping.html) | 2.7确保可使用键盘访问表单控件 | |
| 2.1.3 [键盘（无异常）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-all-funcs.html) | 2.6确保读取和制表符顺序正确 | |
| | 2.7确保可使用键盘访问表单控件 | |
| 2.2 [充足的时间](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits.html) | | |
| 2.2.1 [计时可调](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-required-behaviors.html) | 无特定的LiveCycle技术 | |
| 2.2.2 [暂停，停止，隐藏](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-pause.html) | 2.1保持表单简单易用 | |
| 2.2.3 [无计时](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-no-exceptions.html) | 无特定的LiveCycle技术 | |
| 2.2.4 [中断](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-postponed.html) | 无特定的LiveCycle技术 | |
| 2.2.5 [正在重新进行身份验证](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-server-timeout.html) | 无特定的LiveCycle技术 | |
| 2.3 [癫痫发作] | | |
| 2.3.1 [三个Flash或低于阈值](https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-does-not-violate.html) | 2.1保持表单简单易用 | |
| 2.3.2 [三个Flash](https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-three-times.html) | 2.1保持表单简单易用 | |
| 2.4 [可导航](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms.html) | | |
| 2.4.1 [绕过块](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-skip.html) | 2.10提供可导航表单结构 | |
| 2.4.2 [页面标题为](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-title.html) | 无特定的LiveCycle技术 | |
| 2.4.3 [焦点顺序](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-focus-order.html) | 2.6确保读取和制表符顺序正确 | |
| 2.4.4 [链接目的（在上下文中）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-refs.html) | 无特定的LiveCycle技术 | 链接目的取决于作者是否为链接的元素选择有意义的文本。 |
| 2.4.5 [多种方式](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-mult-loc.html) | 2.10提供可导航表单结构 | |
| 2.4.6 [标题和标签](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-descriptive.html) | <ul><li>2.5为表单控件提供适当的标签</li><li>2.10提供可导航表单结构</li> | |
| 2.4.7 [焦点可见](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-focus-visible.html) | 无特定的LiveCycle技术 | LiveCycle表单中的默认焦点可见。 |
| 2.4.8 [位置](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-location.html) | 无特定的LiveCycle技术 | 不适用：LiveCycle表单不需要导航系统。 |
| 2.4.9 [链接目的（仅限链接）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-link.html) | 无特定的LiveCycle技术 | 链接目的取决于作者是否为链接的元素选择有意义的文本。 |
| 2.4.10 [节标题](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-headings.html) | 2.10提供可导航表单结构 | |
| 3.1 [可读](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning.html) | | |
| 3.1.1 [页面语言](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-doc-lang-id.html) | 2.13识别自然语言和语言的任何变化 | |
| 3.1.2 [部分语言](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-other-lang-id.html) | 2.13识别自然语言和语言的任何变化 | |
| 3.1.3 [不寻常的单词](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-idioms.html) | 无特定的LiveCycle技术 | |
| 3.1.4 [缩写](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-located.html) | 无特定的LiveCycle技术 | |
| 3.1.5 [正在读取级别](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-supplements.html) | 无特定的LiveCycle技术 | |
| 3.1.6 [发音](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-pronunciation.html) | 无特定的LiveCycle技术 | |
| 3.2 [可预测](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior.html) | | |
| 3.2.1 [聚焦](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-receive-focus.html) | 2.11避免中断脚本编写 | |
| 3.2.2 [输入](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-unpredictable-change.html) | 2.11避免中断脚本编写 | |
| 3.2.3 [一致的导航](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-consistent-locations.html) | 2.10提供可导航表单结构 | |
| 3.2.4 [一致的标识](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-consistent-functionality.html) | <ul><li>2.3选择正确的控件</li><li>2.5为表单控件提供适当的标签</li> | |
| 3.2.5 [更改请求](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-no-extreme-changes-context.html) | 2.11避免中断脚本编写 | |
| 3.3 [输入辅助](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error.html) | | |
| 3.3.1 [错误标识](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-identified.html) |  | LiveCycleDesigner提供了一些工具，用于根据需要标记表单字段和执行表单输入验证。 |
| 3.3.2 [标签或说明](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-cues.html) | 2.5为表单控件提供适当的标签 | |
| 3.3.3 [错误建议](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-suggestions.html) |  | LiveCycleDesigner提供了一些工具，用于根据需要标记表单字段和执行表单输入验证。 |
| 3.3.4 [错误预防（法律、金融、数据）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-reversible.html) | 无特定的LiveCycle技术 | |
| 3.3.5 [帮助](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-context-help.html) | 无特定的LiveCycle技术 | |
| 3.3.6 [错误预防（全部）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-reversible-all.html) | 无特定的LiveCycle技术 | |
| 4.1 [兼容](https://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat.html) | | |
| 4.1.1 [解析](https://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat-parses.html) | 无特定的LiveCycle技术 | |
| 4.1.2 [名称，角色，值](https://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat-rsv.html) | <ul><li>2.3选择正确的控件</li> <li>2.5为表单控件提供适当的标签</li> | |



