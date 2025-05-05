---
title: 缓解AEM Forms on JEE的Spring Framework漏洞
description: 缓解AEM Forms on JEE的Spring Framework漏洞
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 61cce7cd8290156bec6dcc351a59093f545a4ec7
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 1%

---


# 缓解JEE上AEM Forms的Spring Framework漏洞

本文档提供了有关解决影响JEE上AEM Forms的两个关键Spring Framework漏洞的指南：

- **[CVE-2024-38819](https://spring.io/security/cve-2024-38819)**：功能Web框架中存在路径遍历漏洞
- **[CVE-2024-38820](https://spring.io/security/cve-2024-38820)**： Spring Framework DataBinder区分大小写匹配异常

## 受影响的版本

- JEE上的Adobe Experience Manager 6.5 Forms
- 将AEM 6.5 Forms GA版本更改为6.5.22.0

## 解决方法

### 特定于版本的解决方案

| AEM Forms 版本 | 必需操作 |
|-------------------|-----------------|
| 6.5.22.0 | 1. [下载适用于您环境的修补程序](/help/release-notes/aem-forms-hotfix.md)。 </br> 2. 要安装此修补程序，请按照说明[在JEE](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)上的AEM表单上安装Service Pack。 |
| 6.5.17.0 - 6.5.21.0 | [应用手动缓解步骤](#manual-mitigation-steps)。 |
| 6.5 - 6.5.16.0 | 1. [安装最新的Service Pack](/help/release-notes/release-notes.md)<br>2。 [根据您的更新版本实施适当的解决方案](#version-specific-solutions)。 |

> **注意**： AEM Forms正式仅支持最新的六个服务包。 旧版本的用户应首先升级到最新的Service Pack，然后安装所需的修补程序。

## 部署注意事项

### 对于群集环境

使用群集部署时：

- 在群集中的&#x200B;**所有节点**&#x200B;上应用JAR文件替换(步骤#4)
- 通过在所有服务器中使用相同的JAR版本来维护一致性
- 在启动任何服务重新启动之前，完成所有节点的更新
- 实施协调的重启策略以最大限度地减少系统停机时间

### 对于单节点环境

使用独立部署时：

- 由于没有要管理的定位器服务器，因此请遵循简化的流程
- 省略与定位器服务器配置或启动相关的任何步骤
- 按照说明完成所有其他步骤，特别是JAR替换和清单更新
- 实施所有更改后重新启动应用程序服务器

## 手动缓解步骤

1. 停止应用程序服务器。
1. 停止和定位服务器。
1. 从核心EAR中删除Spring JAR：
   1. 导航到 `[Adobe_Experience_Manager_Forms installation directory]/deploy`。
   1. 使用存档管理器工具打开`adobe-core-<appserver>.ear`文件。 其中`<appserver>`可以是JBoss、WebLogic或WebSphere，具体取决于您的环境：
   - **对于JBoss：**&#x200B;导航到`ear/lib`文件夹并删除以下JAR文件：
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

   - **对于WebLogic或WebSphere：**&#x200B;从EAR的根目录中删除以下JAR文件：
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

   - **对于所有应用程序服务器：**&#x200B;在`adobe-core-<appserver>.ear`的根级别，打开`adobe-dscf.jar`文件并编辑`META-INF/MANIFEST.MF`文件以删除对以下JAR文件的任何引用：
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

1. 替换Geode分发中的JAR文件：
   1. 导航到`<Adobe_Experience_Manager_Forms>/lib/caching/lib`
   1. 将现有JAR文件替换为更新版本：
   - `spring-context-<version>.jar` → `spring-context-6.1.14.jar`
   - `spring-beans-<version>.jar` → `spring-beans-6.1.14.jar`
   - `spring-core-<version>.jar` → `spring-core-6.1.14.jar`
   - `spring-jcl-<version>.jar` → `spring-jcl-6.1.14.jar`
   - `spring-web-<version>.jar` → `spring-web-6.1.14.jar`

   要获取较新的JAR文件，请从[Adobe软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/spring-6.1.14-jars.zip)下载spring-6.1.14-jars.zip文件，并解压缩ZIP文件以访问更新的Spring framework JAR文件。

   1. 更新以下JAR文件中的MANIFEST.MF文件：
   - `geode-server-all-<version>.jar`
   - `gfsh-dependencies.jar`

   对于每个JAR：
   - 使用归档文件管理器工具打开JAR
   - 找到并提取`META-INF/MANIFEST.MF`文件
   - 在文本编辑器中编辑MANIFEST.MF文件
   - 找到“Class-Path”部分，并更新所有Spring框架引用：
      - `spring-core-<version>.jar`至`spring-core-6.1.14.jar`
      - `spring-web-<version>.jar`至`spring-web-6.1.14.jar`
      - `spring-context-<version>.jar`至`spring-context-6.1.14.jar`
      - `spring-beans-<version>.jar`至`spring-beans-6.1.14.jar`
      - `spring-jcl-<version>.jar`至`spring-jcl-6.1.14.jar`
   - 保存修改的MANIFEST.MF文件
   - 将JAR中的原始MANIFEST.MF替换为更新版本
   - 保存JAR文件

   1. 需要注意的常见问题：
      - 确保清单中没有重复条目
      - 维护正确的行结尾
      - 验证指定位置中存在所有引用的JAR

   1. 验证步骤：
      - 检查清单是否已正确更新
      - 验证是否正确引用了所有弹簧依赖项
      - 确保没有保留旧版本引用
      - 测试应用程序以确认没有类加载问题

1. 运行Configuration Manager。

1. 重新启动服务器：
   - 使用JDK 17启动定位器服务器
   - 使用以前使用的相同JDK版本（JDK 8或JDK 11）启动应用程序服务器。
