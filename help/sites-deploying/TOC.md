---
cloud: experience-cloud
product: adobe experience manager
solution: Experience Manager, Experience Manager Sites
audience: end-user
user-guide-title: AEM 6.5 Deploying 指南
breadcrumb-title: Deploying 指南
user-guide-description: 详细了解 Adobe Experience Manager 6.5 的安装、部署和架构，包括我们的 Adobe Managed Services 云部署。
translation-type: tm+mt
source-git-commit: fa2002950bbfb902db8c98a418b3a3d9185efea0
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 18%

---


# AEM 6.5部署用户指南{#deploying}

+ [部署用户指南](home.md)
+ AEM Platform {#introduction}简介
   + [AEM Platform简介](platform.md)
   + [技术要求](technical-requirements.md)
   + [AEM 6.5中的存储元素](storage-elements-in-aem-6.md)
   + [AEM with MongoDB](aem-with-mongodb.md)
+ 部署 AEM {#deploying}
   + [部署和维护](deploy.md)
   + [建议的部署](recommended-deploys.md)
   + [应用程序服务器安装](application-server-install.md)
   + [自定义独立安装](custom-standalone-install.md)
   + [命令行启动和停止](command-line-start-and-stop.md)
   + [在AEM 6中配置节点存储和数据存储](data-store-config.md)
   + [修订版清理](revision-cleanup.md)
   + [Oak查询和索引](queries-and-indexing.md)
   + [如何使用TarMK冷备用运行AEM](tarmk-cold-standby.md)
   + [AEM 6.5中的RDBMS支持](rdbms-support-in-aem.md)
   + [通过Oak-run Jar进行索引](indexing-via-the-oak-run-jar.md)
   + [Oak-run.jar索引用例](oak-run-indexing-usecases.md)
   + [Oak索引疑难解答](troubleshooting-oak-indexes.md)
   + [选择汇总的使用情况统计信息收集](opt-in-aggregated-usage-statistics.md)
   + [疑难解答](troubleshooting.md)
+ 配置AEM {#configuring}
   + [基本配置概念](configuring.md)
   + [记录](configure-logging.md)
   + [配置OSGi](configuring-osgi.md)
   + [OSGi配置设置](osgi-configuration-settings.md)
   + [运行模式](configure-runmodes.md)
   + [Web 控制台](web-console.md)
   + [复制](replication.md)
   + [使用互相SSL进行复制](mssl-replication.md)
   + [复制故障排除](troubleshoot-rep.md)
   + [静态对象过期](expiration-static-objects.md)
   + [版本清除](version-purging.md)
   + [监视和维护您的AEM实例](monitoring-and-maintaining.md)
   + [卸载作业](offloading.md)
   + [单一登录](single-sign-on.md)
   + [资源映射](resource-mapping.md)
   + [启用HTTP Over SSL](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/ssl-by-default.html)
   + [一致性和遍历检查](consistency-check.md)
   + [性能指南](performance-guidelines.md)
   + [性能优化](configuring-performance.md)
   + [资产性能指南](assets-performance-sizing.md)
   + [配置操作方法文章](ht-deploy.md)
   + [配置Web控制台](configuring-web-console.md)
+ 升级到AEM 6.5 {#upgrading}
   + [升级到AEM 6.5](upgrade.md)
   + [计划升级](upgrade-planning.md)
   + [利用模式检测器评估升级复杂度](pattern-detector.md)
   + [AEM 6.5中的向后兼容性](backward-compatibility.md)
   + [升级过程](upgrade-procedure.md)
   + [执行就地升级](in-place-upgrade.md)
   + [使用脱机重新索引减少升级期间的停机时间](upgrade-offline-reindexing.md)
   + [延迟内容迁移](lazy-content-migration.md)
   + [使用CRX2Oak迁移工具](using-crx2oak.md)
   + [升级前维护任务](pre-upgrade-maintenance-tasks.md)
   + [升级后检查和疑难解答](post-upgrade-checks-and-troubleshooting.md)
   + [升级自定义搜索Forms](upgrading-custom-search-forms.md)
   + [可持续升级](sustainable-upgrades.md)
   + [升级代码和自定义](upgrading-code-and-customizations.md)
   + [应用程序服务器安装的升级步骤](app-server-upgrade.md)
   + [列表升级后卸载的过时捆绑包](obsolete-bundles.md)
+ 存储库重组{#restructuring}
   + [AEM 6.5中的存储库重组](repository-restructuring.md)
   + [AEM 6.5中的通用存储库重组](all-repository-restructuring-in-aem-6-5.md)
   + [AEM 6.5中的Sites Repository Restructing](sites-repository-restructuring-in-aem-6-5.md)
   + [AEM 6.5中的资产存储库重组](assets-repository-restructuring-in-aem-6-5.md)
   + [Dynamic Media 6.5中的存储库重组](dynamicmedia-repository-restructuring-in-aem-6-5.md)
   + [Forms 6.5中的存储库重组](forms-repository-restructuring-in-aem-6-5.md)
   + [AEM 6.5中的电子商务存储库重组](ecommerce-repository-restructuring-in-aem-6-5.md)
   + [6.5中的AEM Communities存储库重组](communities-repository-restructuring-in-aem-6-5.md)
+ 电子商务 {#ecommerce}
   + [电子商务概述](ecommerce.md)
   + [SAPCommerce Cloud](sap-commerce-cloud.md)
   + [SalesforceCommerce Cloud](https://github.com/adobe/commerce-salesforce)
   + [Magento](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)
+ 最佳实践 {#practices}
   + [部署最佳实践](best-practices.md)
   + [性能树](performance-tree.md)
   + [性能测试的最佳实践](best-practices-for-performance-testing.md)
   + [查询和索引的最佳实践](best-practices-for-queries-and-indexing.md)
   + [面向客户的用户界面Recommendations](ui-recommendations.md)
   + [性能和可伸缩性](performance.md)
