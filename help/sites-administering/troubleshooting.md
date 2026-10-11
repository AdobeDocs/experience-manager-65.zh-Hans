---
title: 使用日志
description: 了解如何使用日志对AEM进行故障排除。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: ab4fc41f-e0e9-4577-aab2-f0b4298f9a59
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 5ef752af-d616-5b23-8312-06964e46b208
    internal-label: Administering
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 5%
---
# 使用日志{#working-with-logs}

此部分包含有关日志的详细信息，可帮助您进行故障排除。

>[!NOTE]
>
>有关日志的详细信息，请参阅：
>
>* AEM中的[审核日志维护](/help/sites-administering/operations-audit-log.md)
>* [使用审核记录和日志文件](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)

CRX会记录详细的日志。 打开包装并启动“快速入门”后，您可以在以下位置找到日志：

* crx-quickstart/launchpad/logs
* crx-quickstart/server/logs
* crx-quickstart/logs

## 激活DEBUG日志级别 {#activating-the-debug-log-level}

默认日志级别为INFO，即不记录DEBUG消息。

要激活DEBUG日志级别，请使用CRX资源管理器设置

```xml
/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level
```

要调试的属性。 不要将日志保留在DEBUG日志级别的时间超过所需时间，因为它会生成大量日志。

调试文件中的行通常以DEBUG开头，然后提供日志级别、安装程序操作和日志消息。 例如：

```xml
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

日志级别如下所示：

| 0 | 致命错误 | 操作失败，安装程序无法继续。 |
|---|---|---|
| 1 | 错误 | 操作失败。 虽然安装会继续，但部分CRX未正确安装，因此将无法正常运行。 |
| 2 | 警告 | 操作已成功，但遇到了问题。 CRX可能会正常工作，也可能无法正常工作。 |
| 3 | 信息 | 操作已成功。 |

## 用于故障排除的详细选项 {#verbose-option-used-for-troubleshooting}

启动CRX时，您可以将 — v (verbose)选项添加到命令行中，如下所示：

` java -jar crx-<*version*>-<*edition*>.jar -v`

使用verbose选项进行故障排除，因为此选项在控制台上显示一些快速启动日志输出。
