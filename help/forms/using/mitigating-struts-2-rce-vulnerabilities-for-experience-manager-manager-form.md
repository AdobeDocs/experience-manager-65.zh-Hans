---
title: 缓解JEE上Experience Manager Forms的Struts 2漏洞
description: 缓解JEE上Experience Manager Forms的Struts 2漏洞
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
source-git-commit: 5f5fcc10927d62cdfaeb0770c34052ceda02b2e8
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 1%

---


# 缓解Experience Manager Forms的Struts 2漏洞 {#mitigatin-struts2-rce-vulnerabilities-for-aem-forms}

## 问题

Struts 2 RCE是一种用于开发Java EE Web应用程序的流行开放源码Web应用程序框架，已经报告了它存在严重的安全漏洞。 已分析以下漏洞：

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

1. 关闭所有服务器实例和定位器。
1. 下载 [struts-core 2.5.33 jar](https://repo1.maven.org/maven2/org/apache/struts/struts2-core/2.5.33/struts2-core-2.5.33.jar).
1. 从下载AEM Forms on JEE手动修补工具 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/patch_utility/archive-patcher-1.0.0.zip).
1. 解压缩手动修补工具存档。 它提取以下文件：
   * archive-patcher-1.0.0.jar
   * patch-archive.bat
   * patch-archive.sh
1. 打开终端窗口，并导航到包含提取文件的文件夹。
1. 使用手动打补丁工具搜索、列出和替换所有struts2 jar文件。 该工具需要互联网连接，因为它在运行时下载依赖项。 因此，在运行该工具之前，请确保已连接到Internet。

要搜索和替换struts2-core-2.5.30 jar文件和struts2-core.jar，请执行以下操作：


>[!BEGINTABS]

>[!TAB Windows]

1. 运行以下命令列出所有struts2 jar文件。 运行命令之前，将命令中的路径替换为AEM Forms服务器的路径：

   ```
   patch-archive.bat -root=C:\Adobe\Adobe_Experience_Manager_Forms\...\export -pattern=.*struts2-core-2.5.30.jar$
   ```

1. 按照列出的顺序运行以下命令，以替换递归原位。 运行命令之前。 将命令中的路径替换为AEM Forms服务器的路径，并且 `struts2-core-2.5.33.jar` 文件。


   ```
   patch-archive.bat -root=C:\Adobe\Adobe_Experience_Manager_Forms\...\export -pattern=.*struts2-core-2.5.30.jar$ -action=replace C:\temp\struts2-core-2.5.33.jar
   
   
   patch-archive.bat -root=C:\Users\labuser\Desktop\check -pattern=.*struts2-core.jar$ -action=replace C:\Users\labuser\Desktop\struts2-core.jar -action=replace C:\Users\labuser\Desktop\struts2-core.jar
   ```

1. 启动AEM Forms服务器。


>[!TAB Linux]

1. 运行以下命令列出所有struts2 jar文件。 运行命令之前，将命令中的路径替换为AEM Forms服务器的路径：

   ```
   patch-archive.sh -root=\Users\labuser\Adobe\Adobe_Experience_Manager_Forms\...\export -pattern=.*struts2-core-2.5.30.jar$
   ```

1. 按照列出的顺序运行以下命令，以替换递归原位。 运行命令之前，将命令中的路径替换为AEM Forms服务器的路径，并且 `struts2-core-2.5.33.jar` 文件。

   ```
   patch-archive.sh -root=\Users\labuser\Adobe\Adobe_Experience_Manager_Forms\...\export -pattern=.*struts2-core-2.5.30.jar$ -action=replace \temp\struts2-core-2.5.33.jar
   
   
   patch-archive.sh -root=\Users\labuser\Desktop\check -pattern=.*struts2-core.jar$ -action=replace \Users\labuser\Desktop\struts2-core.jar -action=replace \Users\labuser\Desktop\struts2-core.jar
   ```

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