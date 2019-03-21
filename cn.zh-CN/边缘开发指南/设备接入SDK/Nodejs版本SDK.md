# Nodejs版本SDK {#concept_ycs_pcp_32b .concept}

设备接入SDK用于您在边缘计算节点上开发驱动，将设备连接到边缘计算节点，进而连接到物联网平台。Node.js版本开源的SDK源码请见[开源的Node.js库](https://github.com/aliyun/linkedge-thing-access-sdk-nodejs)。

## Node.js版本设备接入SDK使用说明 {#section_o42_tbs_n2b .section}

使用设备接入SDK前需要执行npm install linkedge-thing-access-sdk命令，安装SDK。

设备接入SDK的使用格式如下：

```
const {
    ThingAccessClient
} = require('linkedge-thing-access-sdk');
```

## ThingAccessClient {#section_qyh_4gm_n2b .section}

设备接入客户端，您可以通过该客户端来主动上报设备属性或事件，也可被动接受云端下发的指令。

**常量定义**

|名称|类型|描述|
|--|--|--|
|PRODUCT\_KEY|String|配置对象（传给ThingAccessClient构造函数）的键值，指定云端分配的productKey。|
|DEVICE\_NAME|String|配置对象（传给ThingAccessClient构造函数）的键值，指定云端分配的deviceName。|
|LOCAL\_NAME|String|配置对象（传给ThingAccessClient构造函数）的键值，指定本地自定义的设备名。|
|RESULT\_SUCCESS|Number|操作成功。用于回调函数返回状态码。|
|RESULT\_FAILURE|Number|操作失败。用于回调函数返回状态码。|
|CALL\_SERVICE|String|回调对象（传给ThingAccessClient构造函数）的键值，指定调用设备服务回调函数。|
|GET\_PROPERTIES|String|回调对象（传给ThingAccessClient构造函数）的键值，指定获取设备属性回调函数。|
|SET\_PROPERTIES|String|回调对象（传给ThingAccessClient构造函数）的键值，指定设置设备属性回调函数。|

## ThingAccessClient\(config, callbacks\) {#section_tcz_ydr_n2b .section}

**功能介绍**

构造函数，使用指定的config和callbacks构造。

**请求参数**

|名称|类型|描述|
|--|--|--|
|config|Object|元数据，用于配置该客户端。取值格式为：```
{
    "productKey": "Your Product Key", 
    "deviceName": "Your Device Name"
}
```

|
|callbacks|Object|回调函数对象。-   指定设置设备属性的回调参数，请参见[callbacks.setProperties](#)
-   指定获取设备属性的回调参数，请参见[callbacks.getProperties](#)
-   指定调用设备服务的回调参数，请参见[callbacks.callService](#)

|

**回调说明**

```
callbacks: {
  setProperties: function(properties) {},
  getProperties: function(keys) {},
  callService: function(name, args) {}
}
```

## callbacks.setProperties {#section_test1 .section}

**功能介绍**

设置具体设备属性的回调函数。通过回调函数，实现设置设备的属性。

**请求参数**

|名称|类型|描述|
|--|--|--|
|properties|Object|设置属性的对象，取值格式为：```
{
    "key1": "value1", 
    "key2": "value2"
}
```

|

## callbacks.getProperties {#section_test2 .section}

**功能介绍**

获取具体设备属性的回调函数。通过回调函数，实现获取设备的属性。

**请求参数**

|名称|类型|描述|
|--|--|--|
|keys|String\[\]|获取属性对应的名称，取值格式为：```
['key1', 'key2']
```

|

## callbacks.callService {#section_test3 .section}

**功能介绍**

调用设备服务回调函数。通过回调函数，实现调动设备服务。

**请求参数**

|名称|类型|描述|
|--|--|--|
|name|String|设备服务名称。|
|args|Object|服务入参列表，取值格式为：```
{
    "key1": "value1", 
    "key2": "value2"
}
```

|

## setup\(\) -\> \{Promise<Void\>\} {#section_q5d_g52_h2b .section}

**功能介绍**

设备接入客户端初始化。该接口必须调用。

**返回参数**

```
Promise<Void>
```

## registerAndOnline\(\) -\> \{Promise<Void\>\} {#section_gk2_g52_h2b .section}

**功能介绍**

将设备注册到边缘节点中并通知边缘节点上线设备。设备需要注册并上线后，设备端才能收到云端下发的指令或者发送数据到云端。

**返回参数**

```
Promise<Void>
```

## reportEvent\(eventName, args\) {#section_zty_3jm_n2b .section}

**功能介绍**

主动上报设备事件。

**请求参数**

|名称|类型|描述|
|--|--|--|
|eventName|String|事件对应的名称，与您在产品定义中创建事件的名称一致。|
|args|Object|事件中包含的属性key与value，取值格式为：```
{
    "key1": "value1", 
    "key2": "value2"
}
```

|

## reportProperties\(properties\) {#section_uhx_wv2_h2b .section}

**功能介绍**

主动上报设备属性。

**请求参数**

|名称|类型|描述|
|--|--|--|
|properties|Object|属性中包含的属性key与value，取值格式为：```
{
    "key1": "value1", 
    "key2": "value2"
}
```

|

## cleanup\(\) -\> \{Promise<Void\>\} {#section_l1g_g52_h2b .section}

**功能介绍**

资源回收接口，您可以使用该接口回收您的资源。

**返回参数**

```
Promise<Void>
```

## getTsl\(\) -\> \{Promise<Void\>\} {#section_w4g_g52_h2b .section}

**功能介绍**

返回TSL字符串，数据格式与云端一致。

**返回参数**

```
Promise<Void>
```

## unregister\(\) -\> \{Promise<Void\>\} {#section_hdh_g52_h2b .section}

**功能介绍**

从边缘计算节点移除设备。请谨慎使用该接口。

**返回参数**

```
Promise<Void>
```

## online\(\) -\> \{Promise<Void\>\} {#section_ath_g52_h2b .section}

**功能介绍**

通知边缘节点设备上线，该接口一般在设备离线后再次上线时使用。

**返回参数**

```
Promise<Void>
```

## offline\(\) -\> \{Promise<Void\>\} {#section_wq3_g52_h2b .section}

**功能介绍**

通知边缘节点设备已离线。

**返回参数**

```
Promise<Void>
```

