---
title: JEE WebLogic服务器上的EAR部署失败
seo-title: EAR Deployment failing on JEE Weblogic Server
description: 解决JEE WebLogic服务器上的EAR部署失败的步骤
exl-id: 109d9182-5e3f-477e-9417-abc83d5ea3bc
source-git-commit: 04cdc51ea2059daed6573987052feb893bd5f634
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 14%
---
# 在 JEE WebLogic 服务器上部署 EAR 失败 {#ear-deployment-failing-on-jee-weblogic-server}

## 问题 {#issue}

当用户尝试部署`adobe-livecycle-weblogic.ear`时，遇到`Null Pointer`异常。

## 应用到 {#applies-to}

此解决方案适用于：

* WebLogic JEE服务器版本12.2.1.x上的AEM Forms。

## 解决办法 {#solution}

要解决此问题，请执行以下步骤：

1. 转到已安装的WebLogic JEE服务器的`<domain_home>\bin`目录。

1. 编辑`setDomainEnv.cmd`或`setDomainEnv.sh`文件，作为`applicable`。

1. 搜索最后出现的`JAVA_OPTS`并添加`-DANTLR_USE_DIRECT_CLASS_LOADING=true`。 例如，更新的字符串显示为：

       设置&#39;JAVA_OPTIONS=%JAVA_OPTIONS% -DANTLR_USE_DIRECT_CLASS_LOADING=true&#39;
   
1. 保存更改。
