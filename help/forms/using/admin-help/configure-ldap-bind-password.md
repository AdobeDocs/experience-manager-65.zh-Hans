---
title: 配置LDAP绑定口令
seo-title: Configure the LDAP bind password
description: 了解在将配置文件导入其他系统之前，如何配置绑定密码字段。
seo-description: Learn how to configure the bind password field before you import the configuration file into another system.
uuid: 1ab1907c-8b55-4b6f-bd5b-49f22d78b8a8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 165b3950-b03f-4848-8361-ffb0a26d2658
exl-id: c72794f5-8767-409e-a1df-91a8fdc54d18
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# 配置LDAP绑定口令{#configure-the-ldap-bind-password}

为避免安全风险，未配置导出配置文件(config.xml)中的绑定密码字段。 在将配置文件导入另一个系统之前，请确保配置此密码。 此密码将覆盖数据库中存储的现有密码。 Null口令不会覆盖现有的非Null口令值。

1. 在管理控制台中，单击设置>用户管理>配置>导入和导出配置文件。
1. 要将当前配置设置导出到文件，请单击“导出”并将配置文件保存到其他位置。
1. 在文件中，找到 `Domains` > *[您的域名]* > `DirectoryConfigs` > `LDAPGroupConfig` 节点。 示例如下：

   ```xml
    <node name="LDAPGroupConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="batchSize" value="200" />
            <entry key="binduser" value="cn=Directory Manager" />
            <entry key="bindpassword" value="" />
        </map>
   ```

   键入值 `bindpassword` 并保存更改。

1. 在文件中，找到 `Domains` > *[您的域名]* > `DirectoryConfigs` > `LDAPGroupConfig` > `LDAPUserConfig` 节点。 示例如下：

   ```xml
    <node name="LDAPUserConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="batchSize" value="200" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="bindpassword" value="" />
            <entry key="binduser" value="cn=Directory Manager" />
        </map>
   ```

   键入值 `bindpassword` 并保存更改。

1. 要导入更新的文件，请在“用户管理”中单击“配置”>“导入和导出配置文件”。
1. 单击“浏览”查找文件，单击“导入”，然后单击“确定”。
