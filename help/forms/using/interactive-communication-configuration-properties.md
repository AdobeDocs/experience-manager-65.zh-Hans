---
title: 交互式通信的配置属性
description: 编辑交互式通信的默认配置属性
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: interactive-communications
docset: aem65
feature: Interactive Communication
exl-id: 09eeade6-e16d-4159-b26a-803c7201097a
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: aa28c6c8-3ede-445b-a351-eeb0c9f9aec4
    internal-label: Interactive Communication
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 9%
---
# 交互式通信的配置属性{#interactive-communications-configuration-properties}

交互式通信包括在安装[AEM Forms附加组件](../../forms/using/installing-configuring-aem-forms-osgi.md)包后自动配置的属性。 交互式通信作者可以使用&#x200B;**Adobe Experience Manager Web控制台配置**&#x200B;页编辑这些默认配置属性。

使用以下URL打开&#x200B;**Adobe Experience Manager Web控制台配置**&#x200B;页面：

`https:/[server]:[port]/<contextPath>/system/console/configMgr`

配置属性包括：

* [文档片段配置](#document-fragments-configuration)
* [创建通信配置](#create-correspondence-configuration)
* [自适应表单和交互式通信Web渠道配置](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [自适应表单和交互式通信Web渠道主题配置](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## 文档片段配置 {#document-fragments-configuration}

在&#x200B;**Adobe Experience Manager Web控制台配置**&#x200B;页面上选择&#x200B;**文档片段配置**&#x200B;以查看文档片段的配置属性。

<table>
 <tbody> 
  <tr> 
   <td>属性</td> 
   <td>描述</td> 
   <td>默认</td> 
   <td>可接受值</td> 
  </tr> 
  <tr> 
   <td>数据显示格式</td> 
   <td>为打印和Web渠道创建交互式通信时，可用的字段、变量和表单数据模型元素的特定于区域设置的显示格式。</td> 
   <td> 
    <ul> 
     <li>locale = en_US、de_DE、fr_FR和ja_JP</li> 
     <li>日期格式= dd-MM-yyyy</li> 
     <li>numberDecimalSeparator = 。</li> 
     <li>numberGroupSeparator = ，</li> 
     <li>numberUseGroupSeparator = true</li> 
    </ul> </td> 
   <td><p>--</p> </td> 
  </tr> 
  <tr> 
   <td>缩进</td> 
   <td>应用于列表文档片段中文本的单缩进单位宽度。</td> 
   <td>12.7毫米</td> 
   <td>数字</td> 
  </tr> 
  <tr> 
   <td>罗马数字最小宽度</td> 
   <td>在列表文档片段中使用罗马数字时，应用于项目符号或数字字段的最小宽度。 </td> 
   <td>12.7毫米</td> 
   <td>数字</td> 
  </tr> 
  <tr> 
   <td>数字最小宽度</td> 
   <td>在列表文档片段中使用除罗马数字之外的编号列表时，应用于项目符号或数字字段的最小宽度。</td> 
   <td>8.0毫米</td> 
   <td>数字</td> 
  </tr> 
 </tbody> 
</table>

## 创建通信配置 {#create-correspondence-configuration}

在&#x200B;**Adobe Experience Manager Web控制台配置**&#x200B;页面上选择&#x200B;**创建通信配置**&#x200B;以查看代理UI的配置属性。

<table>
 <tbody> 
  <tr> 
   <td>属性</td> 
   <td>描述</td> 
   <td>默认</td> 
   <td>可接受值</td> 
  </tr> 
  <tr> 
   <td>显示已解析的内容以进行编辑</td> 
   <td>选中该复选框以在代理UI上编辑文本模块时显示已解析的内容（实际值而不是占位符）。</td> 
   <td>未选定</td> 
   <td>不适用</td> 
  </tr> 
  <tr> 
   <td>在预览期间应用水印</td> 
   <td>选中此复选框以在预览模式下将水印应用于交互式通信的打印渠道。</td> 
   <td>未选定</td> 
   <td>不适用</td> 
  </tr> 
  <tr> 
   <td>在PDF中启用字体嵌入</td> 
   <td><p>选中此复选框可在PDF文档中启用嵌入字体。 选择此选项后，您可以在使用Agent UI生成或预览PDF文档后嵌入新字体。 使用交互式通信的打印渠道生成和预览PDF文档。</p> <p>如果用于生成PDF的计算机上有字体，而访问PDF的客户端计算机上没有字体，则在PDF文档中嵌入字体会很有用。</p> <p>有关嵌入字体的详细信息，请参阅<a href="../../forms/using/customize-text-editor.md" target="_blank">自定义文本编辑器</a>。</p> </td> 
   <td>未选定</td> 
   <td>不适用</td> 
  </tr> 
 </tbody> 
</table>

## 自适应表单和交互式通信Web渠道配置 {#adaptive-form-and-interactive-communication-web-channel-configuration}

在&#x200B;**Adobe Experience Manager Web控制台配置**&#x200B;页面上选择&#x200B;**自适应表单和交互式通信Web渠道配置**，以查看自适应Forms和交互式通信Web渠道的配置属性。 下表描述了与交互式通信相关的属性：

| 属性 | 描述 | 默认 | 可接受值 |
|---|---|---|---|
| 显示占位符 | 选中此复选框可启用自适应表单和交互式通信中包含的字段的占位符显示。 | 已选定 | 不适用 |
| 最大缓存条目 | 设置可使用缓存检索的自适应表单和交互式通信的最大数目。 | 100 | 数字 |
| 使文件名唯一 | 选中此复选框可使Adaptive Forms和交互式通信中作为附件包含的文件具有唯一的名称。 | 未选定 | 不适用 |

## 自适应表单和交互式通信Web渠道主题配置 {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

在&#x200B;**Adobe Experience Manager Web控制台配置**&#x200B;页上选择&#x200B;**自适应表单和交互式通信Web渠道主题配置**，以查看自适应Forms和交互式通信Web渠道主题的配置属性。

<table>
 <tbody> 
  <tr> 
   <td>属性</td> 
   <td>描述</td> 
   <td>默认</td> 
   <td>可接受值</td> 
  </tr> 
  <tr> 
   <td>字体列表名称</td> 
   <td>创建自适应Forms和交互式通信时可用的字体列表。</td> 
   <td><p>Georgia</p> <p>Book Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial Black</p> <p>影响</p> <p>Palatino Linotype</p> </td> 
   <td>所有有效的Adobe服务器字体</td> 
  </tr> 
 </tbody> 
</table>
