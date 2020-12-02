---
title: Client Context Javascript API
seo-title: Client Context Javascript API
description: Client Context的Javascript API
seo-description: Client Context的Javascript API
uuid: be58998c-f23e-4768-8394-1f1ad3994c4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: a6e5810b-dac5-4137-93cf-5d8d53cacc49
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '3163'
ht-degree: 2%

---


# Client Context Javascript API{#client-context-javascript-api}

## CQ_Analytics.ClientContextMgr {#cq-analytics-clientcontextmgr}

CQ_Analytics.ClientContextMgr对象是一个单一的例子，它包含一组自注册的会话存储，并提供用于注册、持久和管理会话存储的方法。

扩展CQ_Analytics.PersistedSessionStore。

### 方法{#methods}

#### getRegisteredStore(name){#getregisteredstore-name}

返回指定名称的会话存储。 另请参阅[访问会话存储](/help/sites-developing/client-context.md#accessing-session-stores)。

**参数**

* 名称：字符串。 会话存储的名称。

**退货**

表示给定名称的会话存储的CQ_Analytics.SessionStore对象。 当给定名称不存在存储时返回`null`。

#### register(sessionstore){#register-sessionstore}

使用Client Context注册会话存储。 完成时触发存储寄存器和存储更新事件。

**参数**

* sessionstore:CQ_Analytics.SessionStore。 要注册的会话存储对象。

**退货**

无返回值。

## CQ_Analytics.ClientContextUtils {#cq-analytics-clientcontextutils}

提供监听会话存储激活和注册的方法。 另请参阅[检查会话存储是否已定义和已初始化](/help/sites-developing/client-context.md#checking-that-a-session-store-is-defined-and-initialized)。

### 方法{#methods-1}

#### onStoreInitialized(storeName, callback, delay){#onstoreinitialized-storename-callback-delay}

注册在初始化会话存储时调用的回调函数。 对于已初始化多次的存储，指定回调延迟，以便回调函数只被调用一次：

* 当存储器在先前初始化的延迟期间被初始化时，取消先前的函数调用，并且再次为当前初始化调用函数。
* 如果延迟期在后续初始化发生之前失效，则执行回调函数两次。

例如，会话存储基于JSON对象，并通过JSON请求进行检索。 可以采用以下初始化方案：

* 请求完成，数据被检索并加载到存储中。 在这种情况下，初始化只进行一次。
* 请求失败（超时）。 在这种情况下，不会进行初始化，并且存储中没有数据。
* 存储预填充了默认值（init属性），但请求失败（超时）。 只有一个具有默认值的初始化。
* 商店已预填充。

当延迟设置为`true`或毫秒时，该方法会在调用回调方法之前等待。 如果在延迟通过之前触发了另一个初始化事件，则会等到延迟时间超出时再触发，而没有初始化事件。 这允许等待第二个初始化事件被触发，并在最优情况下调用回调函数。

**参数**

* storeName:字符串。 要添加监听器的会话存储的名称。
* 回调：功能。 存储初始化时要调用的函数。
* 延迟：布尔值或数字。 延迟调用回调函数的时间（以毫秒为单位）。 布尔值`true`使用默认延迟`200 ms`。 布尔值`false`或负数不会使用延迟。

**退货**

无返回值。

#### onStoreRegistered(storeName, callback){#onstoreregistered-storename-callback}

注册在注册会话存储时调用的回调函数。 将存储注册到[CQ_Analytics.ClientContextMgr](#cq-analytics-clientcontextmgr)时，将发生注册事件。

**参数**

* storeName:字符串。 要添加监听器的会话存储的名称。
* 回调：功能。 存储初始化时要调用的函数。

**退货**

无返回值。

## CQ_Analytics.JSONPStore {#cq-analytics-jsonpstore}

包含JSON数据的非持久会话存储。 从外部JSONP服务检索数据。 使用`getInstance`或`getRegisteredInstance`方法创建此类的实例。

扩展CQ_Analytics.JSONStore。

### 属性 {#properties}

有关继承的属性，请参阅CQ_Analytics.JSONStore和CQ_Analytics.SessonStore。

### 方法{#methods-2}

另请参阅CQ_Analytics.JSONStore和CQ_Analytics.SessonStore以了解继承的方法。

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback){#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback}

创建CQ_Analytics.JSONPStore对象。

**参数**

* storeName:字符串。 用作STORENAME属性的名称。 STOREKEY属性的值设置为storeName，并带有所有大写字符。 如果未提供storeName，则该方法返回null。
* serviceURL:字符串。 JSONP服务的URL
* dynamicData:（可选）对象。 在调用回调函数之前，要追加到存储的初始化数据的JSON数据。
* deferLoading:（可选）布尔值。 如果值为true，则在创建对象时不会调用JSONP服务。 如果值为false，则调用JSONP服务。
* loadingCallback:（可选）字符串。 用于调用处理JSONP服务返回的JSONP对象的函数的名称。 回调函数必须定义一个参数，该参数是CQ_Analytics.JSONPStore对象。

**退货**

新的CQ_Analytics.JSONPStore对象；如果storeName为null，则为null。

#### getServiceURL(){#getserviceurl}

检索此对象用于检索JSON数据的JSONP服务的URL。

**参数**

无.

**退货**

表示服务URL的字符串；如果未配置服务URL，则为null。

#### load(serviceURL, dynamicData, callback){#load-serviceurl-dynamicdata-callback}

呼叫JSONP服务。 JSONP URL是后缀有给予回调函数名称的服务URL。

**参数**

* serviceURL:（可选）字符串。 要呼叫的JSONP服务。 值为null将导致使用已配置的服务URL。 非空值设置要用于此对象的JSONP服务。 （请参阅setServiceURL。）
* dynamicData:（可选）对象。 在调用回调函数之前，要追加到存储的初始化数据的JSON数据。
* 回调：（可选）字符串。 用于调用处理JSONP服务返回的JSONP对象的函数的名称。 回调函数必须定义一个参数，该参数是CQ_Analytics.JSONPStore对象。

**退货**

无返回值。

#### registerNewInstance(storeName, serviceURL, dynamicData, callback){#registernewinstance-storename-serviceurl-dynamicdata-callback}

创建CQ_Analytics.JSONPStore对象，并在Client Context中注册该存储。

**参数**

* storeName:字符串。 用作STORENAME属性的名称。 STOREKEY属性的值设置为storeName，并带有所有大写字符。 如果未提供storeName，则该方法返回null。
* serviceURL:（可选）字符串。 JSONP服务的URL。
* dynamicData:（可选）对象。 在调用回调函数之前，要追加到存储的初始化数据的JSON数据。
* 回调：（可选）字符串。 用于调用处理JSONP服务返回的JSONP对象的函数的名称。 回调函数必须定义一个参数，该参数是CQ_Analytics.JSONPStore对象。

**退货**

已注册的CQ_Analytics.JSONPStore对象。

#### setServiceURL(serviceURL){#setserviceurl-serviceurl}

设置JSONP服务的URL以用于检索JSON数据。

**参数**

* serviceURL:字符串。 提供JSON数据的JSONP服务的URL

**退货**

无返回值。

## CQ_Analytics.JSONStore {#cq-analytics-jsonstore}

JSON对象的容器。 创建此类的实例以创建包含JSON数据的非持久会话存储：

`myjsonstore = new CQ_Analytics.JSONStore`

您可以定义一组数据，在初始化时填充存储。

扩展CQ_Analytics.SessionStore。

### 属性 {#properties-1}

#### STOREKEY {#storekey}

标识商店的密钥。 使用`getInstance`方法检索此值。

#### STORENAME {#storename}

商店的名称。 使用`getInstance`方法检索此值。

### 方法{#methods-3}

另请参阅CQ_Analytics.SessionStore以了解继承的方法。

#### 清除() {#clear}

删除会话存储数据并删除所有初始化属性。

**参数**

无.

**退货**

无返回值。

#### getInstance(storeName,jsonData){#getinstance-storename-jsondata}

使用给定名称创建CQ_Analytics.JSONStore对象，并使用给定JSON数据进行初始化（调用initJSON方法）。

**参数**

* storeName:字符串。 用作STORENAME属性的名称。 STOREKEY属性的值设置为storeName，并带有所有大写字符。
* json数据：对象。 包含JSON数据的对象。

**退货**

CQ_Analytics.JSONStore对象。

#### getJSON(){#getjson}

以JSON格式检索会话存储的数据。

**参数**

无.

**退货**

以JSON格式表示存储数据的对象。

#### init(){#init}

清除会话存储，并用初始化属性对其进行初始化。 将初始化标志设置为`true`，然后触发`initialize`和`update`事件。

**参数**

无.

**退货**

没有返回的数据。

#### initJSON(jsonData, doNotClear){#initjson-jsondata-donotclear}

根据JSON对象中的数据创建初始化属性。 您可以选择删除所有现有初始化属性。

属性名称从JSON对象中的数据层次结构派生。 以下示例代码表示JSON对象：

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

在此示例中，在存储中创建了以下属性：

```xml
A: "valueA"
B/B1: "valueBB1"
```

**参数**

* json数据：包含要存储的数据的JSON对象。
* doNotClear:如果值为true，则保留现有初始化属性并添加从JSON对象派生的属性。 如果值为false，则在添加从JSON对象派生的属性之前删除现有初始化属性。

**退货**

无返回值。

#### registerNewInstance(storeName, jsonData){#registernewinstance-storename-jsondata}

使用给定名称创建CQ_Analytics.JSONStore对象，并使用给定JSON数据进行初始化（调用initJSON方法）。 新对象会自动注册到Clickstream Cloud Manager。

**参数**

* storeName:字符串。 用作STORENAME属性的名称。 STOREKEY属性的值设置为storeName，并带有所有大写字符。
* json数据：对象。 包含JSON数据的对象。

**退货**

CQ_Analytics.JSONStore对象。

## CQ_Analytics.Ovearable {#cq-analytics-observable}

触发事件并允许其他对象侦听这些事件并做出响应。 扩展此类的类会触发导致调用监听器的事件。

### 方法{#methods-4}

#### addListener(事件、fct、范围){#addlistener-event-fct-scope}

为事件注册监听器。 另请参阅[创建监听器以对会话存储更新做出响应](/help/sites-developing/client-context.md#creating-a-listener-to-react-to-a-session-store-update)。

**参数**

* 事件:字符串。 要监听的事件的名称。
* fct:功能。 发生事件时调用的函数。
* 范围：（可选）对象。 执行处理函数的范围。 处理函数的“this”上下文。

**退货**

无返回值。

#### removeListener(事件, fct){#removelistener-event-fct}

删除事件的给定事件处理函数。

**参数**

* 事件:字符串。 事件的名称。
* fct:功能。 事件处理程序。

**退货**

无返回值。

## CQ_Analytics.PersitedJSONPStore {#cq-analyics-persistedjsonpstore}

从远程JSONP服务检索的JSON对象的持久容器。

扩展CQ_Analytics.PersitedJSONStore。

### 方法{#methods-5}

另请参阅CQ_Analytics.PersitedJSONStore以获取继承方法。

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback){#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback-1}

创建CQ_Analytics.PersistedJSONPStore对象。

**参数**

* storeName:字符串。 用作STORENAME属性的名称。 STOREKEY属性的值设置为storeName，并带有所有大写字符。 如果未提供storeName，则该方法返回null。
* serviceURL:字符串。 JSONP服务的URL
* dynamicData:（可选）对象。 在调用回调函数之前，要追加到存储的初始化数据的JSON数据。
* deferLoading:（可选）布尔值。 如果值为true，则在创建对象时不会调用JSONP服务。 如果值为false，则调用JSONP服务。
* loadingCallback:（可选）字符串。 用于调用处理JSONP服务返回的JSONP对象的函数的名称。 回调函数必须定义一个参数，该参数是CQ_Analytics.JSONPStore对象。

**退货**

新的CQ_Analytics.PersistedJSONPStore对象；如果storeName为null，则为null。

#### getServiceURL(){#getserviceurl-1}

检索此对象用于检索JSON数据的JSONP服务的URL。

**参数**

无.

**退货**

表示服务URL的字符串；如果未配置服务URL，则为null。

#### load(serviceURL, dynamicData, callback){#load-serviceurl-dynamicdata-callback-1}

呼叫JSONP服务。 JSONP URL是后缀有给予回调函数名称的服务URL。

**参数**

* serviceURL:（可选）字符串。 要呼叫的JSONP服务。 值为null将导致使用已配置的服务URL。 非空值设置要用于此对象的JSONP服务。 （请参阅setServiceURL。）
* dynamicData:（可选）对象。 在调用回调函数之前，要追加到存储的初始化数据的JSON数据。
* 回调：（可选）字符串。 用于调用处理JSONP服务返回的JSONP对象的函数的名称。 回调函数必须定义一个参数，该参数是CQ_Analytics.JSONPStore对象。

**退货**

无返回值。

#### registerNewInstance(storeName, serviceURL, dynamicData, callback){#registernewinstance-storename-serviceurl-dynamicdata-callback-1}

创建CQ_Analytics.PersistedJSONPStore对象，并在Client Context中注册该存储。

**参数**

* storeName:字符串。 用作STORENAME属性的名称。 STOREKEY属性的值设置为storeName，并带有所有大写字符。 如果未提供storeName，则该方法返回null。
* serviceURL:（可选）字符串。 JSONP服务的URL。
* dynamicData:（可选）对象。 在调用回调函数之前，要追加到存储的初始化数据的JSON数据。
* 回调：（可选）字符串。 用于调用处理JSONP服务返回的JSONP对象的函数的名称。 回调函数必须定义一个参数，该参数是CQ_Analytics.JSONPStore对象。

**退货**

已注册的CQ_Analytics.PersitedJSONPStore对象。

#### setServiceURL(serviceURL){#setserviceurl-serviceurl-1}

设置JSONP服务的URL以用于检索JSON数据。

**参数**

* serviceURL:字符串。 提供JSON数据的JSONP服务的URL

**退货**

无返回值。

## CQ_Analytics.PersitedJSONStore {#cq-analytics-persistedjsonstore}

JSON对象的持久容器。

扩展`CQ_Analytics.PersistedSessionStore`。

### 属性 {#properties-2}

#### STOREKEY {#storekey-1}

标识商店的密钥。 使用`getInstance`方法检索此值。

#### STORENAME {#storename-1}

商店的名称。 使用`getInstance`方法检索此值。

### 方法{#methods-6}

另请参阅CQ_Analytics.PersistedSessionStore以了解继承的方法。

#### getInstance(storeName,jsonData){#getinstance-storename-jsondata-1}

使用给定名称创建CQ_Analytics.PersistedJSONStore对象，并使用给定JSON数据进行初始化（调用initJSON方法）。

**参数**

* storeName:字符串。 用作STORENAME属性的名称。 STOREKEY属性的值设置为storeName，并带有所有大写字符。
* json数据：对象。 包含JSON数据的对象。

**退货**

CQ_Analytics.PersitedJSONStore对象。

#### getJSON(){#getjson-1}

以JSON格式检索会话存储的数据。

**参数**

无.

**退货**

以JSON格式表示存储数据的对象。

#### initJSON(jsonData, doNotClear){#initjson-jsondata-donotclear-1}

根据JSON对象中的数据创建初始化属性。 您可以选择删除所有现有初始化属性。

属性名称从JSON对象中的数据层次结构派生。 以下示例代码表示JSON对象：

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

在此示例中，在存储中创建了以下属性：

```xml
A: "valueA"
B/B1: "valueBB1"
```

**参数**

* json数据：包含要存储的数据的JSON对象。
* doNotClear:如果值为true，则保留现有初始化属性并添加从JSON对象派生的属性。 如果值为false，则在添加从JSON对象派生的属性之前删除现有初始化属性。

**退货**

无返回值。

#### registerNewInstance(storeName, jsonData){#registernewinstance-storename-jsondata-1}

使用给定名称创建CQ_Analytics.PersistedJSONStore对象，并使用给定JSON数据进行初始化（调用initJSON方法）。 新对象将自动注册到Client Context Manager。

**参数**

* storeName:字符串。 用作STORENAME属性的名称。 STOREKEY属性的值设置为storeName，并带有所有大写字符。
* json数据：对象。 包含JSON数据的对象。

**退货**

CQ_Analytics.PersitedJSONStore对象。

## CQ_Analytics.PersistedSessionStore {#cq-analytics-persistedsessionstore}

属性和值的容器。 数据将使用CQ_Analytics.SessionPersistence进行保留。 创建此类的实例以创建持久会话存储：

`mypersistedstore = new CQ_Analytics.PersistedSessionStore`

扩展CQ_Analytics.SessionStore。

### 属性 {#properties-3}

#### STOREKEY {#storekey-2}

默认值为 `key`.

### 方法{#methods-7}

有关继承的方法，请参阅CQ_Analytics.SessionStore。

当使用继承的方法`clear`、`setProperty`、`setProperties`和`removeProperty`来更改存储数据时，将自动保留更改，除非更改的属性被标记为notPersisted。

#### getStoreKey(){#getstorekey}

检索`STOREKEY`属性。

**参数**

无

**退货**

`STOREKEY`属性的值。

#### isPersisted(name){#ispersisted-name}

确定是否保留数据属性。

**参数**

* 名称：字符串。 属性的名称。

**退货**

如果属性被保留，则布尔值为`true`；如果值不是保留属性，则布尔值为`false`。

#### persist(){#persist}

持续会话存储。 默认持久性模式使用浏览器`localStorage`，使用`ClientSidePersistence`作为名称(`window.localStorage.set("ClientSidePersistance", store);`)

如果localStorage不可用或不可写，则该存储将作为窗口的属性进行保留。

完成时触发`persist`事件。

**参数**

无

**退货**

无返回值。

#### reset(deferEvent){#reset-deferevent}

从存储中删除所有数据属性并保留存储。 （可选）完成后不触发`udpate`事件。

**参数**

* deferEvent:值为true可防止触发`update`事件。 值`false`导致更新事件触发。

**退货**

无返回值。

#### setNonPersisted(name){#setnonpersisted-name}

将数据属性标记为未保留。

**参数**

* 名称：字符串。 不要保留的属性的名称。

**退货**

无返回值。

## CQ_Analytics.SessionStore {#cq-analytics-sessionstore}

CQ_Analytics.SessionStore表示会话存储。 创建此类的实例以创建会话存储：

`mystore = new CQ_Analytics.SessionStore`

扩展CQ_Analytics.Ovetable。

### 属性 {#properties-4}

#### STORENAME {#storename-2}

会话存储的名称。 使用getName检索此属性的值。

### 方法{#methods-8}

#### addInitProperty(name, value){#addinitproperty-name-value}

向会话存储初始化数据添加属性和值。

使用loadInitProperties用初始化值填充会话存储数据。

**参数**

* 名称：字符串。 要添加的属性的名称。
* value:字符串。 要添加的属性的值。

**退货**

无返回值。

#### 清除() {#clear-1}

从存储中删除所有数据属性。

**参数**

无.

**退货**

无返回值。

#### getData(excluded){#getdata-excluded}

返回存储数据。 （可选）从数据中排除名称属性。 如果存储的数据属性不存在，则调用`init`方法。

**参数**

excluded:（可选）要从返回的数据中排除的属性名称的数组。

**退货**

属性及其值的对象。

#### getInitProperty(name){#getinitproperty-name}

检索数据属性的值。

**参数**

* 名称：字符串。 要检索的数据属性的名称。

**退货**

数据属性的值。 如果会话存储不包含给定名称的属性，则返回`null`。

#### getName(){#getname}

返回会话存储的名称。

**参数**

无.

**退货**

表示存储名称的字符串值。

#### getProperty(name, raw){#getproperty-name-raw}

返回属性的值。 该值将作为原始属性或XSS筛选的值返回。 如果存储的数据属性不存在，则调用`init`方法。

**参数**

* 名称：字符串。 要检索的数据属性的名称。
* raw:布尔值。 如果值为true，则返回原始属性值。 如果值为false，则返回的值将经过XSS筛选。

**退货**

数据属性的值。

#### getPropertyNames(excluded){#getpropertynames-excluded}

返回会话存储所包含属性的名称。 如果存储的数据属性不存在，则调用`init`方法。

**参数**

excluded:（可选）要从结果中忽略的属性名称的数组。

**退货**

表示会话属性名称的字符串值的数组。

#### getSessionStore(){#getsessionstore}

返回附加到当前对象的会话存储。

**参数**

无.

**退货**

这个

#### init(){#init-1}

将存储标记为已初始化，并触发`initialize`事件。

**参数**

无.

**退货**

无返回值。

#### isInitialized(){#isinitialized}

指示会话存储是否已初始化。

**参数**

无.

**退货**

如果存储已初始化，则值为`true`；如果存储未初始化，则值为`false`。

#### loadInitProperties(obj, setValues){#loadinitproperties-obj-setvalues}

将给定对象的属性添加到会话存储的初始化数据。 或者，对象数据也添加到存储数据。

**参数**

* obj:包含可枚举属性的对象。
* setValues:如果为true，则当存储数据尚未包含同名的属性时，obj属性将添加到会话存储数据。 如果为false，则不向会话存储数据添加任何数据。

**退货**

无返回值。

#### removeProperty(name){#removeproperty-name}

从会话存储中删除属性。 完成时触发`update`事件。 如果存储的数据属性不存在，则调用`init`方法。

**参数**

* 名称：字符串。 要删除的属性的名称。

**退货**

无返回值。

#### 重置() {#reset}

恢复数据存储的初始值。 默认实现只删除所有数据。 完成时触发`update`事件。

**参数**

无.

**退货**

无返回值。

#### setProperties(properties){#setproperties-properties}

设置多个属性的值。 完成时触发`update`事件。 如果存储的数据属性不存在，则调用`init`方法。

**参数**

* 属性：对象。 包含可枚举属性的对象。 每个属性名称和值都会添加到商店。

**退货**

无返回值。

#### setProperty(name, value){#setproperty-name-value}

设置属性的值。 完成时触发`update`事件。 如果存储的数据属性不存在，则调用`init`方法。

**参数**

* 名称：字符串。 属性的名称。
* value:字符串。 属性值。

**退货**

无返回值。
