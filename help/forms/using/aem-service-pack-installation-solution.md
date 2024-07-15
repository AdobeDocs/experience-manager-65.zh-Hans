---
title: 安装最新的6.5.15.0 Service Pack后，出现CRX/捆绑包和Start page Service不可用错误
description: 安装最新的6.5.15.0 Service Pack后，出现CRX/捆绑包和Start page Service不可用错误
exl-id: dfe015a3-3a24-41c5-aede-8e086851d62b
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,AEM Forms on JEE,AEM Forms on OSGi
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 2%

---

# 安装AEM (6.5.15.0) Service Pack后出现“Service Unavailable（服务不可用）”错误 {#steps-to-resolve-error-after-installing-service-pack}

## 问题 {#issue}

安装[AEM 6.5.15.0 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)后，出现以下错误：
* 错误[FelixDispatchQueue] org.apache.sling.scripting.console框架事件错误(org.osgi.framework.BundleException：无法解析org.apache.sling.scripting.console

安装AEM 6.5.15.0 Service Pack后，CRX/捆绑包和起始页显示服务不可用错误。

## 应用到 {#applies-to}

此解决方案适用于：
* 所有JEE服务器（在JBoss EAP 7.4.0上运行的除外）上的AEM Forms

## 解决方案 {#solution}

>[!NOTE]
>
>故障排除步骤适用于除JBoss EAP 7.4之外的所有应用程序服务器。

安装[AEM 6.5.15.0 service pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)后，如果CRX/捆绑包和起始页显示服务不可用错误，请执行以下步骤：

1. 停止应用程序服务器。
1. 导航到 `[aem-forms root]\crx-repository\launchpad\felix\bundle52`。
1. 找到`bundle.info`文件。
1. 在Ant文本编辑器中打开`bundle.info`文件，并搜索作为`org.apache.felix.http.bridge`的包名称。

   >[!NOTE]
   >
   >如果`bundle52`下的`bundle.info`不包含`org.apache.felix.http.bridge`包，请检查`org.apache.felix.http.bridge`旁边方括号中的包编号。 然后导航到[aem-forms根]\crx-repository\launchpad\felix\bundle[x]，并在此位置执行后续步骤。

1. 导航到URL： `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`。
1. 搜索`bundle.jar`并将`bundle.jar`重命名为`bundle.jar.bak`。
1. 从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar)复制此位置的`Bundle for AEM 6.5 Forms on JEE Service Pack 15`。
1. 启动应用程序服务器，等待日志稳定并检查捆绑包状态。
1. 所有包都处于活动状态后，请从`system/console/bundles`在JEE Service Pack 15](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)上安装AEM 6.5 Forms的[片段，并等待应用程序服务器稳定下来。
1. 停止应用程序服务器。
1. 导航到`[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1`并删除`bundle.jar`。
1. 将`bundle.jar.bak`重命名为`bundle.jar`。
1. 启动应用程序服务器。
