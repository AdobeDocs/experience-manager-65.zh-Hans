---
title: AEM Forms的修补程序
description: 提供了有关如何下载和安装AEM Forms修补程序的信息。
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 5e2799505bc6d69cd5898445a9300ad162ef74fd
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---

# Adobe Experience Manager Forms修补程序{#aem-form-hotfix}

本文列出为解决已知问题、提高系统稳定性和增强AEM Forms整体性能而实施的关键修复。

>[!NOTE]
>
> 这些修补程序设计为累积式，包含所有之前的修补程序。 将最新的修补程序应用于某个版本时，该版本不仅解决了最新问题，而且还合并了之前的所有错误修复和增强功能。

## 自适应Forms的修补程序 {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>日期</strong></td>
    <td><strong>修补程序下载链接(AEM Software Distribution链接)</strong></td>
    <td><strong>修复的问题</strong></td>
  </tr>
  <tr>
    <td>2024年5月16日</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1192-010.zip">适用于Microsoft Windows的AEM Service Pack 6.5.20.0的修补程序</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1192-010.zip">适用于Linux的AEM Service Pack 6.5.20.0的修补程序 </a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1192-010.zip">适用于Apple macOS的AEM Service Pack 6.5.20.0的修补程序</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>在基于XDP的自适应表单中，如果复选框上嵌入了脚本，则此类复选框之后的元素将不会执行脚本。 有针对此问题的修补程序。 (FORMS-14244) </li>
     <li> 在弹出小部件中遍历具有编辑/显示模式的字段的月份时，日期选取器小部件中的行会被截断。 有针对此问题的修补程序。 (FORMS-13620) </li>
     <li>尝试在后端使用DOR（记录文档）服务时，表单提交失败。 遇到的错误消息是：“提交操作无法完成，因为未正确分配表单资源。” (FORMS-13798) </li>
     <li>将自适应表单从Adobe Experience Manager发布实例提交到Adobe Experience Manager Workflow时，工作流无法保存附件。  (FORMS-14209) </li>
     <li> 安装AEM 6.5 Forms Service Pack 20包(适用于SP20的AEM Forms附加组件包)时，AEM Sites用户界面(UI)性能会显着降低。  (FORMS-13791) </li>
     <li>预填充服务失败，交互式通信中出现空指针异常。 (CQDOC-21355)</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024年1月29日</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fforms-foundation-qs-content-4.0.170-FORMS-12692-B0001.zip">适用于JEE服务器上Windows的AEM Service Pack 6.5.19.0的修补程序</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>在JEE服务器上的AEM Forms上，无法呈现使用上下文路径的HTML5 Forms 。 (FORMS-12485和FORMS-12691)。</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024年1月29日</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-win-pkg-6.0.1016-004.zip">适用于Microsoft Windows的AEM Service Pack 6.5.18.0的修补程序</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-linux-pkg-6.0.1016-004.zip">适用于Linux的AEM Service Pack 6.5.18.0的修补程序</a></li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-osx-pkg-6.0.1016-004.zip">适用于Apple macOS的AEM Service Pack 6.5.18.0的修补程序</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li> 现成的涂写签名组件无法以自适应表单呈现预览。 (FORMS-12073)。</li>
    </ul>
    </td>    
   </tr>
   <tr>
    <td>2023年11月20日</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">适用于Linux的AEM Service Pack 6.5.18.0的修补程序</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">适用于Microsoft Windows的AEM Service Pack 6.5.18.0的修补程序</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">适用于Apple macOS的AEM Service Pack 6.5.18.0的修补程序</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li>在自适应表单的指南容器中设置重定向URL后，内联签名将停止工作。 (FORMS-10493)</li>
    <li>无法为本地化的自适应Forms发布记录文档(DoR)模板。 (FORMS-10535)</li>
    <li>在编辑模式下无法打开包含大型内嵌图像的交互式通信。 (FORMS-10578)</li>
    </ul>
    </td>    
  </tr>
  <tbody>
</table>

## 下载并安装修补程序 {#download-install-hotfix}

执行以下步骤以下载并安装修补程序：

1. 下载 [修补程序](#hotfix-for-adaptive-forms) 从Software Distribution链接。
1. 解压缩修补程序存档文件，以便获取Experience Manager包(.zip)和捆绑包(.jar)文件。
1. 通过上传并安装包(.zip) [包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).
1. 打开配置管理器包 `https://server:host/system/console/bundles`，上传并安装捆绑包(.jar)。 已安装修补程序。
