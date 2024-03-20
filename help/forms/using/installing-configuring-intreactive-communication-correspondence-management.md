---
title: 安装和配置交互式通信
description: 安装和配置AEM Forms交互式通信以创建业务信函、文档、报表、福利通知、营销邮件、账单和欢迎工具包。
topic-tags: installing
docset: aem65
role: Admin
exl-id: 37fcfad9-2f84-4f0c-aed8-e4a5a3303a06
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1383'
ht-degree: 1%

---

# 安装和配置交互式通信{#install-and-configure-interactive-communications}

## 简介 {#introduction}

AEM Form能够集中创建、汇编、管理和提交安全的交互式文档，如商业信函、文档、对帐单、福利通知、市场营销邮件、账单和欢迎资料包。 此功能称为交互式通信。 此功能包含在AEM Forms附加组件包中。 附加组件包部署在AEM的创作或发布实例上。

您可以使用交互式通信功能以多种格式生成通信。 例如，Web和PDF。 您可以将交互式通信与AEM Workflow集成在一起，通过客户选择的渠道处理和交付组合通信。 例如，通过电子邮件向最终用户发送通信。

如果您从以前的版本进行升级，并且已经在通信管理方面进行了投资，则可以安装 [兼容包](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package) 以继续使用通信管理。 有关交互式通信与通信管理之间区别的信息，请参阅 [交互式通信概述](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management).

AEM Forms是一个功能强大的企业级平台。 交互式通信只是AEM Forms的功能之一。 有关权能的完整列表，请参见 [AEM Forms简介](../../forms/using/introduction-aem-forms.md).

## 部署拓扑 {#deployment-topology}

AEM Forms附加组件包是部署在AEM上的应用程序。 您只需要至少一个AEM创作和处理实例即可运行交互式通信功能。 以下拓扑是指示性拓扑，用于在OSGi功能上运行AEM Forms交互式通信、通信管理、AEM Forms数据捕获和以Forms为中心的工作流。 有关拓扑的详细信息，请参见 [AEM Forms的架构和部署拓扑](/help/forms/using/aem-forms-architecture-deployment.md).

![推荐拓扑](assets/recommended-topology.png)

AEM Forms Interactive Communications在AEM Forms的创作实例上运行管理、创作和代理用户界面。 发布实例托管交互式通信的最终版本，可供最终用户使用。

## 系统要求 {#system-requirements}

在开始安装和配置AEM Forms的交互式通信和通信管理功能之前，请确保：

* 硬件和软件基础架构已准备就绪。 有关支持的硬件和软件的详细列表，请参阅 [技术要求](/help/sites-deploying/technical-requirements.md).

* AEM实例的安装路径不包含空格。
* AEM实例已启动并正在运行。 在AEM术语中，“实例”是在创作或发布模式下在服务器上运行的AEM的副本。 您需要至少一个AEM实例（创作或处理）才能运行AEM Forms交互式通信和通信管理功能：

   * **作者**：用于创建、上载和编辑内容以及管理网站的AEM实例。 内容准备好上线后，即会复制到发布实例。
   * **正在处理：** 处理实例是 [强化的AEM Author](/help/forms/using/hardening-securing-aem-forms-environment.md) 实例。 您可以设置“创作”实例，并在执行安装后进行强化。

   * **Publish**：AEM实例，通过Internet或内部网络向公众提供已发布的内容。

* 满足内存要求。 AEM Forms插件包需要：

   * 15 GB 的临时空间，用于基于 Microsoft® Windows 的安装。
   * 用于基于UNIX的安装的6 GB临时空间。

* 基于UNIX的系统的额外要求：如果您使用的是基于UNIX的操作系统，请从相应操作系统的安装媒体安装以下软件包。

<table>
 <tbody>
  <tr>
   <td>外派人员</td>
   <td>libxcb</td>
   <td>自由类型</td>
   <td>libXau</td>
  </tr>
  <tr>
   <td>libSM</td>
   <td>兹利布</td>
   <td>libICE</td>
   <td>libuuid</td>
  </tr>
  <tr>
   <td>glibc</td>
   <td>libXext</td>
   <td><p>nss-softokn-freebl</p> </td>
   <td>fontconfig</td>
  </tr>
  <tr>
   <td>libX11</td>
   <td>libXrender</td>
   <td>libXrandr</td>
   <td>libXinerama</td>
  </tr>
 </tbody>
</table>

## 安装AEM Forms附加组件包 {#install-aem-forms-add-on-package}

AEM Forms附加组件包是部署在AEM上的应用程序。 该软件包包含AEM Forms交互式通信、通信管理和其他功能。 执行以下步骤以安装附加组件包：

1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
1. 选择 **[!UICONTROL 标题菜单中的 Adobe Experience Manager]** 。
1. **[!UICONTROL 在“筛选器]**”部分中：
   1. 从“解决方案&#x200B;]**”下拉列表中选择**[!UICONTROL “表单&#x200B;]**”。**[!UICONTROL 
   2. 选择包的版本和类型。 您还可以使用“ **[!UICONTROL 搜索下载]** ”选项来筛选结果。
1. 选择适用于您的操作系统的包名称，然后选择 **[!UICONTROL 接受EULA条款]**，并选择 **[!UICONTROL 下载]**.
1. 打开[程序包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)并单击“上传程序包&#x200B;]**”**[!UICONTROL &#x200B;以上传程序包。
1. 选择程序包，然后单击“安装&#x200B;]**”。**[!UICONTROL 

   您还可以通过AEM [Forms版本](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en) 文章中列出的直接链接下载包。

1. 安装包后，系统会提示您重新启动 AEM 实例。 **不要立即重新启动服务器。** 在停止 AEM Forms Server 之前，请等待 ServiceEvent REGISTERED 和 ServiceEvent UNREGISTERED 消息停止显示在 [AEM-Installation-Directory]/crx-quickstart/logs/error.log 文件中，并且日志稳定。

   >[!NOTE]
   >
   > 建议使用“Ctrl + C”命令重新启动SDK。 使用替代方法（例如，停止Java进程）重新启动AEM SDK可能会导致AEM开发环境不一致。

1. 对所有创作实例和发布实例重复步骤1-7。

## 安装后配置 {#post-installation-configurations}

AEM Forms具有一些强制和可选配置。 强制配置包括配置BouncyCastle库和序列化代理。 可选配置包括配置Dispatcher和Adobe Target。

### 强制性安装后配置 {#mandatory-post-installation-configurations}

#### 配置RSA和BouncyCastle库  {#configure-rsa-and-bouncycastle-libraries}

在所有Author和Publish实例上执行以下步骤以引导委派库：

1. 停止基础AEM实例。
1. 打开 [AEM安装目录]\crx-quickstart\conf\sling.properties文件进行编辑。

   如果您使用 [AEM安装目录]\crx-quickstart\bin\start.bat以启动AEM，然后编辑位于的sling.properties [AEM_root]\crx-quickstart\。

1. 将以下属性添加到sling.properties文件：

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. 保存并关闭文件，然后启动AEM实例。
1. 对所有创作实例和发布实例重复步骤1-4。

#### 配置序列化代理 {#configure-the-serialization-agent}

列入允许列表对所有Author和Publish实例执行以下步骤，将包添加到中：

1. 在浏览器窗口中打开AEM Configuration Manager。 默认URL为https://&#39;[服务器]：[端口]&#39;/system/console/configMgr.
1. 搜索并打开 **反序列化防火墙配置**.
1. 添加 **sun.util.calendar** 打包到 **允许列表** 字段。 单击“保存”。
1. 对所有创作实例和发布实例重复步骤1-3。

### 可选安装后配置 {#optional-post-installation-configurations}

#### 安装兼容包 {#install-compatibility-package}

在AEM 6.5 Forms中创建客户通信的默认和推荐方法是交互式通信。 如果您已从以前的版本升级或迁移，并计划继续使用信件（通信管理），请安装 [AEMFD兼容包](https://experienceleague.adobe.com/docs/experience-manager-65/forms/upgrade-aem-forms/aem-forms-osgi-upgrade/compatibility-package.html?lang=en).

通过AEMFD兼容包，您可以使用AEM 6.5 Forms上AEM 6.4 Forms、AEM 6.3 Forms和AEM 6.2 Forms中的以下资源：

* 文档片段
* 书信
* 数据字典
* 自适应表单弃用的模板和页面

#### 配置Dispatch {#configure-dispatcher}

Dispatcher是Adobe Experience Manager的缓存和负载平衡工具，与企业级Web服务器一起使用。 如果您使用 [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hans)，然后为AEM Forms执行以下配置：

1. 配置AEM Forms的访问权限：

   打开dispatcher.any文件进行编辑。 导航到过滤器部分，并将以下过滤器添加到过滤器部分：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   保存并关闭文件。 有关过滤器的详细信息，请参阅 [Dispatcher文档](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hans).

1. 配置反向链接筛选服务：

   以管理员身份登录Apache Felix配置管理器。 配置管理器的默认URL为https://&#39;server&#39; ：[端口号]/system/console/configMgr。 在 **配置** 菜单，选择 **Apache Sling引用过滤器** 选项。 在允许主机字段中，输入Dispatcher的主机名以允许其作为反向链接，然后单击 **保存**. 条目的格式为https://&#39;[服务器]：[端口]’。

#### 集成Adobe Target {#integrate-adobe-target}

如果交互式通信提供的体验不吸引人，您的客户可能会放弃交互式通信。 虽然这令客户感到沮丧，但也提高了贵组织的支持量和成本。 确定并提供提高转化率的正确客户体验是关键而富有挑战性的。 AEM forms拥有解决此问题的关键。

AEM forms与Adobe Experience Cloud解决方案Adobe Target集成，跨多个数字渠道提供个性化且引人入胜的客户体验。 要使用Adobe Target使交互式通信个性化， [将Adobe Target与AEM Forms集成](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

#### 为表单数据模型配置SSL通信  {#configure-ssl-communcation-for-form-data-model}

您可以为表单数据模型启用SSL通信。 要为表单数据模型启用SSL通信，请在启动任何AEM Forms实例之前，向所有实例的Java™信任存储区添加证书。 您可以运行以下命令来添加证书：

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## 后续步骤 {#next-steps}

您已将环境配置为使用交互式通信和通信管理功能。 现在，使用该功能的步骤如下：

* [通信管理概述](/help/forms/using/interactive-communications-overview.md)

* [创建交互式通信](../../forms/using/create-interactive-communication.md)

* [创建通信管理信函](../../forms/using/create-letter.md)
