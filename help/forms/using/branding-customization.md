---
title: 品牌化自定义
description: 自定义应用程序图标、应用程序名称、启动图像和登录页面，为AEM Forms应用程序提供独特的组织特定外观。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 9333705b-9944-4a74-a30f-7d9ec85fd824
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 1%

---

# 品牌化自定义 {#branding-customization}

您可以自定义应用程序图标、应用程序名称、启动图像和登录页面，以便为AEM Forms应用程序提供独特的组织特定外观。 例如，您可以更改图像以使用您组织的徽标。 AEM Forms应用程序支持以下自定义设置：

* 自定义应用程序图标和启动图像
* 自定义应用程序名称
* 在登录页面上自定义图像
* 在应用程序菜单中自定义徽标

## 自定义图标和启动图像 {#customizing-icon-and-launch-images}

执行以下步骤可自定义默认应用程序图标和AEM Forms应用程序的启动图像：

>[!NOTE]
>
>对于所有图标和图像，请使用非隔行PNG格式。

### 自定义图标和启动图像 {#to-customize-icon-and-launch-images}

#### 适用于iOS的 {#for-ios}

1. 打开 `Capture.xcodeproj` Xcode中的项目。
1. (***用于自定义的图标***)在Capture的导航视图中，导航到 **[!UICONTROL 捕获>捕获>支持文件> Capture-info.plist]**. 单击图标文件旁边的下拉菜单。 指定图标文件(.png)的名称，然后将该文件上传到 **[!UICONTROL 捕获>捕获>资源>图标]**. 当前支持的维度为：29x29、50x50、58x58、72x72、100x100和144x144。
1. (***用于自定义启动图像***)确保映像的文件名是：

   * 纵向： `Default-Portrait~ipad.png` 和 `Default-Portrait@2x~ipad.png`
   * 对于横向： `Default-Landscape~ipad.png` 和 `Default-Landscape@2x~ipad.png`

   将它们上载到Capture项目以替换项目中的现有文件。

   >[!NOTE]
   >
   >确保图像的名称和分辨率与您在项目中替换的图像相匹配。

1. 在iOS设备或iOS模拟器上构建并运行AEM Forms应用程序。

#### 适用于Android {#for-android}

1. 将应用程序图标文件命名为：

   `ic_launcher.png`

1. 将相应的图标文件放在以下目录中：

   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-hdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-mdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxxhdpi`

   >[!NOTE]
   >
   >确保图像的名称和分辨率与您在项目中替换的图像相匹配。

1. 重新构建AEM Forms应用程序。

### 对于Windows {#for-windows}

1. 替换路径中的图标：

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\icons\windows`

1. 替换路径中的启动器图像：

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\screens\windows`

   >[!NOTE]
   >
   >确保图像的名称和分辨率与您在项目中替换的图像相匹配。

1. 重新构建AEM Forms应用程序。

## 自定义应用程序名称 {#customize-the-app-name}

### 适用于iOS的 {#for-ios-1}

1. 打开 `Capture.xcodeproj` Xcode中的项目。
1. 在Capture的导航视图中，导航到 **[!UICONTROL 捕获>捕获>支持文件> InfoPlist.strings]**.

   更新值 `CFBundleDisplayName` 属性显示的应用程序名称。

1. 在iOS设备或iOS模拟器上构建并运行AEM Forms应用程序。

   有关为iOS构建应用程序的详细信息，请参阅 [设置Xcode项目并构建iOS应用程序](/help/forms/using/setup-xcode-project-build-installer.md).

### 适用于Android {#for-android-1}

1. 在任意文本或Xml编辑器中打开以下Xml：

   `[User_Home]/Projects/[your-project]/src/android/res/values/strings.xml and android/res/values-en/strings.xml`

1. 更新键的值 `app_name`.
1. 重新构建AEM Forms应用程序。

   有关为Android构建应用程序的详细信息，请参阅 [设置Eclipse项目并构建Android应用程序](/help/forms/using/setup-eclipse-project-build-installer.md).

### 对于Windows {#for-windows-1}

1. 在任意文本编辑器中打开以下Xml：

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\config.xml`

1. 更新中的值 `<name>...</name>` 标记之前。
1. 重新构建AEM Forms应用程序。

   有关为Windows构建应用程序的详细信息，请参阅 [设置Visual Studio项目并构建Windows应用程序](/help/forms/using/setup-visual-studio-project-build-installer.md).

## 在登录页面上自定义图像 {#customizing-images-on-the-login-page}

AEM Forms应用程序的登录页面具有徽标和背景图像。 徽标位于登录对话框的上方，背景图像位于登录对话框的下方。 执行以下步骤以自定义登录页面上的默认映像：

**开始之前**

确保您拥有以下图像：

<table>
 <tbody>
  <tr>
   <th><p>描述</p> </th>
   <th><p>大小</p> </th>
   <th><p>文件名</p> </th>
  </tr>
  <tr>
   <td><p>徽标</p> </td>
   <td><p>72 x 72像素</p> </td>
   <td><p>LC-logo.png</p> </td>
  </tr>
  <tr>
   <td><p>背景图像（纵向）</p> </td>
   <td><p>1280 x 989像素</p> </td>
   <td><p>Landing_bg.jpeg</p> </td>
  </tr>
 </tbody>
</table>

**使用Xcode自定义登录页面上的图像**

1. 打开 `Capture.xcodeproj` Xcode中的项目。

1. 导航至 `www/wsmobile/images`文件夹。
1. 要更改徽标，请替换默认值 `LC-logo.png` 包含自定义的文件 `LC-logo.png` 文件。
1. 要更改背景，请替换默认背景 `Landing_bg.jpeg` 包含自定义的文件 `Landing_bg.jpeg`文件。
1. 在iOS设备或iOS模拟器上构建并运行AEM Forms应用程序。

### 使用Eclipse自定义登录页面上的图像 {#to-customize-images-on-the-login-pages-using-eclipse}

1. 在Eclipse中打开Android项目。

1. 导航至 `assets/www/wsmobile/images`文件夹。
1. 要更改徽标，请替换默认值 `LC-logo.png` 包含自定义的文件 `LC-logo.png` 文件。
1. 要更改背景，请替换默认背景 `Landing_bg.jpeg` 包含自定义的文件 `Landing_bg.jpeg`文件。
1. 在Android设备上构建和运行AEM Forms应用程序。

### 使用Visual Studio自定义登录页上的图像 {#to-customize-images-on-the-login-pages-using-visual-studio}

1. 打开 `MWSWindows.sln` Visual Studio中的项目。

1. 导航至 `MWSWindows\www\wsmobile\images`文件夹。
1. 要更改徽标，请替换默认值 `LC-logo.png` 包含自定义的文件 `LC-logo.png` 文件。
1. 要更改背景，请替换默认背景 `Landing_bg.jpeg` 包含自定义的文件 `Landing_bg.jpeg`文件。
1. 在Windows设备上构建并运行AEM Forms应用程序。

## 在应用程序菜单中自定义徽标 {#customizing_images_on_the_login_page-1}

登录AEM Forms应用程序并选择菜单按钮后，您可以看到菜单上方的徽标。 执行以下步骤以自定义默认徽标：

**开始之前**

确保您拥有以下图像：

<table>
 <tbody>
  <tr>
   <th><p>描述</p> </th>
   <th><p>大小</p> </th>
   <th><p>文件名</p> </th>
  </tr>
  <tr>
   <td><p>徽标</p> </td>
   <td><p>72 x 72像素</p> </td>
   <td><p>aem_icon.png</p> </td>
  </tr>
 </tbody>
</table>

**使用Xcode自定义登录页面上的图像**

1. 打开 `Capture.xcodeproj` Xcode中的项目。

1. 导航至 `www/wsmobile/images`文件夹。
1. 要更改徽标，请替换默认值 `aem_icon.png` 包含自定义的文件 `aem_icon.png` 文件。
1. 在iOS设备或iOS模拟器上构建并运行AEM Forms应用程序。

### 使用Eclipse自定义登录页面上的图像 {#to-customize-images-on-the-login-pages-using-eclipse-1}

1. 在Eclipse中打开Android项目。

1. 导航至 `assets/www/wsmobile/images`文件夹。
1. 要更改徽标，请替换默认值 `aem_icon.png` 包含自定义的文件 `aem_icon.png` 文件。
1. 在Android设备上构建和运行AEM Forms应用程序。

### 使用Visual Studio自定义登录页上的图像 {#to-customize-images-on-the-login-pages-using-visual-studio-1}

1. 打开 `MWSWindows.sln` Visual Studio中的项目。

1. 导航至 `MWSWindows\www\wsmobile\images`文件夹。
1. 要更改徽标，请替换默认值 `aem_icon.png` 包含自定义的文件 `aem_icon.png` 文件。
1. 在Windows设备上构建并运行AEM Forms应用程序。
