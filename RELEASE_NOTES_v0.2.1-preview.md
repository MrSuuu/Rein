## Rein for iOS · 0.2.1 Preview

只修一条线：**本地 OCR 的可用性与可诊断性**。

### 变化

- **四档回退**：`accurate+指定语言 → accurate+自动 → fast+指定语言 → fast+自动`，
  任一档识别出文字就用它。某些设备上「精准档」的 Vision 模型加载失败
  （`Error loading network -5 -1`），而「快速档」用的是另一套模型，通常仍可用
- **图像归一化**：交给 Vision 前统一转 RGB8、长边压到 ≤2400，
  规避 `CVPixelBuffer 创建失败`（带 alpha / 16 位 / 超大图都可能触发）
- **错误不再被吞**：失败时输出 `error` 与 `attempts`（每档各自的原因），
  不再是「0 行」

### 说明

`medialib ocr` 调用的是系统 `Vision.framework`，**识别模型由 iOS 提供**，不在安装包内。
若四档全部失败且原因一致，说明该设备上的 Vision 模型资产异常，与安装包无关。

其余功能与 0.2.0 一致。
