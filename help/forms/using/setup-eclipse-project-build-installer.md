---
title: 构建AEM Forms Android应用程序
description: 为Android版AEM Forms应用程序设置Android Studio项目和构建.apk文件的步骤
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 3fb069cf-d3ed-47b0-b6bf-82e110b3b059
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 2%

---

# 构建AEM Forms Android应用程序 {#build-the-aem-forms-android-app}

要构建适用于AEM Forms的Android应用程序，请按照建议的顺序执行以下步骤。

1. [下载AEM Forms应用程序源代码包](#download-android-zip)
1. [设置环境变量](#set-environment-variable-android)
1. [构建标准AEM Forms应用程序](#set-up-the-xcode-project)

## 下载AEM Forms应用程序源代码包 {#download-android-zip}

AEM Forms应用程序源代码包是指 `adobe-lc-mobileworkspace-src-<version>.zip` 存档。 此存档包含构建自定义AEM Forms应用程序所需的源代码。 存档包含在 `adobe-aemfd-forms-app-src-pkg-<version>.zip`软件包在Software Distribution上可用。

要下载 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 文件，请执行以下步骤：

1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
1. 选择 **[!UICONTROL Adobe Experience Manager]** 在标题菜单中可用。
1. 在 **[!UICONTROL 过滤器]** 部分：
   1. 选择 **[!UICONTROL Forms]** 从 **[!UICONTROL 解决方案]** 下拉列表。
   2. 选择包的版本和类型。 您也可以使用 **[!UICONTROL 搜索下载]** 用于筛选结果的选项。
1. 选择适用于您的操作系统的包名称，然后选择 **[!UICONTROL 接受EULA条款]**，并选择 **[!UICONTROL 下载]**.
1. 打开 [包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  并单击 **[!UICONTROL 上传包]** 以上传包。
1. 选择包并单击 **[!UICONTROL 安装]**.
1. 要下载源代码存档，请打开 **https://&lt;server>：&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip** 在浏览器中。 将在您的设备上下载Android应用程序.zip文件。
1. 将.zip文件的内容解压到本地文件系统中的文件夹中。 例如， *C:\&lt;folder structure=&quot;&quot;>\adobe-lc-mobileworkspace-src-2.4.20*

下图显示了 `adobe-lc-mobileworkspace-src-<version>.zip\android`文件夹。

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## 设置环境变量 {#set-environment-variable-android}

在开始AEM Forms应用程序的构建过程之前，请设置以下环境变量：

* 将JAVA_HOME环境变量设置为本地文件系统上JDK软件的位置。 例如，C:\Program Files\Java\jdk1.8.0_181
* 设置 `ANDROID_SDK_ROOT` 将系统环境变量更改为Android的SDK位置。 例如，C:\Users\&amp;lt；username>\AppData\Local\Android\Sdk
* 设置 `Path` 系统环境变量，以包含Android的平台工具和工具文件夹位置。 例如，C:\Users\&amp;lt；username>\AppData\Local\Android\Sdk\platform-tools和C:\Users\&amp;lt；username>\AppData\Local\Android\Sdk\tools。

## 构建标准AEM Forms应用程序 {#set-up-the-xcode-project}

保存adobe-lc-mobileworkspace-src后 — &lt;version>.zip文件并设置环境变量，使用以下任意选项构建标准AEM Forms Android应用程序：

* [使用Android Studio构建AEM Forms应用程序](#using-android-studio)
* [使用Android Studio生成.apk文件](#generate-apk-android-studio)

### 使用Android Studio构建AEM Forms应用程序 {#using-android-studio}

要使用Android Studio构建AEM Forms应用程序，请执行以下步骤：

1. 在您的计算机上启动Android Studio应用程序。
1. 单击 **打开现有的Android Studio项目**. 如果用于打开现有项目的对话框未自动显示，请选择 **文件** > **打开**.
1. 导航到 *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* ，然后单击 **确定**.

   此 **android** 选项将显示在左窗格中。

   ![android_folder_studio](assets/android_folder_studio.png)

1. 选择 **android** 从左窗格中单击 **运行** > **运行&#39;android&#39;**.
1. 从选择部署目标对话框上的连接的设备部分中选择Android设备，然后单击确定。

   成功构建开发环境后，您现在可以在应用程序上应用自定义设置。 使用以下文章可自定义应用程序：

   * [品牌化自定义](/help/forms/using/branding-customization.md)
   * [主题自定义](/help/forms/using/theme-customization.md)
   * [手势自定义](/help/forms/using/gesture-customization.md)

   将适当的自定义应用于应用程序后，可以生成用于分发的.apk文件。

### 使用Android Studio生成.apk文件 {#generate-apk-android-studio}

要使用Android Studio生成.apk文件，请执行以下操作：

1. 在您的计算机上启动Android Studio应用程序。
1. 选择 **打开现有的Android Studio项目**. 如果用于打开现有项目的对话框未自动显示，请选择 **文件** > **打开**.
1. 导航到 *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* ，然后单击 **确定**.

   Android选项将显示在左窗格中。

1. 要生成.apk文件，请选择 **生成** > **构建APK**.

   （可选）选择 **生成** > **生成已签名的APK** 生成 [已签名版本](https://developer.android.com/studio/publish/app-signing) .apk文件中的。

## 使用Android Debug Bridge {#build-android-debug-bridge}

生成.apk文件后，使用以下命令在Android设备上安装应用程序 [Android Debug Bridge](https://developer.android.com/tools/adb).

**Windows用户：** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**Mac用户：** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
