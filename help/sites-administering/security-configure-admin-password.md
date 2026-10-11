---
title: 安装时配置管理员密码
description: 了解如何在安装 Adobe Experience Manager 时修改管理员密码。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: b55ff9d5-8139-4ecf-ba09-5cf88207c5c4
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c35bc059-fd80-4a01-91a6-e48da3c76758
    internal-label: Security practices
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 100%
---
# 安装时配置管理员密码{#configure-the-admin-password-on-installation}

## 概述 {#overview}

自 6.3 版本起，Adobe Experience Manager（AEM）允许在安装新实例时通过命令行设置管理员密码。

在更早的 AEM 版本中，管理员帐户密码以及其他控制台的密码都必须在安装完成后再进行更改。

此功能允许在安装 AEM 实例时为存储库和 Servlet 引擎设置新的管理员密码，从而无需事后手动修改。

>[!CAUTION]
>
>该功能不涵盖 Felix 控制台，其密码仍需手动修改。 有关详细信息，请参阅相关的[安全检查清单章节](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts)。

## 如何使用？ {#how-do-i-use-it}

如果您选择通过命令行安装 AEM（而非在文件系统资源管理器中双击 JAR 文件），此功能会自动触发。

通过命令行运行 AEM 实例的一般语法为：

```shell
java -jar aem6.3.jar
```

通过命令行运行实例后，在安装过程中，系统会提示您修改管理员密码：

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>修改管理员密码的提示仅会在安装新的 AEM 实例期间出现。

## 使用 -nointeractive 标志 {#using-the-nointeractive-flag}

您还可以选择通过属性文件来指定密码。 此方法需结合使用 `-nointeractive` 标志与 `-Dadmin.password.file` 系统属性。

示例如下：

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

`passwordfile.properties` 文件中的密码必须符合以下格式：

```xml
admin.password = 12345678
```

>[!NOTE]
>
>如果仅使用 `-nointeractive` 参数，而未指定 `-Dadmin.password.file` 系统属性，AEM 将会直接使用默认管理员密码，而不会提示您修改，这与早期版本的行为一致。 这种非交互模式可用于通过安装脚本在命令行中执行自动化安装。
