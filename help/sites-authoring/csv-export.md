---
title: 导出到 CSV
description: 将与页面相关的信息导出到本地系统上的 CSV 文件
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: 18910143-f2f2-4cfe-88b9-651df90d9cb9
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 78%

---

# 导出到 CSV{#export-to-csv}

**创建 CSV 报表**&#x200B;允许您将页面的相关信息导出到本地系统上的 CSV 文件。

* 所下载的文件名为 `export.csv`
* 其内容取决于您选择的属性。
* 您可以定义导出的路径以及深度。

>[!NOTE]
>
>系统将使用您浏览器的下载功能及默认目标位置。

**创建 CSV 导出**&#x200B;向导让您选择以下内容：

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
      * 页面视图
      * 独特访客
      * 页面停留时间
* 深度
   * 父项路径
   * 仅直接子项
   * 其他级别的子项
   * 级别

生成的 `export.csv` 文件可以用 Excel 或任何其他兼容的应用程序打开。

![etc-01](assets/etc-01.png)

创建 **CSV报表** 选项在浏览 **站点** 控制台（在列表视图中）：它是 **创建** 下拉菜单：

![etc-02](assets/etc-02.png)

要创建 CSV 导出，请执行以下操作：

1. 打开 **站点** 导航到所需的位置（如有必要）。
1. 从工具栏中，选择&#x200B;**创建**，然后选择 **CSV 报表**，以打开向导：

   ![etc-03](assets/etc-03.png)

1. 选择需要导出的属性。
1. 选择&#x200B;**创建**。
