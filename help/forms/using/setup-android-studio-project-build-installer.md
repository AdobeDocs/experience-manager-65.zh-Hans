---
title: 设置Android&amp；trade； studio项目并构建Android&amp；trade；应用程序
description: 设置Android&amp；trade； Studio项目并构建Adobe Experience Manager (AEM) Forms应用程序安装程序的步骤
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
exl-id: 47d6af00-34d8-4e5d-8117-86fc1b6f58cb
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 2%

---

# 设置Android™ studio项目并构建Android™应用程序 {#set-up-the-android-studio-project-and-build-the-android-app}

本文适用于构建AEM Forms应用程序6.3.1.1及更高版本。 要通过AEM Forms App 6.3的源代码构建应用程序，请参阅[设置Eclipse项目并构建Android™应用程序](/help/forms/using/setup-eclipse-project-build-installer.md)。

AEM Forms提供AEM Forms应用程序的完整源代码。 源包含用于构建自定义AEM Forms应用程序的所有组件。 源代码存档`adobe-lc-mobileworkspace-src-<version>.zip`是Software Distribution上`adobe-aemfd-forms-app-src-pkg-<version>.zip`包的一部分。

要获取AEM Forms应用程序源，请执行以下步骤：

1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
1. 选择标题菜单中的&#x200B;**[!UICONTROL Adobe Experience Manager]**。
1. 在&#x200B;**[!UICONTROL 筛选器]**&#x200B;部分中：
   1. 从&#x200B;**[!UICONTROL 解决方案]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL Forms]**。
   2. 选择包的版本和类型。 您还可以使用&#x200B;**[!UICONTROL 搜索下载]**&#x200B;选项来筛选结果。
1. 选择适用于您的操作系统的包名称，选择&#x200B;**[!UICONTROL 接受EULA条款]**，然后选择&#x200B;**[!UICONTROL 下载]**。
1. 打开[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hans)，然后单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
1. 选择包并单击&#x200B;**[!UICONTROL 安装]**。

以下图像显示`adobe-lc-mobileworkspace-src-<version>.zip`的提取内容。

![解压缩的Android™源内容](assets/mws-content-1.png)

下图显示了`src`文件夹中`android`文件夹的目录结构。

src![&#128279;](assets/android-folder.png)中Android文件夹的目录结构

## 构建标准AEM Forms应用程序 {#set-up-the-xcode-project}

1. 执行以下步骤可在Android™ Studio中设置项目并提供签名标识：

   登录到已安装并配置Android™ Studio的计算机。

1. 将下载的`adobe-lc-mobileworkspace-src-<version>.zip`存档复制到：

   对于Mac用户&#x200B;**&#x200B;**： `[User_Home]/Projects`

   Windows®用户&#x200B;**&#x200B;**： `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >对于Windows®，建议将Android™项目保留在系统驱动器中。

1. 在以下目录中解压缩归档文件：

   对于Mac用户&#x200B;**&#x200B;**： `[User_Home]/Projects/[your-project]`

   Windows®用户&#x200B;**&#x200B;**： `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >建议在将提取的Android项目导入Android™ Studio之前，先将其保留在系统驱动器中。

1. 启动Android™ Studio。

   **对于Mac用户**：更新`[User_Home]/Projects/[your-project]/android`文件夹中存在的`local.properties`文件，并将`sdk.dir`变量指向桌面上的`SDK`位置。

   **对于Windows®用户**：更新`%HOMEPATH%\Projects\[your-project]\android`文件夹中存在的`local.properties`文件，并将`sdk.dir`变量指向桌面上的`SDK`位置。

1. 单击&#x200B;**[!UICONTROL 完成]**&#x200B;以生成项目。

   该项目可在ADT项目资源管理器中使用。

   构建应用程序后![eclipse项目](assets/eclipsebuildmws.png)

1. 在Android™ Studio中，选择&#x200B;**[!UICONTROL 导入项目（Eclipse ADT、Gradle等）]**。
1. 在项目资源管理器中，选择要在&#x200B;**根目录**&#x200B;文本框中生成的项目的根目录：

   对于Mac用户：**&#x200B;**&#x200B;[User_Home]/Projects/MobileWorkspace/src/android

   对于Windows®用户&#x200B;**：** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. 导入项目后，会显示一个弹出窗口，其中包含用于更新Android™插件Gradle的选项。 根据您的要求，单击相应的按钮。

   ![dontremindmeagainforthisproject](assets/dontremindmeagainforthisproject.png)

1. 成功构建Gradle后，将显示以下屏幕。 将相应的设备或模拟器连接到系统，然后单击&#x200B;**[!UICONTROL 运行Android™]**。

   ![gradleconsole](assets/gradleconsole.png)

1. Android™ Studio显示连接的设备和可用的模拟器。 选择要运行应用程序的设备，然后单击“**确定**”。

   ![connecteddevice](assets/connecteddevice.png)

生成项目后，您可以选择使用Android™Debug Bridge或Android™ Studio安装应用程序。

### 使用Android™ Debug Bridge {#andriod-debug-bridge}

您可以使用以下命令通过[Android™ Debug Bridge](https://developer.android.com/tools/adb)在Android™设备上安装应用程序：

对于Mac用户&#x200B;**&#x200B;**： `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

Windows®用户&#x200B;**&#x200B;**： `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
