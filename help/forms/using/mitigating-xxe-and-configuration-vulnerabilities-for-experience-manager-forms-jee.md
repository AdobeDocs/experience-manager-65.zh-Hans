---
title: 缓解JEE上AEM Forms的XXE、Struts开发模式配置和远程代码执行漏洞
description: 缓解JEE上AEM Forms的XXE、配置和远程代码执行漏洞
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 9fade12f-a038-4fd6-8767-1c30966574c5
solution: Experience Manager, Experience Manager Forms
release-date: 2025-08-05T00:00:00Z
source-git-commit: 9be9bfc9e20a151afdb9ae2cddcc39b4d2701c1b
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 5%

---

# 缓解JEE上AEM Forms的RCE (CVE-2025-49533)、Struts开发模式配置(CVE-2025-54253)、XXE (CVE-2025-54254)和漏洞 {#mitigating-xxe-configuration-rce-vulnerabilities-aem-forms}

## 快速参考

| **影响级别** | **受影响的版本** | **建议的操作** |
|---|---|---|
| **关键** | JEE Service Pack 23 (6.5.23.0)上的AEM 6.5 Forms | [安装最新的修补程序](#option-1-for-users-on-version-65230-install-latest-hotfix) |
| **关键** | JEE Service Pack 18至22 (6.5.18.0 - 6.5.22.0)上的AEM 6.5 Forms | [手动安装修补程序](#option-2-for-users-on-65180---65220-manual-hotfix-installation) |
| **关键** | JEE Service Pack 17 (6.5.17.0)或更早版本上的AEM 6.5 Forms | 升级到支持的Service Pack版本，然后为您的新版本应用建议的缓解步骤 |
| **不受影响** | OSGi、Workbench、Cloud Service上的AEM Forms | 无需执行任何操作 |

已解决的&#x200B;**漏洞：**

- 远程代码执行(CVE-2025-49533)
- 配置安全问题(CVE-2025-54253)
- XML外部实体(XXE)处理(CVE-2025-54254)

## 概述

### 受影响的内容

| 漏洞 | 影响 | 受影响的组件 |
|---|---|---|
| **CVE-2025-49533**：远程代码执行 | 在GetDocumentServlet中执行未经身份验证的代码 | JEE Service Pack 23 (6.5.23.0)及更早版本上的AEM 6.5 Forms |
| **CVE-2025-54253**：配置问题 | 在管理UI中启用Struts开发模式 | JEE Service Pack 23 (6.5.23.0)及更早版本上的AEM 6.5 Forms |
| **CVE-2025-54254**： XXE正在处理 | Document Security模块允许未经授权的文件访问 | JEE Service Pack 23 (6.5.23.0)及更早版本上的AEM 6.5 Forms |


### 未受影响的内容

- Experience Manager Forms Workbench（所有版本）
- OSGi上的Experience Manager Forms（所有版本）
- Experience Manager Forms as a Cloud Service

## 分辨率选项


### 开始之前

在进行任何更改之前，请备份要修改或更新的EAR文件或DSC文件：

- 在部署目录中找到原始EAR或DSC文件。
- 将文件复制到部署目录之外的安全备份位置。
- 在继续进行任何更新之前，请确保备份完整且可访问。

如果您在更新过程中遇到任何问题，可使用此预防措施恢复原始状态。

### 选项1： （对于版本6.5.23.0的用户）安装最新的修补程序

1. [下载6.5.23.0](/help/release-notes/aem-forms-hotfix.md)的修补程序。
1. 按照标准的[修补程序/修补程序安装说明](/help/release-notes/jee-patch-installer-65.md)操作
1. 如果您在IBM WebSphere或Oracle WebLogic上使用Document Security(以前称为Rights Management)，请在启动AEM Forms服务器之前设置以下Java系统属性（JVM参数）：

   ```
   -Dcom.adobe.forms.jee.services.allowDoctypeDeclaration=true
   ```

1. 重新启动应用程序服务器

### 选项2： （对于6.5.18.0 - 6.5.22.0上的用户）手动安装修补程序

+++通过6.5.18.0为6.5.22.0手动安装修补程序

**步骤1：下载并解压缩修补程序包**

- 从Adobe软件分发门户下载适用于[ - 6.5.22.6.5.18.0的](/help/release-notes/aem-forms-hotfix.md)修补程序
- 本地提取

**步骤2：导航到正确的版本文件夹**

- 根据环境中安装的Service Pack版本，转到匹配的文件夹。

  对于Service Pack 20，文件夹为：

  ```
  <extracted-hotfix>/SP20/
  ```

**步骤3：找到部署目录**

- 在JEE服务器上的AEM Forms上，转到：

  ```
  [AEM installation directory]/deploy
  ```

  示例：`adobe/adobe-experience-manager-forms/deploy`



**步骤4：更新和替换EAR文件**

>[!BEGINTABS]

>[!TAB JBoss]

1. 打开`adobe-core-jboss.ear`并将`adminui.war`替换为

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adminui.war
   ```

   例如，`adobe-xxe-configuration-hotfix/SP20/jboss/adminui.war`

1. 在`adobe-core-jboss.ear`内，转到`lib/`文件夹并将`adobe-uisupport.jar`替换为：

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   例如，`adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`

1. 保存耳朵。 确保正确保存了更改。


1. 将`adobe-edcserver-jboss.ear`替换为

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adobe-edcserver-jboss.ear
   ```

   例如，`adobe-xxe-configuration-hotfix/SP20/jboss/adobe-edcserver-jboss.ear`

1. 将`adobe-forms-jboss.ear`替换为

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adobe-forms-jboss.ear
   ```

   例如，`adobe-xxe-configuration-hotfix/SP20/jboss/adobe-forms-jboss.ear`



>[!TAB WebLogic]

1. 打开`adobe-core-weblogic.ear`并将`adminui.war`替换为

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adminui.war
   ```

   例如，`adobe-xxe-configuration-hotfix/SP20/weblogic/adminui.war`

1. 在`adobe-core-weblogic.ear`内，将`adobe-uisupport.jar`替换为：

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   例如，`adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`

1. 保存耳朵。 确保正确保存了更改。


1. 将`adobe-edcserver-weblogic.ear`替换为

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adobe-edcserver-weblogic.ear
   ```

   例如，`adobe-xxe-configuration-hotfix/SP20/weblogic/adobe-edcserver-weblogic.ear`

1. 将`adobe-forms-weblogic.ear`替换为

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adobe-forms-weblogic.ear
   ```

   例如，`adobe-xxe-configuration-hotfix/SP20/weblogic/adobe-forms-weblogic.ear`

>[!TAB WebSphere]

1. 打开`adobe-core-websphere.ear`并将`adminui.war`替换为

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adminui.war
   ```

   例如，`adobe-xxe-configuration-hotfix/SP20/websphere/adminui.war`

1. 在`adobe-core-websphere.ear`内，将`adobe-uisupport.jar`替换为：

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   例如，`adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`

1. 保存耳朵。 确保正确保存了更改。


1. 将`adobe-edcserver-websphere.ear`替换为

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adobe-edcserver-websphere.ear
   ```

   例如，`adobe-xxe-configuration-hotfix/SP20/websphere/adobe-edcserver-websphere.ear`

1. 将`adobe-forms-websphere.ear`替换为

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adobe-forms-websphere.ear
   ```

   例如，`adobe-xxe-configuration-hotfix/SP20/websphere/adobe-forms-websphere.ear`

>[!ENDTABS]



**步骤5：使用`adobe-rightsmanagement-<appserver>-dsc.jar`更新**&#x200B;文件

```
adobe-xxe-configuration-hotfix/SP[version]/<appserver>/adobe-rightsmanagement-<appserver>-dsc.jar
```

例如，`adobe-xxe-configuration-hotfix/SP20/jboss/adobe-rightsmanagement-jboss-dsc.jar`

**步骤6： WebSphere和WebLogic上的Document Security的其他配置**：

如果您使用的是Document Security(以前称为Rights Management)，请在启动AEM Forms服务器之前设置以下Java系统属性（JVM参数）：

```
-Dcom.adobe.forms.jee.services.allowDoctypeDeclaration=true
```


**步骤7：重新运行配置管理器**

- 启动配置管理器以重新部署更新的EAR并应用修补程序

+++

### 选项3：（对于6.5.17.0和更早版本上的用户）升级路径

1. [升级到支持的服务包版本](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)
1. 根据您的新版本，按照上面的选项1或选项2操作

## 引用

- [CWE-611： XML外部实体引用](https://cwe.mitre.org/data/definitions/611.html)的限制不正确
- [CWE-16：配置](https://cwe.mitre.org/data/definitions/16.html)
- [OWASP XXE防范备忘单](https://owasp.org/www-community/vulnerabilities/XML_External_Entity_XXE_Processing)
- [Adobe Experience Manager Forms安全最佳实践](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?lang=zh-Hans)
