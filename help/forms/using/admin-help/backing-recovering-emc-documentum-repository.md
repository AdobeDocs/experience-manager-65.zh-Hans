---
title: 备份和恢复EMC Documentum存储库
seo-title: 备份和恢复EMC Documentum存储库
description: 本文档描述了备份和恢复为AEM表单环境配置的EMC Documentum存储库所需的任务。
seo-description: 本文档描述了备份和恢复为AEM表单环境配置的EMC Documentum存储库所需的任务。
uuid: ab3b1fb1-25b3-4c95-801f-82d4b58f05ff
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f146202f-25f1-46a0-9943-c483f5f09f9f
translation-type: tm+mt
source-git-commit: 8bc99ed3817398ae358d439a5c1fcc90bbd24327

---


# 备份和恢复EMC Documentum存储库 {#backing-up-and-recovering-the-emc-documentum-repository}

本节介绍备份和恢复为AEM表单环境配置的EMC Documentum存储库所需的任务。

>[!NOTE]
>
>这些说明假定已根据需要安装和配置带有Connectors for ECM和EMC Documentum Content server的AEM表单。

对于备份和还原进程，有两个主要任务：

* 备份（或恢复）AEM表单环境。
* 备份（或恢复）EMC Documentum Content Server。

>[!NOTE]
>
>在备份EMC Documentum系统之前备份您的AEM表单数据，然后在恢复AEM表单环境之前恢复EMC Documentum系统。

## 软件要求 {#software-requirements}

要在您的EMC Documentum Content server上执行必要的备份任务，请从EMC购买适当的第三方实用程序，如EMC netWorker或从CYA为EMC Documentum购买CYA smartRecovery。 以下说明介绍了使用EMC netWorker Module version 7.2.2的步骤。

您需要以下EMC netWorker模块：

* NetWorker Module
* NetWorker配置向导
* NetWorker设备配置向导
* NetWorker Module for the database type by your Content Server
* NetWorker Module for Documentum

## 准备EMC Document Content Server进行备份和恢复 {#preparing-the-emc-document-content-server-for-backup-and-recovery}

本节介绍在Content server上安装和配置EMC netWorker软件。

**为备份准备EMC Documentum服务器**

1. 在EMC Documentum Content server上，安装EMC netWorker模块，接受所有默认值。

   在安装过程中，系统会提示您输入Content server计算机的服务器名作为 *NetWorker服务器名*。 在为数据库安装EMC netWorker模块时，请选择“完整”安装。

1. 使用下面的示例内容，创建一个名为 *nsrnmd_win.cfg的配置文件* ，并将其保存到Content server上的可访问位置。 此文件将由备份和还原命令调用。

   以下文本包含换行符的格式。 如果将此文本复制到本文档外的某个位置，则一次复制一个部分，并在将其粘贴到新位置时删除格式设置字符。

   ```as3
    ################################################
    # NetWorker Module for Documentum v1.2 nsrnmd_win.cfg D5.3+ example with
    # typical set of working parameters.  THIS FILE MUST BE SITE-CUSTOMISED.
    #
    # Parameters not shown can be set in this file (as per site customisation) #or from the command-line.
    #
    # Please refer to the user Guides for details on all parameters, including
    # those not listed below.
    # Note: DCTM environment for D6 is slightly different from D5, refer to D6
    # Installation Guide to update the values.
    ################################################
    #Can get values for most of below from doing as the dctm inst owner: cmd> set DOCUMENTUM=C:\Documentum
    DM_HOME=C:\Documentum\product\6.0
    JAVA_HOME=C:\Progra~1\Documentum\java\1.5.0_12
    JAVA_PATH=C:\Progra~1\Documentum\java\1.5.0_12\bin
    PATH=C:\WINNT\system32;C:\WINNT;C:\WINNT\system32\WBEM;C:\Documentum\product\6.0\bin;C:\Documentum\fulltext\fast;C:\Documentum\product\6.0\fusion;C:\Program Files\Documentum\Shared;C:\Program Files\Legato\nsr\bin;C:\Program Files\Microsoft SQL Server\80\Tools\Binn;C:\Program Files\Microsoft SQL Server\90\DTS\Binn\;C:\Program Files\Microsoft SQL Server\90\Tools\binn;C:\Program Files\Microsoft SQL Server\90\Tools\Binn\VSShell\Common7\IDE;C:\Program Files\Documentum\java\1.5.0_12\bin;C:\Documentum\config;C:\Documentum
    #See also manifest dctm.jar file for class path locations
    CLASSPATH=.;C:\Program Files\Legato\nsr\bin;C:\Program Files\Legato\nsr\bin\nsrnmdde.jar;C:\Program Files\Documentum\java\1.5.0_12\lib\tools.jar;C:\Program Files\Documentum\Shared\dfc.jar;C:\Program Files\Documentum\Shared\aspectjrt.jar;C:\Program Files\Documentum\dctm.jar;C:\Program Files\Documentum\Shared\workflow.jar;C:\Program Files\Documentum\Shared\log4j.jar;C:\Program Files\Documentum\java\1.5.0_12\lib\dt.jar;C:\Documentum\config
   
    ################################################
    #If not using nsrnmdsv -m ALL|DB|DB_LOG|FTI|FTI_ALL|ICF|SA|SA_ALL, set #for backup
    NMD_SCOPE=ALL
    #Mandatory when scope (backup or restore) is FTI/SA without -a option
    #NMD_OBJECT_NAME=filestore_01
    ################################################
    NMDDE_DM_DOCBASE=Docbase
    NMDDE_DM_USER=Administrator
    #NMDDE_DM_PASSWD must be set via running: nsrnmdsv -f <nmdcfg> -P <pwd>.
    ################################################
    #DB related hooks to invoke arbitrary scripts:
    #Set if DB is on a remote host
    #NMD_DB_HOST=dbhost
    #Pure basename implies remote host execution; absolute path ... local
    #execution as in NMD v1.0.
    #
    #Remote execution requires script be put in remote nsrexecd bin directory
    #and D5.3+ host be added to remote nsr\res\servers file w/ nsrexecd recycled
    #
    #Refer to user Guides for sample script code.
    NMD_DB_FULL_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbf.bat
    NMD_DB_LOG_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbl.bat
    NMD_DB_INCR_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbi.bat
    ################################################
    #For D5.3+ only: NMD_FTI_INCLUDED, NMD_FTI_HOST, NMD_FTI_USER,
    #NMD_FTI_PASSWD & NMD_FTI_SUBDIRS.
    #Optional for remote D5.3+ FTI server
    NMD_FTI_INCLUDED=no
    #NMD_FTI_HOST=ftihost
    #Recommended for D5.3+ FTI server quiesce/unquiesce
    #NMD_FTI_USER=ftiadmin
    #The index name: optional for D5.3+ FTI server, used with -M FTI_ALL or
    #-M ALL
    #NMD_FTI_NAME=rep_name_ftindex_01
    #Recommended for D5.3+ FTI server quiesce/unquiesce
    #NMDDE_FTI_PASSWD must be set via running: nsrnmdsv -f <nmdcfg> -P <pwd>
    #-M FTI.
    #Pure basename implies remote host execution; absolute path ... local execution
    #as in NMD v1.0.
    #
    #Remote execution requires script be put in remote nsrexecd bin directory
    #and D5.3+ host be added to remote nsr\res\servers file w/ nsrexecd
    #recycled.
    #
    #See example nsrnmdfti*.bat examples.
    #
    #Mandatory for D5.3+
    #NMD_BACKUP_FTI_QUIESCE=nsrnmdftiq.bat
    #NMD_BACKUP_FTI_UNQUIESCE=nsrnmdftiu.bat
    #Used for D5.3+ to get InstallProfile.xml FTI file in multinode
    #discovery.
    #Optional, if not specified, will treat as single-node FTI.
    #NMD_FTI_GET_INSTPROF=nsrnmdfti_instprof.bat
    #Mandatory for D5.3+. No spaces in paths or around comma separators.
    #For remote FTI, paths must be valid at the FTI host.
    #NMD_FTI_SUBDIRS=F:\Documentum_idx\data\fulltext\fixml,F:\Documentum_idx
    #\data\fulltext\index
    ################################################
    #Mandatory. No spaces in paths or before comma
    #separators in NMD_ICF_SUBDIRS_xxx:
    #NMD_ICF_INCLUDED=yes
    #NMD_ICF_SUBDIRS=C:\Documentum\dba,C:\Documentum\product\5.3
    ################################################
    NMD_FILEREPORT_INCLUDED=yes
    NMDDE_METADATA_OUTPUT_DEST=C:\docbase_freports\
    ################################################
    #Other misc recommended NMD_xxx parameters
    #Recommended to get more meaningful saveset names
    NMD_USE_DEFAULT_SAVESET_NAMES=yes
    #Use following to skip unwanted ICF, FTI and non-SnapImage SA dirs/files.
    #For example, "<</>> +skip: dm_ftwork_dir" line will skip non-data
    #files.
    #
    #The path will be the same and must exist on D5.3+, remote FTI host, and
    #RCS hosts correspondingly if used.
    #NMD_DIRECTIVES_FILE=E:\Program Files\Legato\nsr\res\nsrnmddirectives.txt
    #For non-SnapImage SA backup
    #NMD_SA_FULL_NUM_SAVESET=16
    #NMD_SA_INCR_NUM_SAVESET=4
    #NMD_USE_SNAPIMAGE=yes
    ################################################
    # DSA setup
    ################################################
    # Name of the config file at the remote sites;
    # Mandatory, listed in the config file at the primary host.
    # (if skipped, backup is treated as local)
    # NMD_RCS_CFG_FILE=rep_name_rcs.cfg
   
    # SA-host mapping add, optional, will override far-store list info.
    # No space around comma.
    # NMD_HOST_SAS_MAP=host01,sa_01,sa_02
    # NMD_HOST_SAS_MAP=host02,sa_03
    ################################################
    NSR_SERVER=con-dctm
    #NSR_CLIENT=d5svrhost
    NSR_GROUP=Default
    NSR_DATA_VOLUME_POOL=Default
    #NSR_SNAPIMAGE_DATA_VOLUME_POOL=Default
    #Relocation dir will be the same on D5+ and remote FTI/SA hosts.
    NSR_RELOCATION=C:\reloc
    #NSR_PARALLELISM=16
    NSR_DEBUG_FILE=C:\Program Files\Legato\nsr\applogs\nmd.log
    NSR_DEBUG_LEVEL=9
    ################################################
    NMDDE_DM_PASSWD=XAtup9pl
   ```

   将配置文件密码字段保留 `NMDDE_DM_PASSWD` 为空。 您将在下一步中设置密码。

1. 按如下方式设置配置文件密码：

   * 打开命令提示符，并更改 *[到NetWorker_root]*\Legato\nsr\bin。
   * 运行以下命令： `-nsrnmdsv.exe -f`*&lt;path_to_cfg_file> -P &lt;password>*

1. 创建用于备份数据库的可执行批处理(.bat)文件。 （请参阅NetWorker文档。）根据您的安装设置批处理文件中的详细信息。

   * 完整数据库备份(nsrnmddbf.bat):

      *[NetWorker数据库_module_root]*`-s`*&lt;NetWorker_Server_Name>用户名&#x200B;*,`-U`*[password ]*Database`-P`*[]*`-l full`*&lt;数据库名>*

   * 增量式数据库备份(nsrnmddbi.bat):

      *[NetWorker数据库_module_root]*`-s`*&lt;NetWorker_Server_Name>用户名&#x200B;*,`-U`*[password ]*Database`-P`*[]*`-l 1 -R`*&lt;数据库名>*

   * 数据库日志备份(nsrnmddbl.bat):

      *[NetWorker数据库_module_root]*`-s`*&lt;NetWorker_Server_Name>用户名&#x200B;*,`-U`*[password ]*Database`-P`*[]*`-l incr -R`*&lt;数据库名>*

      其中：

      `[NetWorker_database_module_root]` 是NetWorker模块的安装目录。 例如， netWorker Module for SQL server的默认安装目录为C:\Program Files\Legato\nsr\bin\nsrsqlsv。

      `NetWorker_Server_Name` 是NetWorker安装在的服务器。

      `username` &amp;是 `password` 数据库管理员用户的用户名和密码。

      `database_name` 是要备份的数据库的名称。

**创建备份设备**

1. 在EMC Documentum服务器上新建一个目录，并通过授予所有用户完全权限来共享该文件夹。
1. 启动EMC netWorker Administrator ，然后单击“介质管理”>“设备”。
1. 右键单击设备，然后选择创建。
1. 输入以下值，然后单击“确定”:

   **** 名称：共享目录的完整路径

   **** 媒体类型： `File`

1. 右键单击新设备，然后选择“操作”。
1. 单击“标签”，输入名称，单击“确定”，然后单击“装载”。

将添加一个设备，备份的文件将保存到该设备中。 您可以添加不同格式的多个设备。

## 备份EMC Documentum Content Server {#back-up-the-emc-documentum-content-server}

在完成AEM表单数据的完整备份后，请执行以下任务。 (请参 [阅备份AEM表单数据](/help/forms/using/admin-help/backing-aem-forms-data.md#backing-up-the-aem-forms-data)。)

>[!NOTE]
>
>命令脚本需要您在准备EMC Document Content server以进行备份和恢复中创建的nsrnmd_win.cfg文件的完整路径 [](backing-recovering-emc-documentum-repository.md#preparing-the-emc-document-content-server-for-backup-and-recovery)。

1. 打开命令提示符，并更改 *[到NetWorker_root]*\Legato\nsr\bin。
1. 运行以下命令：

   ```as3
    - nsrnmdsv.exe -f <path_to_cfg_file>
   ```

## 恢复EMC Documentum Content Server {#restore-the-emc-documentum-content-server}

在恢复AEM表单数据之前，请执行以下任务。 (请参 [阅恢复AEM表单数据](/help/forms/using/admin-help/recovering-aem-forms-data.md#recovering-the-aem-forms-data)。)

>[!NOTE]
>
>命令脚本需要您在准备EMC Document Content server以进行备份和恢复中创建的nsrnmd_win.cfg文件的完整路径 [](backing-recovering-emc-documentum-repository.md#preparing-the-emc-document-content-server-for-backup-and-recovery)。

1. 停止要恢复的Docbase服务。
1. 为数据库模块启动NetWorker User Utility(例如， *NetWorker User for SQL Server*)。
1. 单击“恢复”工具，然后选择“正常”。
1. 在屏幕的左侧，选择Docbase的数据库，然后单击工具栏上的“开始”按钮。
1. 恢复数据库后，重新启动Docbase服务。
1. 打开命令提示符并更改 *[到NetWorker_root]*\Legato\nsr\bin
1. 运行以下命令：

   ```as3
    - nsrnmdrs.exe -B <docbase_name> -f <path_to_cfg_file> -C SA
   ```

