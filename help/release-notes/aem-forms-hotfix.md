---
title: AEM Forms的修补程序
description: 提供了有关如何下载和安装AEM Forms修补程序的信息。
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: fb689e86deaabcc4033ed75f615086b630a9a525
workflow-type: tm+mt
source-wordcount: '903'
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
    <td>2024年7月10日</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-jboss.zip.zip">适用于Windows上的AEM Service Pack 6.5.21.0的修补程序，适用于JBoss JEE服务器</a> </li>
      <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-jboss.tar.gz">适用于Linux上的AEM Service Pack 6.5.21.0的修补程序，适用于JBoss JEE服务器</a> </li>
       <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-websphere.zip.zip">适用于Windows上的AEM Service Pack 6.5.21.0的修补程序，适用于Webshpere JEE服务器</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-websphere.tar.gz">适用于Linux上的AEM Service Pack 6.5.21.0的修补程序，适用于Webshpere JEE服务器</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-weblogic.zip.zip">适用于Windows上的AEM Service Pack 6.5.21.0的修补程序，适用于Weblogic JEE服务器</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-weblogic.tar.gz">适用于Linux上的AEM Service Pack 6.5.21.0的修补程序，适用于Weblogic JEE服务器</a> </li>
     </ul>
     </td>
    <td>
    <ul><li>当用户更新到JEE服务器上的AEM Forms Service Pack 20 (6.5.20.0)并使用输出服务生成PDF时，PDF呈现时的辅助功能问题。 (LC-3922112)</li><li>在AEM Forms JEE上使用输出服务生成的标记PDF显示“结构不适当警告”。 (LC-3922038)</li><li>在AEM Forms JEE上提交表单时，将从数据中删除重复XML元素的实例。 (LC-3922017)</li><li>当Linux环境中的用户在HTML中渲染自适应表单（在JEE上）时，该表单无法正确渲染。 (LC-3921957)</li><li>当用户使用AEM Forms JEE上的输出服务将XTG文件转换为PostScript格式时，它会失败，并出现以下错误：AEM_OUT_001_003：意外异常：PAExecute失败：XFA_RENDER_FAILURE。 (LC-3921720)</li><li>在JEE服务器上升级到AEM Forms Service Pack 18 (6.5.18.0)后，当用户提交表单时，将无法呈现HTML5或PDF forms，并且XMLFM崩溃。 (LC-3921718)
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024年6月21日</td>
     <td>
     <ul>
     <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">适用于JBoss JEE服务器</a>上AEM Service Pack 6.5.21.0的修补程序 </li>
      <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">适用于Weblogic JEE服务器</a>上AEM Service Pack 6.5.21.0的修补程序 </li>
       <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">适用于Webshpere JEE服务器</a>上AEM Service Pack 6.5.21.0的修补程序 </li>
        <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">适用于OSGi服务器</a>上AEM Service Pack 6.5.21.0的修补程序 </li>
     </ul>
     </td>
    <td>
    <ul>
    <li> 升级到AEM Forms Service Pack 6.5.21.0后，PaperCapture服务无法在PDF上执行OCR（光学字符识别）操作。 有关安装说明，请参阅<a href="/help/forms/using/papercapture-service-resolution.md">疑难解答</a>文章。(CQDOC-21680) </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024年6月21日</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Fccm-ccr-content-10.0.206.zip">适用于AEM Service Pack 6.5.21.0的修补程序</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>预览期间，包含XML数据的草稿信件卡在加载状态。 有关该修补程序的下载和安装说明，请参阅<a href="#install-hotfix">下载并安装草稿信件问题</a>的修补程序。(FORMS-14521)</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024年5月16日</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1192-010.zip">适用于Microsoft Windows的AEM Service Pack 6.5.20.0的修补程序</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1192-010.zip">适用于Linux的AEM Service Pack 6.5.20.0的修补程序</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1192-010.zip">适用于Apple macOS的AEM Service Pack 6.5.20.0的修补程序</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>在基于XDP的自适应表单中，如果复选框上嵌入了脚本，则此类复选框之后的元素将不会执行脚本。 有针对此问题的修补程序。 (FORMS-14244) </li>
     <li> 在弹出小部件中遍历具有编辑/显示模式的字段的月份时，日期选取器小部件中的行会被截断。 有针对此问题的修补程序。 (FORMS-13620) </li>
     <li>尝试在后端使用DOR（记录文档）服务时，表单提交失败。 遇到的错误消息是：“提交操作无法完成，因为未正确分配表单资源。” (FORMS-13798) </li>
     <li>将自适应表单从Adobe Experience Manager Publish实例提交到Adobe Experience Manager Workflow时，工作流无法保存附件。  (FORMS-14209) </li>
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

1. 从Software Distribution链接下载[修补程序](#hotfix-for-adaptive-forms)。
1. 解压缩修补程序存档文件，以便获取Experience Manager包(.zip)和捆绑包(.jar)文件。
1. 通过[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing)上载并安装包(.zip)。
1. 打开配置管理器包`https://server:host/system/console/bundles`，上载并安装该包(.jar)。 已安装修补程序。


## 下载并安装草稿书信问题的修补程序 {#install-hotfix}

要解决此问题，请执行以下步骤：

1. 从软件分发门户下载[修补程序](#hotfix-for-adaptive-forms)。
2. 使用[CRX包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing)上载并安装包(.zip)。