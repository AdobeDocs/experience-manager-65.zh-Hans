---
title: 管理证书吊销列表
description: 了解如何管理证书吊销列表。 您可以使用信任存储区管理导入、编辑和删除证书吊销列表(CRL)。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 01e966f6-a650-4565-80d1-e2297f25da5c
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
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
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 4%
---
# 管理证书吊销列表{#managing-certificate-revocationlists}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

使用信任存储区管理，您可以导入、编辑和删除证书吊销列表(CRL)。 支持Base64和DER编码的证书吊销列表。

## 导入CRL {#import-a-crl}

1. 在管理控制台中，单击“设置”>“信任存储区管理”>“证书吊销列表”，然后单击“导入”。
1. 在“别名”框中，键入CRL的标识符。
1. 单击“浏览”以找到CRL，然后单击“确定”。

## 导出CRL {#export-a-crl}

1. 在管理控制台中，单击“设置”>“信任存储区管理”>“证书吊销列表”。
1. 单击CRL的别名以便导出，然后单击“导出”。
1. 按照说明导出CRL。 CRL以Base64编码导出。
1. 单击“确定”。

## 删除CRL {#delete-a-crl}

1. 在管理控制台中，单击“设置”>“信任存储区管理”>“证书吊销列表”。
1. 选中要删除的CRL的复选框，单击“删除”，然后单击“确定”。
