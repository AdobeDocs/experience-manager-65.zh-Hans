---
title: 社区疑难解答
description: 了解社区疑难解答，包括已知问题和顾虑。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: ef4f4108-c485-4e2e-a58f-ff64eee9937e
source-git-commit: f03d0ab9d0f491441378e16e1590d33651f064b5
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 1%

---

# 社区疑难解答 {#troubleshooting}

本节包含社区故障诊断时的常见问题和已知问题。

## 已知问题 {#known-issues}

### Dispatcher重新获取失败 {#dispatcher-refetch-fails}

将Dispatcher 4.1.5与较新版本的Jetty一起使用时，重新获取可能会在等待请求超时后导致“无法从远程服务器接收响应”。

使用Dispatcher 4.1.6或更高版本解决了此问题。

### 从CQ 5.4升级后无法访问论坛 {#cannot-access-forum-post-after-upgrading-from-cq}

如果在CQ 5.4上创建论坛并发布主题，然后站点升级到AEM 5.6.1或更高版本，则尝试查看现有帖子可能会导致页面上出现错误：

非法的模式字符“a”无法将请求提供给 `/content/demoforums/forum-test.html` 和日志中包含以下内容：

```xml
20.03.2014 22:49:35.805 ERROR [10.177.45.32 [1395380975744] GET /content/demoforums/forum-test.html HTTP/1.1] com.day.cq.wcm.tags.IncludeTag Error while executing script content.jsp
org.apache.sling.api.scripting.ScriptEvaluationException:
at org.apache.sling.scripting.core.impl.DefaultSlingScript.call(DefaultSlingScript.java:388)
at org.apache.sling.scripting.core.impl.DefaultSlingScript.eval(DefaultSlingScript.java:171)
```

问题是com.day.cq.commons.date.RelativeTimeFormat的格式字符串在5.4到5.5之间发生了更改，因此不再接受“ago”的“a”。

因此，任何使用RelativeTimeFormat() API的代码都必须更改：

* 发件人: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r a", resourceBundle);`
* 收件人: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r", resourceBundle);`

在“创作”和“发布”页面上，失败情况不同。 在创作时，它静默失败，只是不显示论坛主题。 发布时，会在页面上引发错误。

请参阅 [com.day.cq.commons.date.RelativeTimeFormat](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/date/RelativeTimeFormat.html) API以了解更多信息。

## 常见问题 {#common-concerns}

### 日志中的警告：已弃用Handlebars {#warning-in-logs-handlebars-deprecated}

在启动期间（不是第一个，但之后的每一个），日志中可能会显示以下警告：

* `11.04.2014 08:38:07.223 WARN [FelixStartLevel]com.github.jknack.handlebars.Handlebars Helper 'i18n'` 已替换为 `com.adobe.cq.social.handlebars.I18nHelper@15bac645`

可以安全地忽略此警告，因为 `jknack.handlebars.Handlebars`，用于 [SCF](scf.md#handlebarsjavascripttemplatinglanguage)，自带了i18n助手实用程序。 启动时，它会被替换为特定于AEM的 [i18n助手](handlebars-helpers.md#i-n). 此警告由第三方库生成，用于确认覆盖现有帮助程序。

### 日志中的警告： OakResourceListener processOsgiEventQueue {#warning-in-logs-oakresourcelistener-processosgieventqueue}

发布多个社交社区论坛主题可能会导致OakResourceListener processOsgiEventQueue中的大量警告和信息日志。

可以安全地忽略这些警告。

```xml
23.04.2014 14:21:18.900 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.frq/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.908 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.prx/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
```

### 日志错误：IndexElementFactory的NoClassDefFoundError {#error-in-logs-noclassdeffounderror-for-indexelementfactory}

将AEM 5.6.1升级到最新的cq-socialcommunities-pkg-1.4.x或升级到AEM 6.0会导致日志文件中出现错误。 此问题在启动期间发生，针对一种条件自动解析，其证据为重新启动时未看到错误。

```xml
14.11.2013 20:52:39.453 ERROR [Apache Sling JCR Resource Event Queue Processor for path '/'] com.adobe.cq.social.storage.index.impl.IndexService Error occurred while processing event java.util.ConcurrentModificationException
14.11.2013 20:52:40.716 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory) java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory
14.11.2013 20:52:40.717 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Failed creating the component instance; see log for reason
```
