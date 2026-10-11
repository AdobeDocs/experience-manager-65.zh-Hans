---
title: 在JBoss® Linux®环境中安装AEM Forms JEE 6.5.15.0 Service Pack时出现问题
description: AEM Forms JEE 6.5.15.0 service pack未在JBoss® Linux®环境中正确安装，任何修补程序更改都不会应用到应用程序服务器。 将'RUP_BOM.xml'文件添加到XML目录中。
SEO Description: AEM Forms JEE 6.5.15.0 service pack  is not installed properly on the JBoss Linux environment.
exl-id: 96ecbe58-a859-4432-a2d8-3d5dc0eaf989
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 16%
---
# JBoss®环境中的AEM Forms 6.5.15.0 JEE Service Pack安装问题 {#aem-forms-installation-issue-environment}

## 问题 {#issue}

未在JBoss® Linux®环境中正确安装AEM Forms JEE 6.5.15.0 Service Pack。 在`PatchInstallerProcessing[1-9*].log`文件中记录日志条目`[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component is not in the installation. Skipping Processing`。 该条目表示 AEM Forms JEE 6.5.15.0 服务包未安装成功。

## 应用到 {#applies-to}

此解决方案适用于：
* JBoss® Linux®环境

>[!NOTE]
>
> 在执行[将RUP_BOM.xml文件添加到XML目录](#solution-solution)的步骤之前，请确保应用程序服务器上至少安装一次AEM Forms JEE 6.5.15.0 Service Pack。

## 解决办法 {#solution}

要修复安装问题，请将`RUP_BOM.xml`文件添加到AEM Forms JEE 6.5.15.0 Service Pack的XML目录中：
1. 导航到从中提取修补程序`AEMForms-6.5.0-0057_jboss_linux.tar.gz`的文件夹。
1. 导航到`/CDROM_Installers/Linux/Disk1/InstData`位置并找到`Resource1.zip`文件。
1. 将`Resource1.zip`文件复制到解压缩文件夹之外的其他位置，然后解压缩`Resource1.zip`文件。
1. 导航到`/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml`并复制`RUP_BOM.xml`文件。
1. 将RUP_BOM.xml文件粘贴到`[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`。
1. 重新安装[AEM Forms JEE 6.5.15.0 Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)。
