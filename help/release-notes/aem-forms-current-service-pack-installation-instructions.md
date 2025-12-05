---
title: AEM Forms 补丁安装说明
description: AEM Forms 服务包在 OSGi 和 JEE 环境中的安装说明
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: ae4c7e9d-9af8-4288-a6f9-e3bcbe7d153d
source-git-commit: 69761b38aec51f080e53235ae3cff5d4049427f2
workflow-type: tm+mt
source-wordcount: '1722'
ht-degree: 99%

---

# AEM 6.5 Forms 服务包安装说明 {#aem-form-patch-installation-instructions}

## 发行版本信息

| 产品 | Adobe Experience Manager 6.5 Forms |
|---|---|
| 版本 | 6.5.24.0 |
| 类型 | 服务包发行 |
| 日期 | 2025年12月4日 |
| 下载 URL | [最新 AEM Forms 版本](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) |

>[!NOTE]
>
>请参阅最新的 [AEM 服务包发行说明](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html)，获取已修复问题的完整列表。

## Experience Manager Forms 6.5 包含的功能

Adobe Experience Manager（AEM）Forms 服务包包含了新的和升级的功能，例如客户重点请求的增强功能，以及性能、稳定性和安全性改进。AEM Forms 会定期发布服务包，以提供最新的功能和改进。根据您的技术栈，选择以下路径之一，以在您的环境中下载并安装服务包：

* [在 JEE 环境下的 AEM Form 下载并安装服务包](#download-and-install-for-jee-service-pack)
* [在 OSGi 环境下的 AEM Form 下载并安装服务包](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> * Adobe 会在每发布六个服务包时发布完整安装程序。AEM 6.5 Forms 服务包 18（6.5.18.0）是最新的 JEE 完整安装程序。完整安装程序支持新平台，而常规服务包安装程序则包含新功能、错误修复和常规改进。如果您计划在 JEE 环境下的 AEM 6.5 Forms 执行全新安装或使用最新的软件，Adobe 建议使用 2023 年 8 月 31 日发布的 JEE 上的 AEM 6.5.18.0 Forms 完整安装程序，而不是使用 2019 年 4 月 8 日发布的 AEM 6.5 Forms 安装程序或 2022 年 3 月 3 日发布的 AEM 6.5.12.0 Forms 安装程序。在使用完整安装程序后，请安装最新的服务包。
> * [AEM 6.5 QuickStart](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html) 中提供的 AEM Forms 功能（如自适应表单）仅供探索和评估使用。必须获得 AEM Forms 的有效许可证才能用于生产。

<!--

## Prerequisites {#prerequisites}

From AEM Service Pack 6.5.19.0 and onwards, XMLFM (XML output) will be available in 64-bit only, therefore you require the latest [Microsoft Visual C++ Redistributable (2015-2022) 64-bit](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170) to be installed on Windows Server prior to JEE or OSGi installation.

>[!NOTE]
> This prerequisite is required in addition to the already existing Microsoft Visual C++ Redistributable 32-bit.

-->

## 在 JEE 环境下的 AEM Form 下载并安装服务包 {#download-and-install-for-jee-service-pack}

<!--
![JEE Installation](/help/forms/using/assets/jeeinstallation.png) -->

+++&#x200B;1. 备份您现有的环境

1. 备份您的 [CRX 存储库、数据库架构和 GDS（全局文档存储）](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html)。
1. 备份 *AEM_forms_root*>/deploy 文件夹。

>[!NOTE]
>
> 在运行 AEM 服务包安装程序之前，请确保您对 AEM 安装目录具有写入权限。

+++

+++2.下载所需软件

* [JEE 上的 AEM Forms 服务包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)

* [片段 Servlet](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Forg.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

* [AEM 服务包](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html)
* [Forms 附加组件包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)


+++

+++&#x200B;3. 安装 Microsoft Visual C++ 可再发行组件包

* 在安装了 AEM 6.5 Forms 的计算机上，下载并安装[适用于 Visual Studio 2015、2017、2019 和 2022 的 64 位 Microsoft Visual C++ 可再发行组件包](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022)。

>[!NOTE]
>
> 请务必安装该可再发行组件包，即使系统中已存在旧版本，也需安装以确保最新版本的可用性。

+++

+++&#x200B;4. 安装 JEE 上的 AEM Forms 服务包：

1. 停止应用程序服务器。
1. 将 **JEE 上的 AEM Forms 服务包安装程序存档**&#x200B;提取到您的硬盘驱动器：

   * **Windows**
进入安装介质或您复制安装程序的硬盘文件夹中的相应目录，然后双击 `aemforms65_cfp_install.exe` 文件。

      * （Windows 32 位）`Windows\Disk1\InstData\VM`
      * （Windows 64 位）`Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
进入相应目录，在 Shell 中输入 `./aem65_cfp_install.bin`。

      * （Linux®）`Linux/Disk1/InstData/NoVM`

   这会启动安装向导，引导您完成安装。

1. 在“Introduction”面板上，单击 **[!UICONTROL Next]**。
1. 在&#x200B;**选择安装文件夹**&#x200B;屏幕上，确认默认显示的位置是否正确匹配您现有的安装，或单击&#x200B;**[!UICONTROL 浏览]**&#x200B;选择 AEM Forms 安装的替代文件夹，然后单击&#x200B;**[!UICONTROL 下一步]**。
1. 阅读服务包摘要信息，然后单击&#x200B;**[!UICONTROL 下一步]**。
1. 阅读“Pre-Installation Summary”信息，然后单击 **[!UICONTROL Install]**。
1. 安装完成后，单击 **[!UICONTROL Next]** 以将快速修补程序更新应用到已安装的文件。
1. **[仅适用于 Windows]：**&#x200B;执行以下步骤之一：

   * 在单击&#x200B;**[!UICONTROL 完成]**&#x200B;之前，取消选择&#x200B;**启动配置管理器**&#x200B;选项。使用 `[aem-forms root]\configurationManager\bin` 中的 **ConfigurationManager.bat** 文件运行&#x200B;**配置管理器**。

   * 或者在单击&#x200B;**[!UICONTROL 完成]**&#x200B;之前，取消选择&#x200B;**启动配置管理器**&#x200B;选项。如果要通过 **ConfigurationManager.exe** 或 **ConfigurationManager_IPv6.exe** 运行&#x200B;**配置管理器**，请先进入 *`<AEMForms_Install_Dir>\configurationManager\bin`* 目录，将 **ConfigurationManager.lax** 和 **ConfigurationManager_IPV6.lax** 替换为最新的 [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) 和 [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) 文件，然后在这两个文件中查找并将 **axis-1.4.1.1.jar** 替换为 **axis-1.4.1.2.jar**。

     >[!NOTE]
     >
     >* 更新或替换 **ConfigurationManager.bat** 文件可以避免手动更新 .lax 文件。

1. **[仅适用于基于 Unix 的系统]：****启动配置管理器**&#x200B;复选框默认已选中。单击&#x200B;**[!UICONTROL 完成]**&#x200B;可立即运行配置管理器，或者如果希望稍后再运行&#x200B;**配置管理器**，请在单击&#x200B;**[!UICONTROL 完成]**&#x200B;之前取消选中&#x200B;**启动配置管理器**&#x200B;选项。您也可以稍后通过运行 `[AEM_forms_root]/configurationManager/bin` 目录下的相应脚本来启动&#x200B;**配置管理器**。

1. 根据您所使用的应用程序服务器，选择以下文档之一，并按&#x200B;*配置和部署 AEM Forms* 部分的说明进行操作。

   * [安装和部署 AEM forms for JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [安装和部署 AEM forms for WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)
   * [安装和部署 AEM Forms for WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_65)
   * [安装和部署 AEM forms for JBoss® 群集](https://helpx.adobe.com/cn/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-jboss.pdf)
   * [安装和部署 AEM forms for WebSphere® 群集](https://helpx.adobe.com/cn/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-websphere.pdf)
   * [安装和部署 AEM Forms for WebLogic 群集](https://helpx.adobe.com/cn/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-weblogic.pdf)


>[!NOTE]
>
>* 安装完 JEE 上的 AEM Forms 服务包后，必须在重启应用程序服务器之前，从 `crx-repository\install` 文件夹中移除 Forms 附加组件包。从[软件分发门户](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)下载最新的 Forms 附加组件包。
>* 建议使用 “Ctrl + C” 命令重新启动 SDK。如果使用其他方式（例如停止 Java 进程）重新启动 AEM SDK，则可能会导致 AEM 开发环境出现不一致情况。
>* 对于[用于缓解 JEE 上的 AEM Forms 中 Spring Framework 漏洞的热修复补丁](/help/release-notes/aem-forms-hotfix.md)，在群集环境中部署时，必须确保定位器使用 JDK 17 启动。

+++

+++&#x200B;5. 如果尚未安装 Servlet 片段，请进行安装（**必需步骤**）

<!-- >[!NOTE] > > * If you are upgrading from **AEM Service Pack 6.5.15.0**, the installation of the **servlet fragment** is not required. For versions **AEM Service Pack 6.5.14.0** or earlier, it is **mandatory to install** the servlet fragment. -->

下载并安装 Servlet 片段的方法：

1. 如果尚未下载该片段，请从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)下载。

2. 启动应用程序服务器，等待日志稳定后检查捆绑包状态。

3. 打开网页控制台捆绑包。默认 URL 为 `http://[Server]:[Port]/system/console/bundles`。

4. 单击“安装/更新”。选择已下载的片段 `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`。点击&#x200B;**安装**&#x200B;或&#x200B;**更新**。等待应用程序服务器稳定

5. 停止应用程序服务器。

+++

+++&#x200B;6. 安装 AEM 服务包

1. 如果实例处于更新模式（即由早期版本升级而来），请在安装前先重启该实例。如果实例已长时间运行，Adobe 建议先重启。
1. 在安装之前，请为您的 [!DNL Experience Manager] 实例创建快照或执行一次全新的备份。
1. 从[软件分发](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)下载服务包。<!-- UPDATE FOR EACH NEW RELEASE -->
1. 打开包管理器，然后选择&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传该包。如需了解更多信息，请参阅[包管理器](/help/sites-administering/package-manager.md)。
1. 选择该包，然后选择&#x200B;**[!UICONTROL 安装]**。

**自动安装**

您可以通过以下两种方式之一自动安装 [!DNL ExperienceManager] 服务包。<!--       UPDATE FOR EACH NEW RELEASE -->

* 当服务器在线时，将包放入 `../crx-quickstart/install` 文件夹中。
该包会自动安装。

* 使用[包管理器的 HTTP API](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)。请使用 `cmd=install&recursive=true` 以便安装嵌套的包。

  >[!NOTE]
  >
  >Experience Manager 服务包不支持 Bootstrap 安装。<!-- UPDATE FOR EACH NEW RELEASE -->

  **验证安装**

  要了解与此版本兼容的已经过认证的平台，请参阅[技术要求](/help/sites-deploying/technical-requirements.md)。

   1. 在[!UICONTROL 已安装的产品]下，产品信息页面（`/system/console/productinfo`）会显示更新后的版本字符串 `Adobe Experience Manager (spversion)`。<!-- UPDATE FOR EACH NEW RELEASE -->
   1. 在 OSGi 控制台中，所有 OSGi 捆绑包均应处于&#x200B;**[!UICONTROL 活跃]**&#x200B;或&#x200B;**[!UICONTROL 片段]**&#x200B;状态（使用网页控制台：`/system/console/bundles`）。
   1. OSGi 捆绑包 `org.apache.jackrabbit.oak-core` 的版本应为 1.22.14 或更高版本（使用网页控制台：`/system/console/bundles`）。

+++

+++&#x200B;7. 安装 AEM Experience Manager Forms 附加组件包

1. 请确保已安装相应的 [!DNL Experience Manager] 服务包。
1. 下载适用于您的操作系统的 [AEM Forms 版本](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)中列出的相应 Forms 附加组件包。
1. 按照[安装 AEM Forms 附加组件包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)中的所述安装 Forms 附加组件包。
1. 如果您在 Experience Manager 6.5 Forms 中使用书信，请安装[最新的 AEMFD 兼容包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)。

+++

## 在 OSGi 环境下的 AEM Form 下载并安装服务包 {#download-and-install-for-osgi-service-pack}


<!-- ![OSGi Installation Steps](/help/forms/using/assets/osgiinstallation.png)
-->

+++&#x200B;1. 备份您现有的环境

1. 备份您的 [CRX 存储库和数据库架构](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html)。

>[!NOTE]
>
> 如果您为关系型数据库安装 AEM Forms 服务包，则必须备份 DB_schema。

+++

+++2.下载所需软件

* [AEM 服务包](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html)
* [Forms 附加组件包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)

+++

+++ &#x200B;3. 安装 Microsoft Visual C++ 可再发行组件包

* 在安装了 AEM 6.5 Forms 的计算机上，下载并安装[适用于 Visual Studio 2015、2017、2019 和 2022 的 64 位 Microsoft Visual C++ 可再发行组件包](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022)。

>[!NOTE]
>
>
> 请务必安装该可再发行组件包，即使系统中已存在旧版本，也需安装以确保最新版本的可用性。

+++

+++&#x200B;4. 安装 AEM 服务包

1. 如果实例处于更新模式（即由早期版本升级而来），请在安装前先重启该实例。如果实例已长时间运行，Adobe 建议先重启。
1. 在安装之前，请为您的 [!DNL Experience Manager] 实例创建快照或执行一次全新的备份。
1. 从[软件分发](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)下载服务包。<!-- UPDATE FOR EACH NEW RELEASE -->
1. 打开包管理器，然后选择&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传该包。如需了解更多信息，请参阅[包管理器](/help/sites-administering/package-manager.md)。
1. 选择该包，然后选择&#x200B;**[!UICONTROL 安装]**。

**自动安装**

您可以通过以下两种方式之一自动安装 [!DNL Experience Manager] 服务包。<!--  UPDATE FOR EACH NEW RELEASE -->

* 当服务器在线时，将包放入 `../crx-quickstart/install` 文件夹中。该包会自动安装。
* 使用[包管理器的 HTTP API](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)。请使用 `cmd=install&recursive=true` 以便安装嵌套的包。

  >[!NOTE]
  >
  >Experience Manager 服务包不支持 Bootstrap 安装。<!-- UPDATE FOR EACH NEW RELEASE -->

  **验证安装**

  要了解与此版本兼容的已经过认证的平台，请参阅[技术要求](/help/sites-deploying/technical-requirements.md)。

   1. 在[!UICONTROL 已安装的产品]下，产品信息页面（`/system/console/productinfo`）会显示更新后的版本字符串 `Adobe Experience Manager (spversion)`。<!-- UPDATE FOR EACH NEW RELEASE -->

   1. 在 OSGi 控制台中，所有 OSGi 捆绑包均应处于&#x200B;**[!UICONTROL 活跃]**&#x200B;或&#x200B;**[!UICONTROL 片段]**&#x200B;状态（使用网页控制台：`/system/console/bundles`）。

      1. OSGi 捆绑包 `org.apache.jackrabbit.oak-core` 的版本应为 1.22.14 或更高版本（使用网页控制台：`/system/console/bundles`）。

+++

+++&#x200B;5. 安装 Adobe Experience Manager Forms（AEM）附加组件包

1. 请确保已安装相应的 [!DNL Experience Manager] 服务包。
1. 下载适用于您的操作系统的 [AEM Forms 版本](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)中列出的相应 Forms 附加组件包。
1. 按照[安装 AEM Forms 附加组件包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)中的所述安装 Forms 附加组件包。
1. 如果您在 Experience Manager 6.5 Forms 中使用书信，请安装[最新的 AEMFD 兼容包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)。

+++

## 疑难解答

* 如果在安装服务包过程中&#x200B;**包管理器 UI 对话框**&#x200B;意外退出，请等待错误日志稳定后再访问部署。在确认安装成功之前，请先等待与卸载更新程序包相关的特定日志出现。通常，该问题会在 Safari 浏览器中出现，但也可能会在其他浏览器中间歇出现。

* 安装完成后，请检查监控日志（error.log），确认是否还有活动。请等待几分钟，直到日志中不再有任何活动。重启 AEM 实例。

* 如果在安装 AEM Forms 6.5.15.0 或更高版本的服务包后遇到&#x200B;**服务不可用错误**，请[安装 Servlet 片段和捆绑包](/help/forms/using/aem-service-pack-installation-solution.md)以修复该错误。
