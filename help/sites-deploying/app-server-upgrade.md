---
title: 应用程序服务器安装的升级步骤
description: 了解如何升级通过应用程序服务器部署的AEM实例。
feature: Upgrading
exl-id: 86dd10ae-7f16-40c8-84b6-91ff2973a523
source-git-commit: 5e875e0420540ca209e7d677046e8d010ae4e145
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# 应用程序服务器安装的升级步骤{#upgrade-steps-for-application-server-installations}

本节介绍为更新AEM for Application Server安装而需要遵循的过程。

此过程中的所有示例都使用Tomcat作为应用程序服务器，这意味着您已部署了AEM的工作版本。 此过程用于记录从 **AEM版本6.4至6.5**.

1. 首先，启动TomCat。 在大多数情况下，您可以通过运行 `./catalina.sh` 通过从终端运行以下命令启动启动脚本：

   ```shell
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. 如果已部署AEM 6.4，请通过访问以下内容检查包是否正常运行：

   ```shell
   https://<serveraddress:port>/cq/system/console/bundles
   ```

1. 接下来，取消部署AEM 6.4。这可以从TomCat应用程序管理器(`http://serveraddress:serverport/manager/html`)

1. 现在，使用crx2oak迁移工具迁移存储库。 为此，请从下载最新版本的crx2oak [此位置](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/).

   ```shell
   SLING_HOME= $AEM-HOME/crx-quickstart java -Xmx4096m -XX:MaxPermSize=2048M -jar crx2oak.jar --load-profile segment-fds
   ```

1. 通过执行以下操作，删除sling.properties文件中的必需属性：

   1. 打开位于 `crx-quickstart/launchpad/sling.properties`
   1. 步骤文本删除以下属性并保存文件：

      1. `sling.installer.dir`

      1. `felix.cm.dir`

      1. `granite.product.version`

      1. `org.osgi.framework.system.packages`

      1. `osgi-core-packages`

      1. `osgi-compendium-services`

      1. `jre-*`

      1. `sling.run.mode.install.options`

1. 删除不再需要的文件和文件夹。 您需要具体删除的项目包括：

   * 的 **launchpad/startup文件夹**. 您可以通过在终端中运行以下命令来删除它： `rm -rf crx-quickstart/launchpad/startup`

   * 的 **base.jar文件**: `find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * 的 **BootstrapCommandFile_timestamp.txt文件**: `rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

   * 删除 **sling.options.file** 运行时： `find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf`

1. 现在，创建将与AEM 6.5一起使用的节点存储和数据存储。为此，您可以通过在 `crx-quickstart\install`:

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`
   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   这两个文件将配置AEM以使用TarMK节点存储和文件数据存储。

1. 编辑配置文件以使其可供使用。 更具体地说：

   * 将以下行添加到 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`:

      `customBlobStore=true`

   * 然后，将以下行添加到 `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`:

      ```
      path=./crx-quickstart/repository/datastore
      minRecordLength=4096
      ```

1. 现在，您需要更改AEM 6.5战争文件中的运行模式。 为此，首先创建一个临时文件夹，该文件夹将容纳AEM 6.5战争。 此示例中文件夹的名称将为 `temp`. 复制war文件后，通过从temp文件夹内运行来提取其内容：

   ```
   jar xvf aem-quickstart-6.5.0.war
   ```

1. 提取内容后，转到 **WEB-INF** 文件夹和编辑web.xml文件以更改运行模式。 要查找在XML中设置它们的位置，请查找 `sling.run.modes` 字符串。 找到该代码后，请更改下一行代码中的运行模式，该代码默认设置为创作：

   ```bash
   <param-value >author</param-value>
   ```

1. 将上述创作值更改为，并将运行模式设置为： `author,crx3,crx3tar`. 最终的代码块应当如下所示：

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. 使用修改后的内容重新创建jar:

   ```bash
   jar cvf aem65.war
   ```

1. 最后，在TomCat中部署新的战争文件。
