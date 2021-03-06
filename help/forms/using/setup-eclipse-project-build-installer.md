---
title: 构建AEM Forms Android应用程序
seo-title: 构建AEM Forms Android应用程序
description: 设置Android Studio项目并为适用于Android的AEM Forms应用程序构建.apk文件的步骤
seo-description: 设置Android Studio项目并为适用于Android的AEM Forms应用程序构建.apk文件的步骤
uuid: 2e140aaf-5be5-4d5d-9941-9d1f4bf2debd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f5d6d9bd-4f36-4a4f-8008-15fb853a9219
exl-id: 3fb069cf-d3ed-47b0-b6bf-82e110b3b059
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 6%

---

# 构建AEM Forms Android应用程序{#build-the-aem-forms-android-app}

按照建议的顺序，执行以下步骤来构建适用于AEM Forms的Android应用程序。

1. [下载AEM Forms应用程序源代码包](#download-android-zip)
1. [设置环境变量](#set-environment-variable-android)
1. [构建标准AEM Forms应用程序](#set-up-the-xcode-project)

## 下载AEM Forms应用程序源代码包{#download-android-zip}

AEM Forms应用程序源代码包是指`adobe-lc-mobileworkspace-src-<version>.zip`存档文件。 此存档包含构建自定义AEM Forms应用程序所需的源代码。 存档包含在Software Distribution上提供的`adobe-aemfd-forms-app-src-pkg-<version>.zip`包中。

执行以下步骤下载`adobe-aemfd-forms-app-src-pkg-<version>.zip`文件：

1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
1. 点按标题菜单中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在&#x200B;**[!UICONTROL Filters]**&#x200B;部分中：
   1. 从&#x200B;**[!UICONTROL Solution]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL Forms]**。
   2. 选择包的版本和类型。 您还可以使用&#x200B;**[!UICONTROL 搜索下载]**&#x200B;选项来筛选结果。
1. 点按适用于您的操作系统的包名称，选择&#x200B;**[!UICONTROL 接受EULA条款]**，然后点按&#x200B;**[!UICONTROL 下载]**。
1. 打开[包管理器](https://docs.adobe.com/content/help/zh-Hans/experience-manager-65/administering/contentmanagement/package-manager.html)，并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
1. 选择包并单击&#x200B;**[!UICONTROL Install]**。
1. 要下载源代码存档，请在浏览器中打开&#x200B;**https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip**。 Android应用程序.zip文件将在您的设备上下载。
1. 将.zip文件的内容解压缩到本地文件系统上的文件夹中。 例如， *C:\&lt;文件夹结构>\adobe-lc-mobileworkspace-src-2.4.20*

下图显示了`adobe-lc-mobileworkspace-src-<version>.zip\android`文件夹的结构。

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## 设置环境变量{#set-environment-variable-android}

在开始AEM Forms应用程序的构建过程之前，请设置以下环境变量：

* 将JAVA_HOME环境变量设置为本地文件系统上JDK软件的位置。 例如， C:\Program Files\Java\jdk1.8.0_181
* 将`ANDROID_SDK_ROOT`系统环境变量设置为适用于Android的SDK位置。 例如， C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk
* 设置`Path`系统环境变量以包含Android的platform-tools和tools文件夹位置。 例如， C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\platform-tools and C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\tools。

## 构建标准AEM Forms应用程序{#set-up-the-xcode-project}

在本地文件系统上保存了adobe-lc-mobileworkspace-src-&lt;version>.zip文件并设置了环境变量后，请使用以下任意选项构建标准的AEM Forms Android应用程序：

* [使用Android Studio构建AEM Forms应用程序](#using-android-studio)
* [使用Android Studio生成.apk文件](#generate-apk-android-studio)

### 使用Android Studio {#using-android-studio}构建AEM Forms应用程序

执行以下步骤以使用Android Studio构建AEM Forms应用程序：

1. 在您的计算机上启动Android Studio应用程序。
1. 单击&#x200B;**打开现有Android Studio项目**。 如果用于打开现有项目的对话框未自动显示，请选择&#x200B;**文件** > **打开**。
1. 导航到本地文件系统上的&#x200B;*adobe-lc-mobileworkspace-src-&lt;版本>.zip/android*，然后单击&#x200B;**确定**。

   **android**&#x200B;选项显示在左窗格中。

   ![android_folder_studio](assets/android_folder_studio.png)

1. 从左窗格中选择&#x200B;**android**，然后单击&#x200B;**运行** > **运行“android”**。
1. 从“选择部署目标”对话框的“连接的设备”部分选择Android设备，然后单击“确定”。

   成功构建开发环境后，您现在可以对应用程序应用自定义设置。 使用以下文章自定义应用程序：

   * [品牌化自定义](/help/forms/using/branding-customization.md)
   * [主题自定义](/help/forms/using/theme-customization.md)
   * [手势自定义](/help/forms/using/gesture-customization.md)

   对应用程序应用适当的自定义设置后，您可以生成要分发的.apk文件。

### 使用Android Studio {#generate-apk-android-studio}生成.apk文件

执行以下步骤以使用Android Studio生成.apk文件：

1. 在您的计算机上启动Android Studio应用程序。
1. 选择&#x200B;**打开现有Android Studio项目**。 如果用于打开现有项目的对话框未自动显示，请选择&#x200B;**文件** > **打开**。
1. 导航到本地文件系统上的&#x200B;*adobe-lc-mobileworkspace-src-&lt;版本>.zip/android*，然后单击&#x200B;**确定**。

   Android选项显示在左窗格中。

1. 选择&#x200B;**Build** > **Build APK**&#x200B;以生成.apk文件。

   或者，选择&#x200B;**Build** > **Generate Signed APK**&#x200B;以生成.apk文件的[签名版本](https://developer.android.com/studio/publish/app-signing)。

## 使用Android Debug Bridge {#build-android-debug-bridge}

生成.apk文件后，执行以下命令，以使用[Android Debug Bridge](https://developer.android.com/tools/help/adb.html)在Android设备上安装应用程序。

**Windows用户：** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**MAC用户：** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
