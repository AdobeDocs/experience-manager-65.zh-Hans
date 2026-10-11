---
title: 使用Assets Insights演示包
description: 使用演示包启用Adobe Assets Insights，以便在网页中捕获数据并生成见解。
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 13947513-da76-43e1-ae01-abd24a59752a
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: a4e1c1f5-18fc-592e-bfc7-453ce6ae0030
    internal-label: Asset Insights
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: c29e3a96-cd2b-4e21-b382-a8279aa04553
    internal-label: Asset reports
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 2%
---
# 使用Assets Insights演示包 {#using-demo-package-for-asset-insights}

使用该演示包，您可以启用Adobe Assets Insights以从中捕获数据并生成示例网页的分析。

## 带示例网页的[!DNL Use Experience Manager Assets]分析  {#using-aem-assets-insights-with-sample-web-page}

1. 使用[配置Assets Insights](configure-asset-insights.md)中的说明配置Assets Insights。
1. 从下方下载示例Assets包，并从CRXDE包管理器安装包。

   [获取文件](assets/insightsdemo.zip)

1. 从下面下载包含示例网页的ZIP文件，并在本地文件系统上解压缩。

   [获取文件](assets/demosite.zip)

1. 单击在Web浏览器中打开的网页。

   >[!CAUTION]
   >
   >网页配置为从本地主机服务器加载资产。 如果您的服务器在其他地方运行，请在网页的HTML内容中将服务器地址从localhost更改为服务器地址。

   >[!NOTE]
   >
   >外部网页可以位于[!DNL Experience Manager]本身中。
