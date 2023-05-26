---
title: 导入和导出PDF生成器配置文件
seo-title: Importing and exporting PDF Generator configuration files
description: 了解如何导入和导出PDF生成器配置文件。
seo-description: Learn how to import and export PDF Generator configuration files.
uuid: 3367253b-d222-4c5f-9455-a1810d96112e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e25c1b35-73eb-4353-8e39-a2d4cdccd101
feature: PDF Generator
exl-id: b363b23a-29bb-4ea4-a8f2-5ba9fe3c7b27
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# 导入和导出PDF生成器配置文件 {#importing-and-exporting-pdf-generator-configuration-files}

配置文件包含PDF生成器转换信息，包括PDF、文件类型和安全性设置。

>[!NOTE]
>
>无法通过导入自定义native2pdfconfig.xml文件来更改PDF生成器的超时设置。 该文件中的超时设置仅供参考，并在PDF生成器中显示当前设置。 要更改超时设置，请参阅中的“设置PDF生成器性能参数” [安装和部署AEM Forms](https://www.adobe.com/go/learn_aemforms_installJBoss_63).

## 导出当前配置文件 {#export-your-current-configuration-file}

1. 在管理控制台中，单击“服务”>“PDF生成器”>“配置文件”>“导出配置”。
1. 要导出设置，请选择相应的选项：

   * 要导出所有命名设置，请选择“下载整个配置”。
   * 要仅导出一个Adobe PDF设置、安全设置或文件类型设置，请选择下载最小配置。

      如果要导出最小配置，请选择要导出的Adobe PDF、安全和文件类型设置。

1. 单击“下载”并将XML文件保存在适当的位置。

## 导入配置文件 {#import-a-configuration-file}

>[!NOTE]
>
>系统将根据导入文件中的信息重新配置系统。

1. 在管理控制台中，单击服务>PDF生成器>配置文件>导入配置。
1. 选择导入现有配置文件。
1. 要在“配置文件”框中指定文件位置，请单击“浏览”查找并选择文件，然后单击 **导入**.

## 转换AutoCAD文件中的所有图层 {#convert-all-layers-within-autocad-files}

默认情况下，“PDF生成器”只将AutoCAD文件的默认图层转换为PDF，而不转换文件中的所有图层。 要转换所有图层，请按照以下步骤操作。

1. 在管理控制台中，单击“服务”>“PDF生成器”>“配置文件”>“导出配置”。
1. 选择下载整个配置，然后单击下载。
1. 在文本编辑器中，打开下载的文件，然后在 `AutoCAD` 标记内 `PDFMaker` 标记，添加文本 `convertAllPages="true"`.
1. 在管理控制台中，单击服务>PDF生成器>配置文件>导入配置。
1. 选择“导入现有配置文件”，指定更新的文件，然后单击“导入”。

   使用修改后的配置文件转换的任何AutoCAD文件都将转换所有图层。

## 将配置重置为随PDF生成器一起安装的原始设置 {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}

1. 在管理控制台中，单击服务>PDF生成器>配置文件>导入配置。
1. 选择将配置重置为默认设置，然后单击导入。
