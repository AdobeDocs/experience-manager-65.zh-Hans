---
title: 缓解JEE上Experience Manager Forms的Struts 2漏洞
description: 缓解JEE上Experience Manager Forms的Struts 2漏洞
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 73b5aff2-1320-4d9a-8972-54c4fdd3a2c2
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 1%

---

# 缓解Experience Manager Forms的Struts 2漏洞 {#mitigatin-struts2-rce-vulnerabilities-for-aem-forms}

## 问题

Struts 2是一种用于开发Java EE Web应用程序的流行开放源码Web应用程序框架，已报告了该框架存在的严重安全漏洞。 已分析以下漏洞：

| 漏洞 | 受影响的内容？ | 哪些内容未受影响？ |
|---|---|---|
| [CVE-2023-50164](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2023-50164) | JEE上的Experience Manager6.5 Forms（从6.5 GA到6.5.19.0的所有版本） | <ul><li> Experience Manager Forms Workbench（所有版本）</li> <li> OSGi上的Experience Manager Forms（所有版本） </li> <li> Experience Manager Formsas a Cloud Service </li> <ul> |

## 解决方法

下表列出了所有受影响版本的解决方案：

| 发行版本 | 当前版本 | 用户操作 |
|---|---|---|
| 在JEE上Experience Manager6.5 Forms | 6.5.19.0 | [安装最新的服务包](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=en) |
| 在JEE上Experience Manager6.5 Forms | 6.5.13.0 - 6.5.18.0 | 使用以下方法之一： <ul><li>  <a href="https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=en"> 安装最新的服务包 </a> </li> <li> <a href ="#use-manual-mitigation-steps"> 采用手动缓解步骤 </a> |
| 在JEE上Experience Manager6.5 Forms | 6.5 - 6.5.12.0 | [安装最新的服务包](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=en)  </br> </br> **注意：** AEM Forms当前支持版本6.5.13.0到6.5.19.0。如果您使用的是旧版本，我们建议升级到6.5.13.0或更高版本。 有关安装AEM 6.5.13.0或更高版本的说明，请参阅发行说明。 |

### 采用手动缓解步骤 {#use-manual-mitigation-steps}

您可以使用手动缓解步骤来解决运行Service Pack 13的AEM 6.5表单服务器到运行Service Pack 18 (6.5.13.0 - 6.5.18.0)的AEM 6.5表单服务器上的问题：

1. 下载 [struts-core 2.5.33 jar](https://repo1.maven.org/maven2/org/apache/struts/struts2-core/2.5.33/struts2-core-2.5.33.jar) 到本地文件夹。 例如，C:\Users\labuser\Desktop\struts2-core-2.5.33.jar。
1. 从下载AEM Forms on JEE手动修补工具 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/patch_utility/archive-patcher-1.0.0.zip).
1. 解压缩手动修补工具存档。 例如，提取到 `/Users/labuser/Desktop/archive-patcher-1.0.0 folder`. 将提取以下文件：
   * archive-patcher-1.0.0.jar
   * patch-archive.bat
   * patch-archive.sh

>[!BEGINTABS]

>[!TAB Windows]

1. 关闭所有服务器实例和定位器。

1. 打开终端窗口，并导航到包含AEM Forms on JEE手动修补工具（解压缩的文件）的文件夹。

1. 运行以下命令以搜索具有旧版struts2库的所有文件。 运行命令之前，将命令中的路径替换为AEM Forms服务器的路径：


   ```
   patch-archive.bat -root=C:\Adobe\Adobe_Experience_Manager_Forms\configurationManager\export -pattern=.*struts2-core.*jar$
   ```

   >[!NOTE]
   >
   >
   >该工具需要互联网连接，因为它在运行时下载依赖项。 因此，在运行该工具之前，请确保已连接到Internet。

1. 按照列出的顺序运行以下命令，以替换递归原位。 运行命令之前，将命令中的路径替换为AEM Forms服务器的路径，并且 `struts2-core-2.5.33.jar` 文件。



   ```
   patch-archive.bat -root=C:\Adobe\Adobe_Experience_Manager_Forms\configurationManager\export -pattern=.*struts2-core.*jar$ -action=replace C:\Users\labuser\Desktop\struts2-core-2.5.33.jar
   ```

   上述步骤使用旧版struts2库修补所有ear文件。

1. 取消部署旧版EAR，并将打补丁的EAR文件（位于导出文件夹中）部署到应用程序服务器。

1. 启动AEM Forms服务器。

>[!TAB Linux]

1. 关闭所有服务器实例和定位器。

1. 打开终端窗口，并导航到包含AEM Forms on JEE手动修补工具（解压缩的文件）的文件夹。

1. 运行以下命令以搜索具有旧版struts2库的所有文件。 运行命令之前，将命令中的路径替换为AEM Forms服务器的路径：


   ```
   ./patch-archive.sh -root=/opt/Adobe/Adobe_Experience_Manager_Forms/configurationManager/export/ -pattern=.*struts2-core.*jar$
   ```

   >[!NOTE]
   >
   >
   >该工具需要互联网连接，因为它在运行时下载依赖项。 因此，在运行该工具之前，请确保已连接到Internet。

1. 按照列出的顺序运行以下命令，以替换递归原位。 运行命令之前，将命令中的路径替换为AEM Forms服务器的路径，并且 `struts2-core-2.5.33.jar` 文件。



   ```
   ./patch-archive.sh -root=/opt/Adobe/Adobe_Experience_Manager_Forms/configurationManager/export/ -pattern=.*struts2-core.*jar$ -action=replace /opt/struts2-core-2.5.33.jar
   ```

   上述步骤使用旧版struts2库修补所有ear文件。

1. 取消部署旧版EAR，并将打补丁的EAR文件（位于导出文件夹中）部署到应用程序服务器。

1. 启动AEM Forms服务器。

>[!ENDTABS]




<!-- 
### Manual patching tool 


>[!BEGINTABS]

>[!TAB Windows]

    ```
    
    patch-archive.bat [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.

>[!TAB macOS]

    ```
    
    patch-archive.sh [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.  

>[!TAB Linux]

    ```
    
    patch-archive.sh [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.  



>[!ENDTABS]









-->
