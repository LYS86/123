# OCR 文档

!>稳定性: 实验

## Paddle OCR

**5.6.1 新增**
基于百度飞桨的 OCR

### paddle.ocr(img, path)

- `img` {Image} 图片
- `path` {String} 自定义模型路径,必须是绝对路径
- `return` {Array}

使用自定义模型进行文字识别

```js
// files.path() 将相对路径转为绝对路径
let myModelPath = files.path("./models");
let result = paddle.ocr(img, myModelPath);
```

### paddle.ocr(img[, cpuThreadNum=4, useSlim=true])

- `img` {Image} 图片
- `cpuThreadNum` {Number} 识别使用的 CPU 核心数量
- `useSlim` {Boolean} 加载的模型,可选值:
  - `true` ocr_v2_for_cpu(slim) :快速模型,默认
  - `false` ocr_v2_for_cpu : 精准模型
- `return` {Array}

高精度识别，返回值包含坐标，置信度

```js
let res = paddle.ocr(img);
toastLog(JSON.stringify(res));
```

返回值示例:

```json
[
  {
    "bounds": {
      "bottom": 535,
      "left": 348,
      "right": 631,
      "top": 384
    },
    "confidence": 0.9808736,
    "inferenceTime": 188.0,
    "preprocessTime": 53.0,
    "text": "约定",
    "words": "约定"
  }
]
```

### paddle.ocrText(img[, cpuThreadNum=4, useSlim=true])

- `img` {Image} 图片
- `cpuThreadNum` {Number} 识别使用的 CPU 核心数量
- `useSlim` {Boolean} 加载的模型,可选值:
  - `true` ocr_v2_for_cpu(slim) :快速模型,默认
  - `false` ocr_v2_for_cpu : 精准模型
- `return` {Array} 字符串数组

只返回文本识别信息

```js
let res = paddle.ocrText(img);
toastLog("识别信息: " + JSON.stringify(res));
//["约定","最终相遇"]
```

## Tessract OCR

[**6.2.9 新增**]  
前往 github 下载完整例子：[TessractOCR](https://github.com/wilinz/autoxjs-tessocr)

## ML kit OCR

[**6.3.4 新增**]

### gmlkit.ocr(img,Language)

- `img` {Image} 图片
- `Language` {String} 识别语言，可选值为：
  - `la` 拉丁
  - `zh` 中文
  - `sa` 梵文
  - `ja` 日语
  - `ko` 韩语
  - [更多语言](https://developers.google.cn/ml-kit/vision/text-recognition/v2/languages)
- `retrun` {Object} [MlKitOcrResult](#MlKitOcrResult)

```js
//识别中文
let result = gmlkit.ocr(img, "zh");
log(result.text);
```
### MlKitOcrResult

#### MlKitOcrResult.find(predicate)
- `predicate` {Function}
- `return` {Object}

返回通过函数测试的第一个值，没有则返回null

#### MlKitOcrResult.find(level,predicate)
- `level` {Number} 层级
- `predicate` {Function}
- `return` {Object}

返回指定层级中通过函数测试的第一个值，没有则返回null

#### MlKitOcrResult.filter(predicate)
- `level` {Number} 层级
- `return` {Object}

返回所有通过函数测试的值，没有则返回空对象

#### MlKitOcrResult.filter(level,predicate)
- `level` {Number} 层级
- `predicate` {Function}
- `return` {Object}

返回指定层级中所有通过函数测试的值,没有则返回空对象

#### MlKitOcrResult.toArray()
- `return` {Array}

将结果转换成数组

#### MlKitOcrResult.toArray(level)
- `level` {Number} 层级
- `return` {Array}

将指定层级结果转换成数组

#### MlKitOcrResult.sort()
对结果本身进行排序,没有返回值

#### MlKitOcrResult.sorted()
- `return` {Object}
对结果排序,返回个新对象
