---
title: 使用 Dynamic Media 中的“选择性发布”功能
description: 您可以选择在文件夹级别向Adobe Experience Manager或Dynamic Media发布资产或从中取消发布资产。 您可以使用管理发布或快速Publish ，而不是仅依赖其设置全局应用于Dynamic Media实例中的所有文件夹的Dynamic Media配置。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: cd025e9d-6fb1-436c-9e78-795f2daaf345
feature: Publishing
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '3000'
ht-degree: 3%

---

# 在Dynamic Media中配置文件夹级别的选择性发布 {#selective-publish-configure-folder}

您可以选择在文件夹级别向Adobe Experience Manager或Dynamic Media发布资产或从中取消发布资产。 您可以使用&#x200B;**[!UICONTROL 管理发布]**&#x200B;或&#x200B;**[!UICONTROL 快速Publish]**，而不是仅依赖其设置全局应用于Dynamic Media实例中的所有文件夹的&#x200B;**[!UICONTROL Dynamic Media配置]**。

例如，通过选择性发布，您可以处理尚未上线的产品的资产。 在这种情况下，营销团队可以访问同步到Dynamic Media的智能裁切图像和动态演绎版。 他们可以创建促销材料，而无需将这些资源发布到Dynamic Media进行全球交付。

>[!IMPORTANT]
>
>选择性Publish仅在Dynamic Media - Scene7模式下可用。

>[!NOTE]
>
>*将*&#x200B;资源复制到文件夹或从文件夹复制会清除这些资源的发布状态。 但是，当您&#x200B;*将*&#x200B;资源移动到其文件夹属性设置为&#x200B;**[!UICONTROL 选择性Publish]**&#x200B;的文件夹或从这些文件夹移动时，将保留这些资源的发布状态。

如果您稍后决定更改文件夹中的&#x200B;**[!UICONTROL 选择性Publish]**&#x200B;设置，则这些更改只会影响您此后上传到该文件夹的新资源。 文件夹中现有资源的发布状态保持不变，直到您从&#x200B;**[!UICONTROL 快速Publish]**&#x200B;或&#x200B;**[!UICONTROL 管理发布]**&#x200B;对话框中手动更改它们。

文件夹级别&#x200B;**[!UICONTROL Dynamic Media Publish mode]**&#x200B;选项始终默认为&#x200B;**[!UICONTROL Dynamic Media配置]**&#x200B;中的&#x200B;**[!UICONTROL Publish Assets]**&#x200B;设置中的值。 但是，本主题中的以下步骤向您展示了如何在文件夹级别手动更改此默认值（如以下步骤中所述）以覆盖&#x200B;**[!UICONTROL Dynamic Media配置]**&#x200B;值。

无论您是否依赖以下任一项：

* 在&#x200B;**[!UICONTROL Publish配置]**&#x200B;中设置了&#x200B;**[!UICONTROL Dynamic Media Assets]**&#x200B;值。
* 在文件夹级别属性中设置了&#x200B;**[!UICONTROL Dynamic Media Publish模式]**&#x200B;值。

您可以选择&#x200B;**[!UICONTROL 立即]**、**[!UICONTROL 激活]**&#x200B;或&#x200B;**[!UICONTROL 选择性Publish]**。 例如，您可以将&#x200B;**[!UICONTROL Publish配置]**&#x200B;中的&#x200B;**[!UICONTROL Dynamic Media Assets]**&#x200B;值设置为&#x200B;**[!UICONTROL 激活时]**，但是将文件夹级别的&#x200B;**[!UICONTROL Dynamic Media Publish]**&#x200B;模式值设置为&#x200B;**[!UICONTROL 选择性Publish]**，反之亦然。

在文件夹中配置选择性发布后，可以执行以下任一操作：

* [使用“管理发布”](#selective-publish-manage-publication)有选择地将资源发布到Dynamic Media或Experience Manager。
* [使用管理发布](#selective-unpublish-manage-publication)从Dynamic Media或Experience Manager有选择地取消发布资源。
* [Publish资源到Dynamic Media或使用Quick Publish](#quick-publish-aem-dm)进行Experience Manager。
* [通过搜索结果，有选择地发布或取消发布资源](#selective-publish-unpublish-search-results)。

**要在Dynamic Media中的文件夹级别配置选择性发布，请执行以下操作：**

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台。 在左侧，选择“导航”图标（位于“工具”图标正上方），然后选择&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 文件]**。
1. 执行下列操作之一：
   * 编辑现有文件夹的属性 — 在&#x200B;**[!UICONTROL 卡片视图]**、**[!UICONTROL 列视图]**&#x200B;或&#x200B;**[!UICONTROL 列表视图]**&#x200B;中，导航到要编辑其属性的文件夹。 选择文件夹，然后在工具栏中选择&#x200B;**[!UICONTROL 属性]**。
   * 编辑新文件夹的属性 — 在&#x200B;**[!UICONTROL 卡片视图]**、**[!UICONTROL 列视图]**&#x200B;或&#x200B;**[!UICONTROL 列表视图]**&#x200B;中，在页面的右上角附近，选择&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 文件夹]**。 在&#x200B;**[!UICONTROL 创建文件夹]**&#x200B;对话框中，输入文件夹的标题（必需），然后选择&#x200B;**[!UICONTROL 创建]**。 选择文件夹，然后在工具栏中选择&#x200B;**[!UICONTROL 属性]**。

1. 在&#x200B;**[!UICONTROL 同步模式]**&#x200B;下拉列表中，选择下列选项之一：

   | 同步模式 | 描述 |
   | --- | --- |
   | **[!UICONTROL 已继承]** | 该文件夹没有显式同步值；相反，该文件夹会从其上级文件夹之一或&#x200B;**[!UICONTROL Dynamic Media配置]**&#x200B;中设置的默认模式继承同步值。 **[!UICONTROL 已继承]**&#x200B;的详细状态将通过工具提示显示。 |
   | **[!UICONTROL 将此文件夹子树中的所有内容同步到Dynamic Media]** | 要成功发布到Dynamic Media，必须将资源同步到Dynamic Media。 选择此选项将包含此子树中用于同步到Dynamic Media的所有资源。 文件夹特定的设置将覆盖&#x200B;**[!UICONTROL Dynamic Media配置]**&#x200B;中的默认设置。 |
   | **[!UICONTROL 从Dynamic Media同步中排除此文件夹子树中的所有内容]** | 从同步到Dynamic Media中排除此子树中的所有资源。 |

   ![文件夹级别的选择性发布](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. 在&#x200B;**[!UICONTROL Dynamic Media Publish模式]**&#x200B;下拉列表中选择一个选项。 **[!UICONTROL Dynamic Media Publish mode]**&#x200B;选项始终默认为&#x200B;**[!UICONTROL Dynamic Media配置]**&#x200B;中设置的值。 但是，您可以使用以下选项之一手动覆盖此默认&#x200B;**[!UICONTROL Dynamic Media配置]**&#x200B;值。

   >[!IMPORTANT]
   >
   >无论您选择哪个Dynamic Media Publish模式选项，如果以后对&#x200B;*已*&#x200B;发布的资源进行任何更新，则这些更新将立即发布，用户无需执行任何进一步操作。
   >
   >如果发布的视频已更新，则必须再次发布该视频以反映投放时的更改。

   | Dynamic Media Publish模式选项 | 描述 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 将资源上传到此文件夹后，系统会将这些资源摄取到Experience Manager中，并立即提供URL/Embed。 此选项仅绑定到Experience Manager发布，无需用户干预即可发布资产。<br>如果您在上一步中在&#x200B;**[!UICONTROL 同步模式]**&#x200B;下选择了&#x200B;**[!UICONTROL 从Dynamic Media同步中排除此文件夹子树中的所有内容]**，则此选项&#x200B;*不可用*。 |
   | **[!UICONTROL 激活时]** | 将资源上传到此文件夹后，必须先明确发布资源，然后才能提供URL/嵌入链接。 此选项仅绑定到Experience Manager发布。<br>如果您在上一步中在&#x200B;**[!UICONTROL 同步模式]**&#x200B;下选择了&#x200B;**[!UICONTROL 从Dynamic Media同步中排除此文件夹子树中的所有内容]**，则此选项&#x200B;*不可用*。 |
   | **[!UICONTROL 选择性Publish]** | Assets将发布到您选择的Experience Manager或Dynamic Media以在公共域中交付。 两种发布方法相互排斥。 也就是说，您可以将资源发布到DMS7，以便使用智能裁剪或动态呈现版本等功能。 或者，您也可以将资源专门发布到Experience Manager以便安全预览；这些相同的资源&#x200B;*未*&#x200B;发布到DMS7以便在公共域中交付。 如果您在上一步的&#x200B;**[!UICONTROL 同步模式]**&#x200B;中选择了&#x200B;**[!UICONTROL 从Dynamic Media同步]**&#x200B;中排除此文件夹子树中的所有内容，则此选项不可用。 |

1. 在页面的右上角，选择&#x200B;**[!UICONTROL 保存并关闭]**，然后选择&#x200B;**[!UICONTROL 确定]**&#x200B;以返回到Experience Manager Assets。

## 使用“管理发布”有选择地将资源发布到Dynamic Media或Experience Manager{#selective-publish-manage-publication}

在使用&#x200B;**[!UICONTROL 管理发布]**&#x200B;有选择地将资源发布到Dynamic Media或Experience Manager之前，请确保已设置以下任一设置：

* **[!UICONTROL Publish配置]**&#x200B;到&#x200B;**[!UICONTROL 选择性Assets]**&#x200B;中的&#x200B;**[!UICONTROL Dynamic Media Publish]**&#x200B;选项
* 已配置文件夹级别的选择性发布。

请参阅[创建Dynamic Media配置](#configuring-dynamic-media-cloud-services)或[在Dynamic Media中配置文件夹级别的选择性发布](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>选择性Publish仅在Dynamic Media - Scene7模式下可用。

>[!NOTE]
>
>*将*&#x200B;资源复制到文件夹或从文件夹复制会清除这些资源的发布状态。 但是，当您&#x200B;*将*&#x200B;资源移动到其文件夹属性设置为&#x200B;**[!UICONTROL 选择性Publish]**&#x200B;的文件夹或从这些文件夹移动时，将保留这些资源的发布状态。

**要使用管理发布有选择地将资源发布到Dynamic Media或Experience Manager：**

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台。 在左侧，选择“导航”图标（位于“工具”图标正上方），然后选择&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 文件]**。
1. 在&#x200B;**[!UICONTROL 卡片视图]**、**[!UICONTROL 列视图]**&#x200B;或&#x200B;**[!UICONTROL 列表视图]**&#x200B;中，执行以下操作之一：
   * 导航到要发布其资产的文件夹。 选择文件夹，然后在工具栏中选择&#x200B;**[!UICONTROL 管理发布]**。 使用&#x200B;**[!UICONTROL 列表视图]**，以便更轻松地检查特定文件夹的发布状态。
   * 导航到要发布其资产的文件夹。 打开文件夹，然后选择一个或多个资源。 在工具栏上，选择&#x200B;**[!UICONTROL 管理发布]**。 使用&#x200B;**[!UICONTROL 列表视图]**，以便更轻松地检查特定资源的发布状态。

     >[!NOTE]
     >
     >如果在工具栏上看不到&#x200B;**[!UICONTROL 管理发布]**，请改为选择省略号按钮，然后从列表菜单中选择&#x200B;**[!UICONTROL 管理发布]**。

1. 在&#x200B;**[!UICONTROL 管理发布 — 选项]**&#x200B;页面的&#x200B;**[!UICONTROL 操作]**&#x200B;下，选择所需的激活类型。

   | 操作 | 描述 |
   | --- | --- |
   | **[!UICONTROL Publish]**(要Experience Manager) | 选择此选项可将资源发布到Experience Manager以进行安全预览。 |
   | **[!UICONTROL Publish到Dynamic Media]** | 选择此选项可将资源发布到Dynamic Media以便在公共域中交付，或者也可使用智能裁剪或动态呈现等功能。<br>仅当文件夹属性中的&#x200B;**[!UICONTROL Dynamic Media Publish模式]**&#x200B;设置为&#x200B;**[!UICONTROL 选择性Publish]**&#x200B;时，此选项才可用。 |

1. 在&#x200B;**[!UICONTROL 计划]**&#x200B;下，设置发布时间。

   | 计划 | 描述 |
   | --- | --- |
   | **[!UICONTROL 现在]** | 选择可立即发布资源。 |
   | **[!UICONTROL 稍后]** | 选择以在特定日期和时间发布资源。 |

1. 在&#x200B;**[!UICONTROL 管理发布]**&#x200B;页面的右上角，选择&#x200B;**[!UICONTROL 下一步]**。
1. 在&#x200B;**[!UICONTROL 管理发布 — 范围]**&#x200B;页面中，执行以下操作之一：

   * 如有必要，请选择要从发布中删除的一个或多个资源。
   * 在&#x200B;**[!UICONTROL 管理发布 — 范围]**&#x200B;页面的右上角，选择&#x200B;**[!UICONTROL Publish]**&#x200B;或&#x200B;**[!UICONTROL Publish到Dynamic Media]**。
1. 选择&#x200B;**[!UICONTROL 确定]**。

### 使用管理发布从Dynamic Media或Experience Manager有选择地取消发布资源 {#selective-unpublish-manage-publication}

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台。 在左侧，选择“导航”图标（位于“工具”图标正上方），然后选择&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 文件]**。
1. 在&#x200B;**[!UICONTROL 卡片视图]**、**[!UICONTROL 列视图]**&#x200B;或&#x200B;**[!UICONTROL 列表视图]**&#x200B;中，执行以下操作之一：
   * 导航到要取消发布其资产的文件夹。 选择文件夹，然后在工具栏中选择&#x200B;**[!UICONTROL 管理发布]**。 使用&#x200B;**[!UICONTROL 列表视图]**，以便更轻松地检查特定文件夹的发布状态。
   * 导航到要取消发布其资产的文件夹。 打开文件夹，然后选择一个或多个资源。 在工具栏上，选择&#x200B;**[!UICONTROL 管理发布]**。 使用&#x200B;**[!UICONTROL 列表视图]**，以便更轻松地检查特定资源的发布状态。

     >[!NOTE]
     >
     >如果在工具栏上看不到&#x200B;**[!UICONTROL 管理发布]**，请改为选择省略号按钮，然后从列表菜单中选择&#x200B;**[!UICONTROL 管理发布]**。

1. 在&#x200B;**[!UICONTROL 管理发布 — 选项]**&#x200B;页面的&#x200B;**[!UICONTROL 操作]**&#x200B;下，选择所需的停用类型。

   | 操作 | 描述 |
   | --- | --- |
   | **[!UICONTROL 取消发布]**(从Experience Manager) | 如果要从Experience Manager中取消发布资源，请选择此选项。 |
   | **[!UICONTROL 从Dynamic Media取消发布]** | 如果要从Dynamic Media取消发布资源，请选择此选项。<br>仅当文件夹属性中的&#x200B;**[!UICONTROL Dynamic Media Publish模式]**&#x200B;设置为&#x200B;**[!UICONTROL 选择性Publish]**&#x200B;时，此选项才可用。 |

1. 在&#x200B;**[!UICONTROL 计划]**&#x200B;下，设置停用时间。

   | 计划 | 描述 |
   | --- | --- |
   | **[!UICONTROL 现在]** | 选择可立即取消发布资源。 |
   | **[!UICONTROL 稍后]** | 选择以在特定日期和时间取消发布资源。 |

1. 在&#x200B;**[!UICONTROL 管理发布]**&#x200B;页面的右上角，选择&#x200B;**[!UICONTROL 下一步]**。
1. 在&#x200B;**[!UICONTROL 管理发布 — 范围]**&#x200B;页面中，执行以下操作之一：
   * 选择一个或多个要从取消发布中移除的资产。
   * 在&#x200B;**[!UICONTROL 管理发布 — 范围]**&#x200B;页面的右上角，选择&#x200B;**[!UICONTROL 取消发布]**&#x200B;或&#x200B;**[!UICONTROL 从Dynamic Media取消发布]**。
1. 选择&#x200B;**[!UICONTROL 确定]**。

## Publish资源到Dynamic Media或使用Quick PublishExperience Manager {#quick-publish-aem-dm}

您可以将&#x200B;**[!UICONTROL 快速Publish]**&#x200B;用于简单的资源激活案例。 **[!UICONTROL 快速Publish]**&#x200B;立即发布选定的资源，无需任何进一步的用户交互。 由于此操作，所有未发布的引用也会自动发布。

>[!NOTE]
>
>要使用&#x200B;**[!UICONTROL 快速Publish]**&#x200B;将资源发布到Dynamic Media或Experience Manager，请确保在&#x200B;**[!UICONTROL Publish配置]**&#x200B;或所选文件夹的文件夹属性中启用了&#x200B;**[!UICONTROL 选择性Dynamic Media]**。

**要使用Quick Publish将资源发布到Dynamic Media或Experience Manager：**

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台。 在页面的左侧，选择“导航”图标（位于“工具”图标的正上方），然后在页面的右侧选择&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 文件]**。
1. 在&#x200B;**[!UICONTROL 卡片视图]**、**[!UICONTROL 列视图]**&#x200B;或&#x200B;**[!UICONTROL 列表视图]**&#x200B;中，执行以下操作之一：
   * 导航到要发布其资产的文件夹。 选择文件夹，然后在工具栏中选择&#x200B;**[!UICONTROL 快速Publish]**。 使用&#x200B;**[!UICONTROL 列表视图]**，以便更轻松地检查特定文件夹的发布状态。
   * 导航到要发布其资产的文件夹。 打开文件夹，然后选择一个或多个资源。 在工具栏上，选择&#x200B;**[!UICONTROL 快速Publish]**。 使用&#x200B;**[!UICONTROL 列表视图]**，以便更轻松地检查特定资源的发布状态。

     >[!NOTE]
     >
     >如果在工具栏上看不到&#x200B;**[!UICONTROL 快速Publish]**，请改为选择省略号按钮，然后从列表菜单中选择&#x200B;**[!UICONTROL 快速Publish]**。

     ![文件夹级别的Dynamic Media快速Publish](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. 从&#x200B;**[!UICONTROL 快速Publish]**&#x200B;菜单列表中选择以下选项之一。

   | 快速Publish选项 | 作用 |
   | --- | --- | 
   | Publish到Experience Manager | 将立即发布选定的资源以Experience Manager。 |
   | 发布至 Brand Portal | 将所选资源立即发布到&#x200B;**[!UICONTROL Brand Portal]**。<br>仅当您的Experience Manager Assets实例已配置&#x200B;**[!UICONTROL Brand Portal]**&#x200B;时，此选项才可用。 |
   | 发布到 Dynamic Media | 将选定的资源立即发布到Dynamic Media。<br>必须将资源同步到Dynamic Media。 如有必要，请确保文件夹属性中的&#x200B;**[!UICONTROL 同步模式]**&#x200B;已设置为&#x200B;**[!UICONTROL 将此文件夹子树中的所有内容同步到Dynamic Media]**。 |

1. 选择&#x200B;**[!UICONTROL 确定]**，然后选择&#x200B;**[!UICONTROL 关闭]**。

## 通过搜索结果有选择地发布或取消发布资产 {#selective-publish-unpublish-search-results}

搜索结果可以显示具有不同Dynamic Media发布设置的资源文件夹中的资源。 当您从搜索结果中选择多个资源，且每个资源具有不同的Dynamic Media发布模式设置时，您可以从工具栏中触发&#x200B;**[!UICONTROL 管理发布]**&#x200B;以发布或取消发布。

另请参阅[搜索Experience Manager](/help/assets/search-assets.md)中的资源。

**要通过搜索结果有选择地发布或取消发布资源，请执行以下操作：**

1. 在Experience Manager中，在页面的左上角，选择Experience Manager徽标以访问全局导航控制台。 在页面的左侧，选择“导航”图标（位于“工具”图标的正上方），然后选择&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 文件]**。
1. 在靠近页面右上角的工具栏上，选择“搜索”图标（放大镜）。
1. 在&#x200B;**[!UICONTROL 键入以搜索]**&#x200B;文本字段中，输入关键字，然后按&#x200B;**[!UICONTROL Enter]**。
1. 在页面的右上角附近，选择&#x200B;**[!UICONTROL 列表视图]**&#x200B;图标。
1. 在页面的左上角附近，选择&#x200B;**[!UICONTROL 筛选器]**&#x200B;图标。

   ![搜索结果中的列表视图和筛选器](/help/assets/assets-dm/select-publish-search-result.png)

1. 在左侧面板中，展开&#x200B;**[!UICONTROL 状态]**，然后展开&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;搜索谓词。
1. 使用&#x200B;**[!UICONTROL 已发布]**&#x200B;和&#x200B;**[!UICONTROL 未发布]**复选框可根据Dynamic Media资源的已发布状态进一步优化搜索结果。
或者，您可以将这些复选框与**[!UICONTROL Publish]**&#x200B;搜索谓词一起使用，以优化&#x200B;**[!UICONTROL 已发布]**&#x200B;和&#x200B;**[!UICONTROL 未发布]** Experience Manager资源的搜索结果。
1. 执行下列操作之一：
   * 选择要发布或取消发布的一个或多个资源。
   * 在&#x200B;**[!UICONTROL 搜索结果]**&#x200B;页面的右上角附近，选择&#x200B;**[!UICONTROL 全选]**。
1. 在工具栏上，选择&#x200B;**[!UICONTROL 管理发布]**。 选择工具栏上的省略号图标，以便打开&#x200B;**[!UICONTROL 管理发布]**。
1. 在&#x200B;**[!UICONTROL 管理发布 — 选项]**&#x200B;页面上，选择所需的操作。

   | 选定的操作 | Publish Assets配置中的Dynamic Media设置 | Assets是 |
   | --- | --- | --- |
   | 发布 | 立即激活或激活时 | 已发布到Experience Manager和Dynamic Media。 |
   | 发布 | 选择性发布 | 仅发布到Experience Manager。 |
   | 取消发布 | 立即激活或激活时 | 已从Experience Manager和Dynamic Media取消发布。 |
   | 取消发布 | 选择性发布 | 仅从Experience Manager取消发布。 |
   | 发布到 Dynamic Media | 立即激活或激活时 | 未发布到Experience Manager或Dynamic Media，或同时发布到两者。 |
   | 发布到 Dynamic Media | 选择性发布 | 仅发布到Dynamic Media。 |
   | 从 Dynamic Media 取消发布 | 立即激活或激活时 | 不会从Experience Manager和/或Dynamic Media取消发布。 |
   | 从 Dynamic Media 取消发布 | 选择性发布 | 仅从Dynamic Media取消发布。 |

1. 在&#x200B;**[!UICONTROL 计划]**&#x200B;下，设置停用时间。

   | 选定的计划 | 发生什么情况 |
   | --- | --- |
   | 现在 | 将立即执行选定的操作。 |
   | 稍后 | 选定的操作将在选定的特定日期和时间运行。 |

1. 在&#x200B;**[!UICONTROL 管理发布 — 选项]**&#x200B;页面的右上角，选择&#x200B;**[!UICONTROL 下一步]**。
1. （可选）在&#x200B;**[!UICONTROL 管理发布 — 范围]**&#x200B;页中，查看表中的&#x200B;**[!UICONTROL Publish Target]**&#x200B;列以了解所选资源。

   | Publish Assets配置中的Dynamic Media设置 | 选定的操作 | 发布目标 |
   | --- | --- | --- |
   | 立即或<br>激活时 | 发布 | Experience Manager和Dynamic Media |
   | 立即或<br>激活时 | 发布到 Dynamic Media | 无 |
   | 选择性发布 | 发布 | Experience Manager |
   | 选择性发布 | 发布到 Dynamic Media | Dynamic Media |
   | 立即或<br>激活时 | 取消发布 | Experience Manager和Dynamic Media |
   | 立即或<br>激活时 | 从 Dynamic Media 取消发布 | 无 |
   | 选择性发布 | 取消发布 | Experience Manager |
   | 选择性发布 | 从 Dynamic Media 取消发布 | Dynamic Media |

1. 在&#x200B;**[!UICONTROL 管理发布 — 范围]**&#x200B;页面中，执行以下操作之一：
   * 选择一个或多个要从发布或取消发布中移除的资产。
   * 在&#x200B;**[!UICONTROL 管理发布 — 范围]**&#x200B;页面的右上角，选择&#x200B;**[!UICONTROL Publish]**&#x200B;或&#x200B;**[!UICONTROL 取消发布]**&#x200B;以开始操作。
1. 选择&#x200B;**[!UICONTROL 确定]**。

## 检查资源的发布状态 {#check-publish-status-of-asset}

您可以在Experience Manager中将&#x200B;**[!UICONTROL 时间轴]**&#x200B;与&#x200B;**[!UICONTROL 卡片视图]**、**[!UICONTROL 列视图]**&#x200B;或&#x200B;**[!UICONTROL 列表视图]**&#x200B;一起使用，以快速检查资源的发布状态。

**检查资产的发布状态：**

1. 在Experience Manager中，在页面的左上角，选择Experience Manager徽标以访问全局导航控制台。 在页面的左侧，选择“导航”图标（位于“工具”图标的正上方），然后选择&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 文件]**。
1. 在&#x200B;**[!UICONTROL 卡片视图]**、**[!UICONTROL 列视图]**&#x200B;或&#x200B;**[!UICONTROL 列表视图]**（下面的屏幕快照显示&#x200B;**[!UICONTROL 列表视图]**）中，打开包含您已发布或取消发布的资产的文件夹。
1. 选择一个资产，使其带有复选标记显示。 例如，请参阅下面的屏幕截图。
1. 在页面的左上角附近，从下拉菜单中选择&#x200B;**[!UICONTROL 时间轴]**。 左侧面板中的&#x200B;**[!UICONTROL 状态]**区域显示所选资源的发布状态。
当您使用**[!UICONTROL 列表视图]**&#x200B;时，会出现一列&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;的额外发布状态。
   * 默认情况下，配置为同步到Dynamic Media的文件夹显示&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;列。
   * 配置为同步到Dynamic Media的&#x200B;*非*文件夹不显示Dynamic Media列。
     ![列表视图和时间线](/help/assets/assets-dm/selective-publish-status-timeline.png)

## 选择性Publish故障诊断 {#selective-publish-troubleshoot}

某个资源未同步到Dynamic Media，但却触发了Dynamic Media发布操作，从而导致出现以下错误消息和解决方案：

![选择性Publish错误](/help/assets/assets-dm/selective-publish-error.png)
