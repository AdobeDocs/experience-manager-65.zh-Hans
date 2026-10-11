---
title: 输出、Forms和（记录文档）DoR服务的连接问题
description: 解决SP19之后的AEM Forms连接错误。 停止，安装Microsoft Visual C++，重新启动服务器以获得无缝的解决方案。 排查输出故障、Forms、DoR服务。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
role: Admin
exl-id: bd58099c-08cd-4056-afb6-a5935454429a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 52%
---
# 无法使用 Output 服务、表单服务或记录文档（DoR）服务 {#unable-to-use-output-service-forms-service-or-document-of-record-service}

## 问题

安装AEM Forms 6.5 Service Pack 19后，尝试使用输出服务、Forms服务或记录文档(DoR)服务可能会导致`Connection to failed service`错误。

## 解决办法

要解决此问题：

1. 停止AEM 6.5 Forms实例。
1. 在安装了 AEM 6.5 Forms 的计算机上，下载并安装[适用于 Visual Studio 2015、2017、2019 和 2022 的 64 位 Microsoft Visual C++ 可再发行组件包](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022)。
1. 重新启动AEM Forms服务器。

   >[!NOTE]
   >
   > 建议使用 “Ctrl + C” 命令重新启动 SDK。 如果使用其他方式（例如停止 Java 进程）重新启动 AEM SDK，则可能会导致 AEM 开发环境出现不一致情况。


>[!NOTE]
>
>
> 确保您安装了可再发行组件，即使安装了以前的版本也是如此。
