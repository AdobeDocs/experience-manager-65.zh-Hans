---
title: 资源Digital Rights Management
description: 了解如何在 [!DNL Experience Manager]中管理已许可资源的资源到期状态和信息。
contentOwner: AG
role: User, Admin
feature: DRM,Asset Management
exl-id: a49cfd25-e8d9-492f-be5e-acab0cf67a28
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 6%

---

# 资源的 Digital Rights Management {#digital-rights-management-in-assets}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/drm.html?lang=zh-Hans) |
| AEM 6.5 | 本文 |

数字资产通常与指定使用条款和持续时间的许可证相关联。 由于[!DNL Adobe Experience Manager Assets]已与[!DNL Experience Manager]平台完全集成，因此您可以有效地管理资产到期信息和资产状态。 您还可以将许可信息与资产相关联。

## 资产到期 {#asset-expiration}

资产到期是强制实施资产许可证要求的有效方式。 它可确保已发布的资产在过期时取消发布，从而避免出现任何许可证违规的可能性。 没有管理员权限的用户无法编辑、复制、移动、发布和下载已过期的资源。

您可以在卡片视图和列表视图中，在[!DNL Assets]控制台中查看资源的到期状态。

![expired_flag_list](assets/expired_flag_list.png)

*图：在列表视图中，[!UICONTROL 状态]列显示[!UICONTROL 已过期]横幅。*

您可以在左边栏的[!UICONTROL 时间轴]中查看资产的到期状态。

![chlimage_1-144](assets/chlimage_1-144.png)

>[!NOTE]
>
>对于处于不同时区的用户，资源的到期日期显示方式有所不同。

您还可以在&#x200B;**[!UICONTROL 引用]**&#x200B;边栏中查看资产的到期状态。 它管理资产过期状态以及复合资产与引用的子资产、收藏集和项目之间的关系。

1. 导航到要查看其引用网页和复合资产的资产。
1. 选择资产并在左边栏中打开&#x200B;**[!UICONTROL 引用]**。 对于已过期的资源，[!UICONTROL 引用]边栏的顶部显示到期状态&#x200B;**[!UICONTROL 资源已过期]**。

   ![chlimage_1-147](assets/chlimage_1-147.png)

   如果资源具有过期的子资源，[!UICONTROL 引用]边栏会显示状态&#x200B;**[!UICONTROL 资源具有过期的子Assets]**。

   ![chlimage_1-148](assets/chlimage_1-148.png)

### 搜索过期的资产 {#search-expired-assets}

您可以在“搜索”面板中搜索过期的资源，包括过期的子资源。

1. 在[!DNL Assets]控制台中，单击工具栏中的&#x200B;**[!UICONTROL 搜索]**&#x200B;以显示Omnisearch框。

1. 将光标置于Omnisearch框中，选择`Enter`键以显示搜索结果页面。
1. 在左边栏中打开搜索面板。 单击&#x200B;**[!UICONTROL 到期状态]**&#x200B;选项以展开它。

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. 选择&#x200B;**[!UICONTROL 过期]**。 筛选搜索结果后，仅显示已过期的资产。

当您选择&#x200B;**[!UICONTROL 过期]**&#x200B;选项时，[!DNL Assets]控制台仅显示由复合资源引用的过期资源和子资源。 引用过期子资产的复合资产不会在子资产过期后立即显示。 相反，在[!DNL Experience Manager]检测到下次运行计划程序时引用过期的子资产后，将显示这些子资产。

如果将已发布资源的到期日期修改为早于当前计划程序周期的日期，则该计划仍会在下次运行时将此资源检测为已到期资源，并相应地反映其状态。

此外，如果故障或错误阻止调度程序在当前周期中检测过期资产，则调度程序在下个周期中重新检查这些资产并检测其过期状态。

要启用[!DNL Assets]控制台以显示引用的复合资源以及过期的子资源，请在[!DNL Experience Manager]配置管理器中配置&#x200B;**[!UICONTROL Adobe CQ DAM到期通知]**&#x200B;工作流。

1. 打开[!DNL Experience Manager]配置管理器。
1. 选择&#x200B;**[!UICONTROL Adobe CQ DAM到期通知]**。 默认情况下，已选择&#x200B;**[!UICONTROL 基于时间的计划程序]**，该计划程序将安排在特定时间检查某个资源是否具有过期的子资源。 作业完成后，具有过期子资产和引用资产的资产会在搜索结果中显示为已过期。

1. 要定期运行该作业，请清除&#x200B;**[!UICONTROL 基于时间的计划程序规则]**&#x200B;字段，并在&#x200B;**[!UICONTROL 周期性计划程序]**&#x200B;字段中修改时间（以秒为单位）。例如，示例表达式`0 0 0 * * ?`在00小时触发作业。
1. 选择&#x200B;**[!UICONTROL 发送电子邮件]**&#x200B;以在资产过期时接收电子邮件。

   >[!NOTE]
   >
   >资产过期时，只有资产创建者（将特定资产上传到[!DNL Assets]的人员）会收到电子邮件。 有关在整个[!DNL Experience Manager]级别配置电子邮件通知的其他详细信息，请参阅[如何配置电子邮件通知](/help/sites-administering/notification.md)。

1. 在&#x200B;**[!UICONTROL Previour notification in seconds]**&#x200B;字段中，以秒为单位，指定当您要接收有关资产过期的通知时，资产过期的时间（以秒为单位）。 资源创建者在资源到期前收到一条消息，通知您资源将在指定时间后到期。 资产过期后，您将收到另一通知来确认过期。 此外，还会停用过期的资产。

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 资产状态 {#asset-states}

[!DNL Assets]控制台可以显示资源的各种状态。 根据特定资产的当前状态，其卡片视图会显示一个描述其状态的标签，例如，已过期、已发布、已批准、已拒绝等。

1. 在[!DNL Assets]用户界面中，选择一个资产。
1. 单击工具栏中的&#x200B;**[!UICONTROL Publish]**。 如果在工具栏上看不到&#x200B;**Publish**，请单击工具栏上的&#x200B;**[!UICONTROL 更多]**，然后找到&#x200B;**[!UICONTROL Publish]** ![发布选项](assets/do-not-localize/publish-globe.png)选项。
1. 从菜单中选择&#x200B;**[!UICONTROL Publish]**，然后关闭确认对话框。
1. 退出选择模式。 资源的发布状态显示在卡片视图的资源缩略图底部。 在列表视图中，已发布列显示资产的发布时间。

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. 要显示其资源详细信息页面，请在[!DNL Assets]界面中选择一个资源，然后单击&#x200B;**[!UICONTROL 属性]** ![查看属性](assets/do-not-localize/info-circle-icon.png)。

1. 在[!UICONTROL 高级]选项卡中，通过&#x200B;**[!UICONTROL 过期]**&#x200B;字段设置资源的过期日期。

   ![在“过期”字段中设置资源过期日期和时间](assets/asset-properties-advanced-tab.png)

   *图：资源[!UICONTROL 属性]页面中的[!UICONTROL 高级]选项卡用于设置资源过期。*

1. 单击&#x200B;**[!UICONTROL 保存]**，然后单击&#x200B;**[!UICONTROL 关闭]**&#x200B;以显示资产控制台。
1. 资源的发布状态表示卡片视图中资源缩略图底部的已过期状态。 在列表视图中，资产的状态显示为&#x200B;**[!UICONTROL 已过期]**。

   ![chlimage_1-160](assets/chlimage_1-160.png)

1. 在[!DNL Assets]控制台中，选择一个文件夹，然后在该文件夹上创建审核任务。
1. 审阅并批准/拒绝审阅任务中的资产，然后单击&#x200B;**[!UICONTROL 完成]**。
1. 导航到您为其创建审阅任务的文件夹。 您批准/拒绝的资产状态将显示在卡片视图的底部。 在列表视图中，审批和到期状态显示在相应的列中。

   ![chlimage_1-161](assets/chlimage_1-161.png)

1. 要根据资产的状态搜索资产，请单击&#x200B;**[!UICONTROL 搜索]** ![搜索选项](assets/do-not-localize/search_icon.png)以显示Omnisearch栏。
1. 选择`Return`并单击[!DNL Experience Manager]以显示搜索面板。
1. 在搜索面板中，单击&#x200B;**[!UICONTROL Publish状态]**，然后选择&#x200B;**[!UICONTROL 已发布]**&#x200B;以在[!DNL Assets]中搜索已发布的资源。

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. 单击&#x200B;**[!UICONTROL 批准状态]**，然后单击相应的选项以搜索已批准或已拒绝的资产。

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. 要根据资产的到期状态搜索资产，请在“搜索”面板中选择&#x200B;**[!UICONTROL 到期状态]**，然后选择相应的选项。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 您还可以根据各种搜索彩块化下的状态组合搜索资源。 例如，您可以通过从搜索彩块化中选择适当的选项来搜索已在审核任务中批准且尚未过期的已发布资产。

   ![chlimage_1-166](assets/chlimage_1-166.png)

## 在[!DNL Assets]中Digital Rights Management {#digital-rights-management-in-assets-1}

此功能强制接受许可协议，然后才能从[!DNL Adobe Experience Manager Assets]下载许可资产。

如果您选择受保护的资产并单击&#x200B;**[!UICONTROL 下载]**，则会将您重定向到许可证页面以接受许可协议。 如果不接受许可协议，**[!UICONTROL 下载]**&#x200B;选项将不可用。

如果所选内容包含多个受保护资产，则一次选择一个资产，接受许可协议，然后继续下载资产。

如果满足以下任一条件，则资产被视为受保护：

* 资源元数据属性`xmpRights:WebStatement`指向包含资源的许可协议的页面的路径。
* 资源元数据属性`adobe_dam:restrictions`的值是指定许可协议的原始HTML。

>[!NOTE]
>
>已弃用用于存储[!DNL Experience Manager]早期版本中的许可证的位置`/etc/dam/drm/licenses`。
>
>如果您创建或修改许可证页，或者从以前的[!DNL Experience Manager]版本移植它们，Adobe建议您将它们存储在`/apps/settings/dam/drm/licenses`或`/conf/&ast;/settings/dam/drm/licenses`下。

### 下载受DRM保护的资产 {#downloading-drm-assets}

1. 在卡片视图中，选择要下载的资源并单击&#x200B;**[!UICONTROL 下载]**。
1. 在&#x200B;**[!UICONTROL 版权管理]**&#x200B;页面，从列表中选择要下载的资产。
1. 在[!UICONTROL 许可证]窗格中，选择&#x200B;**[!UICONTROL 同意]**。 资产旁边会显示一个复选标记。 单击&#x200B;**[!UICONTROL 下载]**&#x200B;选项。

   >[!NOTE]
   >
   >仅当您选择同意受保护资产的许可协议时，才会启用&#x200B;**[!UICONTROL 下载]**&#x200B;选项。 但是，如果您的选择包含受保护和不受保护的资产，则窗格中仅列出受保护的资产，并且启用“**[!UICONTROL 下载]**”选项来下载不受保护的资产。 要同时接受多个受保护资产的许可协议，请从列表中选择资产，然后选择“同 **[!UICONTROL 意”]**。

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 在对话框中，单击&#x200B;**[!UICONTROL 下载]**&#x200B;以下载资源或其演绎版。
