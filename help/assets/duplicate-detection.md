---
title: 启用重复资产检测
description: 了解如何在Experience Manager中启用重复资源检测。
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
hide: true
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
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
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%
---
# 启用重复资产检测 {#enable-detection-of-duplicate-assets}

如果您尝试上传[!DNL Adobe Experience Manager Assets]中存在的资产，则重复检测功能会将该资产识别为重复资产。 默认情况下禁用重复检测。 要启用该功能，请执行以下步骤：

1. 通过访问`https://[aem_server]:[port]/system/console/configMgr`打开[!DNL Experience Manager] Web控制台配置页。
1. 编辑Servlet **[!UICONTROL Day CQ DAM创建资产]**&#x200B;的配置。
1. 选择&#x200B;**[!UICONTROL 检测重复项]**&#x200B;选项，然后单击&#x200B;**[!UICONTROL 保存]**。

   ![在Servlet中选择检测重复选项](assets/chlimage_1-377.png)

   *图：在servlet中选择检测重复项选项。*

[!DNL Assets]中现在启用了检测重复项功能。 当用户尝试上传[!DNL Experience Manager]中存在的资源时，系统会检查冲突并指示冲突。 资产使用存储在`jcr:content/metadata/dam:sha1`上的SHA-1哈希进行标识，这意味着不论文件名如何，都会检测到重复的资产。

>[!MORELIKETHIS]
>
>* [复制现有存储库中的资产（社区成员的教程）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)
>* [在AEM as a Cloud Service中检测重复资源](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/detect-duplicate-assets.html)
