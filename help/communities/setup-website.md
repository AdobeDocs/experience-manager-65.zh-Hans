---
title: 设置网站结构
seo-title: 设置网站结构
description: 设置目录
seo-description: 设置目录
uuid: a31edcd5-dab8-4a42-953b-1d076c2182b2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d18c0ece-4c4f-499c-ac94-a9aaa7f883c4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 设置网站结构 {#setup-website-structure}

要设置网站，以下说明将说明要在以下位置创建的文件夹：

* `/apps/an-scf-sandbox`
这是自定义应用程序和模板所在的位置

* `/etc/designs/an-scf-sandbox`
这是可下载的设计元素所在的位置

* `/content/an-scf-sandbox`
这是可下载网页所在的位置

本教程中的代码将依赖于应用程序、设计和内容的主文件夹名称相同。 如果您为网站选择了其他名称，则始终用您 `an-scf-sandbox` 选择的名称替换。

>[!NOTE]
>
>关于名称：
>
>* 在CRXDE中看到的名称是构成可寻址内容路径的节点名称
>* 节点名称可能包含空格，但在URI中使用时，必须将空格编码为“%20”或“+”
>* 节点名称可能包含连字符和下划线，但是当在Java文件中作为包名称引用时，必须对它们进行编码。 连字符和下划线都以下划线转义，后跟它们的Unicode值：
   >
   >  
* 连字符变为&#39;_002d&#39;
>  * 下划线变为&#39;_005f&#39;


## 设置应用程序目录(/apps) {#setup-the-application-directory-apps}

存储库中的/apps目录包含用于实现/content目录中提供的页面的行为和呈现的代码。

/apps目录受保护，且不可公开访问，与/content和/etc/designs目录一样。

1. Create `/apps/an-scf-sandbox` folder.

   使用 **[!UICONTROL CRXDE Lite]**，在资源管理器窗格中

   1. 选择文件 `/apps` 夹
   1. **[!UICONTROL 右键单击]**&#x200B;创建&#x200B;**[!UICONTROL ...或下拉“创]**&#x200B;建……”菜单
   1. **[!UICONTROL 选择]**&#x200B;创建文件夹…….
   1. 在“创建 **[!UICONTROL 文件夹]** ”对话框中，输入 `an-scf-sandbox`
   1. Click **[!UICONTROL OK]**

1. 创建 **[!UICONTROL 组件]** 子文件夹。

   1. 选择文件 `/apps/an-scf-sandbox` 夹
   1. 单击“ **[!UICONTROL 创建”>“创建文件夹”]**
   1. 在创建文 **[!UICONTROL 件夹对话框]** ，输入组 **[!UICONTROL 件]**
   1. Click **[!UICONTROL OK]**

1. 创建 **模板&#x200B;**子文件夹。

   1. 选择文件 `/apps/an-scf-sandbox` 夹
   1. 单击“ **[!UICONTROL 创建”>“创建文件夹”]**
   1. 在“创建 **[!UICONTROL 文件夹]** ”对话框中，输 **[!UICONTROL 入模板]**
   1. Click **[!UICONTROL OK]**
   1. 重新选择 `/apps/an-scf-sandbox`
   1. 选择 **[!UICONTROL 全部保存]**
   与任何编辑过程一样，经常进行保存。 如果您在输入数据时遇到问题，可能是因为登录超时，或者您需要保存以前所做的编辑。

1. CRXDE Lite的资源管理器窗格中的结构现在应类似于：

   ![chlimage_1-44](assets/chlimage_1-44.png)

## 设置设计目录(/etc/designs) {#setup-the-design-directory-etc-designs}

/etc/designs目录包含要与页面内容一起下载的图像、脚本和样式表。

1. 要在经典UI中使用设计器工具，请浏 [览至https://&lt;server>:&lt;port>/miscadmin](http://localhost:4502/miscadmin)。

   注意：如果使用CRXDE lite创建类型为“节点”的节点， `cq:Page`则“访问控制”和“复制”不会设置为页面的默认设置。

1. 在资源管理器窗格中，选择“ **[!UICONTROL Designs]** ”文件夹，然后单 **[!UICONTROL 击“New”（新建）> “New Page]**”（新建页面）。

   输入：

   * 标题：SCF **沙箱**
   * 名称： **an-scf沙箱**
   * 选择 **设计页面模板**
   Click **[!UICONTROL Create]**

   ![chlimage_1-45](assets/chlimage_1-45.png)

1. 如果未显示“SCF沙箱”文件夹，请刷新资源管理器窗格。

1. 返回CRXDE Lite(http:// localhost:4502/crx/de)并展开/etc/designs以查看名为“an-scf-sandbox”的节点。

   在CRXDE的右侧下方窗格中，您可以查看“属性”选项卡、“访问控制”选项卡和“复制”选项卡，以查看使用“设计页面模板”定义的内容。

   ![chlimage_1-46](assets/chlimage_1-46.png)

## 设置内容目录（/内容） {#setup-the-content-directory-content}

存储库中的/content目录是网站内容所在的位置。 /content下的路径包括浏览器请求的URL路径。

*在将页* 面模板创建为初始应用程序的一部分后 [](initial-app.md#createthepagetemplate) ，可以基于模板创建初始页面内容……. [**⇒**](initial-app.md)