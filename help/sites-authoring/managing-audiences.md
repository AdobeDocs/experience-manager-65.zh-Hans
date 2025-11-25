---
title: 管理受众
description: 通过“受众”控制台，您可以创建、组织和管理Adobe Target帐户的受众，或管理ContextHub或客户端上下文的区段
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
docset: aem65
exl-id: 97e02986-049f-4747-a67a-6aa0677b281e
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 63%

---

# 管理受众{#managing-audiences}

通过“受众”控制台，您可以创建、组织和管理Adobe Target帐户的受众，或管理ContextHub或Client Context的区段：

* 添加受众 - Adobe Target 受众或 ContextHub 区段。
* 管理受众。

ContextHub和Client Context中称为&#x200B;*区段*&#x200B;的受众是由特定标准定义的一类访客，可确定哪些人会看到目标活动。 定位活动时，您可以直接在定位流程中选择受众，或在“受众”控制台中创建更多受众。

在“受众”控制台中，各受众按品牌进行组织。

在定位模式下，受众可用于[创作目标内容](/help/sites-authoring/content-targeting-touch.md)，您也可以在该模式下创建受众(但必须在“受众”控制台中创建Adobe Target受众)。 在“定位”模式下创建的受众会显示在“受众”控制台中。

受众显示有相应的标签，用于说明定义的受众类型：

* CH - ContextHub 区段
* CC — 客户端上下文区段
* AT - Adobe Target 受众

## 在“受众”控制台中创建 ContextHub 区段 {#creating-a-contexthub-segment-in-the-audiences-console}

您可以在“受众”控制台中或在定位过程中创建 ContextHub 区段。

要在“受众”控制台中创建 ContextHub 区段，请执行以下操作：

1. 在导航控制台中，单击&#x200B;**Personalization**。 单击&#x200B;**受众**。
1. 单击&#x200B;**创建ContextHub区段**。

   ![screen-shot_2019-03-05at124034](assets/screen-shot_2019-03-05at124034.png)

1. 在&#x200B;**新 ContextHub 区段**&#x200B;对话框中，输入标题并调整提升，然后单击&#x200B;**创建**。新 ContextHub 区段随即会显示在受众列表中。

   >[!NOTE]
   >
   >您可以通过点按或单击&#x200B;**已修改**&#x200B;来对修改列表进行降序排序，以查看任何新创建的受众。

有关使用ContextHub创建区段的更多详细信息，请参阅[使用ContextHub配置分段](/help/sites-administering/segmentation.md)文档。

## 使用“受众”控制台创建 Adobe Target 受众 {#creating-an-adobe-target-audience-using-the-audience-console}

您可以直接在 AEM 中使用“受众”控制台创建 Adobe Target 受众。

受众由确定目标活动中包含哪些人的规则进行定义。受众定义可以包含多个规则，每个规则可以包含多个参数。

使用多个规则时，这些规则会通过布尔运算符 AND 进行组合，这意味着任何潜在的受众成员必须满足所有定义的条件才能包含在活动中。例如，如果您定义了操作系统规则和浏览器规则，则只有同时使用定义的操作系统和定义的浏览器的访客才会包含在活动中。

>[!NOTE]
>
>如果您在&#x200B;**0&rbrace;创建**&#x200B;1&rbrace;菜单中看不到{创建目标受众}，则您没有创建受众的必要权限。 **&#x200B;**&#x200B;您需要具有&#x200B;**/etc/segmentation**&#x200B;下的写入权限才能创建受众。 默认情况下，组内容作者具有写权限。

要创建 Adobe Target 受众，请执行以下操作：

1. 在导航控制台中，单击&#x200B;**Personalization**。 单击&#x200B;**受众**。

   ![screen-shot_2019-03-05at124139](assets/screen-shot_2019-03-05at124139.png)

1. 在“受众”控制台中，单击&#x200B;**创建**，然后单击&#x200B;**创建目标受众**。

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 在&#x200B;**Adobe Target配置**&#x200B;对话框中，选择Target配置，然后单击&#x200B;**确定**。
1. 在“规则#1”区域中，单击属性类型，然后在可用字段中输入任何属性信息。 完成后，选中该属性右侧的复选标记以保存该属性。有关所有属性的信息，请参阅[属性及其选项](#attributes-and-their-options)。
1. 单击 **添加规则** ，以添加其他规则。根据需要输入任意数量的规则。规则与布尔运算符AND相结合，这意味着受众必须满足每个规则的所有要求才能符合活动条件。
1. 单击&#x200B;**下一步**。
1. 输入受众的名称，然后单击&#x200B;**保存**。
1. 单击&#x200B;**保存**。受众随即会列在“受众”列表中。

### 属性及其选项 {#attributes-and-their-options}

您可以为以下每个属性创建定位规则。

| **属性** | **描述** | **有关更多信息** |
|---|---|---|
| **移动设备** | 根据移动设备、设备类型、设备供应商、屏幕尺寸（按像素）等参数锁定移动设备。 | 请参阅 Adobe Target 上的[移动设备文档](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=zh-Hans)。 |
| **自定义** | 自定义参数都是 mbox 参数。如果您将任何 mbox 参数传递给 mbox，或者使用 targetPageParams 函数，这些参数将会显示在此处以供在受众中使用。 | 请参阅 Adobe Target 上的[自定义参数文档](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=zh-Hans)。 |
| **操作系统** | 您可以锁定使用特定操作系统的访客。 | 定位使用Linux®、Macintosh或Windows的用户。 |
| **站点页面** | 锁定特定页面的访客或具有特定 mbox 参数的访客。 | 请参阅 Adobe Target 上的[站点页面文档](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=zh-Hans)。 |
| **浏览器** | 您可以锁定在访问您的页面时使用特定浏览器或特定浏览器选项的用户。 | 请参阅 Adobe Target 上的[浏览器选项文档](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=zh-Hans)。 |
| **访客配置文件** | 锁定满足特定配置文件参数的访客。 | 请参阅 Adobe Target 上的[访客配置文件文档](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile.html?lang=zh-Hans)。 |
| **流量源** | 根据将访客转至您的站点的搜索引擎或登陆页来锁定访客。 | 请参阅 Adobe Target 上的[流量源文档](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=zh-Hans)。 |

## 在“受众”控制台中修改受众 {#modifying-an-audience-in-the-audiences-console}

>[!NOTE]
>
>您只能编辑在当前所编辑的相同 AEM 实例中创建的 Adobe Target 受众。无法编辑在不同的 AEM 环境中创建的目标受众。

您可以从“受众”控制台中编辑任何ContextHub或Client Context受众。 您还可以编辑Adobe Target受众，但只能编辑在AEM中创建的受众：

1. 在导航控制台中，单击&#x200B;**Personalization**。 单击&#x200B;**受众**。
1. 单击要编辑的ContextHub或客户端上下文区段旁边的图标，然后单击&#x200B;**编辑**。
1. 在区段编辑器中进行任何编辑。请参阅[客户端上下文](/help/sites-administering/campaign-segmentation.md)或[ContextHub](/help/sites-developing/ch-configuring.md)文档。
