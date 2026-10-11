---
title: 配置帐户锁定设置
description: 使用“启用帐户锁定”选项可在指定数量的连续身份验证失败后锁定用户帐户。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: eb8c748d-51d9-4684-97c5-e982ad84ba9f
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
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
source-wordcount: '210'
ht-degree: 9%
---
# 配置帐户锁定设置 {#configure-account-locking-settings}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

添加域时，请指定是否启用帐户锁定。 如果选中了“启用帐户锁定”选项，则在连续发生指定次数的身份验证失败后锁定用户帐户。 在指定的时间长度后，用户可以尝试再次进行身份验证。 此功能可防止用户尝试各种凭据组合来访问系统。

使用“域管理”页上的设置可指定验证失败的最大次数以及帐户被锁定的时间长度。 这些设置适用于所有启用了帐户锁定的域。

1. 在管理控制台中，单击&#x200B;**[!UICONTROL 设置>用户管理>域管理]**。
1. 在“最大连续身份验证失败次数”框中，输入在锁定帐户之前，用户连续尝试登录失败的次数。 默认值为 20。
1. 在“在此时间之后解锁帐户（分钟）”框中，输入锁定用户帐户的分钟数。 在指定的分钟数后，用户可以尝试再次登录。 默认值为 30。
1. 单击&#x200B;**[!UICONTROL 保存]**。
