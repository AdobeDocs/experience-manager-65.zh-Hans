---
title: Adobe Experience Manager 中的服务用户
description: 了解 Adobe Experience Manager 中的服务用户。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: ccd8577b-3bbf-40ba-9696-474545f07b84
feature: Administering
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: ht
source-wordcount: '1740'
ht-degree: 100%

---


# Adobe Experience Manager（AEM）中的服务用户 {#service-users-in-aem}

## 概述 {#overview}

过去，在 AEM 中获取管理会话或资源解析器的主要方式，是使用 Sling 提供的 `SlingRepository.loginAdministrative()` 和 `ResourceResolverFactory.getAdministrativeResourceResolver()` 方法。

然而，这两种方法并未围绕[最小权限原则](https://en.wikipedia.org/wiki/Principle_of_least_privilege)进行设计。它使开发人员很容易在早期忽略为内容规划合理的结构及相应的访问控制级别（Access Control Level，简称“ACL”），从而埋下安全隐患。一旦此类服务存在漏洞，往往会导致权限被提升至 `admin` 用户，即使代码本身并不需要以管理员权限运行也是如此。

## 如何逐步淘汰管理员会话 {#how-to-phase-out-admin-sessions}

### 优先级 0：该功能是否活跃/必要/已废弃？ {#priority-is-the-feature-active-needed-derelict}

在某些情况下，管理员会话并未实际使用，或功能已被完全禁用。如果您的实施属于此类情况，请彻底移除该功能，或以 [NOP 代码](https://en.wikipedia.org/wiki/NOP)将其置空。

### 优先级 1：使用请求会话 {#priority-use-the-request-session}

尽可能重构功能，使传入的、已完成身份验证的请求会话能够用于读取或写入内容。若暂无法做到，通常可按下述后续优先级中的措施逐步达成。

### 优先级 2：重构内容 {#priority-restructure-content}

许多问题可通过重构内容结构加以解决。进行重构时，请牢记以下简单准则：

* **更改访问控制**

   * 确保确实需要访问权限的用户或用户组能够获得相应的访问权限；

* **优化内容结构**

   * 将内容移动到其他位置，例如与可用的请求会话相匹配的访问控制位置；
   * 调整内容的粒度；

* **将代码重构为合适的服务**

   * 将业务逻辑从 JSP 代码中移到服务层。这样可以支持不同的内容建模方式。

此外，请确保您开发的任何新功能都遵循以下原则：

* **安全需求应主导内容结构设计**

   * 访问控制应当自然融入管理流程
   * 访问控制必须由存储库强制执行，而不是依赖应用程序

* **使用节点类型**

   * 限制可设置的属性范围

* **遵循隐私设置**

   * 如果存在私有轮廓，例如对于在私有 `/profile` 节点中的信息，则不要暴露其中的轮廓图片、电子邮件或完整姓名。

## 严格的访问控制 {#strict-access-control}

无论您是在重构内容时应用访问控制，还是为新服务用户应用访问控制，都必须尽可能应用最严格的访问控制级别（简称“ACL”）。充分利用所有可用的访问控制功能：

* 例如，不要在 `/apps` 上直接应用 `jcr:read`，而应仅对 `/apps/*/components/*/analytics` 应用

* 使用[限制](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)

* 为节点类型应用 ACL
* 限制权限

   * 例如，当仅需要写入属性时，不要授予 `jcr:write` 权限；而应使用 `jcr:modifyProperties`

## 服务用户与映射 {#service-users-and-mappings}

如果以上方法不可行，Sling 7 提供了服务用户映射服务，它允许您配置从捆绑包到用户的映射，并提供两个对应的 API 方法：

* [`SlingRepository.loginService()`](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)
* [`ResourceResolverFactory.getServiceResourceResolver()`](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)

这些方法会返回仅具有已配置用户的权限的会话/资源解析器。这些方法的特点如下：

* 允许将服务映射到用户
* 支持定义子服务用户
* 核心配置点为：`org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` = `service-name` [&quot;:&quot; subservice-name]

* `service-id` 会映射到一个资源解析器和/或 JCR 存储库用户 ID，以用于身份验证
* `service-name` 是提供服务的捆绑包的符号名称

## 其他建议 {#other-recommendations}

### 用服务用户替换管理会话 {#replacing-the-admin-session-with-a-service-user}

服务用户是一种 JCR 用户，它没有设置密码，并且仅具备执行特定任务所需的最小权限。由于未设置密码，因此无法直接使用服务用户进行登录。

弃用管理会话的一种方式是将其替换为服务用户会话。如有需要，也可以替换为多个子服务用户。

要将管理会话替换为服务用户，应执行以下步骤：

1. 明确服务所需的权限，并遵循最小权限原则。
1. 检查是否已有用户恰好具备所需的权限设置。如果没有符合要求的用户，则创建一个系统服务用户。创建服务用户需要 RTC。在某些情况下，创建多个子服务用户（例如，一个用于写入，一个用于读取）有助于进一步分隔访问权限。
1. 为用户设置并测试 ACE。
1. 为您的服务和 `user/sub-users` 添加 `service-user` 映射

1. 使服务用户 Sling 功能可在您的捆绑包中使用：更新到最新版本的 `org.apache.sling.api`。

1. 在代码中使用 `loginService` 或 `getServiceResourceResolver` API 替换 `admin-session`。

## 创建服务用户 {#creating-a-new-service-user}

在确认 AEM 服务用户列表中没有适用用户，且对应的 RTC 问题已获批准后，将新用户添加到默认内容中。

推荐的方法是通过 *https://&lt;server>:&lt;port>/crx/explorer/index.jsp* 的存储库资源管理器创建服务用户

目标是获取一个有效的 `jcr:uuid` 属性，这是通过安装内容包创建用户时的必填项。

您可以通过以下方式创建服务用户：

1. 前往存储库资源管理器 *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*
1. 点击屏幕左上角的&#x200B;**登录**&#x200B;链接，以管理员身份登录。
1. 接下来，创建并命名系统用户。要将用户创建为系统用户，请将中间路径设置为 `system`，并根据需要添加可选的子文件夹：

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. 确认您的系统用户节点如下所示：

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >服务用户没有关联的 Mixin 类型。这意味着系统用户本身不包含任何访问控制策略。

在将相应的 .content.xml 添加到捆绑包的内容中时，请确保已设置 `rep:authorizableId`，并且主类型为 `rep:SystemUser`。它应该如下所示：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## 在 ServiceUserMapper 配置中添加配置修订 {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

要将您的服务映射到相应的系统用户，需要为 [`ServiceUserMapper`](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html) 服务创建一个工厂配置。为保持模块化，可以通过 [Sling 修改机制](https://issues.apache.org/jira/browse/SLING-3578)提供此类配置。推荐的方式是结合 [Sling 初始内容加载](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html)，将此配置随捆绑包一起安装：

1. 在捆绑包的 src/main/resources 文件夹下创建子文件夹 SLING-INF/content。
1. 在该文件夹中创建一个名为
org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-&lt;您工厂配置的唯一名称>.xml 的文件，并在其中编写您的工厂配置内容（包括所有子服务用户映射）。示例：

1. 在捆绑包的 `src/main/resources` 文件夹下创建一个 `SLING-INF/content` 文件夹；
1. 在该文件夹中，创建一个文件 `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml`，文件内容应包含您的工厂配置，并且包括所有子服务用户映射。

   为了便于说明，以名为 `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml` 的文件为例：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <node>
       <primaryNodeType>sling:OsgiConfig</primaryNodeType>
       <property>
           <name>user.default</name>
           <value></value>
       </property>
       <property>
           <name>user.mapping</name>
           <values>
               <value>com.adobe.granite.auth.saml=authentication-service</value>
           </values>
       </property>
   </node>
   ```

1. 在捆绑包的 `pom.xml` 中的 `maven-bundle-plugin` 配置内，引用 Sling 初始内容。示例：

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. 安装您的捆绑包，并确认工厂配置已成功安装。您可以通过以下方式来实现：

   * 前往位于 *https://serverhost:serveraddress/system/console/configMgr* 的网页控制台
   * 搜索 **Apache Sling 服务用户映射器服务修订**
   * 点击该链接，检查所需配置是否生效。

## 处理服务中的共享会话 {#dealing-with-shared-sessions-in-services}

`loginAdministrative()` 调用通常与共享会话一起出现。这些会话会在服务激活时获取，并且仅在服务停止后才会注销。尽管这种做法很常见，但它会导致两个问题：

* **安全性：**&#x200B;此类管理会话通常用于缓存并返回绑定到共享会话的资源或其他对象。在调用栈的后续过程中，这些对象可能会被转化为具备更高权限的会话或资源解析器。调用者往往并不清楚自己实际在操作的是一个管理会话。
* **性能：**&#x200B;在 Oak 中，共享会话可能会导致性能问题，因此不建议使用。

针对安全风险，最明显的方法是将 `loginAdministrative()` 调用替换为 `loginService()`，并指定一个具有受限权限的用户。但需要注意，这种替换对潜在的性能下降没有帮助。为缓解性能问题，可以将所需信息封装在一个与会话无关的对象中。然后在需要时按需创建（或销毁）会话。

推荐的方法是重构服务的 API，使调用者能够自行控制会话的创建与销毁。

## JSP 中的管理会话 {#administrative-sessions-in-jsps}

JSP 无法使用 `loginService()`，因为没有关联的服务。然而，在 JSP 中使用管理会话通常意味着违反了 MVC 模式。

这可以通过以下两种方式修复：

1. 以一种允许在用户会话期间对其进行操作的方式重构内容；
1. 将逻辑提取到提供 API 的服务中，然后 JSP 可以使用该服务。

其中，方法一是首选方案。

## 处理事件、复制预处理器和作业 {#processing-events-replication-preprocessors-and-jobs}

在处理事件、作业，有时是工作流时，触发事件的相应会话可能丢失。因此，事件处理程序和作业处理器通常会使用管理会话来完成工作。为解决这一问题，有几种可能的方法，这些方法各有优劣：

1. 在事件负载中传递 `user-id`，并使用模拟。

   **优点：**&#x200B;便于使用。

   **缺点：**&#x200B;仍然使用 `loginAdministrative()`。它会对已认证的请求重新认证。

1. 创建或重复使用有权访问数据的服务用户。

   **优点：**&#x200B;与当前设计保持一致。所需改动最小。

   **缺点：**&#x200B;需要功能强大的服务用户来保持灵活性，极易导致权限升级。绕过安全模型。

1. 在事件负载中传递 `Subject` 的序列化，并基于该对象创建 `ResourceResolver`。例如在 `ResourceResolverFactory` 中使用 JAAS 的 `doAsPrivileged`。

   **优点：**&#x200B;从安全角度来看实施更为干净。它可以避免重新认证，并在原有的权限下运行。与安全相关的代码对事件使用者保持透明。

   **缺点：**&#x200B;需要进行重构。与安全相关的代码对事件使用者保持透明可能会带来问题。

第三种方法是推荐的处理方式。

## 工作流流程 {#workflow-processes}

在工作流流程实施中，触发工作流的对应用户会话可能会丢失。因此，工作流流程通常会使用管理会话来执行任务。

为解决这些问题，推荐使用在[处理事件、复制预处理器和作业](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs)中提到的相同方法。

## Sling POST 处理器与已删除的页面 {#sling-post-processors-and-deleted-pages}

在 Sling POST 处理器的实施中，会使用一些管理会话。通常，管理会话用于访问正在处理的 POST 中等待删除的节点。因此，这些节点无法再通过请求会话获取。访问等待删除的节点可能会泄露原本不应被访问的元数据。
