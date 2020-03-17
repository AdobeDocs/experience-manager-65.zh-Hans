---
title: 已知问题
description: Adobe Experience Manager 6.5的特定已知问题发行说明
uuid: 8fbdb167-833a-4179-aad1-0a26a4e5b3a7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: d11fc727-f23a-4cde-9fa6-97e2c81b4ad0
docset: aem65
translation-type: tm+mt
source-git-commit: 86dbd52d44a78401aa50cce299850469c51b691c

---


# 已知问题 {#known-issues}

此页面列出了于 2019 年 4 月发布的 Adobe Experience Manager 6.5 中存在的已知问题列表。

如果您需要了解有关已知问题的更多信息，请[联系支持人员](https://helpx.adobe.com/support/experience-manager.html)。

## 平台 {#platform}

* 将报告删除CRX快速启动及其内容的问题。

   对于每个操作，请确保属性“*htmllibmanager.fileSystemOutputCacheLocation*”从不为空字符串：

   1. 调用“*/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true*”。
   2. 升级到AEM 6.5。
   3. 在AEM 6.5上执行“延迟内容迁移”。
   有一 [篇知识库文章](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) ，其中包含更多详细信息以及此问题的解决方法。

* 如果将JDK 11与AEM 6.5实例一起使用，则部署某些包后，某些页面可能显示为空。 日志文件中显示以下错误消息：

   ```
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

要解决此错误，请执行以下操作：

1. 停止AEM实例。 转到并 `<aem_server_path_on_server>crx-quickstart\conf` 打开文 `sling.properties` 件。 Adobe建议备份此文件。

2. 搜索 `org.osgi.framework.bootdelegation=`. 添加 `jdk.internal.reflect,jdk.internal.reflect.*` 属性以将结果显示为：

   ```
   org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
   ```

3. 保存文件并重新启动AEM实例。

## 资产 {#assets}

* **搜索：** 如果搜索字符串包含前导空格，则搜索不会产生任何返回([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **文件夹元数据架构**：添加选择按钮后，ID 和值字段未按预期呈现，且删除功能不起作用。(CQ-4261144)
* 重命名资产时，无法在资产名称中使用空格。(CQ-4266403)

## Forms {#forms}

* 在 Linux 操作系统上安装 AEM Forms 时，带有硬件安全模块的数字签名不起作用。(CQ-4266721)
* （仅限 WebSphere 上的 AEM Forms）如果您将&#x200B;**用户名**&#x200B;作为搜索条件搜索&#x200B;**管理员**，则 **Forms 工作流** > **任务搜索**&#x200B;选项不会返回任何结果。(CQ-4266457)

* AEM Forms 无法将使用 JPEG 压缩的 .tif 和 .tiff 文件转换为 PDF 文档。(CQ-4265972)
* **AEM Forms 迁移**&#x200B;页面上的 **AEM Forms 资产扫描程序**&#x200B;和&#x200B;**交互式通信迁移字符**&#x200B;选项不起作用。(CQ-4266572)

* （仅限JBoss 7）从先前版本升级到AEM 6.5 Forms，而先前版本具有创建和使用默认提交或默认渲染进程副本的进程(.lca)时，使用此类进程(.lca)的HTML5 Forms将无法执行所需的操作。 (CQ-4243928)
* 在自适应表单中，当从规则编辑器调用表单数据模型服务以动态更新图像选项组件的值时，不会更新图像选项组件的值。(CQ-4254754)
* AEM Forms Designer installer requires the 32-bit version of [Visual C++ redistributable runtime package 2012](https://support.microsoft.com/en-in/help/2977003/the-latest-supported-visual-c-downloads) and [Visual C++ redistributable runtime packages 2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). 确保在开始安装之前已安装上述可再发行运行时包。(CQ-4265668)

* 当自适应表单配置为动态更新组件的值并且通过调度程序访问托管表单的发布实例时，动态更新字段值的功能将停止工作。要解决此问题，请在发布实例上打开 CRXDE，导航到 /libs/fd/af/runtime/clientlibs/guideChartReducer，然后创建下面列出的属性。

   * 名称：allowProxy
   * 类型：布尔型
   * 值：true
   * 受保护：False
   * 必填：False
   * 多选：False
   * 已自动创建：False

该属性让运行时文件夹下的客户端库可以访问代理。(CQ-4268679)

