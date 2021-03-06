---
title: “配置外出”设置
seo-title: “配置外出”设置
description: 配置“不在办公室”设置
seo-description: “配置外出”设置
exl-id: e4c9d74c-e08d-4675-91f2-4f9fc2f1bcea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 0%

---

# 配置“不在办公室”设置{#configure-out-of-office-settings}

如果您计划不在办公室，则可以指定在该期间分配给您的项目会发生什么情况。

您可以选择指定开始日期和时间以及结束日期和时间，以使“不在办公室”设置生效。 如果您位于与服务器不同的时区，则使用的时区是客户端的时区。

您可以设置一个默认人员，将所有项目都发送到该人员。 您还可以为特定流程中的项目指定例外情况，这些项目将发送给其他用户或保留在收件箱中，直到您返回。 如果指定的人员也不在办公室，则该项目将发送给他们指定的用户。 如果无法将项目分配给不在办公室的用户，则该项目会保留在您的收件箱中。

您可以根据工作流模型来分隔项目委派。 例如，您可以将与工作流A相关的项目分配给用户A，并将与工作流B相关的项目分配给用户B。


>[!NOTE]
>
>* 启用“出办公室”设置后，收件箱中所有可用的项目在启用该设置之前都会保留在您的收件箱中。 只会委派启用设置后收到的项目。
>* 关闭“不在办公室”设置后，委派的项目不会自动分配给您。 您可以使用声明功能将项目分配给您。
>* 当用户A将项目委派给用户B，用户B进一步委派给用户C时，项目仅分配给用户C，而不是用户B。
>* 当分配存在循环时，任务将保留在原始用户。 例如，当用户A将项目委派给用户B用户B将项目委派给用户C时，用户C将委派给用户D，用户D将委派给用户B时，会创建一个循环。 在这种情况下，项目将保留为原始用户。 用户A是上例中的原始用户。


## 为帐户{#enable-out-of-office}启用“外出”设置

为您的帐户启用“Enable the Out of Office（外出）”设置，并将您的收件箱项目委派给其他用户：

1. 登录到您的AEM实例。 点按![收件箱](assets/bell.svg)图标，然后点按&#x200B;**[!UICONTROL 查看全部]**。 此时会显示收件箱项目的列表。
1. 点按&#x200B;**[!UICONTROL 创建]**&#x200B;按钮旁边的![视图选择器](assets/viewlist.svg)或![视图选择器](assets/calendar.svg)图标，然后点按&#x200B;**[!UICONTROL 设置]**。 此时会出现“设置”对话框。
1. 打开设置对话框上的&#x200B;**[!UICONTROL Out of Office]**&#x200B;选项卡。
1. 点按&#x200B;**[!UICONTROL 启用/禁用]**&#x200B;按钮以启用“不在办公室”设置。
1. 为设置指定&#x200B;**[!UICONTROL 开始时间]**&#x200B;和&#x200B;**[!UICONTROL 结束时间]**。 项目仅在指定的时间段内委派。 将&#x200B;**[!UICONTROL End Time]**&#x200B;字段留空，以便在不确定的时间段内委派项目。
1. 选中&#x200B;**[!UICONTROL 在此期间转发我的项目]**&#x200B;复选框。 如果未选择选项并未指定代理人，则项目不会转发给任何用户。 尽管您不在，并且已启用该设置，但这些项目仍保留在您的收件箱中。
1. 点按&#x200B;**[!UICONTROL 添加被分派人]**。 在&#x200B;**[!UICONTROL 被分派人]**&#x200B;字段中指定用户以将项目委派到。 指定要委派给指定用户的&#x200B;**[!UICONTROL 工作流模型]**。 您可以选择多个工作流模型。

   此外，要将所有项目（不管工作流模型如何）分配给特定用户，请从“工作流模型”下拉列表中选择&#x200B;**[!UICONTROL 所有工作流]**。<br>

   要为除少数工作流模型之外的所有工作流模型分配项目给特定用户，请从“工作流模型”下拉列表中选择&#x200B;**[!UICONTROL 所有工作流]**，点按&#x200B;**[!UICONTROL +添加例外]**，然后指定要排除的工作流模型。
   <br>

   重复该步骤以添加更多受分配者。<br>

   >[!NOTE]
   >
   >受让人的顺序很重要。 将项目分配给启用了“不在办公室”设置的用户后，将根据订单分配人中指定的受分配人列表评估该项目。 当某个项目与标准匹配时，它将被分配给被分派人，并且不会选中下一个被分派人。

1. 点按&#x200B;**[!UICONTROL 保存]**。该设置在指定的开始日期和时间生效。 如果您在外出时登录，则在更改设置之前不会考虑在办公室中登录。

现在，在“外出”时间期间分配给您的项目会自动分配给指定的代理人。
![不在办公室](assets/out-of-office.png)

>[!NOTE]
>
>(仅限以Forms为中心的工作流项目)启用&#x200B;**允许被分派人使用工作流中**&#x200B;分配任务&#x200B;**步骤的“外出”设置**&#x200B;选项进行委派。 只有启用了上述选项的项目才会委派给其他用户。

## 限制 {#limitations}

* 不支持将项目分配给组。
* 当前不支持为项目任务启用“不在办公室”。
