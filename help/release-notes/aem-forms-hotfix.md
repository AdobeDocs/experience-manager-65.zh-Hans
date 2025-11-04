---
title: AEM Forms 热修复补丁
description: 提供有关如何下载和安装 AEM Forms 热修复补丁的信息。
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 650131b88e06d59e6c206e07b8512149cd360b08
workflow-type: tm+mt
source-wordcount: '1987'
ht-degree: 91%

---

# Adobe Experience Manager Forms 热修复补丁{#aem-form-hotfix}

本文列出了为解决 AEM Forms 的已知问题、提升其系统稳定性以及增强其整体性能而实施的重要修复。

>[!NOTE]
>
> 这些热修复补丁是累积性的，其中包含所有先前的修复。当您将最新的热修复补丁应用于某个版本时，它不仅会解决最新的问题，还会同时集成此前所有的错误修复和功能改进。

## AEM Forms 热修复补丁 {#hotfix-for-aem-forms}

<table>
  <tbody>
  <tr>
    <td><strong>日期</strong></td>
    <td><strong>热修复补丁下载链接（AEM 软件分发链接）</strong></td>
    <td><strong>修复的问题</strong></td>
  </tr>
  <tr>
    <td>
      <strong>2025年10月14日</strong><br>
      <em>应用：</em> ImgToPdf在AEM Forms SP23 Jboss<br>中失败
    </td>
    <td>
    <ul> 要解决此问题，请联系<a href="https://business.adobe.com/in/support/main.html">Adobe Experience Manager Forms支持</a>
    </ul>
    </td>
    <td>
    <ul>
    <li> <b>(FORMS-22029)：</b>通过解决PDF Generator (PDFG)在升级到SP23后无法将图像文件转换为PDF，从而导致意外的后处理错误的问题，提高PDF转换的可靠性。
      <ul>
  <tr>
    <td>
      <strong>2025年9月23日</strong><br>
    </td>
    <td>
    <ul>
    <strong>Jboss：</strong>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/jboss/adobe-aem-forms-jee-hotfix3-6.5.23.0-win-jboss.zip">适用于在 Windows 上运行的 JBoss JEE 服务器的 AEM 服务包 6.5.23.0 的热修复补丁</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/jboss/adobe-aem-forms-jee-hotfix3-6.5.23.0-linux-jboss.tar.gz">适用于在 Linux 上运行的 JBoss JEE 服务器的 AEM 服务包 6.5.23.0 的热修复补丁</a></li>
    <strong>Weblogic：</strong>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/weblogic/adobe-aem-forms-jee-hotfix3-6.5.23.0-win-weblogic.zip">适用于在 WebLogic JEE 服务器上运行的 AEM 服务包 6.5.23.0 的热修复补丁</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/weblogic/adobe-aem-forms-jee-hotfix3-6.5.23.0-linux-weblogic.tar.gz">适用于在 Linux 上运行的 Weblogic JEE 服务器的 AEM 服务包 6.5.23.0 的热修复补丁</a></li>
    <strong>Websphere：</strong>
    <li>Windows — 适用于Websphere JEE服务器的Windows上的<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/websphere/adobe-aem-forms-jee-hotfix3-6.5.23.0-win-websphere.zip">适用于AEM Service Pack 6.5.23.0的修补程序</a></li>
    <li>Linux — 适用于Linux上的AEM Service Pack 6.5.23.0的修补程序，用于Websphere JEE服务器<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/websphere/adobe-aem-forms-jee-hotfix3-6.5.23.0-linux-websphere.tar.gz"></a></li>
    </ul>
    </td>
    <td>
    <ul>
    <strong>此热修复补丁解决了以下问题：</strong> 
    <li> <b>(FORMS-21378)：</b>通过解决在启用服务器端验证(SSV)且计算的Meta信息为空时提交失败的问题，提高了表单提交的可靠性。

<li> <b>(FORMS-21721)：</b>改进了针对6.5.23.0部署修补程序（2025年8月<b>日发布</b>）后，PS到PDF和HTML到PDF (WebKit)转换失败的问题。 
    </li>
    </ul>
    </td>    
  </tr>
    </ul>
    </td>
  <tr>
    <td>
      <strong>2025 年 8 月 5 日</strong><br>
      <em>适用范围：</em> AEM 6.5 Forms 服务包 23<br>
      <em>设置说明：</em>
      <a href="/help/forms/using/mitigating-xxe-and-configuration-vulnerabilities-for-experience-manager-forms-jee.md#option-1-for-users-on-version-65230-install-latest-hotfix">
        用于缓解 JEE 上的 AEM Forms 中的 XXE、配置及远程代码执行（CVE-2025-49533）漏洞
      </a>
    </td>
    <td>
    <ul>
    <li><strong>Jboss：</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.23.0-win-jboss.zip">适用于在 Windows 上运行的 JBoss JEE 服务器的 AEM 服务包 6.5.23.0 的热修复补丁</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.23.0-linux-jboss.tar.gz">适用于在 Linux 上运行的 JBoss JEE 服务器的 AEM 服务包 6.5.23.0 的热修复补丁</a></li>
    <li><strong>Weblogic:</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.23.0-win-weblogic.zip">适用于在 WebLogic JEE 服务器上运行的 AEM 服务包 6.5.23.0 的热修复补丁</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.23.0-linux-weblogic.tar.gz">适用于在 Linux 上运行的 Weblogic JEE 服务器的 AEM 服务包 6.5.23.0 的热修复补丁</a></li>
    <li><strong>Websphere：</strong></li>
    <li>Windows — 适用于Websphere JEE服务器的Windows上的<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.23.0-win-websphere.zip">适用于AEM Service Pack 6.5.23.0的修补程序</a></li>
    <li>Linux — 适用于Linux上的AEM Service Pack 6.5.23.0的修补程序，用于Websphere JEE服务器<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.23.0-linux-websphere.zip"></a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li>通过修复 Adobe Experience Manager（AEM）Forms 中的远程代码执行（RCE）漏洞来增强安全性。该问题与管理用户界面（UI）中的 Struts 开发模式相关，此模式允许通过调试功能执行任意的对象图导航语言（OGNL）计算。此修复确保禁用 Struts 开发模式，并应用适当的安全过滤器以防止未经授权的访问。</li>
    <li>在 Adobe Experience Manager（AEM）Forms 的电子文档组件（EDC）模块中，增强了针对可扩展标记语言（XML）外部实体（XXE）漏洞的防护。这些漏洞源于对缺少 XXE 防护的 XML 文档处理不当，这可能会导致本地文件被读取。此修复包括：
      <ul>
        <li>确保在 SecurityCheckHandler 类中使用的 DocumentBuilderFactory 已正确配置，以防止 XXE 攻击。</li>
        <li>更新 EDC Web 服务以安全地处理 XML 文档，从而防止出现对本地文件的未经授权的访问。</li>
      </ul>
    </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>
      <strong>2025 年 8 月 5 日</strong><br>
      <em>适用范围：</em>AEM 6.5 Forms 服务包 18 – 22<br>
      <em>设置说明：</em>
      <a href="/help/forms/using/mitigating-xxe-and-configuration-vulnerabilities-for-experience-manager-forms-jee.md#option-2-for-users-on-65180---65220-manual-hotfix-installation">
         需对服务包 18–22 执行手动热修复补丁安装
      </a>
    </td>
    <td>
    <ul>
    <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-xxe-configuration-hotfix.zip">适用于 AEM 6.5 Forms 服务包 18 – AEM 6.5 Forms 服务包 22 的补丁 </a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li>通过修复 Adobe Experience Manager（AEM）Forms 中的远程代码执行（RCE）漏洞来增强安全性。该问题与管理用户界面（UI）中的 Struts 开发模式相关，此模式允许通过调试功能执行任意的对象图导航语言（OGNL）计算。此修复确保禁用 Struts 开发模式，并应用适当的安全过滤器以防止未经授权的访问。</li>
    <li>在 Adobe Experience Manager（AEM）Forms 的文档安全模块中，增强了针对可扩展标记语言（XML）外部实体（XXE）漏洞的防护。这些漏洞源于对缺少 XXE 防护的 XML 文档处理不当，这可能会导致本地文件被读取。此修复包括：
      <ul>
        <li>确保在 SecurityCheckHandler 类中使用的 DocumentBuilderFactory 已正确配置，以防止 XXE 攻击。</li>
        <li>更新文档安全 Web 服务以安全地处理 XML 文档，从而防止出现对本地文件的未经授权的访问。</li>
      </ul>
    </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2025 年 7 月 10 日 - </td>
    <td>
    <ul>
    <li><strong>Jboss：</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/jboss/adobe-aem-forms-jee-hotfix-6.5.23.0-win-jboss.zip">适用于在 Windows 上运行的 JBoss JEE 服务器的 AEM 服务包 6.5.23.0 的热修复补丁</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/jboss/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-jboss.tar.gz">适用于在 Linux 上运行的 JBoss JEE 服务器的 AEM 服务包 6.5.23.0 的热修复补丁</a></li>
    <li><strong>Weblogic:</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/weblogic/adobe-aem-forms-jee-hotfix-6.5.23.0-win-weblogic.zip">适用于在 WebLogic JEE 服务器上运行的 AEM 服务包 6.5.23.0 的热修复补丁</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/weblogic/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-weblogic.tar.gz">适用于在 Linux 上运行的 Weblogic JEE 服务器的 AEM 服务包 6.5.23.0 的热修复补丁</a></li>
    <li><strong>Websphere：</strong></li>
    <li>Windows：<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/websphere/adobe-aem-forms-jee-hotfix-6.5.23.0-win-websphere.zip">适用于在 Websphere JEE 服务器上运行的 AEM 服务包 6.5.23.0 的热修复补丁</a></li>
    <li>Linux：<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/websphere/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-websphere.tar.gz">适用于在 Linux 上运行的 Websphere JEE 服务器的 AEM 服务包 6.5.23.0 的热修复补丁</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li><strong>此热修复补丁解决了以下问题：</strong>
      <ul>
        <li><strong>FORMS-20533：</strong>AEM Forms 现已将表单组件中的 Struts 版本从 2.5.33 升级至 6.x。此次升级补充了 SP23 中未包含的 Struts 更新。相关支持已通过热修复补丁提供，您可以下载并安装该热修复补丁，以支持 Struts 的最新版本。</li>
        <li><strong>FORMS-20532：</strong>AEM Forms 现已将输出组件中的 Struts 版本从 2.5.33 升级至 6.x。此次升级补充了 SP23 中未包含的 Struts 更新。相关支持已通过热修复补丁提供，您可以下载并安装该热修复补丁，以支持 Struts 的最新版本。</li>
        <li><strong>FORMS-20203：</strong>当用户将 Struts 从 AEM 服务包 2.5.x 升级至 AEM Forms 服务包 6.x 时，策略 UI 无法显示所有配置，例如添加水印的选项。您可以通过下载并安装热修复补丁来解决此问题。</li>
        <li><strong>FORMS-20360：</strong>在升级到 AEM Forms 服务包 6.5.23.0 后，ImageToPDF 转化服务失败并出现以下错误：<br>
        <code>17:15:44,468 ERROR [com.adobe.pdfg.GeneratePDFImpl] (default task-49) ALC-PDG-001-000-ALC-PDG-011-028-Error occurred while converting the input image file to PDF. com/adobe/internal/pdftoolkit/core/encryption/EncryptionImp</code><br>
        您可以下载并安装热修复补丁来解决此问题。</li>
      </ul>
    </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2025 年 3 月 26 日 </br> </br> 要安装此修复，请按照<a href="/help/forms/using/mitigating-spring-framework-vulnerabilities-for-aem-forms-on-jee.md">缓解 JEE 上的 AEM Forms 的 Spring Framework 漏洞</a>的说明操作。</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/jboss/adobe-aem-forms-jee-hotfix-6.5.22.0-win-jboss.tar.gz">适用于在 Windows 上运行的 JBoss JEE 服务器的 AEM 服务包 6.5.22.0 的热修复补丁</a> </li>
      <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/jboss/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-jboss.tar.gz">适用于在 Linux 上运行的 JBoss JEE 服务器的 AEM 服务包 6.5.22.0 的热修复补丁</a> </li>
       <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/weblogic/adobe-aem-forms-jee-hotfix-6.5.22.0-win-weblogic.tar.gz">适用于在 WebLogic JEE 服务器上运行的 AEM 服务包 6.5.22.0 的热修复补丁</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/weblogic/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-weblogic.tar.gz">适用于在 Linux 上运行的 Weblogic JEE 服务器的 AEM 服务包 6.5.22.0 的热修复补丁</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/websphere/adobe-aem-forms-jee-hotfix-6.5.22.0-win-websphere.tar.gz">适用于在 Websphere JEE 服务器上运行的 AEM 服务包 6.5.22.0 的热修复补丁</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/websphere/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-websphere.tar.gz">适用于在 Linux 上运行的 Websphere JEE 服务器的 AEM 服务包 6.5.22.0 的热修复补丁</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>缓解 JEE 上的 AEM Forms 的 Spring Framework 漏洞</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024 年 7 月 10 日</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-jboss.zip.zip">适用于在 Windows 上运行的 JBoss JEE 服务器的 AEM 服务包 6.5.21.0 的热修复补丁</a> </li>
      <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-jboss.tar.gz">适用于在 Linux 上运行的 JBoss JEE 服务器的 AEM 服务包 6.5.21.0 的热修复补丁</a> </li>
       <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-websphere.zip.zip">适用于在 Webshpere JEE 服务器上运行的 AEM 服务包 6.5.21.0 的热修复补丁</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-websphere.tar.gz">适用于在 Linux 上运行的 Webshpere JEE 服务器的 AEM 服务包 6.5.21.0 的热修复补丁</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-weblogic.zip.zip">适用于在 WebLogic JEE 服务器上运行的 AEM 服务包 6.5.21.0 的热修复补丁</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-weblogic.tar.gz">适用于在 Linux 上运行的 Weblogic JEE 服务器的 AEM 服务包 6.5.21.0 的热修复补丁</a> </li>
     </ul>
     </td>
    <td>
    <ul><li>当用户在 JEE 服务器上更新至 AEM Forms 服务包 20（6.5.20.0），并使用输出服务生成 PDF 时，生成的 PDF 会出现可访问性问题。（LC-3922112）</li><li>在 AEM Forms JEE 上通过输出服务生成的标记 PDF 会显示“结构不当警告”。（LC-3922038）</li><li>当在 AEM Forms JEE 上提交表单时，数据中的重复 XML 元素实例会被移除。（LC-3922017）</li><li>当用户在 Linux 环境中以 HTML 形式渲染自适应表单（运行于 JEE）时，表单无法正常渲染。（LC-3921957）</li><li>当用户在 AEM Forms JEE 上使用输出服务将 XTG 文件转化为 PostScript 格式时，转化失败并报错：AEM_OUT_001_003: Unexpected Exception: PAExecute Failure: XFA_RENDER_FAILURE。（LC-3921720）</li><li>在 JEE 服务器上升级到 AEM Forms 服务包 18（6.5.18.0）后，当用户提交表单时，无法渲染 HTML5 或 PDF Forms，并且 XMLFM 会崩溃。（LC-3921718）
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024 年 6 月 21 日</td>
     <td>
     <ul>
     <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">适用于 JBoss JEE 服务器上的 AEM 服务包 6.5.21.0 或 AEM Forms 服务包 6.5.22.0 的热修复补丁</a> </li>
      <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">适用于 Weblogic JEE 服务器上的 AEM 服务包 6.5.21.0 或 AEM Forms 服务包 6.5.22.0 的热修复补丁</a> </li>
       <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">适用于 Webshpere JEE 服务器上的 AEM 服务包 6.5.21.0 或 AEM Forms 服务包 6.5.22.0 的热修复补丁</a> </li>
        <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">适用于 OSGi 服务器上的 AEM 服务包 6.5.21.0 或 AEM Forms 服务包 6.5.22.0 的热修复补丁</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li> 在升级到 AEM Forms 服务包 6.5.21.0 或 AEM Forms 服务包 6.5.22.0 后，PaperCapture 服务无法对 PDF 执行 OCR（光学字符识别）操作。有关安装说明，请参阅<a href="/help/forms/using/papercapture-service-resolution.md"> 故障排查</a>文章。（CQDOC-21680） </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024 年 6 月 21 日</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Fccm-ccr-content-10.0.206.zip">AEM 服务包 6.5.21.0 的热修复补丁 </a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>在预览过程中，带有 XML 数据的草稿信件会卡在加载状态。有关该修补程序的下载和安装说明，请参阅<a href="#install-hotfix">下载并安装草稿信件问题热修复补丁</a>部分。（FORMS-14521）</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024 年 5 月 16 日</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1192-010.zip">适用于 Microsoft Windows 的 AEM 服务包 6.5.20.0 的热修复补丁</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1192-010.zip">适用于 Linux 的 AEM 服务包 6.5.20.0 的热修复补丁</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1192-010.zip">适用于 Apple macOS 的 AEM 服务包 6.5.20.0 的热修复补丁</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>在基于 XDP 的自适应表单中，如果复选框中嵌入了脚本，则不会执行复选框之后的元素脚本。针对该问题，现已提供热修复补丁。（FORMS-14244） </li>
     <li> 在具有编辑/显示模式的字段中，日期选择器小组件在弹出窗口中切换月份时，行会被截断。针对该问题，现已提供热修复补丁。（FORMS-13620） </li>
     <li>在后端调用 DOR（记录文档）服务时，表单提交失败。出现的错误信息为：“提交操作无法完成，因为表单资源未正确分配。”（FORMS-13798） </li>
     <li>当从 Adobe Experience Manager 发布实例将自适应表单提交到 Adobe Experience Manager 工作流时，该工作流无法保存附件。（FORMS-14209） </li>
     <li> 安装 AEM 6.5 Forms 服务包 20 软件包（AEM Forms SP20 附加包）后，AEM Sites 用户界面（UI）的性能显著下降。（FORMS-13791） </li>
     <li>在交互式通信中，预填充服务因空指针异常而失败。（CQDOC-21355）</li>
     <li>使用基于用户凭据身份认证的旧版 Adobe Analytics 云服务的配置无法正常运行，导致分析规则无法执行。（FORMS-15428）
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024 年 1 月 29 日</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fforms-foundation-qs-content-4.0.170-FORMS-12692-B0001.zip">适用于在 Windows 上运行的 JEE 服务器的 AEM 服务包 6.5.19.0 的热修复补丁</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>在 JEE 服务器上的 AEM Forms 中，使用上下文路径的 HTML5 Forms 无法正常渲染。（FORMS-12485、FORMS-12691）。</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024 年 1 月 29 日</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-win-pkg-6.0.1016-004.zip">适用于 Microsoft Windows 的 AEM 服务包 6.5.18.0 的热修复补丁</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-linux-pkg-6.0.1016-004.zip">适用于 Linux 的 AEM 服务包 6.5.18.0 的热修复补丁</a></li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-osx-pkg-6.0.1016-004.zip">适用于 Apple macOS 的 AEM 服务包 6.5.18.0 的热修复补丁</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li> 开箱即用的 Scribble Signature 组件在自适应表单的预览中无法渲染。（FORMS-12073）。</li>
    </ul>
    </td>    
   </tr>
   <tr>
    <td>2023 年 11 月 20 日</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">适用于 Linux 的 AEM 服务包 6.5.18.0 的热修复补丁</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">适用于 Microsoft Windows 的 AEM 服务包 6.5.18.0 的热修复补丁</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">适用于 Apple macOS 的 AEM 服务包 6.5.18.0 的热修复补丁</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li>当在自适应表单的引导容器中设置了重定向 URL 时，内嵌签署功能会停止工作。（FORMS-10493）</li>
    <li>用于本地化自适应表单的记录文档（DoR）模板发布失败。（FORMS-10535）</li>
    <li>包含大型内联图像的交互式通信在编辑模式下无法打开。（FORMS-10578）</li>
    </ul>
    </td>    
  </tr>
  <tbody>
</table>

## 下载并安装 OSGi 热修复补丁 {#download-install-hotfix}

请执行以下步骤以下载并安装该热修复补丁：

1. 从软件分发链接下载[热修复补丁](#hotfix-for-adaptive-forms)。
1. 提取热修复补丁存档文件，以获取 Experience Manager 包（.zip）和捆绑包（.jar）文件。
1. 通过[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing)上传并安装包（.zip）。
1. 打开配置管理器捆绑包 `https://server:host/system/console/bundles`，上传并安装捆绑包（.jar）。热修复补丁即已安装完成。

## 安装 JEE 补丁 {#download-install-jee-patch}

有关安装 JEE 补丁的说明，请参阅 [AEM Forms JEE 补丁安装程序文档](/help/release-notes/jee-patch-installer-65.md)。


## 下载并安装草稿信件问题的热修复补丁 {#install-hotfix}

要解决此问题，请执行以下步骤：

1. 从软件分发门户下载[热修复补丁](#hotfix-for-adaptive-forms)。
2. 使用 [CRX 包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing)上传并安装包（.zip）。
