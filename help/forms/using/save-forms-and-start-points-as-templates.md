---
title: 将表单保存为模板
description: 了解如何从包含重复所需数据的表单创建模板。
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: b97175fd-cc3d-457a-af11-1f8c83192eb7
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
source-wordcount: '340'
ht-degree: 2%
---
# 将表单保存为模板 {#save-forms-as-templates}

>[!NOTE]
>
>AEM Forms应用程序当前已被弃用。 如有疑问或需要帮助，请联系[aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com)。

有时，当用户填写表单时，对几个字段的输入将保持不变。 对于这种情况，您可以填写每个实例中需要相同值的字段，并将表单或草稿另存为模板。 现在，每次创建模板的实例时，指定的字段都已填充了模板中指定的值。 这有助于节省填写表单所需的时间和精力。

执行以下步骤可创建模板：

1. 打开表单，然后选择或填写每次使用时值几乎相同的字段。 您可以将附件包含在填写表单时通常添加的模板中。
1. 选择&#x200B;**另存为模板** ![save_as_template](assets/save_as_template.png)图标。 将出现一个用于指定模板名称的对话框。
1. 指定模板的名称，然后选择&#x200B;**保存**。 模板将显示在模板文件夹中。

   如果存在具有相同名称的模板，则将显示一个用于确认覆盖现有模板的对话框。 要使用新模板替换现有模板，请选择&#x200B;**继续**；要使用其他名称保存模板，请选择&#x200B;**取消**。

现在，您可以打开保存的模板。 每次打开模板时，都会创建一个新表单或任务，并且该表单会显示保存的数据和选项。 使用模板，您可以编辑预填数据、添加附件、另存为草稿、提交任务或使用它创建另一个模板。 模板特定于移动设备，且未与Adobe Experience Manager Forms服务器同步。

如果不再需要某个模板，您也可以删除该模板。 要删除模板，请导航到模板文件夹，选择省略号，然后选择&#x200B;**删除模板**。

>[!NOTE]
>
>模板在本地可用，并且未与服务器同步。 清除应用程序的本地数据将删除模板。
