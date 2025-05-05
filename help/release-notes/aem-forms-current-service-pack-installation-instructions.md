---
title: 适用于AEM Forms的AEM Forms修补程序安装说明
description: 适用于OSGi和JEE环境的AEM Forms Service Pack安装说明
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: ae4c7e9d-9af8-4288-a6f9-e3bcbe7d153d
source-git-commit: 652878504d2225e50ea14885ec96bdd408f77ed0
workflow-type: tm+mt
source-wordcount: '1722'
ht-degree: 6%

---

# AEM 6.5 Forms Service Pack安装说明 {#aem-form-patch-installation-instructions}

## 发行版信息

| 产品 | Adobe Experience Manager 6.5 Forms |
|---|---|
| 版本号 | 6.5.22.0 |
| 类型 | Service Pack版本 |
| 日期 | 2024 年 11 月 29 日 |
| 下载 URL | [最新AEM Forms版本](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hans) |

>[!NOTE]
>
>有关已修复问题的完整列表，请参阅最新的[AEM Service Pack发行说明](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=zh-Hans)。

## Experience Manager Forms 6.5中包含的内容

Adobe Experience Manager (AEM) Forms service pack包含新增和升级的功能，例如客户请求的关键增强功能、性能、稳定性和安全性改进。 AEM Forms会定期发布Service Pack，以提供最新功能和改进功能。 根据您的技术栈栈，选择以下路径之一下载服务包并在您的环境中安装：

* [在JEE环境的AEM表单上下载并安装Service Pack](#download-and-install-for-jee-service-pack)
* [在OSGi环境上的AEM表单上下载并安装Service Pack](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> * Adobe每六个Service Pack发布一个完整安装程序。 AEM 6.5 Forms Service Pack 18 (6.5.18.0)是最新的JEE完整安装程序。 完整安装程序支持新平台，而常规Service Pack安装程序包括新增功能、错误修复和常规改进。 如果您要在JEE环境中执行全新安装或计划使用最新软件来安装AEM 6.5 Forms，Adobe建议使用于2023年8月31日发布的AEM 6.5.18.0 Forms on JEE完整安装程序，而不是于2019年4月8日发布的AEM 6.5 Forms安装程序或2022年3月3日发布的AEM 6.5.12.0 Forms安装程序。 使用完整安装程序后，安装最新的Service Pack。
> * [AEM 6.5 QuickStart](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=zh-Hans)中提供的AEM Forms功能(如自适应Forms)仅供探索和评估之用。 必须获得 AEM Forms 的有效许可证才能用于生产。

<!--

## Prerequisites {#prerequisites}

From AEM Service Pack 6.5.19.0 and onwards, XMLFM (XML output) will be available in 64-bit only, therefore you require the latest [Microsoft Visual C++ Redistributable (2015-2022) 64-bit](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170) to be installed on Windows Server prior to JEE or OSGi installation.

>[!NOTE]
> This prerequisite is required in addition to the already existing Microsoft Visual C++ Redistributable 32-bit.

-->

## 在JEE环境的AEM表单上下载并安装Service Pack {#download-and-install-for-jee-service-pack}

<!--
![JEE Installation](/help/forms/using/assets/jeeinstallation.png) -->

+++1. 备份现有环境

1. 备份[CRX存储库、数据库架构和GDS（全局文档存储）](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html?lang=zh-Hans)。
1. 备份&lt;*AEM_forms_root*>/deploy文件夹。

>[!NOTE]
>
> 在运行AEM Service Pack安装程序之前，请确保您对AEM安装目录具有写入访问权限。

+++

+++2. 下载所需的软件

* JEE Service Pack上的[AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hans)

* [片段Servlet](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Forg.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

* [AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=zh-Hans)
* [Forms附加组件包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hans)


+++

+++3. 安装Microsoft Visual C++可再发行软件包

* 在安装了Microsoft 6.5 Forms的计算机上下载并安装适用于Visual Studio 2015、2017、2019和2022[&#128279;](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022)的64位版本的AEM Visual C++可再发行包。

>[!NOTE]
>
> 确保您安装了可再发行组件（即使安装了以前的版本），以保证最新版本的可用性。

+++

+++4. 在JEE Service Pack上安装AEM Forms：

1. 停止应用程序服务器。
1. 将JEE Service Pack安装程序存档&#x200B;**上的** AEM Forms提取到硬盘驱动器：

   * **Windows**
导航到安装介质上的相应目录，或硬盘上您复制该目录的文件夹     安装程序，并双击`aemforms65_cfp_install.exe`文件。

      * （Windows 32位） `Windows\Disk1\InstData\VM`
      * （Windows 64位） `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
从外壳和类型`./aem65_cfp_install.bin`导航到相应的目录。

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   这会启动安装向导，引导您完成安装。

1. 在“Introduction”面板上，单击 **[!UICONTROL Next]**。
1. 在&#x200B;**选择安装文件夹**&#x200B;屏幕上，验证显示的默认位置对于您的现有安装是否正确，或者单击&#x200B;**[!UICONTROL 浏览]**&#x200B;以选择安装AEM表单的替代文件夹，然后单击&#x200B;**[!UICONTROL 下一步]**。
1. 阅读Service Pack摘要信息，然后单击&#x200B;**[!UICONTROL 下一步]**。
1. 阅读“Pre-Installation Summary”信息，然后单击 **[!UICONTROL Install]**。
1. 安装完成后，单击 **[!UICONTROL Next]** 以将快速修补程序更新应用到已安装的文件。
1. **[仅适用于Windows]：**&#x200B;执行以下步骤之一：

   * 在单击&#x200B;**[!UICONTROL 完成]**&#x200B;之前，请取消选择&#x200B;**Start Configuration Manager**&#x200B;选项。 在`[aem-forms root]\configurationManager\bin`中使用&#x200B;**ConfigurationManager.bat**&#x200B;文件运行&#x200B;**Configuration Manager**。

   * 或者取消选择&#x200B;**Start Configuration Manager**&#x200B;选项，然后再单击&#x200B;**[!UICONTROL 完成]**。 在使用&#x200B;**ConfigurationManager.exe**&#x200B;或&#x200B;**ConfigurationManager_IPv6.exe**&#x200B;运行&#x200B;**Configuration Manager**&#x200B;之前，导航到&#x200B;*`<AEMForms_Install_Dir>\configurationManager\bin`*&#x200B;目录，并用最新的[ConfigurationManager.lax](/help/assets/ConfigurationManager.lax)和[ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax)文件替换&#x200B;**ConfigurationManager.lax**&#x200B;和&#x200B;**ConfigurationManager_IPV6.lax**&#x200B;在这两个文件中具有&#x200B;**轴 — 1.4.1.2.jar**&#x200B;的&#x200B;**轴 — 1.4.1.1.jar**。

     >[!NOTE]
     >
     >* 更新或替换&#x200B;**ConfigurationManager.bat**&#x200B;文件有助于避免手动更新.lax文件。

1. **[仅基于Unix]：**&#x200B;默认情况下选中&#x200B;**启动配置管理器**&#x200B;复选框。 单击&#x200B;**[!UICONTROL 完成]**&#x200B;以立即运行配置管理器，或稍后运行&#x200B;**配置管理器**，取消选择&#x200B;**启动配置管理器**&#x200B;选项，然后再单击&#x200B;**[!UICONTROL 完成]**。 稍后可以使用`[AEM_forms_root]/configurationManager/bin`目录中的相应脚本启动&#x200B;**配置管理器**。

1. 根据您的应用程序服务器，选择以下文档之一，然后按照&#x200B;*配置和部署AEM表单*&#x200B;部分中的说明操作。

   * [安装和部署AEM forms for JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65_cn)
   * [安装和部署AEM Forms for WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65_cn)
   * [安装和部署AEM Forms for WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_65_cn)
   * [安装和部署AEM Forms for JBoss®群集](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-jboss.pdf)
   * [安装和部署AEM Forms for WebSphere®群集](https://helpx.adobe.com/cn/content/dam/help/experience-manager/6-5/forms/pdf/install-cluster-websphere.pdf)
   * [安装和部署AEM Forms for WebLogic群集](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-weblogic.pdf)


>[!NOTE]
>
>* 在JEE Service Pack上安装AEM Forms后，需要先从`crx-repository\install`文件夹中删除Forms附加组件包，然后再重新启动appserver。 从[软件分发门户](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hans)下载最新的Forms附加组件包。
>* 建议使用“Ctrl + C”命令重新启动SDK。 使用替代方法（例如，停止Java流程）重新启动AEM SDK可能会导致AEM开发环境不一致。
>* 对于缓解JEE上AEM Forms的Spring Framework漏洞的[修补程序](/help/release-notes/aem-forms-hotfix.md)，在群集环境中部署时，确保使用JDK 17启动定位器至关重要。

+++

+++5. 如果未安装，请安装servlet片段（**强制步骤**）

<!-- >[!NOTE] > > * If you are upgrading from **AEM Service Pack 6.5.15.0**, the installation of the **servlet fragment** is not required. For versions **AEM Service Pack 6.5.14.0** or earlier, it is **mandatory to install** the servlet fragment. -->

要下载并安装servlet片段，请执行以下操作：

1. 如果尚未下载片段，请从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)下载。

2. 启动应用程序服务器，等待日志稳定并检查捆绑包状态。

3. 打开Web控制台包。 默认URL为`http://[Server]:[Port]/system/console/bundles`。

4. 单击安装/更新。 选择下载的片段`org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`。 单击&#x200B;**安装**&#x200B;或&#x200B;**更新**。 等待应用程序服务器稳定

5. 停止应用程序服务器。

+++

+++6. 安装AEM Service Pack

1. 如果实例处于更新模式（从早期版本更新实例时），请在安装之前重新启动该实例。 如果实例的当前正常运行时间较长，Adobe建议重新启动。
1. 安装之前，请为[!DNL Experience Manager]实例拍摄快照或进行全新备份。
1. 从[Software Distribution](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hans)下载Service Pack。<!-- UPDATE FOR EACH NEW RELEASE -->
1. 打开包管理器，然后选择&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。 若要了解更多信息，请参阅[包管理器](/help/sites-administering/package-manager.md)。
1. 选择包，然后选择&#x200B;**[!UICONTROL 安装]**。

**自动安装**

可以使用两种不同的方法来自动安装[!DNL ExperienceManager] Service Pack。<!--       UPDATE FOR EACH NEW RELEASE -->

* 当服务器联机时，将包放入`../crx-quickstart/install`文件夹中。
程序包为      自动安装。

* 使用包管理器[&#128279;](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hans)中的HTTP API。 使用`cmd=install&recursive=true`安装嵌套包。

  >[!NOTE]
  >
  >Experience Manager service pack不支持Bootstrap安装。<!-- UPDATE FOR EACH NEW RELEASE -->

  **验证安装**

  要了解经认证可与此版本配合使用的平台，请参阅[技术要求](/help/sites-deploying/technical-requirements.md)。

   1. 产品信息页面(`/system/console/productinfo`)在[!UICONTROL 已安装的产品].<!-- UPDATE FOR EACH NEW RELEASE -->下显示更新的版本字符串`Adobe Experience Manager (spversion)`
   1. 在OSGi控制台中，所有OSGi包均为&#x200B;**[!UICONTROL 活动]**&#x200B;或&#x200B;**[!UICONTROL 片段]**（使用Web）     控制台： `/system/console/bundles`)。
   1. OSGi捆绑包`org.apache.jackrabbit.oak-core`的版本为1.22.14或更高版本（使用WebConsole： `/system/console/bundles`）。

+++

+++7. 安装AEM Experience Manager Forms附加组件包

1. 确保您已安装[!DNL Experience Manager]服务包。
1. 下载适用于您的操作系统的 [AEM Forms 发行版](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hans)中列出的相应 Forms 附加组件包。
1. 安装Forms附加组件包，如[安装AEM Forms附加组件包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hans)中所述。
1. 如果您在Experience Manager 6.5 Forms中使用字母，请安装[最新的AEMFD兼容包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hans)。

+++

## 在OSGi环境上的AEM表单上下载并安装Service Pack {#download-and-install-for-osgi-service-pack}


<!-- ![OSGi Installation Steps](/help/forms/using/assets/osgiinstallation.png)
-->

+++1. 备份现有环境

1. 备份[CRX存储库和数据库架构](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html?lang=zh-Hans)。

>[!NOTE]
>
> 如果安装关系数据库的AEM Forms Service Pack，则必须备份DB_schema。

+++

+++2. 下载所需的软件

* [AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=zh-Hans)
* [Forms附加组件包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hans)

+++

+++ 3.安装Microsoft Visual C++可再发行软件包

* 在安装了Microsoft 6.5 Forms的计算机上下载并安装适用于Visual Studio 2015、2017、2019和2022[&#128279;](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022)的64位版本的AEM Visual C++可再发行包。

>[!NOTE]
>
>
> 确保您安装了可再发行组件（即使安装了以前的版本），以保证最新版本的可用性。

+++

+++4. 安装AEM Service Pack

1. 如果实例处于更新模式（从早期版本更新实例时），请在安装之前重新启动该实例。 如果实例的当前正常运行时间较长，Adobe建议重新启动。
1. 安装之前，请为[!DNL Experience Manager]实例拍摄快照或进行全新备份。
1. 从[Software Distribution](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hans)下载Service Pack。<!-- UPDATE FOR EACH NEW RELEASE -->
1. 打开包管理器，然后选择&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。 若要了解更多信息，请参阅[包管理器](/help/sites-administering/package-manager.md)。
1. 选择包，然后选择&#x200B;**[!UICONTROL 安装]**。

**自动安装**

可以使用两种不同的方法来自动安装[!DNL Experience Manager] Service Pack。<!--  UPDATE FOR EACH NEW RELEASE -->

* 当服务器联机时，将包放入`../crx-quickstart/install`文件夹中。 程序包为      自动安装。
* 使用包管理器[&#128279;](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hans)中的HTTP API。 使用`cmd=install&recursive=true`安装嵌套包。

  >[!NOTE]
  >
  >Experience Manager service pack不支持Bootstrap安装。<!-- UPDATE FOR EACH NEW RELEASE -->

  **验证安装**

  要了解经认证可与此版本配合使用的平台，请参阅[技术要求](/help/sites-deploying/technical-requirements.md)。

   1. 产品信息页面(`/system/console/productinfo`)在[!UICONTROL 已安装的产品]下显示更新的版本字符串`Adobe Experience Manager (spversion)`。<!-- UPDATE FOR EACH NEW RELEASE -->

   1. 在OSGi控制台中，所有OSGi包均为&#x200B;**[!UICONTROL 活动]**&#x200B;或&#x200B;**[!UICONTROL 片段]**（使用Web控制台： `/system/console/bundles`）。

      1. OSGi捆绑包`org.apache.jackrabbit.oak-core`的版本为1.22.14或更高版本（使用Web控制台： `/system/console/bundles`）。

+++

+++5. 安装Adobe Experience Manager Forms (AEM)附加组件包

1. 确保您已安装[!DNL Experience Manager]服务包。
1. 下载适用于您的操作系统的 [AEM Forms 发行版](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hans)中列出的相应 Forms 附加组件包。
1. 安装Forms附加组件包，如[安装AEM Forms附加组件包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hans)中所述。
1. 如果您在Experience Manager 6.5 Forms中使用字母，请安装[最新的AEMFD兼容包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hans)。

+++

## 疑难解答

* 如果在安装Service Pack期间存在包管理器UI **上的**&#x200B;对话框，请等待错误日志稳定下来，然后再访问部署。 等待与卸载更新程序捆绑包相关的特定日志，然后确定安装成功。 通常，此问题发生在Safari浏览器中，但可能会间歇性地发生在任何浏览器中。

* 安装完成后，检查监视器日志(error.log)中是否有任何活动。 等待几分钟，直到日志中没有活动。 重新启动AEM实例。

* 如果在安装AEM Forms 6.5.15.0或更高版本的Service Pack后出现&#x200B;**服务不可用错误**，请[安装Servlet片段和捆绑包](/help/forms/using/aem-service-pack-installation-solution.md)以修复该错误。
