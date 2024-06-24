---
title: 在JBoss® Linux®环境中安装AEM Forms JEE 6.5.15.0 Service Pack时出现问题
description: AEM Forms JEE 6.5.15.0 service pack未在JBoss® Linux®环境中正确安装，任何修补程序更改都不会应用到应用程序服务器。 将'RUP_BOM.xml'文件添加到XML目录中。
exl-id: 96ecbe58-a859-4432-a2d8-3d5dc0eaf989
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 1%

---

# 在JBoss®环境中安装AEM Forms 6.5.15.0 JEE Service Pack时出现问题 {#aem-forms-installation-issue-environment}

## 问题 {#issue}

AEM Forms JEE 6.5.15.0 service pack未在JBoss® Linux®环境中正确安装。 在 `PatchInstallerProcessing[1-9*].log` 记录日志条目， `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component is not in the installation. Skipping Processing`，将被记录。 此条目表示AEM Forms JEE 6.5.15.0 Service Pack的安装不成功。

## 应用到 {#applies-to}

此解决方案适用于：
* JBoss® Linux®环境

>[!NOTE]
>
> 在执行以下步骤之前，请确保在应用程序服务器中至少安装一次AEM Forms JEE 6.5.15.0 Service Pack [将RUP_BOM.xml文件添加到XML目录](#solution-solution).

## 解决方案 {#solution}

要修复安装问题，请添加AEM Forms JEE 6.5.15.0 Service Pack `RUP_BOM.xml` 文件到XML目录：
1. 导航到从中提取修补程序的文件夹 `AEMForms-6.5.0-0057_jboss_linux.tar.gz`.
1. 导航到 `/CDROM_Installers/Linux/Disk1/InstData` 位置并找到 `Resource1.zip` 文件。
1. 复制 `Resource1.zip` 解压缩解压缩文件夹外部某个不同位置的文件 `Resource1.zip` 文件。
1. 导航到 `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` 并复制 `RUP_BOM.xml` 文件。
1. 将RUP_BOM.xml文件粘贴到 `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`.
1. 重新安装 [AEM Forms JEE 6.5.15.0 Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
