---
title: 扩展多站点管理器
seo-title: 扩展多站点管理器
description: 本页可帮助您扩展多站点管理器的功能
seo-description: 本页可帮助您扩展多站点管理器的功能
uuid: dfa7d050-29fc-4401-8d4d-d6ace6b49bea
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6128c91a-4173-42b4-926f-bbbb2b54ba5b
docset: aem65
exl-id: bba64ce6-8b74-4be1-bf14-cfdf3b9b60e1
source-git-commit: 6bc228866aca785ec768daefb73970fc24568ef0
workflow-type: tm+mt
source-wordcount: '2601'
ht-degree: 2%

---

# 扩展多站点管理器{#extending-the-multi-site-manager}

本页可帮助您扩展多站点管理器的功能：

* 了解MSM Java API的主要成员。
* 创建可在转出配置中使用的新同步操作。
* 修改默认语言和国家/地区代码。

<!-- * Remove the "Chapters" step in the Create Site wizard. -->

>[!NOTE]
>
>本页应结合[重用内容一起阅读：多站点管理器](/help/sites-administering/msm.md)。
>
>AEM 6.4中的站点存储库重组的以下部分可能也值得关注：
>* [多站点管理器Blueprint配置](https://docs.adobe.com/content/help/en/experience-manager-64/deploying/restructuring/sites-repository-restructuring-in-aem-6-4.html#multi-site-manager-blueprint-configurations)
>* [多站点管理器转出配置](https://docs.adobe.com/content/help/en/experience-manager-64/deploying/restructuring/sites-repository-restructuring-in-aem-6-4.html#multi-site-manager-rollout-configurations)


>[!CAUTION]
>
>创作网站时会使用多站点管理器及其API，因此这些管理器仅用于在创作环境中使用。

## Java API概述 {#overview-of-the-java-api}

多站点管理包含以下包：

* [com.day.cq.wcm.msm.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/package-frame.html)
* [com.day.cq.wcm.msm.commons](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/commons/package-frame.html)

主MSM API对象交互如下（另请参阅[使用的术语](/help/sites-administering/msm.md#terms-used)）：

![chlimage_1-73](assets/chlimage_1-73.png)

* **`Blueprint`**

   `Blueprint`（如[blueprint配置](/help/sites-administering/msm.md#source-blueprints-and-blueprint-configurations)中所示）指定Live Copy可从中继承内容的页面。

   ![chlimage_1-74](assets/chlimage_1-74.png)

   * Blueprint配置(`Blueprint`)的使用是可选的，但是：

      * 允许作者在源上使用&#x200B;**转出**&#x200B;选项(以（显式）将修改推送到从此源继承的Live Copy)。
      * 允许作者使用&#x200B;**Create Site**;这允许用户轻松选择语言并配置Live Copy的结构。
      * 为任何生成的Live Copy定义默认转出配置。

* **`LiveRelationship`**

   `LiveRelationship`指定Live Copy分支中的资源与其等效源/Blueprint资源之间的连接（关系）。

   * 在实现继承和转出时会使用关系。
   * `LiveRelationship` 对象提供对转出配置( `RolloutConfig`)、和与关系相 `LiveCopy`关的 `LiveStatus` 对象的访问（引用）。

   * 例如，在`/content/copy/us`中，从`/content/we-retail/language-masters`的源/Blueprint创建Live Copy。 资源`/content/we.retail/language-masters/en/jcr:content`和`/content/copy/us/en/jcr:content`形成关系。

* **`LiveCopy`**

   `LiveCopy` 保存Live Copy资源与其源/Blueprint资源之间关系( `LiveRelationship`)的配置详细信息。

   * 使用`LiveCopy`类可访问页面的路径、源/Blueprint页面的路径、转出配置以及子页面是否也包含在`LiveCopy`中。

   * 每次使用&#x200B;**创建站点**&#x200B;或&#x200B;**创建Live Copy**&#x200B;时，都会创建`LiveCopy`节点。

* **`LiveStatus`**

   `LiveStatus` 对象提供对的运行时状态的访 `LiveRelationship`问。使用查询Live Copy的同步状态。

* **`LiveAction`**

   `LiveAction`是对转出中涉及的每个资源执行的操作。

   * LiveActions仅由RolloutConfigs生成。

* **`LiveActionFactory`**

   创建`LiveAction`对象（给定`LiveAction`配置）。 配置作为资源存储在存储库中。

* **`RolloutConfig`**

   `RolloutConfig`包含要在触发时使用的`LiveActions`列表。 `LiveCopy`继承`RolloutConfig`，结果出现在`LiveRelationship`中。

   * 首次设置Live Copy时还会使用RolloutConfig（这会触发LiveActions）。

## 创建新的同步操作 {#creating-a-new-synchronization-action}

创建要与转出配置一起使用的自定义同步操作。 当[已安装的操作](/help/sites-administering/msm-sync.md#installed-synchronization-actions)不符合您的特定应用程序要求时，创建同步操作。 为此，请创建两个类：

* 执行操作的[ `com.day.cq.wcm.msm.api.LiveAction`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveAction.html)接口的实现。
* 实现[ `com.day.cq.wcm.msm.api.LiveActionFactory`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html)接口并创建`LiveAction`类实例的OSGi组件。

`LiveActionFactory`为给定配置创建`LiveAction`类的实例：

* `LiveAction` 类包括以下方法：

   * `getName`:返回操作的名称该名称用于引用操作，例如在转出配置中。
   * `execute`:执行操作的任务。

* `LiveActionFactory` 类包括以下成员：

   * `LIVE_ACTION_NAME`:包含关联名称的字段 `LiveAction`。此名称必须与`LiveAction`类的`getName`方法返回的值一致。

   * `createAction`:创建的实例 `LiveAction`。可选的`Resource`参数可用于提供配置信息。

   * `createsAction`:返回关联的名称 `LiveAction`。

### 访问LiveAction配置节点 {#accessing-the-liveaction-configuration-node}

在存储库中使用`LiveAction`配置节点存储影响`LiveAction`实例运行时行为的信息。 存储`LiveAction`配置的存储库中的节点在运行时可用于`LiveActionFactory`对象。 因此，您可以向配置节点添加属性，并根据需要在`LiveActionFactory`实施中使用这些属性。

例如，`LiveAction`需要存储Blueprint作者的名称。 配置节点的属性包括用于存储信息的Blueprint页面的属性名称。 在运行时， `LiveAction`从配置中检索属性名称，然后获取属性值。

` [LiveActionFactory](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html).createAction`方法的参数是`Resource`对象。 此`Resource`对象表示转出配置中此实时操作的`cq:LiveSyncAction`节点；请参阅[创建转出配置](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration)。 与使用配置节点时的常规情况一样，您应将其调整为`ValueMap`对象：

```java
public LiveAction createAction(Resource resource) throws WCMException {
        ValueMap config;
        if (resource == null || resource.adaptTo(ValueMap.class) == null) {
            config = new ValueMapDecorator(Collections.<String, Object>emptyMap());
        } else {
            config = resource.adaptTo(ValueMap.class);
        }
        return new MyLiveAction(config, this);
}
```

### 访问目标节点、源节点和LiveRelationship {#accessing-target-nodes-source-nodes-and-the-liverelationship}

以下对象作为`LiveAction`对象的`execute`方法的参数提供：

* 表示Live Copy源的[ `Resource`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html)对象。
* 表示Live Copy目标的`Resource`对象。
* Live Copy的[ `LiveRelationship`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html)对象。
* `autoSave`值指示您的`LiveAction`是否应保存对存储库所做的更改。

* 重置值表示转出重置模式。

从这些对象中，可以获取有关`LiveCopy`的所有信息。 您还可以使用`Resource`对象获取`ResourceResolver`、`Session`和`Node`对象。 这些对象可用于处理存储库内容：

在以下代码的第一行中，源是源页面的`Resource`对象：

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>`Resource`参数可以是不适应`Node`对象的`null`或`Resources`对象，如[ `NonExistingResource`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/NonExistingResource.html)对象。

## 创建新转出配置 {#creating-a-new-rollout-configuration}

当安装的转出配置不符合您的应用程序要求时，创建转出配置：

* [创建转出配置](#create-the-rollout-configuration)。
* [向转出配置添加同步操作](#add-synchronization-actions-to-the-rollout-configuration)。

在 Blueprint 或 Live Copy 页面上设置转出配置时，您可以使用该新转出配置。

>[!NOTE]
>
>另请参阅自定义转出的[最佳实践](/help/sites-administering/msm-best-practices.md#customizing-rollouts)。

### 创建转出配置 {#create-the-rollout-configuration}

要创建新的转出配置，请执行以下操作：

1. 开放CRXDE Lite;例如：
   [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. 导航至 :
   `/apps/msm/<your-project>/rolloutconfigs`

   >[!NOTE]
   >这是您项目的自定义版本：
   >`/libs/msm/wcm/rolloutconfigs`
   >如果这是您的第一个配置，则必须创建。

   >[!NOTE]
   >
   >您不得更改/libs路径中的任何内容。
   >这是因为/libs的内容在您下次升级实例时被覆盖（而且当您应用修补程序或功能包时，很可能会被覆盖）。
   >配置和其他更改的推荐方法是：
   >* 在/apps下重新创建所需项（即/libs中存在的项）
   >* 在/apps中进行任何更改


1. 在此&#x200B;**Create**&#x200B;下，创建具有以下属性的节点：

   * **名称**:转出配置的节点名称。md#installed-synchronization-actions)，例如`contentCopy`或`workflow`。
   * **类型**: `cq:RolloutConfig`

1. 将以下属性添加到此节点：
   * **名称**: `jcr:title`

      **类型**: `String`
      **值**:将在UI中显示的标识标题。
   * **名称**: `jcr:description`

      **类型**: `String`
      **值**:可选描述。
   * **名称**: `cq:trigger`

      **类型**: `String`
      **值**:要使 [用的](/help/sites-administering/msm-sync.md#rollout-triggers) 转出触发器。从以下位置选择：
      * `rollout`
      * `modification`
      * `publish`
      * `deactivate`

1. 单击&#x200B;**Save All**。

### 将同步操作添加到转出配置 {#add-synchronization-actions-to-the-rollout-configuration}

转出配置存储在您在`/apps/msm/<your-project>/rolloutconfigs`节点下创建的[转出配置节点](#create-the-rollout-configuration)下。

添加类型为`cq:LiveSyncAction`的子节点，以向转出配置添加同步操作。 同步操作节点的顺序决定了操作的执行顺序。

1. 仍在CRXDE Lite中，选择[转出配置](#create-the-rollout-configuration)节点。

   例如：
   `/apps/msm/myproject/rolloutconfigs/myrolloutconfig`

1. **** 创建具有以下节点属性的节点：

   * **名称**:同步操作的节点名称。该名称必须与[Synchronization Actions](/help/sites-administering/msm-sync.md#installed-synchronization-actions)下表中的&#x200B;**Action Name**&#x200B;相同，例如`contentCopy`或`workflow`。
   * **类型**: `cq:LiveSyncAction`

1. 根据需要添加和配置任意数量的同步操作节点。 重新排列操作节点，使其顺序与您希望其发生的顺序匹配。 最顶层的操作节点首先出现。

## 创建和使用简单的LiveActionFactory类 {#creating-and-using-a-simple-liveactionfactory-class}

按照此部分中的步骤开发`LiveActionFactory`并将其用于转出配置。 这些过程使用Maven和Eclipse来开发和部署`LiveActionFactory`:

1. [创建Maven项](#create-the-maven-project) 目并将其导入Eclipse。
1. [将依](#add-dependencies-to-the-pom-file) 赖项添加到POM文件。
1. [实施接 `LiveActionFactory` ](#implement-liveactionfactory) 口并部署OSGi包。
1. [创建转出配置](#create-the-example-rollout-configuration)。
1. [创建Live Copy](#create-the-live-copy)。

Maven项目和Java类的源代码可在公共Git存储库中使用。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开experiencemanager-java-msmrollout项目](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout)
* 将项目下载为[a ZIP文件](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout/archive/master.zip)

### 创建Maven项目 {#create-the-maven-project}

以下过程要求您将adobe-public配置文件添加到Maven设置文件。

* 有关adobe-public配置文件的信息，请参阅[获取内容包Maven插件](/help/sites-developing/vlt-mavenplugin.md#obtaining-the-content-package-maven-plugin)
* 有关Maven设置文件的信息，请参阅Maven [设置引用](https://maven.apache.org/settings.html)。

1. 打开终端或命令行会话并更改目录以指向创建项目的位置。
1. 输入以下命令：

   ```xml
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. 在交互提示时指定以下值：

   * `groupId`: `com.adobe.example.msm`
   * `artifactId`:  `MyLiveActionFactory`
   * `version`:  `1.0-SNAPSHOT`
   * `package`:  `MyPackage`
   * `appsFolderName`:  `myapp`
   * `artifactName`:  `MyLiveActionFactory package`
   * `packageGroup`:  `myPackages`

1. 启动Eclipse并[导入Maven项目](/help/sites-developing/howto-projects-eclipse.md#import-the-maven-project-into-eclipse)。

### 将依赖项添加到POM文件 {#add-dependencies-to-the-pom-file}

添加依赖项，以便Eclipse编译器可以引用`LiveActionFactory`代码中使用的类。

1. 从Eclipse项目资源管理器中，打开文件：

   `MyLiveActionFactory/pom.xml`

1. 在编辑器中，单击`pom.xml`选项卡，并找到`project/dependencyManagement/dependencies`部分。
1. 在`dependencyManagement`元素内添加以下XML，然后保存文件。

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
     <version>5.6.2</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
     <version>2.4.3-R1488084</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
     <version>5.6.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
     <version>2.0.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
     <version>2.0.0</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
   ```

1. 从&#x200B;**项目资源管理器**&#x200B;的`MyLiveActionFactory-bundle/pom.xml`打开包的POM文件。
1. 在编辑器中，单击`pom.xml`选项卡，并找到项目/依赖项部分。 在依赖关系元素中添加以下XML，然后保存文件：

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
   ```

### 实施LiveActionFactory {#implement-liveactionfactory}

以下`LiveActionFactory`类实现一个`LiveAction`，用于记录有关源页面和目标页面的消息，并将`cq:lastModifiedBy`属性从源节点复制到目标节点。 实时操作的名称为`exampleLiveAction`。

1. 在Eclipse项目资源管理器中，右键单击`MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm`包，然后单击&#x200B;**新建** > **类**。 对于&#x200B;**名称**，输入`ExampleLiveActionFactory`，然后单击&#x200B;**完成**。
1. 打开`ExampleLiveActionFactory.java`文件，使用以下代码替换内容，然后保存该文件。

   ```java
   package com.adobe.example.msm;
   
   import java.util.Collections;
   
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.Resource;
   import org.apache.sling.api.resource.ResourceResolver;
   import org.apache.sling.api.resource.ValueMap;
   import org.apache.sling.api.wrappers.ValueMapDecorator;
   import org.apache.sling.commons.json.io.JSONWriter;
   import org.apache.sling.commons.json.JSONException;
   
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   
   import com.day.cq.wcm.msm.api.ActionConfig;
   import com.day.cq.wcm.msm.api.LiveAction;
   import com.day.cq.wcm.msm.api.LiveActionFactory;
   import com.day.cq.wcm.msm.api.LiveRelationship;
   import com.day.cq.wcm.api.WCMException;
   
   @Component(metatype = false)
   @Service
   public class ExampleLiveActionFactory implements LiveActionFactory<LiveAction> {
    @Property(value="exampleLiveAction")
    static final String actionname = LiveActionFactory.LIVE_ACTION_NAME;
   
    public LiveAction createAction(Resource config) {
     ValueMap configs;
     /* Adapt the config resource to a ValueMap */
           if (config == null || config.adaptTo(ValueMap.class) == null) {
               configs = new ValueMapDecorator(Collections.<String, Object>emptyMap());
           } else {
               configs = config.adaptTo(ValueMap.class);
           }
   
     return new ExampleLiveAction(actionname, configs);
    }
    public String createsAction() {
     return actionname;
    }
    /************* LiveAction ****************/
    private static class ExampleLiveAction implements LiveAction {
     private String name;
     private ValueMap configs;
     private static final Logger log = LoggerFactory.getLogger(ExampleLiveAction.class);
   
     public ExampleLiveAction(String nm, ValueMap config){
      name = nm;
      configs = config;
     }
   
     public void execute(Resource source, Resource target,
       LiveRelationship liverel, boolean autoSave, boolean isResetRollout)
         throws WCMException {
   
      String lastMod = null;
   
      log.info(" *** Executing ExampleLiveAction *** ");
   
      /* Determine if the LiveAction is configured to copy the cq:lastModifiedBy property */
      if ((Boolean) configs.get("repLastModBy")){
   
       /* get the source's cq:lastModifiedBy property */
       if (source != null && source.adaptTo(Node.class) !=  null){
        ValueMap sourcevm = source.adaptTo(ValueMap.class);
        lastMod = sourcevm.get(com.day.cq.wcm.msm.api.MSMNameConstants.PN_PAGE_LAST_MOD_BY, String.class);
       }
   
       /* set the target node's la-lastModifiedBy property */
       Session session = null;
       if (target != null && target.adaptTo(Node.class) !=  null){
        ResourceResolver resolver = target.getResourceResolver();
        session = resolver.adaptTo(javax.jcr.Session.class);
        Node targetNode;
        try{
         targetNode=target.adaptTo(javax.jcr.Node.class);
         targetNode.setProperty("la-lastModifiedBy", lastMod);
         log.info(" *** Target node lastModifiedBy property updated: {} ***",lastMod);
        }catch(Exception e){
         log.error(e.getMessage());
        }
       }
       if(autoSave){
        try {
         session.save();
        } catch (Exception e) {
         try {
          session.refresh(true);
         } catch (RepositoryException e1) {
          e1.printStackTrace();
         }
         e.printStackTrace();
        }
       }
      }
     }
     public String getName() {
      return name;
     }
   
     /************* Deprecated *************/
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3) throws WCMException {
     }
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3, boolean arg4)
         throws WCMException {
     }
     @Deprecated
     public String getParameterName() {
      return null;
     }
     @Deprecated
     public String[] getPropertiesNames() {
      return null;
     }
     @Deprecated
     public int getRank() {
      return 0;
     }
     @Deprecated
     public String getTitle() {
      return null;
     }
     @Deprecated
     public void write(JSONWriter arg0) throws JSONException {
     }
    }
   }
   ```

1. 使用终端或命令会话，将目录更改为`MyLiveActionFactory`目录（Maven项目目录）。 然后，输入以下命令：

   ```shell
   mvn -PautoInstallPackage clean install
   ```

   AEM `error.log`文件应指示包已启动。

   例如， [https://localhost:4502/system/console/status-slinglogs](https://localhost:4502/system/console/status-slinglogs)。

   ```xml
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

### 创建示例转出配置 {#create-the-example-rollout-configuration}

创建使用您创建的`LiveActionFactory`的MSM转出配置：

1. 使用标准过程](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration)创建和配置[转出配置 — 并使用属性：

   * **标题**:转出配置示例
   * **名称**:examplolloutconfig
   * **cq:trigger**:  `publish`

### 将实时操作添加到示例转出配置 {#add-the-live-action-to-the-example-rollout-configuration}

配置您在上一步骤中创建的转出配置，以便它使用`ExampleLiveActionFactory`类。

1. 开放CRXDE Lite;例如， [https://localhost:4502/crx/de](https://localhost:4502/crx/de)。
1. 在`/apps/msm/rolloutconfigs/examplerolloutconfig/jcr:content`下创建以下节点：

   * **名称**: `exampleLiveAction`
   * **类型**: `cq:LiveSyncAction`

1. 单击&#x200B;**Save All**。
1. 选择`exampleLiveAction`节点并添加以下属性：

   * **名称**: `repLastModBy`
   * **类型**: `Boolean`
   * **值**:  `true`

   此属性指示`ExampleLiveAction`类应将`cq:LastModifiedBy`属性从源复制到目标节点。

1. 单击&#x200B;**Save All**。

### 创建Live Copy {#create-the-live-copy}

[使用转出](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) 配置创建We.Retail引用站点的English/Products分支的实时副本：

* **来源**:  `/content/we-retail/language-masters/en/products`

* **转出配置**:转出配置示例

激活源分支的&#x200B;**Products**（英语）页面，并观察`LiveAction`类生成的日志消息：

```xml
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***ExampleLiveAction has been executed.***
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***Target node lastModifiedBy property updated: admin ***
```

<!--
## Removing the Chapters Step in the Create Site Wizard {#removing-the-chapters-step-in-the-create-site-wizard}

In some cases, the **Chapters** selection is not required in the create site wizard (only the **Languages** selection is required). To remove this step in the default We.Retail English blueprint:

1. In CRX Explorer, remove the node:
   `/etc/blueprints/weretail-english/jcr:content/dialog/items/tabs/items/tab_chap`.

1. Navigate to `/libs/wcm/msm/templates/blueprint/defaults/livecopy_tab/items` and create a new node:

    1. **Name** = `chapters`; **Type** = `cq:Widget`.

1. Add following properties to the new node:

    1. **Name** = `name`; **Type** = `String`; **Value** = `msm:chapterPages`

    1. **Name** = `value`; **Type** = `String`; **Value** = `all`

    1. **Name** = `xtype`; **Type** = `String`; **Value** = `hidden`
-->

## 更改语言名称和默认国家/地区 {#changing-language-names-and-default-countries}

AEM使用一组默认的语言和国家/地区代码。

* 默认语言代码为ISO-639-1定义的小写字母双字母代码。
* 默认国家/地区代码为ISO 3166定义的小写或大写双字母代码。

MSM使用存储的语言和国家/地区代码列表来确定与页面语言版本名称关联的国家/地区名称。 您可以根据需要更改列表的以下方面：

* 语言标题
* 国家/地区名称
* 语言的默认国家/地区（对于代码，例如`en`、`de`等）

语言列表存储在`/libs/wcm/core/resources/languages`节点的下方。 每个子节点表示语言或语言国家/地区：

* 节点的名称是语言代码（如`en`或`de`），或language_country代码（如`en_us`或`de_ch`）。

* 节点的`language`属性存储代码语言的全名。
* 节点的`country`属性存储代码的国家/地区的全名。
* 当节点名称仅包含语言代码（如`en`）时，国家/地区属性为`*`，而额外的`defaultCountry`属性存储语言国家/地区的代码以指示要使用的国家/地区。

![chlimage_1-76](assets/chlimage_1-76.png)

要修改语言，请执行以下操作：

1. 在Web浏览器中打开CRXDE Lite;例如， [https://localhost:4502/crx/de](https://localhost:4502/crx/de)
1. 选择`/apps`文件夹，然后单击&#x200B;**创建**，然后单击&#x200B;**创建文件夹。**

   将新文件夹命名为`wcm`。

1. 重复上一步骤以创建`/apps/wcm/core`文件夹树。 在`core`中创建名为`resources`的`sling:Folder`类型的节点。 <!-- ![chlimage_1-77](assets/chlimage_1-77.png) -->

1. 右键单击`/libs/wcm/core/resources/languages`节点，然后单击&#x200B;**复制**。
1. 右键单击`/apps/wcm/core/resources`文件夹，然后单击&#x200B;**粘贴**。 根据需要修改子节点。
1. 单击&#x200B;**Save All**。
1. 单击&#x200B;**工具**、**操作**，然后单击&#x200B;**Web控制台**。 在此控制台中，单击&#x200B;**OSGi**，然后单击&#x200B;**配置**。
1. 找到并单击&#x200B;**Day CQ WCM语言管理器**，将&#x200B;**语言列表**&#x200B;的值更改为`/apps/wcm/core/resources/languages`，然后单击&#x200B;**Save**。

   ![chlimage_1-78](assets/chlimage_1-78.png)

## 在页面属性（触屏优化UI）上配置MSM锁定 {#configuring-msm-locks-on-page-properties-touch-enabled-ui}

创建自定义页面资产时，您可能需要考虑新资产是否有资格转出到任何Live Copy。

例如，如果添加了两个新页面属性：

* 联系电子邮件:

   * 无需推出此属性，因为此属性在每个国家/地区（或品牌等）都将有所不同。

* 关键可视样式：

   * 项目要求是，此资产将由所有国家/地区（或品牌等）共同使用，因此（通常）应推出此资产。

然后，您需要确保：

* 联系电子邮件:

   * 从已转出的属性中排除；请参阅[从同步中排除属性和节点类型](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization)。

* 关键可视样式：

   * 确保在触屏优化UI中，除非取消继承，否则不允许编辑此属性，您还可以恢复继承；可通过单击链/断链链接来控制此操作，该链链接可切换以指示连接状态。

页面属性是否受到转出的控制，因此在编辑时是否受取消/恢复继承的控制，将由对话框属性控制：

* `cq-msm-lockable`

   * 适用于触屏优化UI对话框中的项目
   * 将在对话框中创建链链接符号
   * 仅允许在取消继承（链式链接断开）时进行编辑
   * 仅适用于资源的第一个子级
   * **类型**: `String`

   * **值**:物业名称(及与物业价值相若 `name`);例如，请参阅
      `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

定义`cq-msm-lockable`后，断开/关闭链将通过以下方式与MSM交互：

* 如果`cq-msm-lockable`的值为：

   * **相对** (例如 `myProperty` 或 `./myProperty`)

      * 它将从`cq:propertyInheritanceCancelled`中添加和删除该属性。
   * **绝对** (例如， `/image`)

      * 通过将`cq:LiveSyncCancelled` mixin添加到`./image`并将`cq:isCancelledForChildren`设置为`true`，中断链将取消继承。

      * 关闭链将还原继承。


>[!NOTE]
>
>`cq-msm-lockable` 应用于要编辑的资源的第一个子级，而且它在任何更深层的上级上不起作用，无论该值被定义为绝对值还是相对值。

>[!NOTE]
>
>重新启用继承时，Live Copy页面属性不会自动与源属性同步。 如果需要，您可以手动请求同步。
