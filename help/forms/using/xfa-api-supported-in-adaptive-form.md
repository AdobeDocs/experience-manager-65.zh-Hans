---
title: 基于XDP的自适应表单中支持XFA
description: 列出自适应表单中支持的XFA事件、属性、脚本和验证。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 255be73f-3169-457c-aaa7-a2fb59f1f2cd
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 11%

---

# 基于XDP的自适应表单中支持XFA{#xfa-support-in-xdp-based-adaptive-forms}

## 简介 {#introduction}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

自适应表单支持XDP文件中定义的各种XFA事件、属性、脚本和验证，包括：

* 执行在XDP文件中的事件上定义的脚本。
* 捕获XDP文件中字段的缺省值和行为属性。
* 执行XDP文件中定义的验证脚本。

在基于XDP文件创建自适应表单时，属性、事件和验证会在表单创作UI中自动填充。 但是，表单作者可以覆盖其中的某些元素以创建替代体验。

本文列出了自适应表单中遵循的受支持XFA事件、属性和验证，并说明了如何在自适应表单中覆盖这些事件、属性和验证。

## 自适应表单中支持的XFA元素及其映射 {#supported-xfa-elements-and-their-mapping-in-adaptive-forms-br}

### 字段 {#fields}

使用XDP文件创建自适应表单时，您可以将XFA字段拖放到自适应表单上。 下表列出了XFA字段如何映射到自适应表单字段。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA字段或容器</strong></p> </td>
   <td><p><strong>相应的自适应表单组件</strong></p> </td>
  </tr>
  <tr>
   <td><p>按钮 </p> </td>
   <td><p>按钮</p> </td>
  </tr>
  <tr>
   <td><p>复选框 </p> </td>
   <td><p>复选框</p> </td>
  </tr>
  <tr>
   <td><p>列表框 </p> </td>
   <td><p>下拉列表</p> </td>
  </tr>
  <tr>
   <td><p>日期/时间字段 </p> </td>
   <td><p>日期选取器</p> </td>
  </tr>
  <tr>
   <td><p>潦草签名</p> </td>
   <td><p>潦草签名</p> </td>
  </tr>
  <tr>
   <td><p>数值字段 </p> </td>
   <td><p>数值框</p> </td>
  </tr>
  <tr>
   <td><p>十进制字段</p> </td>
   <td><p>数值框</p> </td>
  </tr>
  <tr>
   <td><p>文本字段 </p> </td>
   <td><p>文本框</p> </td>
  </tr>
  <tr>
   <td><p>密码字段 </p> </td>
   <td><p>密码框</p> </td>
  </tr>
  <tr>
   <td><p>图像</p> </td>
   <td><p>图像</p> </td>
  </tr>
  <tr>
   <td><p>文本</p> </td>
   <td><p>文本</p> </td>
  </tr>
  <tr>
   <td><p>子表单 </p> </td>
   <td><p>面板</p> </td>
  </tr>
  <tr>
   <td><p>区域（组）</p> </td>
   <td><p>面板</p> </td>
  </tr>
  <tr>
   <td><p>子表单集 </p> </td>
   <td><p>面板</p> </td>
  </tr>
 </tbody>
</table>

### 属性 {#properties}

下表捕获了XDP文件中定义的各种XFA脚本在自适应表单中的行为方式。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA组件属性</strong></p> </td>
   <td><p><strong>自适应表单中的相应行为</strong></p> </td>
  </tr>
  <tr>
   <td><p>somexpression </p> </td>
   <td><p>映射到自适应表单中的绑定引用(bindRef)属性。</p> </td>
  </tr>
  <tr>
   <td><p>存在 </p> </td>
   <td><p>映射到自适应表单中的visible属性。 可以使用“可见性”表达式覆盖它。</p> </td>
  </tr>
  <tr>
   <td><p>访问 </p> </td>
   <td><p>映射到自适应表单中启用的属性。 您可以使用Access表达式覆盖它。</p> </td>
  </tr>
  <tr>
   <td><p>辅助功能：角色 </p> </td>
   <td><p>映射到自适应表单中的role属性。</p> </td>
  </tr>
  <tr>
   <td><p>辅助功能：speakPriority </p> </td>
   <td><p>已映射到自适应表单中的speakPriority属性。</p> </td>
  </tr>
  <tr>
   <td><p>辅助功能： speakText</p> </td>
   <td><p>映射到自适应表单中的自定义辅助功能文本。</p> </td>
  </tr>
  <tr>
   <td><p>辅助功能：工具提示 </p> </td>
   <td><p>映射到自适应表单中的简短描述属性。</p> </td>
  </tr>
  <tr>
   <td><p>题注<em> （所有字段类型）</em></p> </td>
   <td><p>映射到自适应表单中的Title属性。</p> </td>
  </tr>
  <tr>
   <td><p>displayFormat<em> （所有字段类型）</em></p> </td>
   <td><p>已映射到自适应表单中的显示模式。</p> </td>
  </tr>
  <tr>
   <td><p>rawValue<em> （所有字段类型）</em></p> </td>
   <td><p>映射到自适应表单中的值属性。</p> </td>
  </tr>
  <tr>
   <td><p>项<em> （列表框，复选框）</em></p> </td>
   <td><p>映射到自适应表单中的options属性。 可以使用“选项”表达式覆盖它。</p> </td>
  </tr>
  <tr>
   <td><p>maxChar<em> （文本字段）</em></p> </td>
   <td><p>映射到自适应表单中允许的最大字符数属性。</p> </td>
  </tr>
  <tr>
   <td><p>多行<em> （文本字段）</em></p> </td>
   <td><p>映射到自适应表单中的允许多行属性。</p> </td>
  </tr>
  <tr>
   <td><p>fracDigit<em> （数字字段，小数字段）</em></p> </td>
   <td><p>映射到自适应表单中的Frac数字属性。</p> </td>
  </tr>
  <tr>
   <td><p>leadDigital<em> （数字字段，小数字段）</em></p> </td>
   <td><p>映射到自适应表单中的潜在客户数字属性。</p> </td>
  </tr>
  <tr>
   <td><p>multiSelect<em> （列表框）</em></p> </td>
   <td><p>已映射到允许自适应表单中包含多选属性。</p> </td>
  </tr>
 </tbody>
</table>

### 脚本 {#scripts}

下表捕获了XDP文件中定义的各种XFA脚本在自适应表单中的行为方式。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA脚本事件</strong></p> </td>
   <td><p><strong>自适应表单中的相应行为</strong></p> </td>
  </tr>
  <tr>
   <td><p>初始化 </p> </td>
   <td><p>此脚本在运行时执行，无法在自适应表单中覆盖。</p> </td>
  </tr>
  <tr>
   <td><p>计算</p> </td>
   <td><p>映射到自适应表单中的计算表达式。</p> </td>
  </tr>
  <tr>
   <td><p>验证 </p> </td>
   <td><p>映射到自适应表单中的验证表达式。</p> </td>
  </tr>
  <tr>
   <td><p>validationState </p> </td>
   <td><p>此脚本在运行时执行，无法在自适应表单中覆盖。<br /> </p> </td>
  </tr>
  <tr>
   <td><p>退出 </p> </td>
   <td><p>此脚本在运行时执行，无法在自适应表单中覆盖。</p> </td>
  </tr>
  <tr>
   <td><p>单击（按钮字段）</p> </td>
   <td><p>映射到按钮的Click表达式。</p> </td>
  </tr>
  <tr>
   <td><p>支持服务器端脚本</p> </td>
   <td><p>此脚本在运行时执行，无法在自适应表单中覆盖。</p> </td>
  </tr>
  <tr>
   <td><p>支持Web服务</p> </td>
   <td><p>此脚本在运行时执行，无法在自适应表单中覆盖。</p> </td>
  </tr>
  <tr>
   <td><p>更改（涂鸦字段、单选按钮、复选框）</p> </td>
   <td><p>此脚本在运行时执行，无法在自适应表单中覆盖。</p> </td>
  </tr>
 </tbody>
</table>

### 验证 {#validations}

下表捕获了XFA验证如何映射到自适应表单中的验证。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA验证</strong></p> </td>
   <td><p><strong>自适应表单中的相应验证</strong></p> </td>
  </tr>
  <tr>
   <td><p>验证模式(formatTest)</p> </td>
   <td><p>validatePictureClause</p> </td>
  </tr>
  <tr>
   <td><p>验证模式消息(formatTestMessage)</p> </td>
   <td><p>validatePictureMessage</p> </td>
  </tr>
  <tr>
   <td><p>必需(nullTest )</p> </td>
   <td><p>必需 </p> </td>
  </tr>
  <tr>
   <td><p>空消息(nullTestMessage) </p> </td>
   <td><p>message</p> </td>
  </tr>
  <tr>
   <td><p>验证脚本(scriptTest)</p> </td>
   <td><p>validateExp</p> </td>
  </tr>
  <tr>
   <td><p>验证脚本消息(scriptTestMessage)</p> </td>
   <td><p>validateMessage</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>无法覆盖绑定到XFA复选框按钮的自适应表单单选按钮和复选框组的强制属性。
