---
title: 本文介绍了如何使用Forms包管理器卸载CRX附加组件包。
description: 了解使用Forms包管理器卸载CRX附加组件包的步骤。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 2755e414ea23ebc1472e9c08d832eca93f28311b
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 1%

---


# 从AEM实例中卸载AEM Forms附加组件包

本文概述了从AEM Forms SDK实例正确卸载AEM Forms附加组件包所需的步骤。 请按照以下步骤操作，确保删除Forms附加组件包，从而防止您的AEM环境出现潜在问题。

## 先决条件

确保进行备份以避免任何数据丢失。

## 卸载AEM Forms附加组件包

要卸载AEM Forms附加组件包，请执行以下步骤：

1. **卸载AEM Forms附加组件包：**
   1. 导航到`http://[host]:[port]/crx/de/index.jsp`。
   1. 找到并卸载`AEM Forms add-on package`。

   ![卸载包](/help/forms/using/assets/uninstall-aem-forms-package.png)

1. **从CRXDE中删除本机文件夹：**
   1. 导航到`http://[host]:[port]/crx/de/index.jsp`。
   1. 转到`/libs/fd/native/install`并删除CRXDE中的`native`文件夹。

      ![从CRX/de中删除本机节点](/help/forms/using/assets/native-install-folder-crxde.png)
   1. 保存更改。

1. **停止AEM Forms SDK：**
   1. 使用“Ctrl + C”命令停止AEM Forms SDK实例。

1. **检查crx-quickstart文件夹中的基岩并安装文件夹**
   1. 导航到AEM Forms SDK实例中的`..author\crx-quickstart`文件夹。
   1. 搜索名为`bedrock`和`install`的文件夹。
如果找到，请确保将其从AEM Forms SDK实例的`crx-quickstart`文件夹中删除。

   >[!NOTE]
   >
   > 重新启动AEM Forms SDK实例后，将自动再次创建`bedrock`文件夹。

1. **重新启动AEM实例：**
   1. 完成前面的所有步骤后，[重新启动AEM Forms SDK实例](/help/forms/using/restart-aem-sdk.md)。




