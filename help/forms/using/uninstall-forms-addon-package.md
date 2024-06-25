---
title: 本文介绍了如何使用CRX包管理器卸载Forms附加组件包。
description: 了解使用CRX包管理器卸载Forms附加组件包的步骤。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 975f1f580404ea1f2940aec5981f5668dced4b95
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 1%

---


# 从AEM实例中卸载AEM Forms附加组件包

本文概述了从AEM Forms SDK实例正确卸载AEM Forms附加组件包所需的步骤。 执行以下步骤可确保删除Forms附加组件包，防止您的AEM环境出现潜在问题。

## 先决条件

确保对表单和数据进行备份，以避免任何数据丢失。

## 卸载AEM Forms附加组件包

要卸载AEM Forms附加组件包，请执行以下步骤：

1. **卸载AEM Forms附加组件包：**
   1. 导航至 `http://[host]:[port]/crx/de/index.jsp`.
   1. 找到并卸载 `AEM Forms add-on package`.

   ![卸载包](/help/forms/using/assets/uninstall-aem-forms-package.png)

1. **从CRXDE中删除本地文件夹：**
   1. 导航至 `http://[host]:[port]/crx/de/index.jsp`.
   1. 转到 `/libs/fd/native/install` 并删除 `native` CRXDE中的文件夹。

      ![从CRX/de中删除本机节点](/help/forms/using/assets/native-install-folder-crxde.png)
   1. 保存更改。

1. **停止AEM Forms SDK：**
   1. 使用“Ctrl + C”命令停止AEM Forms SDK实例。

1. **检查crx-quickstart文件夹中的基岩并安装文件夹**
   1. 导航到 `..author\crx-quickstart` AEM Forms SDK实例的文件夹。
   1. 搜索名为的文件夹 `bedrock` 和 `install`.
如果找到，请确保将其从 `crx-quickstart` AEM Forms SDK实例的文件夹。

   >[!NOTE]
   >
   > 此 `bedrock` 重新启动AEM Forms SDK实例后，会自动重新创建文件夹。

1. **重新启动AEM实例：**
   1. 完成前面所有步骤后， [重新启动AEM Forms SDK实例](/help/forms/using/restart-aem-sdk.md).




