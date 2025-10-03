---
title: '[!DNL Assets] 主页体验'
description: 个性化  [!DNL Experience Manager Assets]  主页，为用户提供丰富的欢迎界面体验，其中包括与资产相关的近期活动的快照。
contentOwner: AG
feature: Asset Management
role: Admin, User
exl-id: 042bd959-256a-4794-a34d-0848a6b8840d
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '562'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager Assets] 主页体验 {#aem-assets-home-page-experience}

个性化 [!DNL Adobe Experience Manager Assets] 主页，为用户提供丰富的欢迎界面体验，其中包括与资产相关的近期活动的快照。

[!DNL Assets] 主页提供丰富且个性化的欢迎界面体验，其中包含近期活动的快照，例如最近查看或上传的资产。

[!DNL Assets] 主页默认处于禁用状态。若要启用，请执行以下步骤：

1. 打开 [!DNL Experience Manager] 配置管理器 `https://[aem_server]:[port]/system/console/configMgr`。
1. 打开 **[!UICONTROL Day CQ DAM 事件记录器]**&#x200B;服务。
1. 选择&#x200B;**[!UICONTROL 启用此服务]**&#x200B;以启用活动记录。

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. 在&#x200B;**[!UICONTROL 事件类型]**&#x200B;列表中，选择需要记录的事件并保存更改。

   >[!CAUTION]
   >
   >启用“已查看的资产”、“已查看的项目”和“已查看的收藏集”选项后，记录的事件数量将显著增加。

1. 在配置管理器 `https://[aem_server]:[port]/system/console/configMgr` 中打开 **[!UICONTROL DAM 资产主页功能标记]**&#x200B;服务。
1. 选择 `isEnabled.name` 选项以启用 [!DNL Assets] 主页功能。保存更改。

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. 打开&#x200B;**[!UICONTROL 用户首选项]**&#x200B;对话框，并选择&#x200B;**[!UICONTROL 启用资产主页]**。保存更改。

   ![在“用户首选项”对话框中启用资产主页](assets/Annotation-color.png)

启用 [!DNL Assets] 主页后，可以通过“导航”页面进入 [!DNL Assets] 用户界面，或直接从 URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam` 访问。

![在 Assets 用户界面上配置体验链接](assets/config-experience-link.png)

单击&#x200B;**[!UICONTROL 单击此处配置体验链接]**，即可添加用户名、背景图像和轮廓图像。

[!DNL Assets] 主页包括以下部分：

* 欢迎区
* 小组件区

**欢迎区**

如果您的轮廓已存在，“欢迎区”将显示一条对您的欢迎消息。此外，还会显示您的轮廓图片和一张欢迎图像（如果已配置）。

如果您的轮廓不完整，“欢迎区”将显示一条通用欢迎消息，并在轮廓图片位置显示占位符。

**小组件区**

该区域位于“欢迎区”下方，并在以下部分下方显示现成的小组件：

* 活动
* 最近
* 发现

**活动**：在此部分中，**[!UICONTROL 我的活动]**&#x200B;小组件会显示已登录用户最近在资产上的操作（包括没有生成演绎版的资产），例如上传、下载、创建、编辑、评论、批注和共享资产。

**最近**：在此部分中，**[!UICONTROL 最近查看]**&#x200B;小组件会显示已登录用户最近访问的实体，包括文件夹、收藏集和项目。

**发现**：在此部分中，**[!UICONTROL 新内容]**&#x200B;小组件会显示最近上传到 [!DNL Assets] 部署的资产及其演绎版。

若要启用用户活动数据清理功能，请在配置管理器中启用 **[!UICONTROL DAM 事件清理服务]**。启用此服务后，系统会删除超出指定数量的已登录用户的活动记录。

欢迎界面提供便捷的导航工具，例如工具栏上的图标，可用于访问文件夹、收藏集和目录。

>[!NOTE]
>
>启用 [!UICONTROL Day CQ DAM 事件记录器]和 [!UICONTROL DAM 事件清除]服务会增加对 JCR 的写入操作和搜索索引，从而显著提高 [!DNL Experience Manager] 服务器上的负载。[!DNL Experience Manager] 服务器上额外的负载可能会影响性能。

>[!CAUTION]
>
>为 [!DNL Assets] 主页执行的用户活动捕获、筛选和清理操作会增加性能开销。因此，管理员应根据目标用户有效配置主页功能。
>
>Adobe 建议管理员及执行批量操作的用户避免使用资产主页功能，以防止用户活动数量过多。此外，管理员可以通过[!UICONTROL 配置管理器]来配置 [!UICONTROL Day CQ DAM 事件记录器]，从而排除特定用户的活动记录。
>
>如果您启用了该功能，Adobe 建议根据服务器负载情况合理安排清理频率。
