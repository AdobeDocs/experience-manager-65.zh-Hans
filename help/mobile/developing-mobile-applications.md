---
title: 在AEM中开发移动应用程序
description: 按照本页中的说明，开始使用Adobe PhoneGap Enterprise在AEM中开发移动应用程序。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: cf8ba05c-6dcd-4880-b8bf-72382118cd80
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 1%

---

# 在AEM中开发移动应用程序 {#developing-mobile-applications-in-aem}

{{ue-over-mobile}}

AEM使用Adobe PhoneGap和Adobe发布解决方案，允许您创建和管理内容丰富且基于实用工具的跨平台移动应用程序：

* 在一个位置管理您所有公司的移动应用程序。
* 查看开发和暂存环境中的应用程序，而无需复杂的配置配置文件以及额外工作来构建和上传应用程序以进行共享。
* 使用AEM创作环境为您的应用程序创建和管理丰富的内容。
* 将HTML5与Adobe PhoneGap结合使用，通过设备原生功能创建丰富的体验。
* 通过Cordova WebViews将HTML5 Web视图引入新的或预先存在的&#x200B;**原生**&#x200B;应用程序。
* 在所有交付渠道（包括Web、移动Web、移动应用程序和打印）中创建、策划和共享丰富的多媒体内容。

AEM与Adobe PhoneGap Build服务(`https://build.phonegap.com/`)集成以简化应用程序构建和部署过程。

**AdobeContentSync**&#x200B;使用户能够轻松地将Over-The-Air (OTA)页面和内容更新下载到他们的设备，而无需重新安装应用程序，或从appStore、Google Play或其他应用程序源下载。

**Adobe Analytics**&#x200B;已完全集成到AEM应用程序中，允许详细跟踪分发、地理位置、操作系统、设备、点击流、iBeacon跟踪等。

## 创建应用程序 {#creating-apps}

开发人员可以使用[AEM PhoneGap Starter Kit](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit)以及[https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps)中的其他资源来通过PhoneGap引导AEM应用程序，包括运行Cordova Webviews的参考本机应用程序。

Starter Kit Git存储库的自述文件中包含有关使用Starter Kit的教程：

* 自定义品牌
* Maven示例构建和部署目标
* Source控制存储库配置
* 安装并部署到本地或远程AEM实例中
* 从AEM卸载

>[!NOTE]
>
>在GitHub [此处](https://github.com/adobe-marketing-cloud-apps)和“厨房 — 水槽”源[此处](https://github.com/blefebvre/aem-phonegap-kitchen-sink)上可以找到其他参考实施源，包括Labs。

## 针对IOS 9和HTTP主机进行开发 {#developing-for-ios-and-http-hosts}

iOS开发人员应了解在iOS 9上运行的Cordova应用程序存在的未决问题。 此问题会阻止对不安全的主机(如&#x200B;*http://localhost:4502*)发出请求。 此问题将通过即将发布的cordova-ios（由Cordova CLI使用）解决，但与此同时，有两种可用的解决方法：

1. 作为直接的解决方法，您仍然可以使用任何iOS 8模拟器，而不会出现任何问题。
1. 如果必须使用iOS 9，则可以手动编辑您的应用程序 — Info.plist（在“&lt;应用程序根>/platforms/ios/&lt;应用程序名称>/&lt;应用程序名称>-Info.plist”文件中运行`cordova platform add ios`后找到）以包含以下属性：

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>有关“App Transport Security”的更多详细信息，请参阅[Apple的iOS9预发行版文档](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14)的以下部分以及此[栈栈溢出讨论](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/)。

## 在AEM中开发移动应用程序 {#developing-mobile-applications-in-aem-1}

* [启动AEM PhoneGap](/help/mobile/starting-aem-phonegap-app.md)
* [构建移动应用程序](/help/mobile/building-app-mobile-phonegap.md)
* [构建应用程序](/help/mobile/phonegap-structure-an-app.md)
* [使用应用程序控制台创建和编辑应用程序](/help/mobile/phonegap-apps-console.md)
* [单页面应用程序](/help/mobile/phonegap-single-page-applications.md)
* [使用PhoneGap CLI开发应用程序](/help/mobile/phonegap-apps-pg-cli.md)
* [访问设备功能](/help/mobile/phonegap-access-device-features.md)
* [使用AdobeMobile Analytics跟踪应用程序性能](/help/mobile/phonegap-intro-to-app-analytics.md)
* [将Adobe Analytics添加到您的移动应用程序](/help/mobile/phonegap-add-analytics-to-apps.md)
* [推送通知](/help/mobile/phonegap-push-notifications.md)
* [AEM Mobile内容个性化](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [应用程序的剖析](/help/mobile/phonegap-apps-arch.md)
* [您的混合应用程序是否已为AEM Mobile做好准备？](/help/mobile/phonegap-adding-content-to-imported-app.md)

### 其他资源 {#additional-resources}

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [使用AEM为Adobe PhoneGap Enterprise创作](/help/mobile/phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的内容](/help/mobile/administer-phonegap.md)
