---
title: 系统信息服务 API
description: 本文档提供有关System Information Service提供的API的详细信息。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 4da96c8f-8bd0-4cad-9087-18e324f084e7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 2%
---
# 系统信息服务 API {#system-information-service-apis}

系统信息服务提供一组用于检索信息的REST API。 下表提供了有关API的详细信息：

<table>
 <thead>
  <tr>
   <th><p>名称</p></th>
   <th><p>URL</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>系统信息。属性</p></td>
   <td><p>https://'[server]：[port]'/rest/services/SystemInfo.properties'</p></td>
   <td><p>此API是<a href="https://docs.oracle.com/javase/6/docs/api/java/lang/System.html#getProperties()">system.getProperties</a> Java API的包装器。 它会检索当前工作环境的配置。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.envVar</p></td>
   <td><p>https://'[server]：[port]'/rest/services/ SystemInfo.envVar</p></td>
   <td><p>检索主机操作系统的所有环境变量。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.logs</p></td>
   <td><p>https://'[server]：[port]'/rest/services/ SystemInfo.logs</p></td>
   <td><p>下载包含应用程序服务器日志的zip文件。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.config</p></td>
   <td><p>https://'[server]：[port]'/rest/services/ SystemInfo.config</p></td>
   <td><p>检索config.xml文件的所有内容。 </p></td>
  </tr>
  <tr>
   <td><p>系统信息。服务</p></td>
   <td><p>https://'[server]：[port]'/rest/services/ SystemInfo.services</p></td>
   <td><p>检索AEM表单服务的状态和配置参数。</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.vitalDetails</p></td>
   <td><p>https://'[server]：[port]'/rest/services/ SystemInfo.vitalDetails</p></td>
   <td><p>检索服务器正常运行时间、JVM参数、系统内存、栈大小、操作系统名称、活动线程数和线程计数。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.coreSettings</p></td>
   <td><p>https://'[server]：[port]'/rest/services/ SystemInfo.coreSettings</p></td>
   <td><p>检索以下属性的值：</p>
    <ul>
     <li><p>AdobeTempDir</p></li>
     <li><p>AdobeServerFontDir</p></li>
     <li><p>CustomerFontDir</p></li>
     <li><p>GlobalDocumentStorageRootDir</p></li>
     <li><p>DefaultDocumentMaxInlineSize</p></li>
     <li><p>DefaultDocumentDisposalTimeout</p></li>
     <li><p>EnableDocumentDBStorage</p></li>
     <li><p>GlobalDocumentStorageUseNetworkShare</p></li>
     <li><p>EnableFIPS</p></li>
     <li><p>启用WSDL</p></li>
     <li><p>数据服务配置文件 </p></li>
     <li><p>EnableRDS</p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>系统信息。数据库</p></td>
   <td><p>https://'[server]：[port]'/rest/services/ SystemInfo.database</p></td>
   <td><p>检索有关数据库的详细信息。</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.licenseInfo</p></td>
   <td><p>https://'[server]：[port]'/rest/services/ SystemInfo.licenseInfo</p></td>
   <td><p>检索已安装的AEM表单组件的版本和许可证信息。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfNo.serverConfig</p></td>
   <td><p>https://'[server]：[port]'/rest/services/ SystemInfo.serverConfig</p></td>
   <td><p>下载主机应用程序服务器的配置文件。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.threads？delay=[n]&amp;iterations=[n]</p></td>
   <td><p>https://'[server]：[port]'/rest/services/ SystemInfo.threads？delay=[n]&amp;iterations=[n]</p></td>
   <td><p>检索活动线程的计数和栈栈跟踪。 它接受以下参数：</p>
    <ul>
     <li><p>iterations= [n]：指定迭代次数。 将n替换为数字。 </p></li>
     <li><p>Delay= [n]：指定在启动下一个迭代之前等待的毫秒数。 </p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.info</p></td>
   <td><p>https://'[server]：[port]'/rest/services/ SystemInfo.info</p></td>
   <td><p>此API是所有系统信息服务API的包装器。 在内部，它运行所有系统信息API并以zip格式下载信息。 </p><p><i><strong>注意</strong>： SystemInfo.info不提供活动线程的计数和栈栈跟踪。 </i></p></td>
  </tr>
 </tbody>
</table>
