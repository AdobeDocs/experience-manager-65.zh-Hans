---
title: 在 Windows Vista 上配置 SSL
description: 了解如何在Windows Vista上配置SSL。 使用并运行Java Keytool生成包含RSA密钥的SSL证书以进行身份验证。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 36c4300d-7a44-41f4-b294-06f32bb01686
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 5%
---
# 在 Windows Vista 上配置 SSL {#configuring-ssl-on-windows-vista}

要在Windows Vista™上配置SSL，您需要具有RSA密钥的SSL证书以进行身份验证。 可以使用Java keytool创建证书。

>[!NOTE]
>
>Windows Vista不能使用DSA密钥。

您可以使用包含创建证书和密钥库所需的所有信息的单个命令来运行keytool。

**创建SSL证书**

1. 在命令提示符下，导航到&#x200B;*`[JAVA HOME]`*/bin并键入以下命令以创建证书和密钥库：

   `keytool -genkey -keyalg RSA -dname "CN=`*主机名* `, OU=`*组名* `, O=`*公司名* `,L=`*城市名* `, S=`*省/市* `, C=`*国家/地区代码* `" -alias`*&quot;LC证书&quot;* `-keypass` `key`*_* *密码* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >将&#x200B;*`[JAVA_HOME]`替换为安装JDK的目录，并将斜体文本替换为与您的环境对应的值。*

1. 键入`changeit`作为密码。 此密码是Java安装的默认密码，系统管理员可能已更改此密码。
