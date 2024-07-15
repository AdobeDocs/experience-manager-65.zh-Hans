---
title: 缓解AEM中的序列化问题
description: 了解如何减轻AEM中的序列化问题。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 01e9ab67-15e2-4bc4-9b8f-0c84bcd56862
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# 缓解AEM中的序列化问题{#mitigating-serialization-issues-in-aem}

## 概述 {#overview}

Adobe的AEM团队与开源项目[NotSoSerial](https://github.com/kantega/notsoserial)密切合作，帮助缓解&#x200B;**CVE-2015-7501**&#x200B;中描述的漏洞。 NotSoSerial是根据[Apache 2许可证](https://www.apache.org/licenses/LICENSE-2.0)授予许可的，并且包括根据自己的[类似BSD的许可证](https://asm.ow2.io/)授予许可的ASM代码。

此包中包含的代理jar是Adobe修改过的NotSoSerial分发。

NotSoSerial是针对Java™级别问题的Java™级别解决方案，并非特定于AEM。 它会向试图反序列化对象的操作添加预检检查。 此检查针对防火墙样式的允许列表列入阻止列表和/或测试类名。 由于默认阻止列表中的类数量有限，此测试不太可能对您的系统或代码产生影响。

默认情况下，代理会针对当前已知的易受攻击的类执行阻止列表检查。 此阻止列表旨在保护您免受目前使用此类漏洞的漏洞的攻击。

可以按照本文的[配置代理](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent)部分中的说明配置阻止列表列入允许列表和。

该代理旨在帮助缓解最新已知的易受攻击的类别。 如果您的项目正在反序列化不受信任的数据，则它仍可能容易受到拒绝服务攻击、内存不足攻击和未知的未来反序列化攻击。

Adobe正式支持Java™ 6、7和8。 但是，Adobe的理解是NotSoSerial也支持Java™ 5。

## 安装代理 {#installing-the-agent}

>[!NOTE]
>
>如果以前安装过AEM 6.1的序列化修补程序，请从Java™运行行中删除代理启动命令。

1. 安装&#x200B;**com.adobe.cq.cq-serialization-tester**&#x200B;包。

1. 转到位于`https://server:port/system/console/bundles`的捆绑包Web控制台
1. 查找并启动序列化包。 这样做会动态自动加载NotSoSerial代理。

## 在应用程序服务器上安装代理 {#installing-the-agent-on-application-servers}

NotSoSerial代理未包含在应用程序服务器的AEM的标准分发中。 但是，您可以从AEM jar分发中提取它，并将其用于应用程序服务器设置：

1. 首先，下载AEM快速入门文件并将其解压缩：

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. 转到新解压缩的AEM快速入门的位置，并将`crx-quickstart/opt/notsoserial/`文件夹复制到AEM Application Server安装的`crx-quickstart`文件夹。

1. 将`/opt`的所有权更改为运行服务器的用户：

   ```shell
   chown -R opt <user running the server>
   ```

1. 按照本文以下部分所示，配置并检查代理是否已正确激活。

## 配置代理 {#configuring-the-agent}

对于大多数安装，默认配置已足够。 此配置包括已知远程运行易受攻击的类的阻止列表列入允许列表和信任数据的反序列化安全的包。

防火墙配置是动态的，可以随时更改：

1. 转到位于`https://server:port/system/console/configMgr`的Web控制台
1. 正在搜索并单击&#x200B;**反序列化防火墙配置。**

   >[!NOTE]
   >
   >您还可以通过访问位于以下位置的URL直接访问配置页面：
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`

此配置包含允许列表 列入阻止列表、序列化和反序列化日志记录。

**允许列表**

在允许列表部分中，这些列表是允许反序列化的类或包前缀。 如果要将自己的类反序列化，请将类或包添加到此允许列表中。

**阻止列表**

在块列表部分中，是不允许进行反序列化的类。 这些类的初始集仅限于已发现易受远程执行攻击的类。 在任何允许列出的条目之前应用阻止列表。

**诊断日志记录**

在诊断日志记录部分中，您可以选择多个选项，以便在进行反序列化时进行记录。 这些选项仅在首次使用时登录，在后续使用时不再登录。

默认值&#x200B;**class-name-only**&#x200B;通知您正在反序列化的类。

您还可以设置&#x200B;**全栈栈**&#x200B;选项，该选项记录第一次反序列化尝试的Java™栈栈，以通知您正在执行反序列化的位置。 此选项对于在使用中查找和删除反序列化很有用。

## 验证代理的激活 {#verifying-the-agent-s-activation}

您可以通过浏览到以下URL来验证反序列化代理的配置：

* `https://server:port/system/console/healthcheck?tags=deserialization`

访问URL后，将显示与代理相关的运行状况检查列表。 您可以通过验证是否通过运行状况检查来确定是否正确激活了代理。 如果失败，则必须手动加载代理。

有关对代理问题进行故障排除的详细信息，请参阅下面的[处理动态代理加载错误](#handling-errors-with-dynamic-agent-loading)。

>[!NOTE]
>
>如果将`org.apache.commons.collections.functors`添加到允许列表，运行状况检查将始终失败。

## 处理动态代理加载的错误 {#handling-errors-with-dynamic-agent-loading}

如果日志中显示错误，或者验证步骤检测到加载代理时出现问题，请手动加载代理。 如果您使用JRE (Java™ Runtime Environment)而不是JDK (Java™ Development Toolkit)，则也建议使用此工作流，因为用于动态加载的工具不可用。

要手动加载代理，请执行以下操作：

1. 编辑CQ jar的JVM启动参数，并添加以下选项：

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >还需要使用 — nofork CQ/AEM选项以及相应的JVM内存设置，因为未在分支JVM上启用代理。

   >[!NOTE]
   >
   >在AEM安装的`crx-quickstart/opt/notsoserial/`文件夹中可以找到NotSoSerial代理jar的Adobe分发。

1. 停止并重新启动JVM；

1. 请按照[验证代理的激活](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation)中所述步骤再次验证代理的激活。

## 其他注意事项 {#other-considerations}

如果您在IBM® JVM上运行，请查看有关对[此位置](https://www.ibm.com/docs/en/sdk-java-technology/8?topic=documentation-java-attach-api)的Java™附加API支持的文档。
