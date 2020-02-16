---
title: 电子邮件模板的最佳实践
seo-title: 电子邮件模板的最佳实践
description: 查找有关在AEM中创建电子邮件模板的最佳实践。
seo-description: 查找有关在AEM中创建电子邮件模板的最佳实践。
uuid: 07417a63-7ca6-484c-b55d-57b319428329
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 2418777e-4eb2-4d82-aa9e-8d1b0bf740f3
docset: aem65
translation-type: tm+mt
source-git-commit: bd0cb6abe024bc4ff77c9932c99b816c832377f5

---


# 电子邮件模板的最佳实践 {#best-practices-for-email-templates}

>[!CAUTION]
>
>已弃用AEM电子邮件组件。 由于电子邮件的性质将内容和样式结合在一起，AEM提供的现成电子邮件组件对客户的重复使用有限，因为需要将自定义样式实施到项目所需的任何组件中。
>
>可以在项目级别上实施电子邮件组件，已弃用的AEM电子邮件组件说明了如何实现这一点。 但是，这些已弃用的组件不应用于项目。

本文描述了有关电子邮件设计的一些最佳实践，从而生成了一个完善的电子邮件营销活动模板。

AEM中提供的演示营销活动遵循了所有这些最佳实践。 介绍了如何在演示营销活动中实施最佳实践，以了解每个最佳实践。

在创建您自己的新闻稿时，请使用这些最佳实践。

>[!NOTE]
>
>所有营销活动内容都应在类型 `master` 的页面下创建 `cq/personalization/components/ambitpage`。
>
>例如，如果计划的营销活动结构类似于
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>应确保它位于页面下 `master` 方
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>在为Adobe Campaign创建邮件时，必须在模板的jcr:content **节点中包含值** acMapping **，否则将无法在AEM的********** Page Properties（字段禁用）中选择Adobe Campaign模板。

## 模板／页面组件 {#template-page-component}

***/libs/mcm/campaign/components/campaign_newsletterpage***

<table>
 <tbody>
  <tr>
   <td><strong>最佳实践</strong></td>
   <td><strong>实施</strong></td>
  </tr>
  <tr>
   <td><p>指定文档类型以确保一致的渲染。</p> <p>在开头添加DOCTYPE（HTML或XHTML）</p> </td>
   <td><p>可通过设计更改 <i>"/etc/designs/default/jcr:content/campaign_newsletterpage"中的cq:doctype</i><i>属性进行配置</i></p> <p>默认值为“XHTML”:</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>可更改为“HTML_5”:</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>指定字符定义以确保正确呈现特殊字符。</p> <p>将CHARSET声明（例如iso-8859-15, UTF-8）添加到&lt;head&gt;</p> </td>
   <td><p>设置为UTF-8。</p> <p>&lt;meta http-equiv="content-type" content="text/html;charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>使用&lt;table&gt;元素编码所有结构。 对于更复杂的布局，您应嵌套表以构建复杂的结构。</p> <p>即使没有css，电子邮件也应显示良好。</p> </td>
   <td><p>整个模板中都使用表来构造内容。 当前使用最多四个嵌套表（1个基表+最大）。 3个嵌套级别)</p> <p>&lt;div&gt;标记仅在创作模式下使用，以确保正确编辑组件。</p> </td>
  </tr>
  <tr>
   <td>使用元素属性（如单元格边距、有效性和宽度）设置表尺寸。 这会迫使一个箱型结构。</td>
   <td><p>所有表都包含必需的 <i>边框</i>、 <i>cellpadding</i>、 <i>cellspacing和width</i><i></i>等属性。</p> <p>为了协调表内的元素定位，所有表单元格都 <i>设置了valign="top"</i> 属性。</p> </td>
  </tr>
  <tr>
   <td><p>如果可能，请考虑移动友好性。 使用媒体查询增加小屏幕上的文本大小，为链接提供缩略图大小的点击区域。</p> <p>在设计允许的情况下使电子邮件成为响应式电子邮件。</p> </td>
   <td>只要使用CSS样式来说明演示设计，媒体查询就可用于提供移动友好版本。</td>
  </tr>
  <tr>
   <td>内联CSS比将所有CSS放在开头要好。</td>
   <td><p>为了更好地演示底层HTML结构并简化自定义新闻稿结构的可能性，只嵌入了一些CSS定义。</p> <p>基本样式和模板变量已提取到页面&lt;head&gt;中的样式块中。 在最终提交新闻稿时，这些CSS定义应嵌入到HTML中。 已计划自动联机机制，但目前不可用。</p> </td>
  </tr>
  <tr>
   <td>使CSS变得简单。 避免复合样式声明、速记代码、CSS布局属性、复杂的选择器和伪元素。</td>
   <td>只要使用CSS样式来说明演示设计，就会遵循CSS建议。</td>
  </tr>
  <tr>
   <td>电子邮件的最大宽度应为600-800像素。 这将使他们在许多客户端提供的预览窗格大小中表现得更好。</td>
   <td>在演 <i>示设计中</i> ，内容表的宽度限制为600px。</td>
  </tr>
 </tbody>
</table>

### 图像 {#images}

/libs/mcm/campaign/components/image

| **最佳实践** | **实施** |
|---|---|
| 向图 *像添加* alt属性 | 对于 *图像组件* ,alt属性已定义为必填项。 |
| 对图 *像使用* jpg而 *不是png* 格式 | 图像组件始终将图像用作JPG。 |
| 在表 <img> 中使用元素而不是背景图像。 | 模板中不使用背景图像数据。 |
| 在图片上添加属性style=&quot;display block&quot;。 允许在Gmail上显示良好。 | 默认情况下，所有图 *像都包含style=&quot;display block&quot;* 属性。 |

### 文本和链接 {#text-and-links}

/libs/mcm/campaign/components/heading, /libs/mcm/campaign/components/textimage

<table>
 <tbody>
  <tr>
   <td><strong>最佳实践</strong></td>
   <td><strong>实施</strong></td>
  </tr>
  <tr>
   <td>在CSS中使用html &lt;font&gt;而不是样式（字体系列）</td>
   <td>RichTextEditor（例如，在文本时间组件中）现在支持选择字体系列和字体大小并将其应用于选定文本。 它们将呈现为&lt;font&gt;标记。</td>
  </tr>
  <tr>
   <td>使用基本的跨平台字体，如 <i>Arial、Verdana、Georgia</i> 和 <i>Times New Roman</i>。</td>
   <td><p>取决于新闻稿设计。</p> <p>对于演示设计，使用字体“Helvetica”，但如果不存在，将返回到通用的sans-serif字体。</p> </td>
  </tr>
 </tbody>
</table>

### 通用 {#generic}

| **最佳实践** | **实施** |
|---|---|
| 使用W3C验证程序更正HTML代码。 确保正确关闭所有打开的标记。 | 代码已验证。 对于XHTML过渡Doctype，仅缺少 <html> 元素缺失。 |
| 不用再使用JavaScript或Flash了——电子邮件客户端基本上不支持这些技术。 | 新闻稿模板中不使用JavaScript和Flash。 |
| 为多部分发送添加纯文本版本。 | 在页面属性中构建了一个新构件，以便从页面内容中轻松提取纯文本版本。 这可用作最终纯文本版本的起点。 |

## 营销活动新闻稿模板和示例 {#campaign-newsletter-templates-and-examples}

AEM附带了多个模板和组件，供您开箱即用以创建营销活动新闻稿。 您可以使用这些模板和组件创建自定义新闻稿。

### 模板 {#templates}

为了提供坚实的基础并扩大内容流的各种可能性，开箱即用的模板类型有三种略有不同。 您可以轻松使用这些组件来构建自定义Newsletter。

所有组件都 **有页眉**、页 **脚****和** 正文部分。 在正文部分下方，每个模板在列设 **计** （1列、2列或3列）上都不同。

![](assets/chlimage_1-69.png)

### 组件 {#components}

当前有七 [个组件可在营销活动模板中使用](/help/sites-authoring/adobe-campaign-components.md)。 这些组件都基于Adobe标记语言 **HTL**。

| **组件名称** | **组件路径** |
|---|---|
| 标题 | /libs/mcm/campaign/components/heading |
| 图像 | /libs/mcm/campaign/components/image |
| 文本与个性化 | /libs/mcm/campaign/components/personalization |
| Textimage | /libs/mcm/campaign/components/textimage |
| 链接 | /libs/mcm/campaign/components/reference |
| Scene7 图像模板 | /libs/mcm/campaign/s7image |
| 目标引用 | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>这些组件针对邮件内容进行了优化；即，他们遵守本文档中概述的最佳做法。 使用其他现成的组件通常会违反这些规则。

这些组件在 [Adobe Campaign组件中有详细说明](/help/sites-authoring/adobe-campaign-components.md)。