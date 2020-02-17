---
title: 导出到 CSV
seo-title: 导出到 CSV
description: 将页面的相关信息导出到本地系统上的 CSV 文件
seo-description: 将页面的相关信息导出到本地系统上的 CSV 文件
uuid: 6eee607b-3510-4f6a-ba82-b27480a4fbe1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 7be506fb-f5c4-48dd-bec2-a3ea3ea19397
docset: aem65
translation-type: tm+mt
source-git-commit: 2d7492cdee9f7f730dfa6ad2ffae396b3a737b15

---


# 导出到 CSV{#export-to-csv}

**创建 CSV 报表**&#x200B;允许您将页面的相关信息导出到本地系统上的 CSV 文件。

* 所下载的文件名为 `export.csv`
* 其内容取决于您选择的属性。
* 您可以定义导出的路径以及深度。

>[!NOTE]
>
>系统将使用您浏览器的下载功能及默认目标位置。

**创建 CSV 导出**&#x200B;向导允许您选择以下内容：

* 要导出的属性
   * 元数据
      * 名称
      * 修改时间
      * 发布时间
      * 模板
      * 工作流
   * 翻译
      * 已翻译
   * 分析
      * 页面查看次数
      * 独特访客
      * 页面停留时间
* 深度
   * 父级路径
   * 仅直接子项
   * 其他级别的子项
   * 级别

生成的 `export.csv` 文件可以用 Excel 或任何其他兼容的应用程序打开。

![]() ![etc-01](assets/etc-01.png)

The create **CSV Report** option is available when browsing the **Sites** console (in List view): it is an option of the **Create** drop down menu:

![etc-02](assets/etc-02.png)

要创建 CSV 导出，请执行以下操作：

1. 必要时，打开&#x200B;**站点**&#x200B;控制台并导航到所需的位置。
1. From the toolbar, select **Create** then **CSV Report** to open the wizard:

   ![etc-03](assets/etc-03.png)

1. 选择需要导出的属性。
1. 选择&#x200B;**创建**。
