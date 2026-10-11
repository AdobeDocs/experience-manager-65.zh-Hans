---
title: SocialUtils重构
description: AEM 6.1已弃用包com.adobe.cq.social.ugcbase.SocialUtils
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0f731ec6-a12e-4098-a1ec-ee4cd4dc1432
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 1%
---
# SocialUtils重构 {#socialutils-refactoring}

## 已弃用SocialUtils包 {#socialutils-package-deprecated}

AEM 6.1已弃用包`com.adobe.cq.social.ugcbase.SocialUtils`。

下表列出了取代`SocialUtils`方法所需的方法。

## SocialResourceUtilities包  {#socialresourceutilities-package}

| com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities中的方法 | 注释 |
|---|---|
| 布尔型checkPermission(ResourceResolver resolver， String path， String action) |  |
| SocialResourceProvider getSocialResourceProvider(Resource) |  |
| SocialResourceConfiguration getStorageConfig(Resource) |  |
| 资源getUGCResource(Resource userResource) |  |
| 资源getUGCResource(Resource userResource， ResourceResolverFactory rrf) | 新建 |
| 资源getUGCResource(Resource userResource， ResourceResolverFactory rrf， String resourceTypeHint) | 新建 |
| 资源getUGCResource(Resource userResource， String resourceTypeHint) |  |
| boolean hasModeratePermissions(Resource) |  |
| String resourceToACLPath(Resource) |  |
| String resourceToUGCStoragePath(Resource) | 替换String resourceToUGCPath(Resource) |
| 字符串UGCToResourcePath(Resource) |  |
| 字符串UGCToResourcePath（字符串ugcPath） | 方法签名已更改 |
| 字符串UGCToResourcePath（字符串ugcPath， ResourceResolver resolver） | 新建 |

| `com.adobe.cq.social.`实用工具.resource.api.SocialResourceUtilities中的方法 | 注释 |
|---|---|
| SocialResourceProvider getSocialResourceProvider(Resource) | 替换SocialResourceProvider getConfiguredProvider(Resource) |

## SCFUtilities包 {#scfutilities-package}

| `com.adobe.cq.social.`utilities.scf.api.SCFUtilites中的方法 |
|---|
| 字符串getAvatar(UserProperties userProperties) |
| 字符串getAvatar(UserProperties userProperties， int size) |
| 字符串getAvatar(UserProperties userProperties， String absoluteDefaultAvatar) |
| 字符串getAvatar(UserProperties userProperties， String absoluteDefaultAvatar， SocialUtils.AVATAR_SIZE) |
| 页面getContainingPage(Resource) |
| 字符串getSocialProfileURL（字符串用户名，ResourceResolver解析程序，页面） |
| UserProperties getUserProperties(ResourceResolver resolver， String userId) |

## 仅供内部使用 {#for-internal-use-only}

| 布尔值canAddNode（会话会话，字符串路径） |
|---|
| 字符串createUniqueNameHint（字符串消息） |
| 字符串createUniqueNameHint(String message， int numRandomChars) |
| 字符串generateRandomString(int length) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| Page getPage(String path， ResourceResolver resolver) |
| 字符串getPagePath(Resource) |
| 字符串getPagePath（字符串路径） |
| 字符串getResourceTypeForIncludedResource（资源组件，字符串defaultResourceType，字符串designPropertyName） |
| 字符串getResourceTypeFromDesign(Resource， String styleProperty， String defaultValue) |
| boolean isResourceOwner(Resource resource) |
| 字符串mapUGCPath(Resource) |
| 字符串mapUGCPath(String ugcPath， ResourceResolver resolver) |
| 布尔mayPost(ResourceResolver resolver， Resource) |
| String prepareUserGeneratedContent(ResourceResolver resolver， String path) |

## 方法不再可用 {#methods-no-longer-available}

| 节点createNode(ResourceResolver resolver， String path， String nodeType) |
|---|
| 资源getResourceAtPath(ResourceResolver resolver， String path) |
| 资源getResourceAtPath（ResourceResolver解析器，字符串路径，字符串资源类型） |
| 配置getStorageCloudServiceConfig（资源） |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| 布尔值mayAccessUGC(ResourceResolver resolver) |
