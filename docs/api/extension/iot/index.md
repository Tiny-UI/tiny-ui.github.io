---
layout: default
title: iot
nav_order: 6
parent: 扩展
grand_parent: API
---

# iot

{: .no_toc }

## 目录

{: .no_toc .text-delta }

1. TOC
{:toc}

# init
## 说明
联接平台初始化，绑定物服务

## 示例
```javascript
let result = TinyAPI.iot.init({
   connect: () => {
       console.log("connectd")
   },
   disconnect: () => {
       console.log("disconnect")
   }
});

console.log(result); // true, false
```

## 入参

| 属性名        | 类型       | 属性说明   | 必填  | 默认值                         | 取值范围 |
|:-----------|:---------|:-------|:----|:----------------------------|:-----|
| connect    | function | 联接成功回调 | 否   |  |      |
| disconnect | function | 联接失败回调 | 否   |  |      |

## 出参

| 属性名    | 类型      | 属性说明          | 必填  | 默认值                         | 取值范围 |
|:-------|:--------|:--------------|:----|:----------------------------|:-----|
| result | boolean | 判断设备系统中是否有物服务 |     |  |      |

{:toc}

# getService
## 说明
获取指定类型的服务，类型在物模型中定义

## 示例
```javascript
var result = TinyAPI.iot.getService("printer");

// result:
// {
//      msg: null,
//      data:
// [
//    {
//       "deviceId":"VB03211P26005",
//       "deviceType": "",
//       "isAuth":false,
//       "serviceId":"thermal_printer",
//       "serviceType":"printer"
//       "model":""
//       "deviceName":""
//    }
// ]
// }
```

## 入参

| 属性名  | 类型       | 属性说明                   | 必填  | 默认值                         | 取值范围 |
|:-----|:---------|:-----------------------|:----|:----------------------------|:-----|
| type | string   | 服务类型，类似`printer`，`scanner` | 否   |  |      |

## 出参

| 属性名  | 类型     | 属性说明 | 必填  | 默认值                         | 取值范围 |
|:-----|:-------|:-----|:----|:----------------------------|:-----|
| msg  | string | 错误信息 |     |  |      |
| data | arrays | 服务数组 |     |  |      |

## `data`参数

| 属性名         | 类型      | 属性说明 | 必填  | 默认值                         | 取值范围 |
|:------------|:--------|:-----|:----|:----------------------------|:-----|
| deviceId    | string  | 设备id |     |  |      |
| deviceType  | string  | 设备类型 |     |  |      |
| isAuth      | boolean | 是否校验 |     |  |      |
| serviceId   | string  | 服务id |     |  |      |
| serviceType | string  | 服务类型 |     |  |      |
| model       | string  |      |     |  |      |
| deviceName  | string  | 设备名称 |     |  |      |

{:toc}

# registerServiceChange
## 说明
监听系统中的指定类型服务变化

## 示例
```javascript
TinyAPI.iot.registerServiceChange({
    type: "printer",
    add: (res) => {
        console.log(res);
// res:
//    {
//       "deviceId":"VB03211P26005",
//       "isAuth":false,
//       "serviceId":"thermal_printer",
//       "serviceType":"printer"
//    }
    },
    offline: (s1, s2) => {

    },
    fail: (error) => {
        console.log(error)
    }
});
```

## 入参

| 属性名     | 类型       | 属性说明                   | 必填  | 默认值                         | 取值范围 |
|:--------|:---------|:-----------------------|:----|:----------------------------|:-----|
| type    | string   | 服务类型，类似`printer`，`scanner` | 是   |  |      |
| add     | function | 服务添加回调                 | 否   |  |      |
| offline | function | 服务下线回调                 | 否   |  |      |
| fail    | function | 调用失败回调                 | 否   |  |      |

## `add`入参

| 属性名 | 类型     | 属性说明                   | 必填  | 默认值                         | 取值范围 |
|:----|:-------|:-----------------------|:----|:----------------------------|:-----|
| deviceId    | string  | 设备id |     |  |      |
| isAuth      | boolean | 是否校验 |     |  |      |
| serviceId   | string  | 服务id |     |  |      |
| serviceType | string  | 服务类型 |     |  |      |

## `offline`入参

| 属性名 | 类型     | 属性说明                   | 必填  | 默认值                         | 取值范围 |
|:----|:-------|:-----------------------|:----|:----------------------------|:-----|
| s1  | string |  |     |  |      |
| s2  | string |  |     |  |      |

{:toc}

# registerServiceEvent
## 说明
监听指定服务的物模型中定义的`Event`发生，`deviceId` + `serviceId` 确定唯一服务

## 示例
```javascript
TinyAPI.iot.registerServiceEvent({
    deviceId: "VB03211P26005",
    serviceId: "thermal_printer",
    fail: (error) => {
        console.log(error)
    }
});
```

## 入参

| 属性名       | 类型       | 属性说明                   | 必填  | 默认值                         | 取值范围 |
|:----------|:---------|:-----------------------|:----|:----------------------------|:-----|
| deviceId  | string   | `ThingService`中的`deviceId` | 是   |  |      |
| serviceId | string   | `ThingService`中的`serviceId`                 | 是   |  |      |
| event     | function | `IServiceEventListener` 监听回调                 | 否   |  |      |
| fail      | function | 调用失败回调                 | 否   |  |      |

## `event`入参

| 属性名 | 类型     | 属性说明                   | 必填  | 默认值                         | 取值范围 |
|:----|:-------|:-----------------------|:----|:----------------------------|:-----|
| s   | string |  |     |  |      |
| s1  | string |  |     |  |      |
| s2  | string |  |     |  |      |

{:toc}

# registerServiceProperty
## 说明
监听某个服务的物模型中定义的`property`变化，`deviceId` + `serviceId` 确定唯一服务

## 示例
```javascript
TinyAPI.iot.registerServiceProperty({
    deviceId: "VB03211P26005",
    serviceId: "thermal_printer",
    fail: (error) => {
        console.log(error)
    }
});
```

## 入参

| 属性名       | 类型       | 属性说明                   | 必填  | 默认值                         | 取值范围 |
|:----------|:---------|:-----------------------|:----|:----------------------------|:-----|
| deviceId  | string   | `ThingService`中的`deviceId` | 是   |  |      |
| serviceId | string   | `ThingService`中的`serviceId`                 | 是   |  |      |
| event     | function | `IServiceEventListener` 监听回调                 | 否   |  |      |
| fail      | function | 调用失败回调                 | 否   |  |      |

## `event`入参

| 属性名 | 类型     | 属性说明                   | 必填  | 默认值                         | 取值范围 |
|:----|:-------|:-----------------------|:----|:----------------------------|:-----|
| s   | string |  |     |  |      |
| s1  | string |  |     |  |      |
| s2  | string |  |     |  |      |

{:toc}

# execute
## 说明
通用执行

## 示例
```javascript
let result = TinyAPI.iot.execute({
    thing: thing,
    type: "command",
    action: "execute",
    params: params,
    response: (s, map) => {
        console.log(s, JSON.stringify(map))
    },
    fail: (error) => {
        console.log(error)
    }
});
```

## 入参

| 属性名      | 类型       | 属性说明                         | 必填  | 默认值                         | 取值范围                                                                                            |
|:---------|:---------|:-----------------------------|:----|:----------------------------|:------------------------------------------------------------------------------------------------|
| thing    | object   | 通过SDK获取的`service info`       | 是   |  |                                                                                                 |
| type     | string   | action类型                     | 是   |  | command, commands, property                                                                     |
| action   | string   | type对应类型                     | 是   |  | command->execute(执行command); commands->async/sync(串行/并行指令集); property->get/set(对应property获取和设置) |
| params   | string   | 物模型描述的设置属性参数                 | 是   |  |                                                                                                 |
| response | function | `IServiceEventListener` 监听回调 | 否   |  |                                                                                                 |
| fail     | function | 调用失败回调                       | 否   |  |                                                                                                 |

## 出参

| 属性名    | 类型     | 属性说明                   | 必填  | 默认值                         | 取值范围 |
|:-------|:-------|:-----------------------|:----|:----------------------------|:-----|
| result | string | 本次调用的唯一标识符，与回调第一个参数对应 | 是   |  |      |

## `response`入参

| 属性名 | 类型     | 属性说明       | 必填  | 默认值                         | 取值范围 |
|:----|:-------|:-----------|:----|:----------------------------|:-----|
| s   | string | 本次调用的唯一标识符 |     |  |      |
| map | obj    | 调用结果       |     |  |      |

{:toc}

# executeCommand
## 说明
对指定服务执行物模型中定义的`command`。`serviceInfo`中的`deviceId`和`serviceId`必须。否则会出现找不到服务的情况

## 示例
```javascript
let result = TinyAPI.iot.executeCommand({
    thing: thing,
    params: params,
    response: (s, map) => {
        console.log(s, JSON.stringify(map))
    },
    fail: (error) => {
        console.log(error)
    }
});

var thing =
{
   "deviceId":"VB03211P26005",
        "isAuth":false,
        "serviceId":"thermal_printer",
        "serviceType":"printer"
}
var params =
    "{\"command\":\"print_texts\",\"params\":{\"type\":6,\"columns\":[{\"colsWidthArr\":1,\"command\":\"print_text\",\"align\":0,\"anticolor\":0,\"bold\":0,\"size\":24,\"text\":\"名称\",\"textspace\":0,\"type\":1,\"underline\":0},{\"colsWidthArr\":1,\"command\":\"print_text\",\"align\":0,\"anticolor\":0,\"bold\":0,\"size\":24,\"text\":\"单价\",\"textspace\":0,\"type\":1,\"underline\":0},{\"colsWidthArr\":1,\"command\":\"print_text\",\"align\":0,\"anticolor\":0,\"bold\":0,\"size\":24,\"text\":\"单位\",\"textspace\":0,\"type\":1,\"underline\":0},{\"colsWidthArr\":1,\"command\":\"print_text\",\"align\":0,\"anticolor\":0,\"bold\":0,\"size\":24,\"text\":\"总价\",\"textspace\":0,\"type\":1,\"underline\":0}]}}";

//  s:
//  11379289203296cff-b16f-4d2c-a4dd-a3c9af6cd2e4
//  map:
//  { action_type: command, deviceID: PB08203460291, action: execute, serviceID: thermal_printer, response: {"code":200,"data":{"code":"printer_0000","command":"print","msg":"打印成功"},"..." }
```

## 入参

| 属性名      | 类型       | 属性说明                   | 必填  | 默认值                         | 取值范围 |
|:---------|:---------|:-----------------------|:----|:----------------------------|:-----|
| thing    | object   | 通过SDK获取的`service info` | 是   |  |      |
| params   | string   | 物模型描述的 `command` 参数                 | 是   |  |      |
| response | function | `IServiceEventListener` 监听回调                 | 否   |  |      |
| fail     | function | 调用失败回调                 | 否   |  |      |

## 出参

| 属性名    | 类型     | 属性说明                   | 必填  | 默认值                         | 取值范围 |
|:-------|:-------|:-----------------------|:----|:----------------------------|:-----|
| result | string | 本次调用的唯一标识符，与回调第一个参数对应 | 是   |  |      |

## `response`入参

| 属性名 | 类型     | 属性说明       | 必填  | 默认值                         | 取值范围 |
|:----|:-------|:-----------|:----|:----------------------------|:-----|
| s   | string | 本次调用的唯一标识符 |     |  |      |
| map | obj    | 调用结果       |     |  |      |

{:toc}

# executeCommands
## 说明
无序执行多个`command`

## 示例
```javascript
let result = TinyAPI.iot.executeCommands({
    thing: thing,
    params: params,
    sync: true,
    response: (s, map) => {
        console.log(s, JSON.stringify(map))
    },
    fail: (error) => {
        console.log(error)
    }
});

var thing =
{
        "deviceId":"VB03211P26005",
        "isAuth":false,
        "serviceId":"thermal_printer",
        "serviceType":"printer"
}
var params =
    "[{\"command\":\"print_qrcode\",\"params\":{\"size\":10,\"type\":3,\"code\":\"皇马是冠军---\u003e法兰克福也是---\u003e罗马也是\",\"el\":3,\"align\":1}},{\"command\":\"print_text\",\"params\":{\"bold\":0,\"anticolor\":0,\"align\":0,\"size\":18,\"text\":\"simple text-------------end\",\"underline\":0,\"type\":1,\"textspace\":1}},{\"command\":\"print_texts\",\"params\":{\"type\":6,\"columns\":[{\"colsWidthArr\":1,\"command\":\"print_text\",\"align\":0,\"anticolor\":0,\"bold\":0,\"size\":24,\"text\":\"名称\",\"textspace\":0,\"type\":1,\"underline\":0},{\"colsWidthArr\":1,\"command\":\"print_text\",\"align\":0,\"anticolor\":0,\"bold\":0,\"size\":24,\"text\":\"单价\",\"textspace\":0,\"type\":1,\"underline\":0},{\"colsWidthArr\":1,\"command\":\"print_text\",\"align\":0,\"anticolor\":0,\"bold\":0,\"size\":24,\"text\":\"单位\",\"textspace\":0,\"type\":1,\"underline\":0},{\"colsWidthArr\":1,\"command\":\"print_text\",\"align\":0,\"anticolor\":0,\"bold\":0,\"size\":24,\"text\":\"总价\",\"textspace\":0,\"type\":1,\"underline\":0}]}}]";

//  s:
//  11379289203296cff-b16f-4d2c-a4dd-a3c9af6cd2e4
//  map:
//  { action_type: command, deviceID: PB08203460291, action: execute, serviceID: thermal_printer, response: {"code":200,"data":{"code":"printer_0000","command":"print","msg":"打印成功"},"..." }
```

## 入参

| 属性名      | 类型       | 属性说明                   | 必填  | 默认值  | 取值范围 |
|:---------|:---------|:-----------------------|:----|:-----|:-----|
| thing    | object   | 通过SDK获取的`service info` | 是   |      |      |
| params   | string   | 物模型描述的 `command` 参数                 | 是   |      |      |
| sync     | boolean  | 是否串行执行                | 否   | true |      |
| response | function | `IServiceEventListener` 监听回调                 | 否   |      |      |
| fail     | function | 调用失败回调                 | 否   |      |      |

## 出参

| 属性名    | 类型     | 属性说明                   | 必填  | 默认值                         | 取值范围 |
|:-------|:-------|:-----------------------|:----|:----------------------------|:-----|
| result | string | 本次调用的唯一标识符，与回调第一个参数对应 | 是   |  |      |

## `response`入参

| 属性名 | 类型     | 属性说明       | 必填  | 默认值                         | 取值范围 |
|:----|:-------|:-----------|:----|:----------------------------|:-----|
| s   | string | 本次调用的唯一标识符 |     |  |      |
| map | obj    | 调用结果       |     |  |      |

{:toc}

# getProperty
## 说明
获取物模型服务的`property`，`serviceInfo`中的`deviceId`和`serviceId`必传，否则会出现找不到服务的情况

## 示例
```javascript
let result = TinyAPI.iot.getProperty({
    thing: thing,
    params: "thermal_printer",
    fail: (error) => {
        console.log(error)
    }
});

var thing =
    {
        "deviceId":"VB03211P26005",
        "isAuth":false,
        "serviceId":"thermal_printer",
        "serviceType":"printer"
    }
```

## 入参

| 属性名      | 类型       | 属性说明                   | 必填  | 默认值                         | 取值范围 |
|:---------|:---------|:-----------------------|:----|:----------------------------|:-----|
| thing    | object   | 通过SDK获取的`service info` | 是   |  |      |
| params   | string   | 物模型描述的获取属性参数                 | 是   |  |      |
| response | function | `IServiceEventListener` 监听回调                 | 否   |  |      |
| fail     | function | 调用失败回调                 | 否   |  |      |

## 出参

| 属性名    | 类型     | 属性说明                   | 必填  | 默认值                         | 取值范围 |
|:-------|:-------|:-----------------------|:----|:----------------------------|:-----|
| result | string | 本次调用的唯一标识符，与回调第一个参数对应 |     |  |      |

## `response`入参

| 属性名 | 类型     | 属性说明       | 必填  | 默认值                         | 取值范围 |
|:----|:-------|:-----------|:----|:----------------------------|:-----|
| s   | string | 本次调用的唯一标识符 |     |  |      |
| map | obj    | 调用结果       |     |  |      |

{:toc}

# setProperty
## 说明
对指定服务设置模型中定义的`property`，`serviceInfo`中的`deviceId`和`serviceId`必传，否则会出现找不到服务的情况

## 示例
```javascript
let result = TinyAPI.iot.setProperty({
    thing: thing,
    params: "thermal_printer",
    fail: (error) => {
        console.log(error)
    }
});

var thing =
    {
        "deviceId":"VB03211P26005",
        "isAuth":false,
        "serviceId":"thermal_printer",
        "serviceType":"printer"
    }
```

## 入参

| 属性名      | 类型       | 属性说明                   | 必填  | 默认值                         | 取值范围 |
|:---------|:---------|:-----------------------|:----|:----------------------------|:-----|
| thing    | object   | 通过SDK获取的`service info` | 是   |  |      |
| params   | string   | 物模型描述的设置属性参数                 | 是   |  |      |
| response | function | `IServiceEventListener` 监听回调                 | 否   |  |      |
| fail     | function | 调用失败回调                 | 否   |  |      |

## 出参

| 属性名    | 类型     | 属性说明                   | 必填  | 默认值                         | 取值范围 |
|:-------|:-------|:-----------------------|:----|:----------------------------|:-----|
| result | string | 本次调用的唯一标识符，与回调第一个参数对应 |     |  |      |

## `response`入参

| 属性名 | 类型     | 属性说明       | 必填  | 默认值                         | 取值范围 |
|:----|:-------|:-----------|:----|:----------------------------|:-----|
| s   | string | 本次调用的唯一标识符 |     |  |      |
| map | obj    | 调用结果       |     |  |      |