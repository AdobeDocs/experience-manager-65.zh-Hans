---
title: 配置用于Acrobat Reader DC扩展的凭据
seo-title: Configuring credentials for use with Acrobat Reader DC extensions
description: 了解如何配置凭据以与Acrobat Reader DC扩展一起使用。
seo-description: Learn how to configure credentials for use with Acrobat Reader DC extensions.
uuid: 9210e6c9-6f5c-402d-b355-b104cdffd5eb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5bb32fb1-4b6e-412f-aa16-f60db9dcaba1
exl-id: e8015d59-7587-46dc-a672-e0f1108102ad
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---

# 配置用于Acrobat Reader DC扩展的凭据{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

要将使用权限应用于PDF文档，请使用Acrobat Reader DC扩展的有效凭据配置AEM表单。 在安装AEM表单时，可能已配置凭据。 如果在运行Configuration Manager时未配置Acrobat Reader DC扩展凭据，或者如果需要导入新的或替换的凭据，则可以使用“信任存储管理”页面执行此操作。

如果您使用的是评估凭据，请在移动到生产环境时将其替换为生产凭据。 要更新过期的或评估凭据，请首先删除旧的Acrobat Reader DC扩展凭据。

有关获取凭据的信息，请参阅 [准备安装AEM表单（单台服务器）](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

信任存储可能包含多个Acrobat Reader DC扩展凭据。 必须将其中一个凭据指定为默认的Reader扩展凭据。 当Workbench用户无法确定在流程创建过程中要使用的凭据时，将使用默认凭据。 这些规则适用于默认凭据：

* 如果导入Acrobat Reader DC扩展凭据，并且信任存储不包含其他Acrobat Reader DC扩展凭据，则会将其设置为默认凭据。
* 如果导入选中了“默认”选项的Acrobat Reader DC扩展凭据，则会从现有默认凭据中删除默认类型。 导入的凭据将成为默认凭据。
* 您无法删除默认的Acrobat Reader DC扩展凭据。 要删除默认凭据，请首先将另一个凭据设置为默认凭据。 此规则的一个例外是，如果只有一个凭据，则可以删除它，即使它是默认凭据。
* 无法更新默认的Acrobat Reader DC扩展凭据。

>[!NOTE]
>
>您还可以采用编程方式导入和删除凭据。 (请参阅 [使用AEM表单进行编程](https://www.adobe.com/go/learn_aemforms_programming_63).)

## 导入Acrobat Reader DC扩展凭据 {#import-a-acrobat-reader-dc-extensions-credential}

1. 在管理控制台中，单击设置>信任存储管理>本地凭据。
1. 单击导入，然后在信任存储类型下，选择Acrobat Reader DC扩展凭据。
1. （可选）要指示此凭据是与Acrobat Reader DC扩展一起使用的默认凭据，请选择“默认”。
1. 在“别名”框中，键入凭据的标识符。 此标识符用作Acrobat Reader DC扩展中凭据的显示名称。 此别名还用于使用AEM Forms SDK以编程方式访问凭据。

   >[!NOTE]
   >
   >出于显示目的，别名会自动转换为大写。 在流程中引用别名时，别名不区分大小写。

1. 单击选择文件以找到凭据，键入凭据的密码，然后单击确定。

   如果出现错误消息“由于文件格式不正确或密码不正确而导入凭据失败”，请验证密码是否有效。

## 删除Acrobat Reader DC扩展凭据 {#remove-a-acrobat-reader-dc-extensions-credential}

1. 在管理控制台中，单击设置>信任存储管理>本地凭据。
1. 选择凭据，然后单击删除。

## 替换Acrobat Reader DC扩展凭据 {#replace-a-acrobat-reader-dc-extensions-credential}

1. 在管理控制台中，单击设置>信任存储管理>本地凭据。
1. 记下现有凭据的别名，然后选择该凭据并单击删除。
1. 使用完全相同的别名导入新凭据。
