---
title: 指定要嵌入的字体
seo-title: 指定要嵌入的字体
description: 了解如何指定要嵌入的字体。
seo-description: 了解如何指定要嵌入的字体。
uuid: 97de6f98-ed3b-4a93-854a-193a967b4672
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4c83694c-b00f-40be-9ac4-f5785cd60741
exl-id: b2cbf5f3-ee13-47bf-bf7f-f6a1884cee66
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# 指定要嵌入的字体{#specifying-fonts-to-embed}

您可以指定始终嵌入或从不嵌入Forms服务生成的表单的字体。 嵌入字体会增加表单的文件大小。 嵌入了用户在其系统上很少使用的异常字体。 请勿嵌入通常已安装的常用字体。

>[!NOTE]
>
>如果您为Forms指定了自定义XCI文件，则XCI文件中的嵌入字体选项将覆盖这些设置。 (请参阅[配置Forms的位置](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)。)

1. 在管理控制台中，单击&#x200B;**[!UICONTROL 服务> Forms]**。
1. 在&#x200B;**[!UICONTROL 字体嵌入设置]**&#x200B;下的&#x200B;**[!UICONTROL 始终嵌入字体]**&#x200B;框中，键入要与表单嵌入的字体名称，并使用逗号分隔。 仅当在表单中使用您指定的字体时，这些字体才会嵌入生成的表单中。 如果在传递到服务的XCI文件中打开了嵌入字体选项，则忽略此设置，因为在这种情况下，PDF中使用的所有字体都始终嵌入。
1. 在&#x200B;**[!UICONTROL 从不嵌入字体]**&#x200B;框中，键入不要与表单嵌入的字体的名称，并使用逗号分隔。 您指定的字体不会嵌入到PDF中，即使这些字体在生成的PDF中使用也是如此。 如果在传递到服务的XCI文件中关闭了嵌入字体选项，则会忽略此设置，因为在这种情况下，PDF中使用的字体均未嵌入。
1. 单击&#x200B;**[!UICONTROL 保存]**。
