---
title: AEM 中的封闭用户组
description: 了解封闭用户组及其为AEM中的可扩展性和安全性带来的优势。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 39e35a07-140f-4853-8f0d-8275bce27a65
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '6650'
ht-degree: 0%

---

# AEM 中的封闭用户组{#closed-user-groups-in-aem}

## 简介 {#introduction}

自AEM 6.3起，出现了一个新的封闭用户组实施，旨在解决现有实施中存在的性能、可扩展性和安全问题。

>[!NOTE]
>
>为了简单起见，本文档中采用了CUG缩写。

新实施的目标是在需要时涵盖现有功能，同时解决旧版本的问题和设计限制。 最终得到一种具有以下特征的新CUG设计：

* 身份验证和授权要素的明确分离，可以单独使用，也可以结合使用；
* 专用授权模型反映所配置的CUG树上的受限读取访问，而不干扰其它访问控制设置和权限要求；
* 将编写实例所需的受限读取访问权限的访问控制设置与仅发布所需的权限评估分离；
* 编辑受限读取访问而不提升权限；
* 专用节点类型扩展标记认证要求；
* 与身份验证要求关联的可选登录路径。

### 新的自定义用户组实施 {#the-new-custom-user-group-implementation}

在AEM上下文中称为CUG，它包含以下步骤：

* 限制必须保护的树上的读取权限，并且只允许对随给定CUG实例列出或完全从CUG评估中排除的主体进行读取。 这称为&#x200B;**授权**&#x200B;元素。
* 在给定树上强制进行身份验证，并（可选）为该树指定专用登录页面，然后排除该登录页面。 这称为&#x200B;**身份验证**&#x200B;元素。

新实施的设计旨在使身份验证和授权元素之间划出一条界线。 从AEM 6.3开始，可以限制读取访问，而无需明确添加身份验证要求。 例如，如果给定实例完全要求身份验证，或者给定树已驻留在要求身份验证的子树中。

同样，可以在给定树上标记身份验证要求，而无需更改有效权限设置。 组合和结果列在[组合CUG策略和身份验证要求](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement)部分。

## 概述 {#overview}

### 授权：限制读取访问 {#authorization-restricting-read-access}

CUG的关键功能是限制内容存储库中给定树上除选定承担者外的所有人员的读取权限。 新实施通过定义代表CUG的专用类型的访问控制策略而采用不同的方法，而不是快速操作默认访问控制内容。

#### CUG的访问控制策略 {#access-control-policy-for-cug}

这种新类型的策略具有以下特性：

* org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy类型的访问控制策略（由Apache Jackrabbit API定义）；
* PrincipalSetPolicy将权限授予一组可修改的主体；
* 授予的权限和策略的范围是实施详细信息。

用于表示CUG的PrincipalSetPolicy的实施还定义了：

* CUG策略仅向常规JCR项目授予读访问权限（例如，排除访问控制内容）；
* 范围由拥有CUG策略的接入控制节点定义；
* 可以嵌套CUG策略，嵌套CUG不继承“父”CUG的主体集，启动新的CUG；
* 如果启用了评估，则策略的效果将继承到整个子树直至下一个嵌套CUG。

这些CUG策略通过名为oak-authorization-cug的单独授权模块部署到AEM实例。 此模块带有自己的访问控制管理和权限评估。 换言之，默认的AEM设置会提供结合了多个授权机制的Oak内容存储库配置。 有关详细信息，请参阅Apache Oak文档上的[此页面](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)。

在此复合设置中，新的CUG不会替换附加到目标节点的现有访问控制内容。 相反，它是一种增补，以后还可以在不影响原始访问控制的情况下将其删除，默认情况下，AEM中的增补将是一个访问控制列表。

与以前的实施不同，新的CUG策略总是被识别并视为访问控制内容。 这意味着使用JCR访问控制管理API创建和编辑它们。 有关详细信息，请参阅[管理CUG策略](#managing-cug-policies)部分。

#### CUG策略的权限评估 {#permission-evaluation-of-cug-policies}

除了为CUG提供专门的访问控制管理外，新的授权模型还允许您有条件地为其策略启用权限评估。 这使您可以在暂存环境中设置CUG策略，并且仅在复制到生产环境后才能评估有效权限。

CUG策略的权限评估以及与默认授权模型或任何其他授权模型的交互遵循为Apache Jackrabbit Oak中的多个授权机制设计的模式。 也就是说，当且仅当所有模型都授予访问权限时，才授予给定权限集。 有关详细信息，请参阅[此页面](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)。

以下特征适用于与旨在处理和评估CUG策略的授权模型相关联的权限评估：

* 它仅处理常规节点和属性的读取权限，而不处理读取访问控制内容
* 它不处理写权限或修改受保护的JCR内容所需的任何类型的权限（访问控制、节点类型信息、版本控制、锁定或用户管理等）。 这些权限不受CUG策略影响，也不会由关联的授权模型评估。 是否授予这些权限取决于安全设置中配置的其他模型。

单个CUG策略对权限评估的影响可概括如下：

* 拒绝每个人的读取权限，但策略中列出的排除主体或主体除外；
* 该策略对保存该策略及其属性的访问控制节点生效；
* 该效果也会沿层级向下继承 — 即由访问控制节点定义的项目树；
* 但是，它不影响访问控制节点的同级或祖先；
* 给定CUG的继承在嵌套CUG处停止。

#### 最佳实践 {#best-practices}

以下最佳实践应考虑通过CUG定义受限读取访问权限：

* 慎重决定您对CUG的需求是限制读访问还是身份验证要求。 如果是后者，或者同时需要这两者，请查阅最佳实践部分以了解有关身份验证要求的详细信息
* 为必须保护的数据或内容创建威胁模型，以确定威胁边界，并清楚地了解数据的敏感性和与授权访问相关的角色
* 为存储库内容和CUG建模，以遵循与授权相关的一般方面和最佳实践：

   * 请记住，仅当给定的CUG以及在设置授权中部署的其他模块的评估允许给定主题读取给定存储库项目时，才会授予读取权限
   * 避免创建读取访问已被其他授权模块限制的冗余CUG
   * 对嵌套CUG的过度需求可能会突显内容设计中的问题
   * 对CUG的过度需求（例如，在每个页面上）可能表明需要自定义授权模型，该模型可能更适合匹配现有应用程序和内容的特定安全需求。

* 将CUG策略支持的路径限制为存储库中的几棵树，以便优化性能。 例如，自AEM 6.3起，只允许将/content节点下的CUG作为默认值提供。
* CUG策略旨在向一小部分主体授予读取权限。 对大量主体的需求可能会突出显示内容或应用程序设计中的问题，应当重新考虑。

### 身份验证：定义身份验证要求 {#authentication-defining-the-auth-requirement}

CUG功能的与身份验证相关的部分允许您标记需要身份验证的树，并可以选择指定专用登录页面。 根据以前的版本，新的实施允许您在内容存储库中标记需要身份验证的树。 它还可以有条件地启用与负责最终强制实施该要求并重定向到登录资源的`Sling org.apache.sling.api.auth.Authenticator`的同步。

这些要求由提供`sling.auth.requirements`注册属性的OSGi服务向身份验证程序注册。 然后，使用这些属性来动态扩展身份验证要求。 有关更多详细信息，请参阅[Sling文档](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS)。

#### 使用专用Mixin类型定义身份验证要求 {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}

为安全起见，新实施将保留JCR属性的使用替换为名为`granite:AuthenticationRequired`的专用mixin类型，该类型为登录路径`granite:loginPath`定义了类型为STRING的单个可选属性。 只有与此mixin类型相关的内容更改才会导致更新在Apache Sling Authenticator中注册的要求。 在保留任何临时修改时会跟踪这些修改，因此需要`javax.jcr.Session.save()`调用才能生效。

`granite:loginPath`属性也是如此。 只有当它由与身份验证要求相关的mixin类型定义时，才会遵守它。 在非结构化JCR节点中添加具有此名称的剩余属性不会显示所需的效果，并且负责更新OSGi注册的处理程序会忽略该属性。

>[!NOTE]
>
>设置登录路径属性是可选的，并且仅当需要身份验证的树无法回退到默认登录页或继承的登录页时才需要设置。 请参阅下面的[登录路径评估](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path)。

#### 向Sling身份验证器注册身份验证要求和登录路径 {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

由于此类身份验证要求应仅限于某些运行模式以及内容存储库中的一小部分树，因此跟踪要求mixin类型和登录路径属性是有条件的。 此外，它还绑定到定义所支持路径的相应配置（请参阅下面的配置选项）。 因此，仅这些受支持路径范围内的更改才会触发OSGi注册的更新，而其他地方mixin类型和属性都会被忽略。

默认AEM安装程序现在通过允许以创作运行模式设置mixin来使用此配置，但只有在复制到发布实例时才会生效。 有关Sling如何强制实施身份验证要求的详细信息，请参阅[此页面](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html)。

在配置的支持路径中添加`granite:AuthenticationRequired` mixin类型会导致更新负责处理程序的OSGi注册，其中包含具有`sling.auth.requirements`属性的附加新条目。 如果给定的身份验证要求指定了可选的`granite:loginPath`属性，则还会向身份验证程序注册该值，并带有“ — ”前缀，以将其排除在身份验证要求之外。

#### 身份验证要求的评估和继承 {#evaluation-and-inheritance-of-the-authentication-requirement}

Apache Sling身份验证要求通过页面或节点层次结构继承。 继承和身份验证要求评估的详细信息（如顺序和优先级）被视为实施详细信息，本文中不会记录这些详细信息。

#### 登录路径评估 {#evaluation-of-login-path}

身份验证时登录路径和重定向到相应资源的评估是AdobeGranite登录选择器身份验证处理程序( `com.day.cq.auth.impl.LoginSelectorHandler`)的实现详细信息，该处理程序是默认使用AEM配置的Apache Sling AuthenticationHandler。

在调用`AuthenticationHandler.requestCredentials`时，此处理程序尝试确定用户被重定向到的映射登录页面。 这包括以下步骤：

* 区分过期密码和需要定期登录作为重定向的原因；
* 如果是常规登录，测试是否可以按照以下顺序获取登录路径：

   * 通过新`com.adobe.granite.auth.requirement.impl.RequirementService`实现的LoginPathProvider，
   * 旧的、已弃用的CUG实施中的
   * 从登录页面映射（如`LoginSelectorHandler`所定义），
   * 最后，回退到默认登录页面，如`LoginSelectorHandler`所定义。

* 通过以上列出的调用获得有效的登录路径后，用户的请求将被重定向到该页面。

此文档的目标是对内部`LoginPathProvider`接口所公开的登录路径进行评估。 自AEM 6.3以来发布的实施具有以下行为：

* 登录路径的注册取决于区分过期密码和需要定期登录才能进行重定向
* 如果定期登录，则测试是否可以按照以下顺序获取登录路径：

   * 从`LoginPathProvider`（由新`com.adobe.granite.auth.requirement.impl.RequirementService`实现），
   * 旧的、已弃用的CUG实施中的
   * 通过与`LoginSelectorHandler`一起定义的登录页面映射，
   * 最后回退到使用`LoginSelectorHandler`定义的默认登录页面。

* 通过以上列出的调用获得有效的登录路径后，用户的请求将被重定向到该页面。

由Granite中新的身份验证要求支持实现的`LoginPathProvider`公开由`granite:loginPath`属性定义的登录路径，这些路径又由mixin类型定义，如上所述。 保存登录路径的资源路径与属性值本身的映射将保存在内存中，并且被评估为层次结构中的其他节点找到合适的登录路径。

>[!NOTE]
>
>评估仅针对与位于所配置的支持路径中的资源相关联的请求执行。 对于任何其他请求，将评估确定登录路径的替代方法。

#### 最佳实践 {#best-practices-1}

定义身份验证要求时，应考虑以下最佳实践：

* 避免嵌套身份验证要求：在树的开头放置单个身份验证要求标记应该就足够了，并且可以继承到目标节点定义的整个子树。 应将该树中的其他身份验证要求视为冗余，这可能会导致在评估Apache Sling中的身份验证要求时出现性能问题。 通过分离授权和与验证相关的CUG区域，可以限制CUG或其它类型的策略的读取访问，同时强制对整个树进行验证。
* 对存储库内容进行建模，以便身份验证要求适用于整个树，而无需再次从要求中排除嵌套的子树。
* 要避免指定然后注册冗余登录路径，请执行以下操作：

   * 依赖继承并避免定义嵌套登录路径，
   * 不要将可选登录路径设置为与默认值或继承值对应的值，
   * 应用程序开发人员应确定在与`LoginSelectorHandler`关联的全局登录路径配置（默认和映射）中应配置哪些登录路径。

## 存储库中的表示方式 {#representation-in-the-repository}

### 存储库中的CUG策略表示 {#cug-policy-representation-in-the-repository}

Oak文档介绍了新的CUG策略在存储库内容中的反映方式。 有关详细信息，请参阅[此页面](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository)。

### 存储库中的身份验证要求 {#authentication-requirement-in-the-repository}

将专用mixin节点类型放置在目标节点处的存储库内容中，反映了单独的身份验证要求。 mixin类型定义了一个可选属性，用于为目标节点定义的树指定专用登录页面。

与登录路径关联的页面可以位于该树的内部或外部。 它将被排除在身份验证要求之外。

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## 管理CUG策略和身份验证要求 {#managing-cug-policies-and-authentication-requirement}

### 管理CUG策略 {#managing-cug-policies}

使用JCR访问控制管理API管理用于限制CUG读取访问的新类型的访问控制策略，并遵循[JCR 2.0规范](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html)中描述的机制。

#### 设置新的CUG策略 {#set-a-new-cug-policy}

此代码用于在之前未设置CUG的节点上应用新的CUG策略。 请注意，`getApplicablePolicies`只返回以前未设置的新策略。 最后，必须回写策略并保留更改。

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

AccessControlPolicyIterator it = acMgr.getApplicablePolicies(path);
while (it.hasNext()) {
        AccessControlPolicy policy = it.nextAccessControlPolicy();
        if (policy instanceof PrincipalSetPolicy) {
           cugPolicy = (PrincipalSetPolicy) policy;
           break;
        }
}

if (cugPolicy == null) {
   log.debug("no applicable policy"); // path not supported or no applicable policy (for example,
                                                   // the policy was set before)
   return;
}

cugPolicy.addPrincipals(toAdd1, toAdd2);
cugPolicy.removePrincipals(toRemove));

acMgr.setPolicy(path, cugPolicy); // as of this step the policy can be edited/removed
session.save();
```

#### 编辑现有CUG策略 {#edit-an-existing-cug-policy}

编辑现有CUG策略需要执行以下步骤。 必须回写修改后的策略，并且必须使用`javax.jcr.Session.save()`保留更改。

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
     if (policy instanceof PrincipalSetPolicy) {
        cugPolicy = (PrincipalSetPolicy) policy;
        break;
     }
}

if (cugPolicy == null) {
   log.debug("no policy to edit"); // path not supported or policy not set before
   return;
}

if (cugPolicy.addPrincipals(toAdd1, toAdd2) || cugPolicy.removePrincipals(toRemove)) {
   acMgr.setPolicy(path, cugPolicy);
   session.save();
} else {
     log.debug("cug policy not modified");
}
```

### 检索有效的CUG策略 {#retrieve-effective-cug-policies}

JCR访问控制管理定义了一种尽力而为的方法，用于检索在给定路径上生效的策略。 由于评估CUG策略是有条件的，并且取决于要启用的相应配置，因此调用`getEffectivePolicies`是一种验证给定的CUG策略是否在给定安装中生效的简便方法。

>[!NOTE]
>
>`getEffectivePolicies`与后续代码示例之间的差异，后续代码示例向上遍历层次结构以查找给定路径是否已是现有CUG的一部分。

```java
String path = [...] // needs to be a supported, absolute path

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

// log an debug message of all CUG policies that take effect at the given path
// there could be zero, one or many (creating nested CUGs is possible)
for (AccessControlPolicy policy : acMgr.getEffectivePolicies(path) {
     if (policy instanceof PrincipalSetPolicy) {
        String policyPath = "-";
        if (policy instanceof JackrabbitAccessControlPolicy) {
           policyPath = ((JackrabbitAccessControlPolicy) policy).getPath();
        }
        log.debug("Found effective CUG for path '{}' at '{}', path, policyPath);
     }
}
```

#### 检索继承的CUG策略 {#retrieve-inherited-cug-policies}

查找已在给定路径定义的所有嵌套CUG，无论它们是否生效。 有关详细信息，请参阅[配置选项](/help/sites-administering/closed-user-groups.md#configuration-options)部分。

```java
String path = [...]

List<AccessControlPolicy> cugPolicies = new ArrayList<AccessControlPolicy>();
while (isSupportedPath(path)) {
     for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
         if (policy instanceof PrincipalSetPolicy) {
            cugPolicies.add(policy);
         }
      }
      path = (PathUtils.denotesRoot(path)) ? null : PathUtils.getAncestorPath(path, 1);
}
```

#### 按主体管理CUG策略 {#managing-cug-policies-by-pincipal}

由`JackrabbitAccessControlManager`定义的扩展允许您编辑由主体定义的访问控制策略，这些扩展未使用CUG访问控制管理实施，因为根据定义，CUG策略始终影响所有主体：将授予与`PrincipalSetPolicy`一起列出的主体读取权限，而所有其他主体将阻止读取目标节点定义的树中的内容。

相应方法始终返回空策略数组，但不会引发异常。

### 管理身份验证要求 {#managing-the-authentication-requirement}

通过更改目标节点的有效节点类型来实现新身份验证要求的创建、修改或移除。 然后，可以使用常规JCR API写入可选的登录路径属性。

>[!NOTE]
>
>对上面提到的给定目标节点的修改将仅在`RequirementHandler`已配置并且目标包含在由支持的路径定义的树中时反映在Apache Sling身份验证程序上（请参阅配置选项部分）。
>
>有关详细信息，请参阅[分配Mixin节点类型](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3分配Mixin节点类型)和[添加节点并设置属性](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4添加节点并设置属性)

#### 添加新的身份验证要求 {#adding-a-new-auth-requirement}

创建身份验证要求的步骤详述如下。 仅当为包含目标节点的树配置了`RequirementHandler`时，才会向Apache Sling Authenticator注册此要求。

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### 使用登录路径添加新身份验证要求 {#add-a-new-auth-requirement-with-login-path}

创建包含登录路径的身份验证要求的步骤。 仅当为包含目标节点的树配置了`RequirementHandler`时，才会向Apache Sling身份验证器注册登录路径的要求和排除。

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### 修改现有登录路径 {#modify-an-existing-login-path}

下面详细说明了更改现有登录路径的步骤。 仅当为包含目标节点的树配置了`RequirementHandler`时，修改才会在Apache Sling身份验证器中注册。 先前的登录路径值将从注册中删除。 此修改不会影响与目标节点关联的身份验证要求。

```java
Node targetNode = [...]
String newLoginPath = [...] // STRING property

if (targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", newLoginPath);
   session.save();
} else {
     log.debug("cannot modify login path property; mixin type missing");
}
```

#### 删除现有登录路径 {#remove-an-existing-login-path}

删除现有登录路径的步骤。 仅当为包含目标节点的树配置了`RequirementHandler`时，才会从Apache Sling身份验证器中注销登录路径条目。 不影响与目标节点关联的身份验证要求。

```java
Node targetNode = [...]

if (targetNode.hasProperty("granite:loginPath") &&
   targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", null);
   session.save();
} else {
     log.debug("cannot remove login path property; mixin type missing");
}
```

或者，您也可以使用以下方法来达到相同目的：

```java
String path = [...] // absolute path to target node

String propertyPath = PathUtils.concat(path, "granite:loginPath");
if (session.propertyExists(propertyPath)) {
    session.getProperty(propertyPath).remove();
    // or: session.removeItem(propertyPath);
    session.save();
}
```

#### 删除身份验证要求 {#remove-an-auth-requirement}

删除现有身份验证要求的步骤。 仅当为包含目标节点的树配置了`RequirementHandler`时，才会从Apache Sling身份验证器中取消注册该要求。

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### 检索有效的身份验证要求 {#retrieve-effective-auth-requirements}

没有专用公共API来读取在Apache Sling Authenticator中注册的所有有效身份验证要求。 但是，该列表在`https://<serveraddress>:<serverport>/system/console/slingauth`的系统控制台的“**身份验证要求配置**”部分下显示。

下图显示了包含演示内容的AEM发布实例的身份验证要求。 社区页面中突出显示的路径说明了本文档中描述的实施添加的要求如何反映在Apache Sling身份验证程序中。

>[!NOTE]
>
>在此示例中，未设置可选的登录路径属性。 因此，没有向验证者注册第二个条目。

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### 检索有效登录路径 {#retrieve-the-effective-login-path}

当前没有公共API来检索匿名访问需要身份验证的资源时生效的登录路径。 有关如何检索登录路径的实施详细信息，请参阅登录路径评估部分。

但是，请注意，除了使用此功能定义的登录路径之外，还有其他方法可以指定到登录的重定向，在设计内容模型和给定AEM安装的身份验证要求时，应当考虑这些方法。

#### 检索继承的身份验证要求 {#retrieve-the-inherited-auth-requirement}

与登录路径一样，没有公共API来检索内容中定义的继承身份验证要求。 以下示例说明如何列出使用给定层次结构定义的所有身份验证要求，而不管它们是否生效。 有关详细信息，请参阅[配置选项](/help/sites-administering/closed-user-groups.md#configuration-options)。

>[!NOTE]
>
>建议依赖继承机制来满足身份验证要求和登录路径，并避免创建嵌套身份验证要求。
>
>有关详细信息，请参阅[身份验证要求的评估和继承](#evaluation-and-inheritance-of-the-authentication-requirement)、[登录路径的评估](#evaluation-of-login-path)和[最佳实践](#best-practices)。

```java
String path = [...]
Node node = session.getNode(path);

Map<String, String> authRequirements = new ArrayList<String, String>();
while (isSupported(node)) {
     if (node.isNodeType("granite:AuthenticationRequired")) {
         String loginPath = (node.hasProperty("granite:loginPath") ?
                                     node.getProperty("granite:loginPath").getString() :
                                     "";
        authRequirements.put(node.getPath(), loginPath);
        node = node.getParent();
     }
}
```

### 将CUG策略和身份验证要求相结合 {#combining-cug-policies-and-the-authentication-requirement}

下表列出了AEM实例中CUG策略的有效组合以及身份验证要求，该实例通过配置启用了这两个模块。

| **需要身份验证** | **登录路径** | **已限制读取访问** | **预期效果** |
|---|---|---|---|
| 是 | 是 | 是 | 如果有效的权限评估授予访问权限，给定用户将只能查看标记为CUG策略的子树。 未经身份验证的用户将被重定向到指定的登录页面。 |
| 是 | 否 | 是 | 如果有效的权限评估授予访问权限，给定用户将只能查看标记为CUG策略的子树。 未经身份验证的用户将被重定向到继承的默认登录页面。 |
| 是 | 是 | 否 | 未经身份验证的用户将被重定向到指定的登录页面。 是否允许查看标有身份验证要求的树取决于该子树中包含的个别项的有效权限。 没有专用的CUG限制读取访问。 |
| 是 | 否 | 否 | 未经身份验证的用户将被重定向到继承的默认登录页面。 是否允许查看标记有身份验证要求的树，取决于该子树中包含的各个项目的有效权限。 没有专用的CUG限制读取访问。 |
| 否 | 否 | 是 | 如果有效的权限评估授予访问权限，则给定的经过身份验证或未经过身份验证的用户只能查看使用CUG策略标记的子树。 未经身份验证的用户得到同等对待，不会被重定向到登录。 |

>[!NOTE]
>
>“Authentication Requirement”=“No”和“Login Path”=“Yes”的组合未列出，因为“Login Path”是与Auth-Requirement关联的可选属性。 使用该名称指定JCR属性而不添加定义mixin类型没有效果，并且被相应的处理程序忽略。

## OSGi组件和配置 {#osgi-components-and-configuration}

本节概述了OSGi组件以及新的CUG实施中引入的各个配置选项。

另请参阅CUG映射文档，以全面映射旧实施和新实施之间的配置选项。

### 授权：设置和配置 {#authorization-setup-and-configuration}

新的授权相关部件包含在&#x200B;**Oak CUG Authorization**&#x200B;包(`org.apache.jackrabbit.oak-authorization-cug`)中，它是AEM默认安装的一部分。 该捆绑包定义了一个单独的授权模型，旨在作为管理读取访问权限的附加方式部署。

#### 设置CUG授权 {#setting-up-cug-authorization}

[相关Apache文档](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)中详细描述了设置CUG授权。 默认情况下，AEM在所有运行模式下都部署了CUG授权。 分步说明还可用于在那些需要不同的授权设置的安装中禁用CUG授权。

#### 配置反向链接过滤器 {#configuring-the-referrer-filter}

您还必须使用所有可用于访问AEM的主机名配置[Sling反向链接筛选器](/help/sites-administering/security-checklist.md#the-sling-referrer-filter)；例如，通过CDN、负载平衡器和任何其他方式。

如果未配置反向链接筛选条件，则当用户尝试登录CUG网站时，会看到与以下内容类似的错误：

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### OSGi组件的特性 {#characteristics-of-osgi-components}

引入了以下两个OSGi组件来定义身份验证要求并指定专用登录路径：

* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration`
* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl`

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration**

<table>
 <tbody>
  <tr>
   <td>标签</td>
   <td>Apache Jackrabbit Oak CUG配置</td>
  </tr>
  <tr>
   <td>描述</td>
   <td>专门用于设置和评估CUG权限的授权配置。</td>
  </tr>
  <tr>
   <td>配置属性</td>
   <td>
    <ul>
     <li><code>cugSupportedPaths</code></li>
     <li><code>cugEnabled</code></li>
     <li><code>configurationRanking</code></li>
    </ul> <p>另请参阅下面的<a href="#configuration-options">配置选项</a>。</p> </td>
  </tr>
  <tr>
   <td>配置策略</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>引用</td>
   <td><code>CugExclude (ReferenceCardinality.OPTIONAL_UNARY)</code></td>
  </tr>
 </tbody>
</table>

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl**

<table>
 <tbody>
  <tr>
   <td>标签</td>
   <td>Apache Jackrabbit Oak CUG排除列表</td>
  </tr>
  <tr>
   <td>描述</td>
   <td>允许您从CUG评估中排除具有已配置名称的主体。</td>
  </tr>
  <tr>
   <td>配置属性</td>
   <td>
    <ul>
     <li><code>principalNames</code></li>
    </ul> <p>另请参阅下面的配置选项部分。</p> </td>
  </tr>
  <tr>
   <td>配置策略</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>引用</td>
   <td>NA</td>
  </tr>
 </tbody>
</table>

#### 配置选项 {#configuration-options}

关键配置选项包括：

* `cugSupportedPaths`：指定可能包含CUG的子树。 未设置默认值
* `cugEnabled`：配置选项，用于启用当前CUG策略的权限评估。

在[Apache Oak文档](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration)中列出并详细描述了与CUG授权模块关联的可用配置选项。

#### 从CUG评估中排除承担者 {#excluding-principals-from-cug-evaluation}

在前一实施中，已采用免除个人主参与者的CUG评估。 新的CUG授权通过名为CugExclude的专用接口覆盖这一点。 Apache Jackrabbit Oak 1.4附带默认实施，该实施不包括固定主体集和扩展实施，后者允许您配置各个主体名称。 后者在AEM发布实例中配置。

自AEM 6.3起的默认设置可防止以下主体受CUG策略的影响：

* 管理主体（管理员用户、管理员组）
* 服务用户主体
* 存储库内部系统主体

有关详细信息，请参阅下面[自AEM 6.3](#default-configuration-since-aem)以来的默认配置部分中的表。

可以在&#x200B;**Apache Jackrabbit Oak CUG Exclude List**&#x200B;的配置部分的System Console中更改或扩展“管理员”组的排除。

或者，可以提供并部署CugExclude接口的自定义实现，以调整排除的承担者集（如果存在特殊需求）。 有关详细信息和实施示例，请参阅有关[CUG可插性](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)的文档。

### 身份验证：设置和配置 {#authentication-setup-and-configuration}

新的身份验证相关部分包含在&#x200B;**AdobeGranite身份验证处理程序**&#x200B;捆绑包（`com.adobe.granite.auth.authhandler`版本5.6.48）中。 此捆绑包是AEM默认安装的一部分。

要设置身份验证要求以取代已弃用的CUG支持，某些OSGi组件必须在给定AEM安装中存在并处于活动状态。 有关详细信息，请参阅下面的&#x200B;**OSGi组件的特性**。

>[!NOTE]
>
>由于RequirementHandler具有强制配置选项，因此，仅当通过指定一组受支持的路径来启用该功能时，与身份验证相关的部分才会处于活动状态。 在标准AEM安装中，该功能在创作运行模式下禁用，在发布运行模式下为/content启用。

**OSGi组件的特性**

引入了以下两个OSGi组件来定义身份验证要求并指定专用登录路径：

* `com.adobe.granite.auth.requirement.impl.RequirementService`
* `com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler`

**com.adobe.granite.auth.requirement.impl.RequirementService**

<table>
 <tbody>
  <tr>
   <td>标签</td>
   <td>-</td>
  </tr>
  <tr>
   <td>描述</td>
   <td>用于身份验证要求的专用OSGi服务，为影响身份验证要求的内容更改注册观察者（通过<code>granite:AuthenticationRequirement</code> mixin类型）和的登录路径对<code>LoginSelectorHandler</code>公开。 </td>
  </tr>
  <tr>
   <td>配置属性</td>
   <td>-</td>
  </tr>
  <tr>
   <td>配置策略</td>
   <td><code>ConfigurationPolicy.OPTIONAL</code></td>
  </tr>
  <tr>
   <td>引用</td>
   <td>
    <ul>
     <li><code>RequirementHandler (ReferenceCardinality.MANDATORY_UNARY)</code></li>
     <li><code>Executor (ReferenceCardinality.MANDATORY_UNARY)</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

**com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler**

| 标签 | AdobeGranite身份验证要求和登录路径处理程序 |
|---|---|
| 描述 | `RequirementHandler`实施，用于更新Apache Sling身份验证要求和相关登录路径的相应排除项。 |
| 配置属性 | `supportedPaths` |
| 配置策略 | `ConfigurationPolicy.REQUIRE` |
| 引用 | NA |

#### 配置选项 {#configuration-options-1}

CUG重写的身份验证相关部分只附带一个与AdobeGranite身份验证要求和登录路径处理程序关联的配置选项：

**“身份验证要求和登录路径处理程序”**

<table>
 <tbody>
  <tr>
   <td>属性</td>
   <td>类型</td>
   <td>默认值</td>
   <td>描述</td>
  </tr>
  <tr>
   <td><p>标签=支持的路径</p> <p>名称= 'supportedPaths'</p> </td>
   <td>Set&lt;字符串&gt;</td>
   <td>-</td>
   <td>此处理程序将遵循身份验证要求的路径。 如果要将<code>granite:AuthenticationRequirement</code> mixin类型添加到节点而不强制实施它们（例如，在创作实例上），请将此配置保留为未设置。 如果缺少，则禁用该功能。 </td>
  </tr>
 </tbody>
</table>

## 自AEM 6.3以来的默认配置 {#default-configuration-since-aem}

默认情况下，新安装的AEM将新实施用于CUG功能的授权和与身份验证相关的部分。 旧实施“AdobeGranite封闭用户组(CUG)支持”已被弃用，并将在所有AEM安装中默认禁用。 新的实施将改为按以下方式启用：

### 创作实例 {#author-instances}

| **“Apache Jackrabbit Oak CUG配置”** | **解释** |
|---|---|
| 支持的路径`/content` | 已启用CUGpolicies的访问控制管理。 |
| CUG评估启用FALSE | 已禁用权限评估。 CUG政策不起作用。 |
| 等级 | 200 | 请参阅Oak文档。 |

>[!NOTE]
>
>默认创作实例上不存在&#x200B;**Apache Jackrabbit Oak CUG排除列表**&#x200B;和&#x200B;**AdobeGranite身份验证要求和登录路径处理程序**&#x200B;的配置。

### Publish实例 {#publish-instances}

| **“Apache Jackrabbit Oak CUG配置”** | **解释** |
|---|---|
| 支持的路径`/content` | 在配置的路径下启用了CUG策略的访问控制管理。 |
| CUG评估已启用TRUE | 在配置的路径下启用了权限评估。 CUG策略于`Session.save()`生效。 |
| 等级 | 200 | 请参阅Oak文档。 |

| **“Apache Jackrabbit Oak CUG排除列表”** | **解释** |
|---|---|
| 主体名称管理员 | 不包括CUG评估中的管理员主体。 |

| **“AdobeGranite身份验证要求和登录路径处理程序”** | **解释** |
|---|---|
| 支持的路径`/content` | `granite:AuthenticationRequired` mixin类型在存储库中定义的身份验证要求在`Session.save()`后`/content`内生效。 Sling身份验证器已更新。 在支持的路径之外添加mixin类型会被忽略。 |

## 禁用CUG授权和身份验证要求 {#disabling-cug-authorization-and-authentication-requirement}

如果给定的安装不使用CUG或使用不同的身份验证和授权方式，则可能完全禁用新实施。

### 禁用CUG授权 {#disable-cug-authorization}

有关如何从复合授权设置中删除CUG授权模型的详细信息，请参阅[CUG可插拔性](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)文档。

### 禁用身份验证要求 {#disable-the-authentication-requirement}

要禁用`granite.auth.authhandler`模块提供的对身份验证要求的支持，只需删除与&#x200B;**AdobeGranite身份验证要求和登录路径处理程序**&#x200B;关联的配置即可。

>[!NOTE]
>
>但请注意，删除配置将不会取消注册mixin类型，该类型仍适用于未生效的节点。

## 与其他模块的交互 {#interaction-with-other-modules}

### Apache Jackrabbit API {#apache-jackrabbit-api}

为了反映CUG授权模型使用的新类型的访问控制策略，对Apache Jackrabbit定义的API进行了扩展。 由于`jackrabbit-api`模块的2.11.0版本定义了一个名为`org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`的新接口，该接口从`javax.jcr.security.AccessControlPolicy`扩展。

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

已调整Apache Jackrabbit FileVault的导入机制，以处理`PrincipalSetPolicy`类型的访问控制策略。

### Apache Sling内容分发 {#apache-sling-content-distribution}

请参阅上述[Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault)部分。

### AdobeGranite复制 {#adobe-granite-replication}

复制模块已进行了稍微调整，以便能够在不同的AEM实例之间复制CUG策略：

* `DurboImportConfiguration.isImportAcl()`按字面解释，将仅影响实施`javax.jcr.security.AccessControlList`的访问控制策略

* `DurboImportTransformer`将只对真正的ACL遵守此配置
* 将始终复制由CUG授权模型创建的其他策略（如`org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`实例），并忽略配置选项`DurboImportConfiguration.isImportAcl`()。

复制CUG策略有一个限制。 如果未删除相应的mixin节点类型`rep:CugMixin,`就删除了给定的CUG策略，则在复制时将不会反映此删除。 通过在删除策略时始终删除mixin解决了此问题。 但是，如果手动添加mixin类型，则可能会显示此限制。

### AdobeGranite身份验证处理程序 {#adobe-granite-authentication-handler}

随`com.adobe.granite.auth.authhandler`捆绑包提供的身份验证处理程序&#x200B;**AdobeGranite HTTP标头身份验证处理程序**&#x200B;包含对同一模块定义的`CugSupport`接口的引用。 它用于在特定情况下计算“领域”，回退到使用处理程序配置的领域。

已调整此参数，使对`CugSupport`的引用成为可选参数，以确保在给定设置决定重新启用已弃用的实现时实现最大程度的向后兼容性。 使用该实现的安装将不再获得从CUG实现提取的领域，但将始终显示使用&#x200B;**AdobeGranite HTTP标头身份验证处理程序**&#x200B;定义的领域。

>[!NOTE]
>
>默认情况下，**AdobeGranite HTTP标头身份验证处理程序**&#x200B;仅在启用“禁用登录页面”(`auth.http.nologin`)选项的发布运行模式下进行配置。

### AEM LiveCopy {#aem-livecopy}

在存储库中，使用LiveCopy配置CUG时添加了一个额外的节点和一个额外的属性，如下所示：

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

这两个元素均在`cq:Page`下创建。 使用当前设计，MSM仅处理`cq:PageContent` (`jcr:content`)节点下的节点和属性。

因此，CUG组无法从Blueprint转出到Live Copies。 在配置Live Copy时对此进行规划。

## 对新的CUG实施进行的更改 {#changes-with-the-new-cug-implementation}

本节旨在概述对CUG功能所做的更改，并比较新旧实施。 其中列出了影响CUG支持配置方式的更改，并描述了在存储库内容中如何以及谁管理CUG。

### CUG设置和配置的差异 {#differences-in-cug-setup-and-configuration}

已弃用的OSGi组件&#x200B;**AdobeGranite封闭用户组(CUG)支持** (`com.day.cq.auth.impl.cug.CugSupportImpl`)已被新组件替换，以便能够单独处理以前CUG功能的授权和身份验证相关部分。

## 管理存储库内容中的CUG的区别 {#differences-in-managing-cugs-in-the-repository-content}

以下各节从实施和安全角度介绍了新旧实施之间的差异。 虽然新实施旨在提供相同的功能，但在使用新CUG时，务必要了解一些细微的变化。

### 与授权有关的差异 {#differences-with-regards-to-authorization}

授权方面的主要区别概述于以下列表：

**CUG的专用访问控制内容**

在旧实施中，默认授权模型用于处理发布时的访问控制列表策略，按照CUG要求的设置替换任何现有的ACE。 触发此问题的方法是，编写在发布时解释的常规、剩余JCR属性。

在新实施中，默认授权模型的访问控制设置不受任何正在创建、修改或删除的CUG的影响。 而是将名为`PrincipalSetPolicy`的新策略类型作为其他访问控制内容应用到目标节点。 此附加策略位于目标节点的子节点中，如果存在，则将成为默认策略节点的同级。

**在访问控制管理中编辑CUG策略**

从剩余的JCR属性迁移到专用的访问控制策略会影响创建或修改CUG功能的授权部分所需的权限。 由于这被视为对访问控制内容的修改，因此需要将`jcr:readAccessControl`和`jcr:modifyAccessControl`权限写入存储库。 因此，只有有权修改页面的访问控制内容的内容作者才能设置或修改此内容。 这与旧实施形成对比，旧实施写入常规JCR属性的能力已经足够，从而导致权限提升。

**由策略定义的目标节点**

在JCR节点创建CUG策略，定义子树要接受受限读取访问。 如果预计CUG会影响整个树，则这可能是一个AEM页面。

仅将CUG策略放在位于给定页面下方的jcr：content节点上，只会限制对给定页面内容s.str的访问，而不会对任何同级页面或子页面生效。 这可能是有效的用例，可以使用存储库编辑器实现，该编辑器允许您应用细粒度访问内容。 但是，它与以前的实施形成了对比，以前的实施是在jcr：content节点上放置cq：cugEnabled属性时，将内部重新映射到页面节点。 不再执行此映射。

使用CUG策略&#x200B;**权限评估**

从旧的CUG支持迁移到额外的授权模型，改变了评估有效读取权限的方式。 如[Jackrabbit文档](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)中所述，仅当Oak存储库中配置的所有模型的权限评估授予读取权限时，才向允许查看`CUGcontent`的给定主体授予读取权限。

换言之，为了评估有效权限，`CUGPolicy`和默认访问控制条目都将被考虑在内，并且只有在这两种策略都授予了CUG内容的情况下，才会授予对该内容的读取访问权限。 在默认AEM发布安装中，向所有人授予对完整`/content`树的读取权限，CUG策略的效果与旧实施相同。

**按需评估**

CUG授权模型允许您单独打开访问控制管理和权限评估：

* 如果模块具有一个或多个支持创建CUG的路径，则会启用访问控制管理
* 仅当同时选中选项&#x200B;**CUG Evaluation Enabled**&#x200B;时才启用权限评估。

在对CUG策略进行的新的AEM默认设置评估中，仅在“发布”运行模式下启用它。 有关更多详细信息，请参阅AEM 6.3](#default-configuration-since-aem)之后的[默认配置的详细信息。 这可以通过比较给定路径的有效策略与内容中存储的策略来验证。 只有启用CUG的权限评估后，才会显示有效的策略。

如上所述，CUG访问控制策略现在始终存储在内容中，但是只有在Apache Jackrabbit Oak **CUG配置的系统控制台中打开**&#x200B;启用CUG评估&#x200B;**，才会强制评估由这些策略产生的有效权限。**&#x200B;默认情况下，仅在“发布”运行模式下启用它。

### 与身份验证有关的差异 {#differences-with-regards-to-authentication}

下面介绍了有关身份验证的差异。

#### 身份验证要求的专用Mixin类型 {#dedicated-mixin-type-for-authentication-requirement}

在以前的实现中，CUG的授权和身份验证方面均由单个JCR属性( `cq:cugEnabled`)触发。 就身份验证而言，这导致更新了随Apache Sling Authenticator实施一起存储的身份验证要求列表。 使用新实施时，使用专用的mixin类型( `granite:AuthenticationRequired`)标记目标节点可获得相同的结果。

#### 用于排除登录路径的属性 {#property-for-excluding-login-path}

mixin类型定义了一个名为`granite:loginPath`的可选属性，该属性基本上与`cq:cugLoginPage`属性相对应。 与以前的实现不同，登录路径属性仅在其声明节点类型是上面提到的mixin时才被考虑。 添加具有该名称的属性而不设置mixin类型不会产生任何效果，并且不会向验证者报告对登录路径的新要求或排除项。

#### 身份验证要求的权限 {#privilege-for-authentication-requirement}

添加或删除mixin类型需要授予`jcr:nodeTypeManagement`权限。 在上一个实现中，`jcr:modifyProperties`权限用于编辑剩余属性。

就`granite:loginPath`而言，添加、修改或删除属性需要相同的权限。

#### 由Mixin类型定义的目标节点 {#target-node-defined-by-mixin-type}

在JCR节点创建身份验证要求，定义要强制登录的子树。 如果预计CUG会影响整个树，则这可能是AEM页面，因此新实施的UI会在页面节点上添加身份验证要求mixin类型。

仅将CUG策略放置在位于给定页面下方的jcr：content节点上，只会限制对内容的访问。 但是，它不会影响页面节点本身，也不会影响任何子页面。

这可能是有效的方案，并且可以通过存储库编辑器将mixin放置在任何节点上。 但是，该行为与以前的实施相反，在前一种实施中，对jcr：content节点放置cq：cugEnabled或cq：cugLoginPage属性最终会在内部重新映射到页面节点。 不再执行此映射。

#### 已配置支持的路径 {#configured-supported-paths}

`granite:AuthenticationRequired` mixin类型和granite：loginPath属性仅在由&#x200B;**AdobeGranite身份验证要求和登录路径处理程序**&#x200B;的&#x200B;**受支持的路径**&#x200B;配置选项集定义的范围内受尊重。 如果未指定路径，则身份验证要求功能将完全禁用。 在这种情况下，将mixin类型nor属性添加到给定JCR节点或对其进行设置时，它们将生效。

### JCR内容、OSGi服务和配置的映射 {#mapping-of-jcr-content-osgi-services-and-configurations}

以下文档提供了旧实施与新实施之间的OSGi服务、配置和存储库内容的全面映射。

AEM 6.3之后的CUG映射

[获取文件](assets/cug-mapping.pdf)

## 升级CUG {#upgrade-cug}

### 使用已弃用CUG的现有安装 {#existing-installations-using-the-deprecated-cug}

旧的CUG支持实施已弃用，并将在未来版本中删除。 从AEM 6.3之前的版本升级时，建议迁移到新实施。

对于升级后的AEM安装，请务必确保仅启用一个CUG实施。 新旧弃用的CUG支持组合未经测试，并且可能会导致意外行为：

* Sling身份验证程序中与身份验证要求相关的冲突
* 当与旧CUG关联的ACL设置与新CUG策略冲突时，拒绝读取访问。

### 迁移现有CUG内容 {#migrating-existing-cug-content}

Adobe提供了迁移到新的CUG实施的工具。 要使用它，请执行以下步骤：

1. 转到`https://<serveraddress>:<serverport>/system/console/cug-migration`以访问该工具。
1. 输入要检查CUG的根路径，然后按&#x200B;**执行试运行**&#x200B;按钮。 这将扫描选定位置中符合转换条件的CUG。
1. 查看结果后，按&#x200B;**执行迁移**&#x200B;按钮以迁移到新实施。

>[!NOTE]
>
>如果遇到问题，可以在`com.day.cq.auth.impl.cug`上的&#x200B;**DEBUG**&#x200B;级别设置特定记录器以获取迁移工具的输出。 有关如何执行此操作的详细信息，请参阅[日志记录](/help/sites-deploying/configure-logging.md)。
