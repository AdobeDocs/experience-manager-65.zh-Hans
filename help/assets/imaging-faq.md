---
title: 智能成像
description: 智能成像应用每个用户的独特查看特性，自动为用户提供针对其体验而优化的正确图像，从而提高性能和参与度。
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
feature: Asset Management,Renditions
role: User, Admin
exl-id: e427d4ee-d5c8-421b-9739-f3cf2de36e41
solution: Experience Manager, Experience Manager Assets
source-git-commit: 0b90fdd13efc5408ef94ee1966f04a80810b515e
workflow-type: tm+mt
source-wordcount: '3300'
ht-degree: 0%

---

# 智能成像 {#smart-imaging}

智能成像应用每个用户的独特查看特性，自动为用户提供针对其体验而优化的正确图像，从而提高性能和参与度。

## 关于智能成像 {#what-is-smart-imaging}

智能成像技术可应用Adobe Sensei AI功能，并与现有“图像预设”配合使用。 它致力于通过基于客户端浏览器功能自动优化图像格式、大小和质量来增强图像投放性能。

现在，通过改进的智能成像（现在同时具有AVIF和WebP支持），获得更好的Google Core Web Vital LCP（最大内容绘制）分数。

>[!IMPORTANT]
>
>智能成像要求您使用与Adobe Experience Manager - Dynamic Media捆绑在一起的现成CDN（内容分发网络）。 此功能不支持任何其他自定义CDN。

>[!TIP]
>
>尝试使用Dynamic Media [_快照_](https://snapshot.scene7.com/)来发现Dynamic Media图像修饰符和智能成像的好处。
>
>Snapshot是一种可视化演示工具，旨在说明Dynamic Media在优化和动态图像投放方面的强大功能。 试验测试图像或Dynamic Media URL，以可视化方式观察各种Dynamic Media图像修饰符的输出，并优化以下内容的智能成像：
>
>* 文件大小（使用WebP和AVIF交付）
>* 网络带宽
>* DPR（设备像素比率）
>
>要了解使用快照的容易程度，请播放[快照培训视频](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot)（3分17秒）。

智能成像技术与Adobe一流的高级CDN（内容分发网络）服务完全集成，可进一步提升性能。 此服务可找到服务器、网络和对等点之间的最佳Internet路由。 它可以找到具有最低延迟和最低数据包丢失率的路由，而不使用Internet上的默认路由。

以下图像资产示例描述了新增的智能成像优化：

| 图像(URL) | 缩略图 | 大小(JPEG) | 使用智能成像调整大小(WebP) | 使用智能成像调整大小(AVIF) | 使用WebP减少% | AVIF降低% |
|---|---|---|---|---|---|---|
| [图像1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&fmt=jpg&qlt=85&resmode=bisharp&op_usm=5,0.125,5,0) | ![图片1](/help/assets/assets-dm/picture1.png) | 145 KB | 106 KB | 90.2 KB | 26.89% | 37.79% |
| [图像2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&fmt=jpg&qlt=85&resmode=bisharp&op_usm=5,0.125,5,0) | ![图片2](/help/assets/assets-dm/picture2.png) | 412 KB | 346 KB | 113 KB | 16.01% | 72.57% |
| [图像3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&fmt=jpg&qlt=85&resmode=bisharp&op_usm=5,0.125,5,0) | ![图片3](/help/assets/assets-dm/picture3.png) | 221 KB | 189 KB | 87.1 KB | 14.47% | 60.58% |
| [图像4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&qlt=85&resmode=bisharp&op_usm=5,0.125,5,0) | ![图片4](/help/assets/assets-dm/picture4.png) | 594 KB | 545 KB | 286 KB | 8.25% | 51.85% |

与上述内容类似，Adobe还使用较大的样本集运行了测试。 与WebP相比，AVIF格式提供了20%的额外尺寸缩减，比JPEG提供了27%的缩减。 视觉质量都一样。 与JPEG相比，AVIF的平均大小缩减率高达41%。

将WebP和AVIF与PNG进行比较，可以看到WebP的大小减少了84%，AVIF的大小减少了87%。 此外，由于WebP和AVIF格式都支持透明度和多种图像动画，因此非常适合替代透明的PNG和GIF文件。

另请参阅[使用新一代图像格式（WebP和AVIF）的图像优化](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)

<!-- HIDDEN ON MAY 19, 2022 BASED ON CQDOC-19280 On the mobile web, the challenges are compounded by two factors:

* Large variety of devices with different form factors and high-resolution displays.
* Constrained network bandwidth.

In terms of images, the goal is to serve the best quality images as efficiently as possible. -->

## 智能成像的优势 {#what-are-the-key-benefits-of-smart-imaging}

智能成像可根据用户的浏览器、设备显示和网络条件自动优化文件大小，从而增强图像交付。 此方法可确保加快加载速度，并跨不同的环境获得更好的观看体验。 由于图像构成了页面加载时间的大部分，因此任何性能改进都会对业务KPI产生深远的影响，例如：

* 更高的转化率。
* 网站逗留时间。
* 较低的网站跳出率。

最新智能成像的最新主要优势包括：

* 支持下一代AVIF格式。
* PNG到WebP和AVIF现在支持有损转换。 由于PNG是一种无损格式，因此早期传送的WebP和AVIF是无损的。
* 浏览器格式转换(`bfc`)
* 设备像素比率(`dpr`)
* 网络带宽(`network`)

### 关于浏览器格式转换(bfc) {#bfc}

通过将`bfc=on`附加到图像URL来启用浏览器格式转换，对于不同的浏览器，自动将JPEG和PNG转换为有损AVIF、有损WebP、有损JPEGXR、有损JPEG2000。 对于不支持这些格式的浏览器，智能成像将继续提供JPEG或PNG。 智能成像会随着格式更改重新计算新格式的质量。

您可以通过将`bfc=off`附加到图像的URL来关闭智能成像。

另请参阅Dynamic Media图像服务和渲染API中的[bfc](https://experienceleague.adobe.com/zh-hans/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-bfc)。

### 关于设备像素比(dpr)优化 {#dpr}

设备像素比率(DPR)，也称为CSS像素比率，表示设备的物理像素与逻辑像素之间的关系。 随着视网膜显示器的兴起，现代移动设备的像素分辨率也迅速提高。

启用“设备像素比”优化将以屏幕的本机分辨率呈现图像，从而使图像更加清晰。

当前，显示的像素密度来自Akamai CDN标头值。

| 图像URL中允许的值 | 描述 |
|---|---|
| `dpr=off` | 在单个图像URL级别关闭DPR优化。 |
| `dpr=on,dprValue` | 使用自定义值（任何客户端逻辑或其他方法检测到值）覆盖智能成像检测到的DPR值。 `dprValue`允许的值是大于0的任何数字。 |

>[!NOTE]
>
>* 即使公司级别的DPR设置为off，您仍可以使用`dpr=on,dprValue`。
>* 由于DPR优化，当生成的图像大于MaxPix Dynamic Media设置时，始终通过保持图像的宽高比来识别MaxPix宽度。

| 请求的图像大小 | 设备像素比率(dpr)值 | 投放的图像大小 |
|---|---|---|
| 816 x 500 | 1 | 816 x 500 |
| 816 x 500 | 2 | 1632 x 1000 |

另请参阅[处理图像时](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-images)和[处理智能裁剪时](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop)。

### 关于网络带宽优化 {#network}

打开网络带宽可根据实际网络带宽自动调整提供的图像质量。 对于较差的网络带宽，DPR（设备像素比）优化会自动关闭，即使它已经打开。

通过将`network=off`附加到图像URL，您的公司可以禁用单个图像的网络带宽优化。

| 图像的URL中允许的值 | 描述 |
|---|---|
| `network=off` | 关闭单个图像URL级别的网络优化。 |

DPR和网络带宽值基于捆绑的CDN所检测到的客户端值。 这些值有时不准确。 例如，DPR=2的iPhone5和`dpr=3`的iPhone12均显示`dpr=2`。 但是，对于高分辨率设备，发送`dpr=2`比发送`dpr=1`好。 但是，克服这种不准确性的最佳方法是使用客户端DPR为您提供100%准确的值。 它适用于任何设备，无论是Apple还是任何其他已启动的设备。 请参阅[使用客户端设备像素比](/help/assets/client-side-dpr.md)的智能成像。

### 智能成像的其他主要优势

* 改进了使用最新智能成像的网页的Google SEO排名。
* 立即提供优化的内容（在运行时）。
* 使用Adobe Sensei技术根据图像请求中指定的质量(`qlt`)进行转换。
* TTL（生存时间）独立。 以前，智能成像工作必须至少12小时的TTL。
* 以前，原始图像和派生图像都被缓存，缓存失效需要两步过程。 在最新的智能成像中，仅缓存派生项，从而允许执行单步缓存失效过程。
* 在规则集中使用自定义标头的客户受益于最新的智能成像，因为与以前的智能成像版本不同，这些标头不会受到阻止。

## 常见问题解答

+++智能成像是否有任何许可成本？

不行。智能成像随现有许可证一起提供。 这条规则适用于Dynamic Media Classic或Experience Manager - Dynamic Media(内部部署、AMS和Experience Manager as a Cloud Service)。

>[!NOTE]
>
>智能成像不适用于Dynamic Media — 混合型客户。

+++

+++智能成像如何工作？

当用户请求图像时，智能成像会分析用户特征并根据浏览器将其转换为相应的格式。 这些格式转换以不降低视觉保真度的方式进行。 智能成像会根据浏览器功能，通过以下方式自动将图像转换为不同的格式。

* 如果您的浏览器支持格式，则自动转换为AVIF
* 如果AVIF转换无益或浏览器不支持AVIF，则自动转换为WebP
* 如果Safari不支持WebP，则自动转换为JPEG2000
* 自动转换为IE 9+的JPEGXR，或如果Edge不支持WebP

  | 图像格式 | 支持的浏览器 |
  |---|---|
  | AVIF | [https://caniuse.com/avif](https://caniuse.com/avif) |
  | WebP | [https://caniuse.com/webp](https://caniuse.com/webp) |
  | JPEG 2000 | [https://caniuse.com/jpeg2000](https://caniuse.com/jpeg2000) |
  | JPEGXR | [https://caniuse.com/jpegxr](https://caniuse.com/jpegxr) |

* 对于不支持这些格式的浏览器，将提供最初请求的图像格式。

如果原始图像大小小于智能成像生成的尺寸，则会提供原始图像。

+++

+++支持哪些图像格式？

智能成像支持以下图像格式：

* JPEG
* PNG

在转换为新格式时，智能成像会重新计算JPEG图像文件格式的质量。

对于支持透明度的图像文件格式（如PNG），您可以配置智能成像以传递有损的AVIF和WebP。 对于有损格式转换，智能成像使用图像URL中所述的质量，或在Dynamic Media公司帐户中配置的质量。

+++

+++智能成像如何与已在使用的现有图像预设一起使用？

智能映像可与您现有的映像预设无缝集成，同时遵循您所有的映像设置。

唯一的调整涉及图像格式、质量或两者。 在格式转换过程中，智能成像会根据预设设置保留完整的视觉保真度，但会提供较小的文件大小。 只需通过将`bfc=on`、`dpr=on,dprValue`、`network=on`或全部三个参数设置添加到现有URL或预设中即可启用它。

例如，假设图像预设指定了500 × 500像素的JPEG格式，即`quality=85`和`unsharp mask=0.1,1,5`。 智能成像可检测用户是否使用Chrome浏览器。 然后，它会将图像转换为具有相同尺寸(500 × 500)的WebP以及与JPEG设置相匹配的钝化蒙版。 然后，系统会比较WebP版本和JPEG版本的文件大小，并将较小版本提供给用户。

+++

<!--

### Do I have to change any URLs, image presets, or deploy any new code on my site for Smart Imaging? 

No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add code to your website to detect a user's browser. All of this functionality is handled automatically.

<!-- Smart Imaging works seamlessly with your existing image URLs and image presets if you configure Smart Imaging on your existing custom domain. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. It is all handled automatically.

In case you must configure a new custom domain to use Smart Imaging, the URLs must be updated to reflect this custom domain.

To understand pre-requisites for Smart Imaging, see [Am I eligible to use Smart Imaging?](#am-i-eligible-to-use-smart-imaging) -->

<!-- OLD As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

+++智能成像是否适用于HTTPS？ HTTP/2怎么样？

智能成像处理通过HTTP或HTTPS交付的图像。 此外，它还适用于HTTP/2。

+++

+++我是否符合使用智能成像的资格？

智能成像功能可立即供所有客户使用。 若要开始享受它的好处，只需将`bfc=on`、`dpr=on,dprValue`、`network=on`或全部三个参数设置添加到您现有的URL或预设中。

要使用智能成像，贵公司的Dynamic Media Classic或Experience Manager上的Dynamic Media帐户必须将Adobe捆绑的CDN（内容分发网络）作为许可证的一部分提供。

+++

+++为帐户启用智能成像的流程是什么？

要开始使用智能成像，请将`bfc=on`、`dpr=on,dprValue`、`network=on`或全部三个参数设置附加到现有URL或预设。 如果您不想手动进行这些更改，则可以通过创建支持案例来默认启用“智能成像”。

创建支持案例时，请指定要在帐户上激活的智能成像功能：

* 浏览器格式转换（WebP或AVIF）
* 网络带宽优化

>[!NOTE]
>
>DPR需要客户端调整以确定正确的`dprValue`。 因此，Adobe建议通过附加`dpr=on,dprValue`来通过URL启用DPR。

**要创建支持案例以在您的帐户上启用智能成像：**

1. [使用Admin Console开始创建新的支持案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)。
1. 在您的支持案例中提供以下信息：

   * **主要联系人详细信息：**

      * 提供您的姓名、电子邮件和电话号码。

   * **要启用的智能成像功能：**

      * 列出您想要为您的帐户提供的功能：

         * 浏览器格式转换：WebP或AVIF
         * 网络带宽优化
         * DPR： DPR需要客户端调整以确定正确的`dprValue`。 因此，Adobe建议通过附加`dpr=on,dprValue`来通过URL启用DPR。

   * 智能成像的&#x200B;**域：**

      * 列出所有相关域，如&#x200B;*`company.com`*&#x200B;或&#x200B;*`mycompany.scene7.com`*
      * 智能成像支持通用域和自定义域。
      * 要识别您的域，请打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/zh-hans/docs/dynamic-media-classic/using/getting-started/signing-out#getting-started)，然后登录到您的公司帐户。

         1. 导航到&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 常规设置]**。
         1. 查找&#x200B;**[!UICONTROL 发布的服务器名称]**&#x200B;字段以确认您的域。
         1. 验证您使用的是Adobe的CDN，而不是由其他提供商管理的CDN。

   * **指示HTTP/2支持：**

      * 指定是否需要智能成像来处理HTTP/2。

1. 默认情况下，Adobe客户支持会启用所请求的智能成像功能，而无需手动将参数附加到URL。
1. Adobe建议将生存时间(TTL)设置为至少24小时，以通过缓存最大限度地提高性能。
要调整TTL，请执行以下操作：

   1. Dynamic Media Classic的&#x200B;**：**
      1. 导航到&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 发布设置]** > **[!UICONTROL 图像服务器]**。
      1. 将&#x200B;**[!UICONTROL 默认客户端缓存生存时间]**&#x200B;值设置为24小时或更长。
   1. 适用于Adobe Experience Manager上的Dynamic Media的&#x200B;**：**
      1. 按照[这些说明](/help/assets/dm-publish-settings.md#common-thumbnail-attributes-tab)操作。
      1. 将&#x200B;**[!UICONTROL Expiration]**&#x200B;值设置为24小时或更长时间。

+++

+++我何时可以预期帐户启用智能成像？

客户支持按照请求接收顺序处理请求，并遵循等待列表。

>[!NOTE]
>
>由于启用智能成像涉及Adobe清除缓存，因此可能会存在较长的准备时间。 因此，在任何给定时间只能处理少数客户过渡。

+++

+++切换到“智能成像”有何风险？

客户网页没有风险。 但是，过渡到智能成像确实会清除CDN缓存。 此操作涉及在Experience Manager上迁移到Dynamic Media Classic或Dynamic Media的新配置。

在初始过渡期间，未缓存的图像直接点击Adobe的原始服务器，直到再次重建缓存为止。 因此，Adobe计划一次处理几个客户过渡，以便在从源拉取请求时保持可接受的性能。 对于大多数客户，会在1 - 2天内在CDN上再次完全构建缓存。

+++

+++如何验证智能成像是否按预期工作？

1. 为您的帐户配置了智能成像后，在浏览器中加载Dynamic Media Classic或Adobe Experience Manager - Dynamic Media图像URL。
1. 在浏览器中转到&#x200B;**[!UICONTROL 查看]** > **[!UICONTROL 开发人员]** > **[!UICONTROL 开发人员工具]**，打开Chrome开发人员窗格。 或者，选择您选择的任何浏览器开发人员工具。

1. 确保在打开开发人员工具时禁用缓存。

   * 在Windows®上，导航到开发人员工具窗格中的设置，然后选择&#x200B;**[!UICONTROL 禁用缓存（在设备工具打开时）]**&#x200B;复选框。
   * 在macOS上的“开发人员”窗格的&#x200B;**[!UICONTROL 网络]**&#x200B;选项卡下，选择&#x200B;**[!UICONTROL 禁用缓存]**。

1. 请注意，内容类型已转换为相应的格式。 以下屏幕截图显示了在Chrome上动态转换为WebP的PNG图像。 如果您的域启用了AVIF，则内容类型中也会显示AVIF。
1. 在不同的浏览器和用户条件下重复此测试。

>[!NOTE]
>
>并非所有图像都会被转换。 智能成像可决定转换是否可以改善性能。 有时，当没有预期的性能提升或格式不是JPEG或PNG时，不会转换图像。

![image2017-11-14_15398](/help/assets/assets/image2017-11-14_15398.png)

+++

+++如何知道性能提升？ 是否有办法了解智能成像的好处？

智能成像页眉决定了智能成像的优势。 启用智能成像后，在&#x200B;**[!UICONTROL 响应标头]**&#x200B;标题下请求图像后，您可以看到`-X-Adobe-Smart-Imaging`，如以下高亮显示的示例中所示：

![智能成像标头](/help/assets/assets-dm/smart-imaging-header2.png)

此标头可告知您以下内容：

* 智能成像为公司服务。
* 正值表示转换成功。 在这种情况下，将返回新的WebP图像。
* 负值表示转换不成功。 在这种情况下，将返回请求的原始图像(如果未指定，则默认为JPEG)。
* 正值显示请求的图像和新图像之间的字节数差异。 在上面的示例中，保存的字节数为`75048`，即一个图像的大约75 KB。
* 负值表示所请求的图像小于新图像。 虽然显示的是负大小差异，但提供的图像只是请求的原始图像。

>[!NOTE]
>
>**X-Adobe-Smart-Imaging = -1，正在传递WebP**
>
>如果`X-Adobe-Smart-Imaging`的值为–1且仍在传递WebP，则智能成像处于活动状态。 但是，由于缓存已过时，未计算大小优势。 您可以在图像的URL中使用`cache=update`（仅限一次）来解决此问题。
>&#x200B;>使用修饰符的示例：
>&#x200B;>`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`
>&#x200B;>要使整个缓存失效，必须创建支持案例。

+++

+++如何在智能成像中禁用AVIF优化？

如果您希望切换回默认提供WebP，请为它创建支持案例。 与往常一样，可以通过将参数`bfc=off`添加到图像的URL来关闭智能成像。 但是，您不能在用于智能成像的URL修饰符中选择WebP或AVIF。 该功能在您的公司帐户级别进行维护。

+++

+++智能成像是否可以因任何请求而关闭？

是。您可以通过添加以下任何修饰符来关闭智能成像：

* `bfc=off`以关闭浏览器格式转换。 另请参阅[浏览器格式转换](#bfc)。
* `dpr=off`以关闭设备像素比。 另请参阅[设备像素比](#dpr)。
* `network=off`以关闭网络带宽。 另请参阅[网络带宽](#network)。

+++

+++有哪些“调整”可用？ 是否可以定义任何设置或行为？

“智能成像”有三个选项，您可以启用或禁用。

* [浏览器格式转换](#bfc)
* [设备像素比](#dpr)
* [网络带宽](#network)

+++

+++我在Chrome Web浏览器上有一个带fmt=tif的URL。 但我的请求失败，并出现ImageServer错误。 为什么？

如果您的帐户未启用智能成像，则不会发生此错误。 智能成像仅适用于JPEG或PNG格式。

要避免此错误，您可以：

* 指定JPEG或PNG，或
* 根本不使用`fmt`修饰符，或
* 使用由智能成像定义的浏览器首选格式。 例如，您可以将WebP用于Chrome Web浏览器。

+++

+++我想从图像的URL下载TIFF图像。 我该怎么做？

将`fmt=tif`和`bfc=off`添加到图像的URL路径。

+++

+++智能成像是只管理图像格式，还是同时管理图像质量设置以获得最佳结果？

智能成像同时使用格式和质量。 如果收到图像URL中的请求，其余参数将保持不变。

+++

+++如果智能成像确实可以管理质量设置，是否可以设置最小值和最大值？ 换句话说，一个不小于60且不大于80的品质？

目前没有此类配置。

+++

+++智能成像是自动调整百分比质量输出设置，还是手动调整且适用于所有图像的设置？ 在什么范围内？

智能成像可自动调整质量百分比。 此质量使用Adobe开发的机器学习算法来确定。 此百分比不特定于范围。

+++

+++对于智能成像，支持或忽略哪些图像提供命令？

唯一被忽略的命令是`fmt`和`qlt`。 支持所有其余命令。

+++

+++只有JPEG图像会被智能成像替换吗？ 如果我请求WebP、PNG或其他什么怎么办？

此功能仅适用于JPEG和PNG。

+++

+++为何JPEG图像有时会返回到Chrome而不是WebP？

智能成像可确定转换是否有效。 它只返回转换有利的新图像。

+++

+++为什么设备像素比(dpr)功能无法按预期用于复合图像？

如果复合图像涉及太多图层，则在使用position修饰符时，dpr功能可能会受到影响。 此问题已知，应在未来版本的智能成像中修复。 如果其他智能成像功能无法按预期工作，您可以创建支持案例以报告问题。

+++

+++为什么智能成像PNG仍会转换为无损WebP/AVIF？

由于PNG是一种无损格式，因此传送的早期WebP和AVIF是无损的，从而导致比预期更大的大小。 智能成像现在支持有损转换。 您可以在图像请求中使用修饰符`cache=update`（仅限一次）来修复此问题。 使用此修饰符的示例：

`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`

要使整个缓存失效，您必须创建一个请求此类工作的支持案例。

+++

+++如何在智能成像中继续使用PNG无损转换？

智能成像现在支持基于质量级别的有损转换。 您可以通过公司的设置将质量设置为100，或者通过将`qlt=100`添加到图像的URL路径来继续使用无损转换。

+++

