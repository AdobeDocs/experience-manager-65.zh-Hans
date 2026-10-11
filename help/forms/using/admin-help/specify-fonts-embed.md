---
title: 指定要嵌入的字体
description: 了解如何指定要嵌入自适应表单中的字体。 您可以指定哪些字体嵌入或从未嵌入到Forms服务生成的表单。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 02c28b2c-0cab-4431-9fab-fa332c96e092
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
source-wordcount: '283'
ht-degree: 3%
---
# 指定要嵌入的字体{#specify-fonts-to-embed}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

您可以指定哪些字体始终嵌入或从不嵌入到输出使用的表单中。 嵌入字体会增加表单的文件大小。 嵌入用户不太可能在其系统上拥有的异常字体，并且不嵌入他们即将安装的常用字体。

>[!NOTE]
>
>如果已为输出指定了自定义XCI文件，则XCI文件中的嵌入字体选项将覆盖这些设置。 （请参阅[为输出](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)指定文件位置。）

1. 在管理控制台中，单击“服务”>“输出”。
1. 在“字体嵌入设置”下的“始终嵌入字体”框中，键入要嵌入表单的字体名称，并用逗号分隔。 您指定的字体仅会嵌入到生成的表单中（如果它们在表单中使用）。 如果在传递到服务的XCI文件中启用了嵌入字体选项，则会忽略此设置。 在这种情况下，PDF中使用的所有字体始终都会嵌入。
1. 在“从不嵌入字体”框中，键入不嵌入表单的字体的名称，名称之间用逗号分隔。 您指定的字体不会嵌入到PDF中，即使这些字体用于生成的PDF中也是如此。 如果在传递到服务的XCI文件中关闭了嵌入字体选项，则会忽略此设置。 在这种情况下，PDF中使用的字体都不会被嵌入。
1. 单击“保存”。
