---
layout: default
title: album
nav_order: 1
parent: 媒体
grand_parent: API
---

# select
## 说明
打开手机图库，选择/拍摄图片

## 示例
```javascript
var data;
TinyAPI.album.select(
    {
        result: function (res) {
            data = res;
        }
    }
);

console.log(data);
// [
//     {
//         "bucketId":1028075469,
//         "chooseModel":1,
//         "compressPath":"/storage/emulated/0/Android/data/com.sunmi.elephant.yzk/cache/luban_disk_ca...",
//         "compressed":true,
//         "cropImageHeight":0,
//         "cropImageWidth":0,
//         "cropOffsetX":0,
//         "cropOffsetY":0,
//         "cropResultAspectRatio":0,
//         "dateAddedTime":1651384785,
//         "duration":0,
//         "fileName":"Screenshot_20220501_135941_com.tencent.mm.png",
//         "height":521,
//         "id":2069553,
//         "isChecked":false,
//         "isCut":false,
//         "isEditorImage":false,
//         "isGalleryEnabledMask":false,
//         "isMaxSelectEnabledMask":false,
//         "isOriginal":true,
//         "mimeType":"media/png",
//         "num":1,
//         "originalPath":"content://media/external/images/media/2069553",
//         "parentFolderName":"Screenshots",
//         "path":"content://media/external/images/media/2069553",
//         "position":15,
//         "realPath":"/storage/emulated/0/Pictures/Screenshots/Screenshot_20220501_135941_com.ten...",
//         "sandboxPath":"/storage/emulated/0/Android/data/com.sunmi.elephant.yzk/cache/luban_disk_ca...",
//         "size":273130,
//         "width":659
//     }
// ]
```

## 入参

| 属性名          | 类型       | 属性说明     | 必填  | 默认值     | 取值范围                 |
|:-------------|:---------|:---------|:----|:--------|:---------------------|
| theme        | string   | 主题       | 否   | default | light, dark, default |
| origin       | boolean  | 可选原图     | 否   | true    | true, false          |
| compress     | boolean  | 压缩图片     | 否   | false   | true, false          |
| maxSelectNum | integer  | 最多选择图片数量 | 否   | 9       |   |
| minSelectNum | integer  | 最少选择图片数量 | 否   | 0       |   |
| result       | function | 已选图片信息   | 是   |         |   |
| selected     | arrays   | 上一次已选图片  | 否   |         |   |

## `result`入参

| 属性名    | 类型     | 属性说明                      | 必填  | 默认值     | 取值范围                 |
|:-------|:-------|:--------------------------|:----|:--------|:---------------------|
| res    | object | 已选图片信息（如果取消选择则返回"cancel"） |     |  |  |

## `res`参数

| 属性名          | 类型      | 属性说明      | 必填  | 默认值     | 取值范围                 |
|:-------------|:--------|:----------|:----|:--------|:---------------------|
| compressPath | string  | 压缩图片地址    |     |  |  |
| fileName     | string  | 图片名称      |     |  |  |
| width        | string  | 图片宽度      |     |  |  |
| height       | string  | 图片高度      |     |  |  |
| isOriginal     | boolean | 图片是否原图    |     |  |  |
| position     | integer | 图片位于相册中位置 |     |  |  |
| realPath     | string  | 图片真实路径    |     |  |  |
| size     | integer | 图片大小/B    |     |  |  |
