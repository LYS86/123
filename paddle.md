# paddle

>  Paddle OCR 在5.6.1版本加入

## paddle.ocr(image,useSlim)

使用指定的 OCR 模型来执行 OCR。

- `image` {Image} 要执行 OCR 的图像。
- `useSlim` {Boolean} 加载的模型,可选值:
  - `true` ocr_v2_for_cpu(slim) :快速模型
  - `false` ocr_v2_for_cpu : 精准模型
- `return` {Array} 识别结果数组,值为 [OcrResult](#ocrresult)

## paddle.ocr(image,[cpuThreadNum,useSlim])

使用指定的 CPU 核心数和 OCR 模型来执行 OCR。

- `image` {Image} 要执行 OCR 的图像。
- `cpuThreadNum` {Number} 用于执行 OCR 的 CPU 核心数。默认值:系统的 CPU 核心数
- `useSlim` {Boolean} 加载的模型,可选值:
  - `true` ocr_v2_for_cpu(slim) :快速模型,默认
  - `false` ocr_v2_for_cpu : 精准模型
- `return` {Array} 识别结果数组,值为 [OcrResult](#ocrresult)

## paddle.ocr(image,cpuThreadNum,myModelPath)

使用指定的 CPU 核心数和自定义 OCR 模型来执行 OCR。

- `image` {Image} 要执行 OCR 的图像。
- `cpuThreadNum` {Number} 用于执行 OCR 的 CPU 核心数。
- `myModelPath` {String} 自定义 OCR 模型的绝对路径。
- `return` {Array} 识别结果数组,值为 [OcrResult](#ocrresult)

## paddle.ocr(image,myModelPath)

使用自定义 OCR 模型来执行 OCR。

- `image` {Image} 要执行 OCR 的图像。
- `myModelPath` {String} 自定义 OCR 模型的绝对路径。
- `return` {Array} 识别结果数组,值为 [OcrResult](#ocrresult)

### OcrResult

`OcrResult` 是一个表示 OCR 结果的类。它包含以下字段：

- `confidence` {Number} 识别的置信度。
- `preprocessTime` {Number} 预处理时间。
- `inferenceTime` {Number} 推理时间。
- `text` {String} 识别出的文本。
- `bounds` {[Rect](https://developer.android.google.cn/reference/kotlin/android/graphics/Rect?hl=en)} 文本在图像中的位置

> 示例

```js
let img = images.read("./1.png");
img = getBestThreshold(img);
let res1 = paddle.ocr(img);
let res2 = paddle.ocr(img, false);
let res3 = paddle.ocr(img, 4, false);
let myModelPath = files.path("./models");
let res4 = paddle.ocr(img, 4, myModelPath);
let res5 = paddle.ocr(img, myModelPath);
log({ res1, res2, res3, res4, res5 });
log(res1.text);
click(res1.bounds);

function getBestThreshold(img) {
  let img1 = images.grayscale(img);
  img1 = images.threshold(img1, 0, 255, "OTSU");
  return img1;
}
```
