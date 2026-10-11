---
title: 视频演绎版
description: 了解如何使用Adobe Experience Manager Assets为各种格式（包括OGG、FLV等）的视频资源生成视频演绎版。
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
exl-id: a644558e-5be9-4ba2-b560-fc300497fbdf
solution: Experience Manager, Experience Manager Assets
feature: Video
role: User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: d4b6216b-4a89-4ff0-8ac0-5a699ba23100
    internal-label: Images and videos
subfeature_v2:
  - id: cb04d42d-1b70-43b0-9951-45998eb6e842
    internal-label: Video
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 3%
---
# 视频演绎版 {#video-renditions}

Adobe Experience Manager Assets为各种格式（包括OGG、FLV等）的视频资源生成视频演绎版。

Experience Manager Assets支持Media Assets的静态和动态呈现（DM编码的呈现）。

使用FFMPEG（安装在系统路径上并可用）原生生成静态演绎版，并将其存储在内容存储库中。

DM编码的演绎版存储在代理服务器中，并在运行时提供服务。

Experience Manager Assets在客户端为这些演绎版提供播放支持。

要查看特定视频资源的演绎版，请打开其资源页面，然后选择全局导航图标。 然后，从列表中选择&#x200B;**[!UICONTROL 呈现版本]**。

![chlimage_1-478](assets/chlimage_1-478.png)

视频演绎版列表显示在&#x200B;**[!UICONTROL 演绎版]**&#x200B;面板中。

![chlimage_1-479](assets/chlimage_1-479.png)

若要为DM编码的呈现配置代理服务器，[配置Dynamic Media云服务](config-dynamic.md)。

若要使用所需的参数生成视频演绎版，[请创建对应的视频配置文件](video-profiles.md)。

配置代理服务器并创建视频配置文件后，您可以在处理配置文件中包含此视频预设，并将处理配置文件应用到文件夹。

>[!NOTE]
>
>音频播放不适用于® Internet Explorer 11上的OGG和WAV文件。 对于扩展名为OGG或WAV的资源，资源详细信息页面上会显示错误`Invalid Source`。
>
>在MS® Edge和iPad上，OGG文件不会播放并引发不支持的格式错误。
