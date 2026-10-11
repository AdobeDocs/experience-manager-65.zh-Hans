---
title: 为JEE上的AEM Forms将JBoss EAP群集从7.4.10升级到7.4.23
description: 为JEE上的AEM Forms将JBoss EAP群集从7.4.10升级到7.4.23的其他步骤。
SEO Description: Additional cluster upgrade steps for JBoss EAP 7.4.10 to 7.4.23 on AEM Forms on JEE.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
exl-id: 2c9e7f41-a8d6-4b03-8e5c-1a4f6d9e0b72
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms Upgrade,AEM Forms on JEE
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
  - id: d49d6117-dd89-469c-a774-cc96b7eee433
    internal-label: Administration
subfeature_v2:
  - id: b9cdd520-e7a7-4af9-a95f-296f28882b69
    internal-label: AEM Forms upgrade
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 1%
---
# 为JEE上的AEM Forms将JBoss EAP群集从7.4.10升级到7.4.23 {#upgrade-jboss-eap-cluster-from-7-4-10-to-7-4-23}

## 概述 {#overview}

对于JEE上的AEM Forms，当您将JBoss EAP群集从版本7.4.10升级到7.4.23时，除了独立升级步骤之外，还需要进行其他配置。 在新的JBoss安装中，必须更新特定于群集的设置，如缓存定位器、主从身份验证、主机绑定和域控制器配置。

## 应用到 {#applies-to}

本文适用于：

* 在集群环境中，在JBoss EAP 7.4.10上运行的JEE上的AEM Forms
* Windows和Linux上的主从式JBoss EAP配置

## 先决条件 {#prerequisites}

完成[为JEE上的AEM Forms](/help/forms/using/upgrade-jboss-eap-from-7-4-10-to-7-4-23.md)将JBoss EAP从7.4.10升级到7.4.23中的所有步骤，包括将连接URL、用户名和密码从现有安装复制到新配置文件。

## 步骤 {#steps}

执行以下特定于群集的其他步骤：

### 更新domain.conf.bat {#update-domain-conf-bat}

1. 在`domain.conf.bat`中，将现有设置中的定位符信息添加到新文件中：

   ```text
   set "JAVA_OPTS=%JAVA_OPTS% -Doak.documentMK.maxServerTimeDiffMillis=-1"
   set "JAVA_OPTS=%JAVA_OPTS% -Dadobe.cache.cluster-locators=<ip-address-master>[22345],<ip-address-slave>[22345]"
   set "JAVA_OPTS=%JAVA_OPTS% -DentityExpansionLimit=10000"
   ```

### 配置主从身份验证 {#configure-master-slave-authentication}

1. 在主节点上为主从身份验证创建新的用户。
1. 在从属节点上，更新`host.xml`中的用户密码：

   ```xml
   <server-identities>
       <secret value="Y2hhbmdlaXQ="/>
   </server-identities>
   ```

### 更新host.xml中的IP地址 {#update-ip-addresses-in-host-xml}

1. 更新`host.xml`中主节点和从节点的IP地址：

   ```xml
   <interfaces>
       <interface name="management">
           <inet-address value="${jboss.bind.address.management:<ip-address>}"/>
       </interface>
       <interface name="public">
           <inet-address value="${jboss.bind.address:<ip-address>}"/>
       </interface>
   </interfaces>
   ```

### 从域配置中删除部署 {#remove-deployments-from-domain-configuration}

1. 确保新`domain_<db>.xml`文件中没有`<deployments>`节。
1. 请勿从现有配置复制以下块：

   ```xml
   <deployments>
       <deployment name="adobe-forms-ivs-jboss.ear" runtime-name="adobe-forms-ivs-jboss.ear"/>
       <deployment name="adobe-livecycle-cq-author.ear" runtime-name="adobe-livecycle-cq-author.ear"/>
       <deployment name="adobe-livecycle-jboss.ear" runtime-name="adobe-livecycle-jboss.ear"/>
       <deployment name="adobe-livecycle-native-jboss-x86_win32.ear" runtime-name="adobe-livecycle-native-jboss-x86_win32.ear"/>
       <deployment name="adobe-livecycle-native-jboss-x86_win64.ear" runtime-name="adobe-livecycle-native-jboss-x86_win64.ear"/>
       <deployment name="adobe-output-ivs-jboss.ear" runtime-name="adobe-output-ivs-jboss.ear"/>
       <deployment name="adobe-workspace-client.ear" runtime-name="adobe-workspace-client.ear"/>
   </deployments>
   ```

### 更新域配置中的驱动程序类 {#update-driver-class-in-domain-configuration}

1. 根据您的数据库引擎更新`domain_<db>.xml`中的驱动程序类部分：

   **MSSQL：**

   ```xml
   <xa-datasource-class>com.microsoft.sqlserver.jdbc.SQLServerXADataSource</xa-datasource-class>
   ```

   **Oracle：**

   ```xml
   <xa-datasource-class>oracle.jdbc.xa.client.OracleXADataSource</xa-datasource-class>
   ```

### 在从属节点上更新域控制器 {#update-domain-controller-on-slave-nodes}

1. 使用主IP地址、端口`9999`、用户名`slave1`和领域`ManagementRealm`更新`host.xml`中从节点上的域控制器块：

   ```xml
   <remote host="<ip-address>" port="9999" username="slave1" realm="ManagementRealm"/>
   ```

### 更新jboss-cli.xml {#update-jboss-cli-xml}

1. 在主节点和从节点上更新`jboss-cli.xml`中的`<host>`条目。
