---
title: AEM Forms JEE修补程序安装程序
description: 了解如何使用AEM Forms JEE修补程序安装程序来修复AEM 6.5 Forms组件中的问题。
content-type: reference
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
hide: true
hidefromtoc: true
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 17%

---

# AEM Forms JEE修补程序安装程序 {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[联系支持人员](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support)以获取详细信息或获取修补程序。

## 关于修补程序安装程序 {#about-the-patch-installer}

AEM 6.5 Forms JEE修补程序安装程序包含在此修补程序发布之前可用的AEM 6.5 Forms JEE所有组件的所有已修复问题。 有关已修复问题的完整列表，请参阅最新的[Service Pack发行说明](release-notes.md)。

## 安装补丁程序的先决条件 {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## 安装和配置修补程序 {#installing-and-configuring-the-patch}

1. 备份&lt;*AEM_forms_root*>/deploy文件夹。 如果您决定卸载快速修补程序，则必须执行此操作。
1. 停止应用程序服务器。
1. 将补丁安装程序存档文件提取到硬盘驱动器。
1. 在根据您所使用的操作系统命名的目录中：

   * **Windows**
导航到安装介质上的相应目录或硬盘上复制安装程序的文件夹，然后双击aemforms65_cfp_install.exe文件。

      * （Windows 32位） `Windows\Disk1\InstData\VM`
      * （Windows 64位） `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
导航到相应的目录，然后在命令提示符下键入`./aem65_cfp_install.bin`。

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   这会启动安装向导，引导您完成安装。

1. 在“Introduction”面板上，单击 **[!UICONTROL Next]**。
1. 在&#x200B;**选择安装文件夹**&#x200B;屏幕上，验证显示的默认位置对于您的现有安装是否正确，或者单击&#x200B;**[!UICONTROL 浏览]**&#x200B;以选择安装AEM表单的备用文件夹，然后单击&#x200B;**[!UICONTROL 下一步]**。
1. 阅读“Quick Fix Patch Summary”信息，然后单击 **[!UICONTROL Next]**。
1. 阅读“Pre-Installation Summary”信息，然后单击 **[!UICONTROL Install]**。
1. 安装完成后，单击 **[!UICONTROL Next]** 以将快速修补程序更新应用到已安装的文件。

1. **[仅适用于Windows]：**&#x200B;执行以下操作：
   * 在单击&#x200B;**[!UICONTROL 完成]**&#x200B;之前，请取消选择&#x200B;**Start Configuration Manager**&#x200B;选项。 在`[aem-forms root]\configurationManager\bin`中使用&#x200B;**ConfigurationManager.bat**&#x200B;文件运行&#x200B;**Configuration Manager**。

   * 或者取消选择&#x200B;**Start Configuration Manager**&#x200B;选项，然后再单击&#x200B;**[!UICONTROL 完成]**。 在使用&#x200B;**ConfigurationManager.exe**&#x200B;或&#x200B;**ConfigurationManager_IPv6.exe**&#x200B;运行&#x200B;**Configuration Manager**&#x200B;之前，导航到&#x200B;*`<AEMForms_Install_Dir>\configurationManager\bin`*&#x200B;目录，并用最新的[ConfigurationManager.lax](/help/assets/ConfigurationManager.lax)和[ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax)文件替换&#x200B;**ConfigurationManager.lax**&#x200B;和&#x200B;**ConfigurationManager_IPV6.LAX**。这两个文件中包含&#x200B;**AXIS-1.4.1.2.JAR**&#x200B;的1.1.JAR **。**

   >[!NOTE]
   >
   >使用&#x200B;**ConfigurationManager.bat**&#x200B;文件有助于避免手动更新.lax文件的名称。
   >

1. **[仅基于Unix]：**

   * 默认情况下，**启动配置管理器**&#x200B;复选框处于选中状态。 单击&#x200B;**[!UICONTROL 完成]**&#x200B;以立即运行配置管理器，或稍后运行&#x200B;**配置管理器**，取消选择&#x200B;**启动配置管理器**&#x200B;选项，然后再单击&#x200B;**[!UICONTROL 完成]**。 稍后可以使用`[AEM_forms_root]/configurationManager/bin`目录中的相应脚本启动&#x200B;**配置管理器**。

1. 根据您的应用程序服务器，选择以下文档之一，然后按照&#x200B;*配置和部署AEM表单*&#x200B;部分中的说明操作。

   * [安装和部署AEM forms for JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [安装和部署AEM Forms for WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)

1. (仅限JBoss®)安装修补程序并配置服务器后，删除JBoss®应用程序服务器的tmp和工作目录。

## Post部署配置 {#post-deployment-configurations}

### SAML配置 {#saml-configurations}

如果已配置SAML身份验证并且遇到大型IDP元数据问题，请在安装修补程序后执行以下操作：

1. 在应用程序服务器中设置以下系统属性：\
   `um.saml.enable.large.xml=true`
1. 重新启动服务器。
1. 按照SAML设置中的说明，删除现有的SAML身份验证提供程序，然后为现有域再次添加它们。

>[!NOTE]
>
> 建议使用“Ctrl + C”命令重新启动SDK。 使用替代方法（例如，停止Java进程）重新启动AEM SDK可能会导致AEM开发环境不一致。

## 受影响的模块 {#impacted-modules}

* 文档服务
* 文档安全
* Foundation JEE

[联系支持人员](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support)
