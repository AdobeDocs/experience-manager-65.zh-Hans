---
title: 为AEM Forms应用程序设置环境
description: 用于构建和部署AEM Forms应用程序的硬件、软件和许可证。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 1d1f9db2-83cf-4612-ac8c-d2638c3bbaea
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# 为AEM Forms应用程序设置环境{#set-up-environment-for-aem-forms-app}

您需要以下硬件、软件和许可证来构建和部署AEM Forms应用程序：

## 对于Windows设备 {#for-windows-devices}

* Microsoft® Windows 10
* Microsoft® Visual Studio 2015
* Microsoft® Visual Studio Tools for Apache Cordova

## 对于iOS设备 {#for-ios-devices}

* 运行macOS X 10.9.5或更高版本的基于英特尔的Apple Mac
* iOS SDK 8.4或更高版本
* Xcode版本：适用于OS X或更高版本的Xcode 6.4
* iOS开发人员企业计划成员
* 用于分发内部iOS应用程序的企业证书
* Apple iPad与iOS 8.4或更高版本

## 对于Android™设备 {#for-android-devices}

* 可从[https://developer.android.com/studio](https://developer.android.com/studio)下载的Android™ Development Toolkit （ADT包）
* 如果在Mac系统上设置了环境，则ADT应安装在Applications文件夹中。
* 如果ADT安装在Mac上的任何其他位置，或者如果在Windows系统上设置了环境，则必须在`local.properties`文件中更新ADT SDK路径。 此文件在提取的源存档`mobileworkspace-src.zip`的`src\android`文件夹中可用。 在此文件中，将`sdk.dir`变量指向桌面上的ADT SDK位置。

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zip包含PhoneGap SDK 5.0。确保未预安装PhoneGap SDK。
