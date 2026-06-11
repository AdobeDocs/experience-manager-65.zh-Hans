---
title: 为JEE上的AEM Forms将JBoss EAP从7.4.10升级到7.4.23
description: 对于JEE独立环境上的AEM Forms，将JBoss EAP从7.4.10升级到7.4.23的步骤。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
exl-id: 8f4c2a91-6b3d-4e7f-9c12-5d8e1f0a2b34
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms Upgrade,AEM Forms on JEE
role: User, Developer
source-git-commit: cb190feb41152d40c36ea2f152ee04cc8c8eba1d
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 1%

---

# 为JEE上的AEM Forms将JBoss EAP从7.4.10升级到7.4.23 {#upgrade-jboss-eap-from-7-4-10-to-7-4-23}

## 概述 {#overview}

在AEM Forms on JEE独立环境上，将JBoss EAP从版本7.4.10升级到7.4.23。 升级需要将配置文件、数据库凭据和CRX存储库迁移到新的JBoss安装，并运行Configuration Manager以完成安装。

## 应用到 {#applies-to}

本文适用于：

* 在独立环境中运行于JBoss EAP 7.4.10上的JEE上的AEM Forms
* Windows和Linux上的全包和部分全包安装模式

## 先决条件 {#prerequisites}

开始之前：

* 从[Adobe软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fjboss-eap-7.4.23-1.0.17.zip)下载JBoss 7.4.23包。
* 确保您对目标环境具有管理访问权限。
* 对现有JBoss安装进行完整备份。

## 步骤 {#steps}

要将JBoss EAP从7.4.10升级到7.4.23，请执行以下步骤：

### 下载并解压缩JBoss {#download-and-extract-jboss}

1. 从Adobe软件分发门户下载JBoss 7.4.23 ZIP包。
1. 将ZIP文件解压缩到本地目录。
1. 重命名提取的JBoss文件夹，以使其与现有JBoss安装目录的精确名称匹配。

### 备份现有安装 {#back-up-the-existing-installation}

1. 创建当前JBoss安装目录的完整备份。
1. 验证备份是否包含所有配置文件和自定义项。

### 配置数据库文件 {#configure-database-files}

1. 导航到配置目录：

   * Windows： `<JBoss_Home>\standalone\configuration`
   * Linux： `<JBoss_Home>/standalone/configuration`

1. 根据安装模式配置数据库文件：

   **统包模式：**

   1. 将`lc_mysql.xml`重命名为`lc_turnkey.xml`。
   1. 删除以下文件：

      * `lc_oracle.xml`
      * `lc_mssql.xml`

   **部分快速键模式：**

   1. 仅保留与数据库引擎对应的`lc_db.xml`文件。
   1. 删除另外两个`lc_db.xml`配置文件。

### 更新数据库凭据 {#update-database-credentials}

1. 从备份的JBoss安装中打开`lc_turnkey.xml`文件。
1. 复制以下值：

   * 数据源URL
   * 数据库用户名
   * 数据库密码

1. 更新新`lc_turnkey.xml`文件中的相应条目。

### 迁移CRX存储库 {#migrate-crx-repository}

1. 在旧的JBoss安装中导航到以下目录：

   `<old_jboss>\bin\`

1. 复制`crx-quickstart`文件夹。
1. 将文件夹粘贴到：

   `<new_jboss>\bin\`

### 运行配置管理器 {#run-configuration-manager}

1. 启动升级后的JBoss环境。
1. 启动LiveCycle Configuration Manager (LCM)。
1. 执行完整的端到端的Configuration Manager工作流。
1. 验证所有配置任务是否成功完成。

### 升级后验证 {#post-upgrade-validation}

升级后，确认以下内容：

* 所有服务启动成功。
* 已验证数据库连接。
* 已验证应用程序功能。
