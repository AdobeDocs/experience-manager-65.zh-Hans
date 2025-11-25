---
title: AEM Forms JEE 补丁安装程序
description: 了解如何使用 AEM Forms JEE 补丁安装程序修复 AEM 6.5 Forms 组件中的问题。
content-type: reference
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
hide: true
hidefromtoc: true
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 100%

---

# AEM Forms JEE 补丁安装程序 {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>如需了解更多信息或获取补丁，请[联系支持人员](https://experienceleague.adobe.com/?support-solution=General&support-tab=home#support)。

## 关于补丁安装程序 {#about-the-patch-installer}

AEM 6.5 Forms JEE 补丁安装程序包含此补丁发布之前 AEM 6.5 Forms JEE 所有组件的所有已修复问题。请参阅最新的[服务包发行说明](release-notes.md)，获取已修复问题的完整列表。

## 安装补丁的先决条件 {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## 安装和配置补丁 {#installing-and-configuring-the-patch}

1. 请先备份 &lt;*AEM_forms_root*>/deploy 文件夹。如果您决定卸载快速修补程序，则必须执行此操作。
1. 停止应用程序服务器。
1. 将补丁安装程序存档文件提取到硬盘驱动器。
1. 在根据您所使用的操作系统命名的目录中：

   * **Windows**
进入安装介质中的相应目录，或进入硬盘上复制安装程序的文件夹，双击运行 aemforms65_cfp_install.exe 文件。

      * （Windows 32 位）`Windows\Disk1\InstData\VM`
      * （Windows 64 位）`Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
进入相应目录，在命令提示符下输入 `./aem65_cfp_install.bin`。

      * （Linux®）`Linux/Disk1/InstData/NoVM`

   这会启动安装向导，引导您完成安装。

1. 在“Introduction”面板上，单击 **[!UICONTROL Next]**。
1. 在&#x200B;**选择安装文件夹**&#x200B;屏幕上，确认默认显示的位置是否正确匹配您现有的安装，或单击&#x200B;**[!UICONTROL 浏览]**&#x200B;选择安装有 AEM Forms 的其他文件夹，然后单击&#x200B;**[!UICONTROL 下一步]**。
1. 阅读“Quick Fix Patch Summary”信息，然后单击 **[!UICONTROL Next]**。
1. 阅读“Pre-Installation Summary”信息，然后单击 **[!UICONTROL Install]**。
1. 安装完成后，单击 **[!UICONTROL Next]** 以将快速修补程序更新应用到已安装的文件。

1. **[仅适用于 Windows]：**&#x200B;请执行以下操作：
   * 在单击&#x200B;**[!UICONTROL 完成]**&#x200B;之前，取消选择&#x200B;**启动配置管理器**&#x200B;选项。使用 `[aem-forms root]\configurationManager\bin` 中的 **ConfigurationManager.bat** 文件运行&#x200B;**配置管理器**。

   * 或者在单击&#x200B;**[!UICONTROL 完成]**&#x200B;之前，取消选择&#x200B;**启动配置管理器**&#x200B;选项。如果要通过 **ConfigurationManager.exe** 或 **ConfigurationManager_IPv6.exe** 运行&#x200B;**配置管理器**，请先进入 *`<AEMForms_Install_Dir>\configurationManager\bin`* 目录，将 **ConfigurationManager.lax** 和 **ConfigurationManager_IPV6.lax** 替换为最新的 [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) 和 [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) 文件，然后在这两个文件中查找并将 **axis-1.4.1.1.jar** 替换为 **axis-1.4.1.2.jar**。

   >[!NOTE]
   >
   >通过使用 **ConfigurationManager.bat** 文件，可以避免手动更新 .lax 文件名称。
   >

1. **[仅适用于基于 Unix 的系统]：**

   * 默认情况下会选中&#x200B;**启动配置管理器**&#x200B;复选框。单击&#x200B;**[!UICONTROL 完成]**&#x200B;可立即运行配置管理器，或者如果希望稍后再运行&#x200B;**配置管理器**，请在单击&#x200B;**[!UICONTROL 完成]**&#x200B;之前取消选中&#x200B;**启动配置管理器**&#x200B;选项。您也可以稍后通过运行 `[AEM_forms_root]/configurationManager/bin` 目录下的相应脚本来启动&#x200B;**配置管理器**。

1. 根据您所使用的应用程序服务器，选择以下文档之一，并按&#x200B;*配置和部署 AEM Forms* 部分的说明进行操作。

   * [安装和部署 AEM forms for JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [安装和部署 AEM forms for WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)

1. （仅适用于 JBoss®）在安装补丁并配置服务器后，请删除 JBoss® 应用程序服务器下的 tmp 和 work 目录。

## 部署后的配置 {#post-deployment-configurations}

### SAML 配置 {#saml-configurations}

如果您已配置了 SAML 身份验证，并在处理大型 IDP 元数据时遇到问题，请在安装补丁后执行以下操作：

1. 在应用程序服务器中设置以下系统属性：\
   `um.saml.enable.large.xml=true`
1. 重新启动服务器。
1. 删除现有的 SAML 身份验证提供程序，并根据 SAML 设置为现有域重新添加这些身份验证提供程序。

>[!NOTE]
>
> 建议使用 “Ctrl + C” 命令重新启动 SDK。如果使用其他方式（例如直接停止 Java 进程）重新启动 AEM SDK，则可能会导致 AEM 开发环境出现不一致情况。

## 受影响的模块 {#impacted-modules}

* 文档服务
* 文档安全
* 基础 JEE

[联系支持人员](https://experienceleague.adobe.com/?support-solution=General&support-tab=home#support)
