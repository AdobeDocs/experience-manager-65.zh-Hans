---
title: 使用模式检测器评估升级复杂性
description: 了解如何使用模式检测器来评估升级的复杂性。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
docset: aem65
feature: Upgrading
exl-id: c42373e9-712e-4c11-adbb-4e3626e0b217
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---

# 使用模式检测器评估升级复杂性

## 概述 {#overview}

此功能允许您通过检测使用中的模式来检查现有AEM实例的可升级性，这些模式包括：

1. 违反某些规则，并在升级将影响或覆盖的区域中执行
1. 使用AEM 6.x功能或AEM 6.5上无法向后兼容且在升级后可能中断的API。

这可以作为对升级到AEM 6.5所涉及的开发工作的评估。

## 如何设置 {#how-to-set-up}

模式检测器作为[一个包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/compatpack/pd-all-aem65)单独发布，用于从6.1到6.5的任何源AEM版本，目标为AEM 6.5升级。 可以使用[包管理器](/help/sites-administering/package-manager.md)安装它。

## 使用方法 {#how-to-use}

>[!NOTE]
>
>模式检测器可在任何环境中运行，包括本地开发实例。 但是，要：
>
>* 提高检测率
>* 避免业务关键型实例速度减慢
>
>同时，建议在尽可能接近用户应用程序、内容和配置领域的生产环境的暂存环境&#x200B;**上运行**。

您可以使用多种方法检查模式检测器输出：

* **通过Felix清单控制台：**

1. 通过浏览到&#x200B;*https://serveraddress:serverport/system/console/configMgr*&#x200B;转到AEM Web Console
1. 选择&#x200B;**状态 — 模式检测器**，如下图所示：

   ![屏幕快照–2018-2-5pattern-detector](assets/screenshot-2018-2-5pattern-detector.png)

* **通过基于反应文本或常规JSON接口**
* **通过反应式JSON行接口，**&#x200B;可在每行中生成单独的JSON文档。

这两种方法详述如下：

## 反应式接口 {#reactive-interface}

反应接口允许在检测到可疑时立即处理违规报告。

输出当前在2个URL下可用：

1. 纯文本界面
1. JSON界面

## 处理纯文本界面 {#handling-the-plain-text-interface}

输出中的信息被格式化为一系列事件条目。 有两个渠道 — 一个用于发布违规，另一个用于发布当前进度。

可使用以下命令获取它们：

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep SUSPICION
```

输出将如下所示：

```
2018-02-13T14:18:32.071+01:00 [SUSPICION] The pattern=ECU/extraneous.content.usage was found by detector=ContentAccessDetector with id=a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f message="Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid". More info at=https://www.adobe.com/go/aem6_EC
```

可以使用`grep`命令过滤进度：

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep PROGRESS
```

这将导致以下输出：

```
2018-02-13T14:19:26.909+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=45780/16 MB items, found=0 suspicions so far in period=PT5.005S (throughput=34667 items/sec)
2018-02-13T14:19:31.904+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=106050/39 MB items, found=0 suspicions so far in period=PT10S (throughput=23378 items/sec)
2018-02-13T14:19:35.685+01:00 [PROGRESS] Finished in period=PT13.782
```

## 处理JSON接口 {#handling-the-json-interface}

同样，JSON一发布就可以使用[jq工具](https://stedolan.github.io/jq/)进行处理。

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == true)'
```

对于输出：

```
{
  "timestamp": "2018-02-13T14:20:18.894+01:00",
  "suspicion": true,
  "pattern": {
    "code": "ECU",
    "type": "extraneous.content.usage",
    "detective": "ContentAccessDetector",
    "moreInfo": "https://www.adobe.com/go/aem6_ECU"
  },
  "item": {
    "id": "a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f",
    "message": "Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid"
  }
}
```

每5秒报告一次进度，可以通过排除标记为可疑的其他消息来获取进度：

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == false)'
```

对于输出：

```
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:17.279+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 57209,
    "itemsAnalysedSize": "26 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT5.003S",
    "elapsedTimeMilliseconds": 5003,
    "itemsPerSecond": 36965
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:22.276+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 113194,
    "itemsAnalysedSize": "46 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT10S",
    "elapsedTimeMilliseconds": 10000,
    "itemsPerSecond": 24092
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:25.762+01:00",
  "type": "FINISHED",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 140744,
    "itemsAnalysedSize": "63 MB",
    "suspicionsFound": 1
  },
  "progress": {
    "elapsedTime": "PT13.486S",
    "elapsedTimeMilliseconds": 13486,
    "itemsPerSecond": 19907
  }
}
{
  "suspicion": false,
  "type": "SUMMARY",
  "suspicionsFound": 1,
  "totalTime": "PT13.487S"
}
```

>[!NOTE]
>
>建议的方法是将curl的整个输出保存到文件中，然后通过`jq`或`grep`处理该输出以筛选信息类型。

## 检测范围 {#scope}

当前模式检测器允许您检查以下内容：

* OSGi捆绑导出和导入不匹配
* Sling资源类型和超级类型（具有搜索路径内容叠加）的使用情况
* Oak索引的定义（兼容性）
* VLT包（过度使用）
* rep：用户节点兼容性（在OAuth配置的上下文中）

>[!NOTE]
>
>模式检测器尝试准确地预测升级警告。 但是，在某些情况下，它可能会产生误报。
