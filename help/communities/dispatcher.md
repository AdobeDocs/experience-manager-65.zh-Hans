---
title: 为社区配置Dispatcher
seo-title: 为社区配置Dispatcher
description: 为AEM Communities配置调度程序
seo-description: 为AEM Communities配置调度程序
uuid: c17daca9-3244-4b10-9d4e-2e95df633dd9
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: 23745dd3-1424-4d22-8456-d2dbd42467f4
translation-type: tm+mt
source-git-commit: 7f5bfce7fb9d7056e7c0848f92eac3f8c31aad24
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 2%

---


# 为社区配置调度程序{#configuring-dispatcher-for-communities}

## AEM Communities {#aem-communities}

对于AEM Communities，必须配置调度程序以确保[社区站点](overview.md#community-sites)正常工作。 包括社区启用和社交登录等功能时，需要进行其他配置。

了解特定部署和站点设计的必要条件

* 联系[客户服务](https://helpx.adobe.com/cn/marketing-cloud/contact-support.html)

另请参阅主[调度程序文档](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)。

## 调度程序缓存{#dispatcher-caching}

### 概述 {#overview}

针对AEM Communities的调度程序缓存是调度程序提供社区站点页面完全缓存版本的功能。

目前，它仅受匿名网站访客（如浏览社区站点或登录社区页面作为搜索结果的用户）以及为页面编制索引的搜索引擎支持。 优势在于，匿名用户和搜索引擎将体验到改进的性能。

对于已登录的成员，调度程序会绕过缓存，将请求直接转发给发布者，这样所有页面都会动态生成并传送。

当配置为支持调度程序缓存时，将在标头中添加一个基于TTL的“最大页面”过期，以确保调度程序缓存页面是最新的。

### 要求{#requirements}

* 调度程序4.1.2或更高版本（有关最新版本，请参阅[安装Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)）
* [ACS AEM公共资源包](https://adobe-consulting-services.github.io/acs-aem-commons/)

   * 版本3.3.2或更高版本
   * `ACS AEM Commons - Dispatcher Cache Control Header - Max Age` OSGi配置

### 配置 {#configuration}

OSGi配置&#x200B;**ACS AEM Commons - Dispatcher Cache Control Header - Max Age**&#x200B;设置在指定路径下显示的缓存页面的过期时间。

* 从[Web控制台](../../help/sites-deploying/configuring-osgi.md)

   * 例如，[http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 找到`ACS AEM Commons - Dispatcher Cache Control Header - Max Age`
* 选择“+”图标以创建新连接配置

   ![dispatcher](assets/dispatcher.png)

* **滤镜图案**

   *（必需）* 指向社区页面的一个或多个路径。例如，`/content/sites/engage/(.*)`。

* **高速缓存控制最大时间**

   *（必需）* 要添加到“Cache Control（缓存控制）”标头的最大时间（以秒为单位）。值必须大于零(0)。

## 调度程序客户端标头{#dispatcher-client-headers}

在`dispatcher.any`的/clientheaders部分，如果列出一组特定的标头，则必须包含`"CSRF-Token"`，这样[启用功能](enablement.md)才能正常工作。

## 调度程序过滤器{#dispatcher-filters}

`dispatcher.any`文件的/filter部分在[配置内容访问- /filter](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#filter)中有说明。

本节介绍Communities功能正常运行可能需要的条目。

过滤器属性名称遵循使用四位数来指示应用过滤器模式的顺序的惯例。 当多个过滤器模式应用于请求时，应用的最后一个过滤模式将有效。 因此，通常使用第一过滤器模式来拒绝所有内容，以使以下模式以受控方式恢复访问。

以下示例使用的属性名称可能需要进行修改以适合任何特定调度程序。any文件。

另请参阅：

* [调度程序安全核对清单](https://helpx.adobe.com/experience-manager/dispatcher/using/security-checklist.html)

>[!NOTE]
>
>**属性名称示例**
>所显示的所有属性名称（如&#x200B;**/0050**&#x200B;和&#x200B;**/0170**）都应调整为适合现有调度程序。any配置文件。


>[!CAUTION]
>
>有关使用Dispatcher限制访问时的进一步注意事项，请参阅[调度程序安全清单](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=en)。 另外，请阅读[AEM安全检查列表](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/security-checklist.html)，了解有关AEM安装的其他安全详细信息。


应将以下条目添加到/filter部分的末尾，尤其是所有拒绝条目之后。

<!-- New code wrt CQDOC-16081, changed by Vishabh on 10 Dec 2020.
-->

```shell
# design and template assets
/0050 { /type "allow" /url "/etc/designs/*" }

# collected JS/CSS from the components and design
/0051 { /type "allow" /url "/etc/clientlibs/*" }

# foundation search component - write stats
/0052 { /type "allow" /url "/bin/statistics/tracker/*" }

# allow users to edit profile page
/0054 { /type "allow" /url "* /home/users/*/*/profile.form.html*" }

# all profile data
/0057 { /type "allow" /url "/home/users/*/profile/*" }

# required for social "Sign In" link.
/0059 { /type "allow" /url "/etc/clientcontext/*" }

# required for "Sign Out" operation
/0063 { /type "allow" /url "* /system/sling/logout*" }

# enable Facebook and Twitter signin
/0064 { /type "allow" /url "/etc/cloudservices/*" }

# enable personalization
/0062 { /type "allow" /url "/libs/cq/personalization/*" }

# for Enablement features
/0170 { /type "allow" /url "/libs/granite/csrf/token.json*" }
/0171 { /type "allow" /url "/content/sites/*/resources/en/*" }
/0172 { /type "allow" /url "/content/communities/enablement/reports/*" }
/0173 { /type "allow" /url "/content/sites/*" }
/0174 { /type "allow" /url "/content/communities/scorm/*" }
/0175 { /type "allow" /url "/content/sites/*" }
/0176 { /type "allow" /url "/libs/granite/security/userinfo.json"}
/0177 { /type "allow" /url "/libs/granite/security/currentuser.json" }

# Enable CSRF token otherwise nothings works.
/5001 { /type "allow" /url "/libs/granite/csrf/token.json *"}
# Allow SCF User Model to bootstrap as it depends on the granite user
/5002 { /type "allow" /url "/libs/granite/security/currentuser.json*" }

# Allow Communities Site Logout button work
/5003 { /type "allow" /url "/system/sling/logout.html*" }

# Allow i18n to load correctly
/5004 { /type "allow" /url "/libs/cq/i18n/dict.en.json *" }

# Allow social json get pattern.
/6002 { /type "allow" /url "*.social.*.json*" }

# Allow loading of templates
/6003 { /type "allow" /url "/services/social/templates*" }

# Allow SCF User model to check moderator rules
/6005 { /type "allow" /url "/services/social/getLoggedInUser?moderatorCheck=*" }

# Allow CKEditor to load which uses a query pattern.
/6006 { /type "allow" /url "/etc/clientlibs/social/thirdparty/ckeditor/*.js?t=*" }
/6007 { /type "allow" /url "/etc/clientlibs/social/thirdparty/ckeditor/*.css?t=*" }

# Allow Fonts from Communities to load
/6050 { /type "allow" /url "*.woff" }
/6051 { /type "allow" /url "*.ttf" }

# Enable CQ Security checkpoint for component guide.
/7001 { /type "allow" /url "/libs/cq/security/userinfo.json?cq_ck=*"
```


<!-- existing content as of Dec 10, wrt CQDOC-16081

```shell
# design and template assets
/0050 { /type "allow" /glob "GET /etc/designs/*" }

# collected JS/CSS from the components and design
/0051 { /type "allow" /glob "GET /etc/clientlibs/*" }

# foundation search component - write stats
/0052 { /type "allow" /glob "GET /bin/statistics/tracker/*" }

# allow users to edit profile page
/0054 { /type "allow" /glob "* /home/users/*/*/profile.form.html*" }

# all profile data
/0057 { /type "allow" /glob "GET /home/users/*/profile/*" }

# required for social "Sign In" link.
/0059 { /type "allow" /glob "GET /etc/clientcontext/*" }

# required for "Sign Out" operation
/0063 { /type "allow" /glob "* /system/sling/logout*" }

# enable Facebook and Twitter signin
/0064 { /type "allow" /glob "GET /etc/cloudservices/*" }

# enable personalization
/0062 { /type "allow" /url "/libs/cq/personalization/*" }

# for Enablement features
/0170 { /type "allow" /url "/libs/granite/csrf/token.json*" }
/0171 { /type "allow" /glob "POST /content/sites/*/resources/en/*" }
/0172 { /type "allow" /glob "GET /content/communities/enablement/reports/*" }
/0173 { /type "allow" /glob "GET /content/sites/*" }
/0174 { /type "allow" /glob "GET /content/communities/scorm/*" }
/0175 { /type "allow" /url "GET /content/sites/*" }
/0176 { /type "allow" /url "GET /libs/granite/security/userinfo.json"}
/0177 { /type "allow" /url "GET /libs/granite/security/currentuser.json" }

# Enable CSRF token otherwise nothings works.
/5001 { /type "allow" /glob "GET /libs/granite/csrf/token.json *"}
# Allow SCF User Model to bootstrap as it depends on the granite user
/5002 { /type "allow" /glob "GET /libs/granite/security/currentuser.json*" }

# Allow Communities Site Logout button work
/5003 { /type "allow" /glob "GET /system/sling/logout.html*" }

# Allow i18n to load correctly
/5004 { /type "allow" /glob "GET /libs/cq/i18n/dict.en.json *" }

# Allow social json get pattern.
/6002 { /type "allow" /glob "GET *.social.*.json*" }

# Allow loading of templates
/6003 { /type "allow" /glob "GET /services/social/templates*" }

# Allow SCF User model to check moderator rules
/6005 { /type "allow" /glob "GET /services/social/getLoggedInUser?moderatorCheck=*" }

# Allow CKEditor to load which uses a query pattern not sufficed by regular glob above.
/6006 { /type "allow" /glob "GET /etc/clientlibs/social/thirdparty/ckeditor/*.js?t=*" }
/6007 { /type "allow" /glob "GET /etc/clientlibs/social/thirdparty/ckeditor/*.css?t=*" }

# Allow Fonts from Communities to load
/6050 { /type "allow" /glob "GET *.woff *" }
/6051 { /type "allow" /glob "GET *.ttf *" }

# Enable CQ Security checkpoint for component guide.
/7001 { /type "allow" /glob "GET /libs/cq/security/userinfo.json?cq_ck=*"

```
-->

## 调度程序规则{#dispatcher-rules}

`dispatcher.any`的规则部分定义应根据所请求的URL缓存哪些响应。 对于“社区”，规则部分用于定义不应缓存的内容。

<!-- New code wrt CQDOC-16081, changed by Vishabh on 10 Dec 2020.
-->

```shell
# Never cache the client-side .social.json calls
/0001 { /type "deny" /url "*.social.json*" }

# Never cache the user-specific .json requests
/0002 { /type "deny" /url "/libs/granite/csrf/token.json*" }
/0003 { /type "deny" /url "/libs/granite/security/currentuser.json*" }
/0004 { /type "deny" /url "/libs/granite/security/userinfo.json*" }

# Never cache the private community groups pages in case - add your own deny rules in there
/0005 { /type "deny" /url "/content/*/groups/*" }

# Never cache the assignments page in case the Enablement feature is in use - add your own deny rules in there
/0006 { /type "deny" /url "/content/*/assignments/*" }

# Never cache user generated content
/0208 { /type "deny" /url "/content/usergenerated/*" }
```

<!-- existing content as of Dec 10, wrt CQDOC-16081

```shell
# Never cache the client-side .social.json calls
/0001 { /type "deny" /glob "*.social.json*" }

# Never cache the user-specific .json requests
/0002 { /type "deny" /glob "/libs/granite/csrf/token.json*" }
/0003 { /type "deny" /glob "/libs/granite/security/currentuser.json*" }
/0004 { /type "deny" /glob "/libs/granite/security/userinfo.json*" }

# Never cache the private community groups pages in case - add your own deny rules in there
/0005 { /type "deny" /glob "/content/*/groups/*" }

# Never cache the assignments page in case the Enablement feature is in use - add your own deny rules in there
/0006 { /type "deny" /glob "/content/*/assignments/*" }

# Never cache user generated content
/0208 { /type "deny" /glob "/content/usergenerated/*" }
```
-->

## 疑难解答 {#troubleshooting}

一个主要问题是插入筛选器规则时不注意对早期规则的影响，尤其是添加规则以拒绝访问时。

第一个过滤器模式通常用于拒绝所有内容，以便以受控方式过滤器恢复访问。 当多个过滤器应用到请求时，应用的最后一个过滤器是有效的过滤器。

## 调度程序示例。any {#sample-dispatcher-any}

以下是包含Communities /过滤器和/rules的示例`dispatcher.any`文件。

<!-- New code wrt CQDOC-16081, changed by Vishabh on 10 Dec 2020.
-->

```shell
# Each farm configures a set of load balanced renders (i.e. remote servers)
/farms
  {
  # First farm entry
  /website
    {
    # Request headers that should be forwarded to the remote server.
    /clientheaders
      {
      # Forward all request headers that are end-to-end. If you want
      # to forward a specific set of headers, you'll have to list
      # them here.
      "*"
      }

    # Hostname matching for farm selection (virtual domain addressing)
    /virtualhosts
      {
      # Entries will be compared against the "Host" request header
      # and an optional request URL prefix.
      #
      # Examples:
      #
      #   www.company.com
      #   intranet.*
      #   myhost:8888/mysite
      "*"
      }

    # The load will be balanced among these render instances
    /renders
      {
      /rend01
        {
        # Hostname or IP of the render
        /hostname "127.0.0.1"
        # Port of the render
        /port "4503"
        # Connect timeout in milliseconds, 0 to wait indefinitely
        # /timeout "0"
        }
      }

    # The filter section defines the requests that should be handled by the dispatcher.
    #
    # Entries can be either specified using urls, or elements of the request line:
    #
    # (1) urls will be compared against the entire request line, e.g.:
    #
    #     /0001 { /type "deny" /url "* /index.html *" }
    #
    #   matches request "GET /index.html HTTP/1.1" but not "GET /index.html?a=b HTTP/1.1".
    #
    # (2) method/url/query/protocol will be compared againts the respective elements of
    #   the request line, e.g.:
    #
    #     /0001 { /type "deny" /method "GET" /url "/index.html" }
    #
    #   matches both "GET /index.html" and "GET /index.html?a=b HTTP/1.1".
    #
    # Note: specifying elements of the request line is the preferred method.
    /filter
      {
      # Deny everything first and then allow specific entries
      /0001 { /type "deny" /url "*" }

      # Open consoles
#     /0011 { /type "allow" /url "/admin/*"  }  # allow servlet engine admin
#     /0012 { /type "allow" /url "/crx/*"    }  # allow content repository
#     /0013 { /type "allow" /url "/system/*" }  # allow OSGi console

      # Allow non-public content directories
#     /0021 { /type "allow" /url "/apps/*"   }  # allow apps access
#     /0022 { /type "allow" /url "/bin/*"    }
      /0023 { /type "allow" /url "/content*" }  # disable this rule to allow mapped content only

#     /0024 { /type "allow" /url "/libs/*"   }
#     /0025 { /type "deny"  /url "/libs/shindig/proxy*" } # if you enable /libs close access to proxy

#     /0026 { /type "allow" /url "/home/*"   }
#     /0027 { /type "allow" /url "/tmp/*"    }
#     /0028 { /type "allow" /url "/var/*"    }

      # Enable specific mime types in non-public content directories
      /0041 { /type "allow" /url "*.css"   }  # enable css
      /0042 { /type "allow" /url "*.gif"   }  # enable gifs
      /0043 { /type "allow" /url "*.ico"   }  # enable icos
      /0044 { /type "allow" /url "*.js"    }  # enable javascript
      /0045 { /type "allow" /url "*.png"   }  # enable png
      /0046 { /type "allow" /url "*.swf"   }  # enable flash
      /0047 { /type "allow" /url "*.jpg"   }  # enable jpg
      /0048 { /type "allow" /url "*.jpeg"  }  # enable jpeg

      # Deny content grabbing
      /0081 { /type "deny"  /url "*.infinity.json" }
      /0082 { /type "deny"  /url "*.tidy.json"     }
      /0083 { /type "deny"  /url "*.sysview.xml"   }
      /0084 { /type "deny"  /url "*.docview.json"  }
      /0085 { /type "deny"  /url "*.docview.xml"  }

      /0086 { /type "deny"  /url "*.*[0-9].json" }
#     /0087 { /type "allow" /method "GET" /url "*.1.json" }  # allow one-level json requests

      # Deny query
   /0090 { /type "deny"  /url "*.query.json" }

      #######################################
      ## BEGIN: AEM COMMUNITITES ADDITIONS
   #######################################
   /0050 { /type "allow" /url "/etc/designs/*" }
   /0051 { /type "allow" /url "/etc/clientlibs/*" }
   /0052 { /type "allow" /url "/bin/statistics/tracker/*" }
   /0054 { /type "allow" /url "* /home/users/*/*/profile.form.html*" }
   /0057 { /type "allow" /url "/home/users/*/profile/*" }
   /0059 { /type "allow" /url "/etc/clientcontext/*" }
   /0063 { /type "allow" /url "* /system/sling/logout*" }
   /0064 { /type "allow" /url "/etc/cloudservices/*" }
   /0062 { /type "allow" /url "/libs/cq/personalization/*"  }  # enable personalization

   # For Enablement features
   /0170 { /type "allow" /url "/libs/granite/csrf/token.json*" }
   /0171 { /type "allow" /url "/content/sites/*/resources/en/*" }
   /0172 { /type "allow" /url "/content/communities/enablement/reports/*" }
   /0173 { /type "allow" /url "/content/sites/*" }
   /0174 { /type "allow" /url "/content/communities/scorm/*" }
   /0175 { /type "allow" /url "/content/sites/*" }
   /0176 { /type "allow" /url "/libs/granite/security/userinfo.json"}
   /0177 { /type "allow" /url "/libs/granite/security/currentuser.json" }

      # Enable CSRF token otherwise nothings works.
   /5001 { /type "allow" /url "/libs/granite/csrf/token.json *"}

   # Allow SCF User Model to bootstrap as it depends on the granite user
   /5002 { /type "allow" /url "/libs/granite/security/currentuser.json*" }

      # Allow Communities Site Logout button work
      /5003 { /type "allow" /url "/system/sling/logout.html*" }

   # Allow i18n to load correctly
   /5004 { /type "allow" /url "/libs/cq/i18n/dict.en.json *" }

   # Allow social json get pattern.
   /6002 { /type "allow" /url "*.social.*.json*" }

   # Allow loading of templates
   /6003 { /type "allow" /url "/services/social/templates*" }

   # Allow SCF User model to check moderator rules
   /6005 { /type "allow" /url "/services/social/getLoggedInUser?moderatorCheck=*" }

   # Allow CKEditor to load which uses a query pattern.
   /6006 { /type "allow" /url "/etc/clientlibs/social/thirdparty/ckeditor/*.js?t=*" }
   /6007 { /type "allow" /url "/etc/clientlibs/social/thirdparty/ckeditor/*.css?t=*" }

   # Allow Fonts from Communities to load
   /6050 { /type "allow" /url "*.woff" }
   /6051 { /type "allow" /url "*.ttf" }

      # Enable CQ Security checkpoint for component guide.
   /7001 { /type "allow" /url "/libs/cq/security/userinfo.json?cq_ck=*"}

      #######################################
      ## END: AEM COMMUNITITES ADDITIONS
   #######################################

      }

    # The cache section regulates what responses will be cached and where.
    /cache
      {
      # The docroot must be equal to the document root of the webserver. The
      # dispatcher will store files relative to this directory and subsequent
      # requests may be "declined" by the dispatcher, allowing the webserver
      # to deliver them just like static files.
      /docroot "/opt/dispatcher"

      # Sets the level upto which files named ".stat" will be created in the
      # document root of the webserver. When an activation request for some
      # page is received, only files within the same subtree are affected
      # by the invalidation.
      #/statfileslevel "0"

      # Flag indicating whether to cache responses to requests that contain
      # authorization information.
      /allowAuthorized "1"

      # Flag indicating whether the dispatcher should serve stale content if
      # no remote server is available.
      #/serveStaleOnError "0"

      # The rules section defines what responses should be cached based on
      # the requested URL. Please note that only the following requests can
      # lead to cacheable responses:
      #
      # - HTTP method is GET
      # - URL has an extension
      # - Request has no query string
      # - Request has no "Authorization" header (unless allowAuthorized is 1)
      /rules
        {
        /0000
          {
          # the matching pattern to be compared against the url
          # example: * -> everything
          #        : /foo/bar.* -> only the /foo/bar documents
          #        : /foo/bar/* -> all pages below /foo/bar
          #        : /foo/bar[./]* -> all pages below and /foo/bar itself
          #        : *.html        -> all .html files
          /url "*"
          /type "allow"
          }

      #######################################
      ## BEGIN: AEM COMMUNITITES ADDITIONS
     #######################################

   # Never cache the client-side .social.json calls
   /0001 { /type "deny" /url "*.social.json*" }

   # Never cache the user-specific .json requests
   /0002 { /type "deny" /url "/libs/granite/csrf/token.json*" }
   /0003 { /type "deny" /url "/libs/granite/security/currentuser.json*" }
   /0004 { /type "deny" /url "/libs/granite/security/userinfo.json*" }

   # Never cache the private community groups pages in case - add your own deny rules in there
   /0005 { /type "deny" /url "/content/*/groups/*" }

   # Never cache the assignments page in case the enablement feature is in use - add your own deny rules in there
   /0006 { /type "deny" /url "/content/*/assignments/*" }

      #######################################
      ## END: AEM COMMUNITITES ADDITIONS
      #######################################

        }

      # The invalidate section defines the pages that are "invalidated" after
      # any activation. Please note that the activated page itself and all
      # related documents are flushed on an modification. For example: if the
      # page /foo/bar is activated, all /foo/bar.* files are removed from the
      # cache.
      /invalidate
        {
        /0000
          {
          /url "*"
          /type "deny"
          }
        /0001
          {
          # Consider all HTML files stale after an activation.
          /url "*.html"
          /type "allow"
          }
        /0002
          {
          /url "/etc/segmentation.segment.js"
          /type "allow"
          }
        /0003
          {
          /url "*/analytics.sitecatalyst.js"
          /type "allow"
          }
        }

      # The allowedClients section restricts the client IP addresses that are
      # allowed to issue activation requests.
      /allowedClients
        {
        # Uncomment the following to restrict activation requests to originate
        # from "localhost" only.
        #
        #/0000
        #  {
        #  /url "*"
        #  /type "deny"
        #  }
        #/0001
        #  {
        #  /url "127.0.0.1"
        #  /type "allow"
        #  }
        }

      # The ignoreUrlParams section contains query string parameter names that
      # should be ignored when determining whether some request's output can be
      # cached or delivered from cache.
      #
      # In this example configuration, the "q" parameter will be ignored.
      #/ignoreUrlParams
      #  {
      #  /0001 { /url "*" /type "deny" }
      #  /0002 { /url "q" /type "allow" }
      #  }

    /enableTTL "1"

      }

    # The statistics sections dictates how the load should be balanced among the
    # renders according to the media-type.
    /statistics
      {
      /categories
        {
        /html
          {
          /url "*.html"
          }
        /others
          {
          /url "*"
          }
        }
      }
    }
  }
```

<!-- existing content as of Dec 10, wrt CQDOC-16081

```shell
# Each farm configures a set of load balanced renders (i.e. remote servers)
/farms
  {
  # First farm entry
  /website
    {
    # Request headers that should be forwarded to the remote server.
    /clientheaders
      {
      # Forward all request headers that are end-to-end. If you want
      # to forward a specific set of headers, you'll have to list
      # them here.
      "*"
      }

    # Hostname globbing for farm selection (virtual domain addressing)
    /virtualhosts
      {
      # Entries will be compared against the "Host" request header
      # and an optional request URL prefix.
      #
      # Examples:
      #
      #   www.company.com
      #   intranet.*
      #   myhost:8888/mysite
      "*"
      }

    # The load will be balanced among these render instances
    /renders
      {
      /rend01
        {
        # Hostname or IP of the render
        /hostname "127.0.0.1"
        # Port of the render
        /port "4503"
        # Connect timeout in milliseconds, 0 to wait indefinitely
        # /timeout "0"
        }
      }

    # The filter section defines the requests that should be handled by the dispatcher.
    #
    # Entries can be either specified using globs, or elements of the request line:
    #
    # (1) globs will be compared against the entire request line, e.g.:
    #
    #     /0001 { /type "deny" /glob "* /index.html *" }
    #
    #   matches request "GET /index.html HTTP/1.1" but not "GET /index.html?a=b HTTP/1.1".
    #
    # (2) method/url/query/protocol will be compared againts the respective elements of
    #   the request line, e.g.:
    #
    #     /0001 { /type "deny" /method "GET" /url "/index.html" }
    #
    #   matches both "GET /index.html" and "GET /index.html?a=b HTTP/1.1".
    #
    # Note: specifying elements of the request line is the preferred method.
    /filter
      {
      # Deny everything first and then allow specific entries
      /0001 { /type "deny" /glob "*" }

      # Open consoles
#     /0011 { /type "allow" /url "/admin/*"  }  # allow servlet engine admin
#     /0012 { /type "allow" /url "/crx/*"    }  # allow content repository
#     /0013 { /type "allow" /url "/system/*" }  # allow OSGi console

      # Allow non-public content directories
#     /0021 { /type "allow" /url "/apps/*"   }  # allow apps access
#     /0022 { /type "allow" /url "/bin/*"    }
      /0023 { /type "allow" /url "/content*" }  # disable this rule to allow mapped content only

#     /0024 { /type "allow" /url "/libs/*"   }
#     /0025 { /type "deny"  /url "/libs/shindig/proxy*" } # if you enable /libs close access to proxy

#     /0026 { /type "allow" /url "/home/*"   }
#     /0027 { /type "allow" /url "/tmp/*"    }
#     /0028 { /type "allow" /url "/var/*"    }

      # Enable specific mime types in non-public content directories
      /0041 { /type "allow" /url "*.css"   }  # enable css
      /0042 { /type "allow" /url "*.gif"   }  # enable gifs
      /0043 { /type "allow" /url "*.ico"   }  # enable icos
      /0044 { /type "allow" /url "*.js"    }  # enable javascript
      /0045 { /type "allow" /url "*.png"   }  # enable png
      /0046 { /type "allow" /url "*.swf"   }  # enable flash
      /0047 { /type "allow" /url "*.jpg"   }  # enable jpg
      /0048 { /type "allow" /url "*.jpeg"  }  # enable jpeg

      # Deny content grabbing
      /0081 { /type "deny"  /url "*.infinity.json" }
      /0082 { /type "deny"  /url "*.tidy.json"     }
      /0083 { /type "deny"  /url "*.sysview.xml"   }
      /0084 { /type "deny"  /url "*.docview.json"  }
      /0085 { /type "deny"  /url "*.docview.xml"  }

      /0086 { /type "deny"  /url "*.*[0-9].json" }
#     /0087 { /type "allow" /method "GET" /url "*.1.json" }  # allow one-level json requests

      # Deny query
   /0090 { /type "deny"  /url "*.query.json" }

      #######################################
      ## BEGIN: AEM COMMUNITITES ADDITIONS
   #######################################
   /0050 { /type "allow" /glob "GET /etc/designs/*" }
   /0051 { /type "allow" /glob "GET /etc/clientlibs/*" }
   /0052 { /type "allow" /glob "GET /bin/statistics/tracker/*" }
   /0054 { /type "allow" /glob "* /home/users/*/*/profile.form.html*" }
   /0057 { /type "allow" /glob "GET /home/users/*/profile/*" }
   /0059 { /type "allow" /glob "GET /etc/clientcontext/*" }
   /0063 { /type "allow" /glob "* /system/sling/logout*" }
   /0064 { /type "allow" /glob "GET /etc/cloudservices/*" }
   /0062 { /type "allow" /url "/libs/cq/personalization/*"  }  # enable personalization

   # For Enablement features
   /0170 { /type "allow" /url "/libs/granite/csrf/token.json*" }
   /0171 { /type "allow" /glob "POST /content/sites/*/resources/en/*" }
   /0172 { /type "allow" /glob "GET /content/communities/enablement/reports/*" }
   /0173 { /type "allow" /glob "GET /content/sites/*" }
   /0174 { /type "allow" /glob "GET /content/communities/scorm/*" }
   /0175 { /type "allow" /url "GET /content/sites/*" }
   /0176 { /type "allow" /url "GET /libs/granite/security/userinfo.json"}
   /0177 { /type "allow" /url "GET /libs/granite/security/currentuser.json" }

      # Enable CSRF token otherwise nothings works.
   /5001 { /type "allow" /glob "GET /libs/granite/csrf/token.json *"}

   # Allow SCF User Model to bootstrap as it depends on the granite user
   /5002 { /type "allow" /glob "GET /libs/granite/security/currentuser.json*" }

      # Allow Communities Site Logout button work
      /5003 { /type "allow" /glob "GET /system/sling/logout.html*" }

   # Allow i18n to load correctly
   /5004 { /type "allow" /glob "GET /libs/cq/i18n/dict.en.json *" }

   # Allow social json get pattern.
   /6002 { /type "allow" /glob "GET *.social.*.json*" }

   # Allow loading of templates
   /6003 { /type "allow" /glob "GET /services/social/templates*" }

   # Allow SCF User model to check moderator rules
   /6005 { /type "allow" /glob "GET /services/social/getLoggedInUser?moderatorCheck=*" }

   # Allow CKEditor to load which uses a query pattern not sufficed by regular glob above.
   /6006 { /type "allow" /glob "GET /etc/clientlibs/social/thirdparty/ckeditor/*.js?t=*" }
   /6007 { /type "allow" /glob "GET /etc/clientlibs/social/thirdparty/ckeditor/*.css?t=*" }

   # Allow Fonts from Communities to load
   /6050 { /type "allow" /glob "GET *.woff *" }
   /6051 { /type "allow" /glob "GET *.ttf *" }

      # Enable CQ Security checkpoint for component guide.
   /7001 { /type "allow" /glob "GET /libs/cq/security/userinfo.json?cq_ck=*"}

      #######################################
      ## END: AEM COMMUNITITES ADDITIONS
   #######################################

      }

    # The cache section regulates what responses will be cached and where.
    /cache
      {
      # The docroot must be equal to the document root of the webserver. The
      # dispatcher will store files relative to this directory and subsequent
      # requests may be "declined" by the dispatcher, allowing the webserver
      # to deliver them just like static files.
      /docroot "/opt/dispatcher"

      # Sets the level upto which files named ".stat" will be created in the
      # document root of the webserver. When an activation request for some
      # page is received, only files within the same subtree are affected
      # by the invalidation.
      #/statfileslevel "0"

      # Flag indicating whether to cache responses to requests that contain
      # authorization information.
      /allowAuthorized "1"

      # Flag indicating whether the dispatcher should serve stale content if
      # no remote server is available.
      #/serveStaleOnError "0"

      # The rules section defines what responses should be cached based on
      # the requested URL. Please note that only the following requests can
      # lead to cacheable responses:
      #
      # - HTTP method is GET
      # - URL has an extension
      # - Request has no query string
      # - Request has no "Authorization" header (unless allowAuthorized is 1)
      /rules
        {
        /0000
          {
          # the globbing pattern to be compared against the url
          # example: * -> everything
          #        : /foo/bar.* -> only the /foo/bar documents
          #        : /foo/bar/* -> all pages below /foo/bar
          #        : /foo/bar[./]* -> all pages below and /foo/bar itself
          #        : *.html        -> all .html files
          /glob "*"
          /type "allow"
          }

      #######################################
      ## BEGIN: AEM COMMUNITITES ADDITIONS
     #######################################

   # Never cache the client-side .social.json calls
   /0001 { /type "deny" /glob "*.social.json*" }

   # Never cache the user-specific .json requests
   /0002 { /type "deny" /glob "/libs/granite/csrf/token.json*" }
   /0003 { /type "deny" /glob "/libs/granite/security/currentuser.json*" }
   /0004 { /type "deny" /glob "/libs/granite/security/userinfo.json*" }

   # Never cache the private community groups pages in case - add your own deny rules in there
   /0005 { /type "deny" /glob "/content/*/groups/*" }

   # Never cache the assignments page in case the enablement feature is in use - add your own deny rules in there
   /0006 { /type "deny" /glob "/content/*/assignments/*" }

      #######################################
      ## END: AEM COMMUNITITES ADDITIONS
      #######################################

        }

      # The invalidate section defines the pages that are "invalidated" after
      # any activation. Please note that the activated page itself and all
      # related documents are flushed on an modification. For example: if the
      # page /foo/bar is activated, all /foo/bar.* files are removed from the
      # cache.
      /invalidate
        {
        /0000
          {
          /glob "*"
          /type "deny"
          }
        /0001
          {
          # Consider all HTML files stale after an activation.
          /glob "*.html"
          /type "allow"
          }
        /0002
          {
          /glob "/etc/segmentation.segment.js"
          /type "allow"
          }
        /0003
          {
          /glob "*/analytics.sitecatalyst.js"
          /type "allow"
          }
        }

      # The allowedClients section restricts the client IP addresses that are
      # allowed to issue activation requests.
      /allowedClients
        {
        # Uncomment the following to restrict activation requests to originate
        # from "localhost" only.
        #
        #/0000
        #  {
        #  /glob "*"
        #  /type "deny"
        #  }
        #/0001
        #  {
        #  /glob "127.0.0.1"
        #  /type "allow"
        #  }
        }

      # The ignoreUrlParams section contains query string parameter names that
      # should be ignored when determining whether some request's output can be
      # cached or delivered from cache.
      #
      # In this example configuration, the "q" parameter will be ignored.
      #/ignoreUrlParams
      #  {
      #  /0001 { /glob "*" /type "deny" }
      #  /0002 { /glob "q" /type "allow" }
      #  }

    /enableTTL "1"

      }

    # The statistics sections dictates how the load should be balanced among the
    # renders according to the media-type.
    /statistics
      {
      /categories
        {
        /html
          {
          /glob "*.html"
          }
        /others
          {
          /glob "*"
          }
        }
      }
    }
  }

```

-->

