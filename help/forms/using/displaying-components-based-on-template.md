---
title: 根据使用的模板显示组件
seo-title: 根据使用的模板显示组件
description: 创建表单时，了解如何根据所选模板在侧栏中启用组件。
seo-description: 创建表单时，了解如何根据所选模板在侧栏中启用组件。
uuid: 790d201b-318d-4d02-9bc5-9d6bc41d057a
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
content-type: reference
discoiquuid: f658da57-0134-4458-9ef9-a99787b66742
docset: aem65
exl-id: 1fc56829-db81-4450-b1d8-b4a31110199e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# 根据使用的模板显示组件{#displaying-components-based-on-the-template-used}

当表单作者使用[template](../../forms/using/template-editor.md)创建自适应表单时，表单作者可以根据模板策略查看和使用特定组件。 您可以指定模板内容策略，以便选择表单作者在创作表单时看到的组件组。

## 更改模板{#changing-the-content-policy-of-a-template}的内容策略

创建模板时，会在内容存储库的`/conf`下创建模板。 根据您在`/conf`目录中创建的文件夹，模板的路径为：`/conf/<your-folder>/settings/wcm/templates/<your-template>`。

根据模板的内容策略，执行以下步骤以在侧栏中显示组件：

1. 打开CRXDE lite。\
   URL: `https://<server>:<port>/crx/de/index.jsp`
1. 在CRXDE中，导航到创建模板的文件夹。

   例如：`/conf/<your-folder>/`

1. 在CRXDE中，导航到：`/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/`

   要选择一组组件，需要新的内容策略。 要创建新策略，请复制并粘贴默认策略，然后对其重命名。

   默认内容策略的路径是：`/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/default`

   在`gridFluidLayout`文件夹中，复制并粘贴默认策略，然后对其重命名。 例如，`myPolicy`。

   ![复制默认策略](assets/crx-default1.png)

1. 选择您创建的新策略，然后在类型为`string[]`的右侧面板中选择&#x200B;**components**&#x200B;属性。

   选择并打开组件属性后，您会看到编辑组件对话框。 在“编辑组件”对话框中，您可以使用&#x200B;**+**&#x200B;和&#x200B;**-**&#x200B;按钮添加或删除组件组。 您可以添加组件组，其中包含您希望作者使用的表单中的组件。

   ![在策略中添加或删除组件](assets/add-components-list1.png)

   添加组件组后，单击&#x200B;**确定**&#x200B;以更新列表，然后单击CRXDE地址栏上方的&#x200B;**保存所有**&#x200B;并刷新。

1. 在模板中，将内容策略从默认更改为您创建的新策略。 （本例中为`myPolicy`。）

   要更改策略，请在CRXDE中，导航到`/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/guideContainer/rootPanel/items`。

   在`cq:policy`属性中，将`default`更改为新策略名称(`myPolicy`)。

   ![更新了模板内容策略](assets/updated-policy.png)

   使用模板创建表单时，您可以在侧栏中看到添加的组件。
