## Rein for iOS · 0.2.2 Preview

这一版把「编译链、插件、图像输入、思考档位、余额」五条线全部对齐到官方真实数据。

### 编译链（此前三个 SDK 全报错）

- **静态库随包解出**：iOS 上 Theos 每个构建都要 `-lroot_oldabi`，而 `.a` 不能留在 `.app`（ldid 预检会回滚）。
  现在压成 `vendor-libs.tar.gz`，首次启动解到可写目录
- **可写 `lib` / `bin` / `vendor`**：`lib` 是 Theos 的输出目录（原来链到只读 bundle，rsync 报 Permission denied）；
  `bin` 下全是脚本（原来被摘了 +x，`dm.pl` 起不来）
- **`theos-local` 骨架补全**：`Prefix.pch` 等 14 项（缺它所有构建都 `file not found`）
- **运行时根直连包内路径**：不再走 `/rootfs` 前缀软链，`CA_THEOS_DPKG_DEB` 能被正确识别，
  打包走 `dpkg-deb` 而不是坏掉的 `dm.pl`
- 实测：`make package` 产出 `com.rein.buildtest_0.0.1-2+debug_iphoneos-arm64.deb`

### 插件与工具

- `rein-vision` 补回 `export apply`（此前完全不加载，`read_image` 落到核心工具）
- 16 个工具的 JSON Schema 全部合法（`type: "object"` + `properties` + `required`）
- 参数名不再与 schema 关键字冲突（`deb_publish` 的 `description` → `summary`）
- 移除与官方 `dsh-tool-web` 重名的 `web_fetch` / `web_search`
- `image_ocr` 输出改为宽松 schema（失败时不再报 `invalid output`）

### 图像输入（不再被误判为纯文本）

模型能力现在来自**服务端元数据**，不再靠猜：

```
GET /models → input_modalities:["text","image"]
              context_window:1048576
              max_output_tokens:393216
              effort.supported_levels:["low","high","max"]
```

- patch 里写入 `input: [text, image]`、真实 `contextWindow` 与 `maxOutputTokens`
- 兼容 OpenRouter 的 `architecture.input_modalities`、部分网关的 `capabilities.vision`
- 未知网关可在「供应商 → 模型」里手动开关「允许图片输入」

### 思考档位（真实生效，不是 UI）

- 只显示**当前模型真实支持**的档位（+ Off），换模型时自动落到可用档
- patch 同时声明：`reasoningEfforts` 映射表、`compat.supportsReasoningEffort: true`、
  `thinkingFormat: deepseek|openai`、以及 `agent-default-model.reasoningEffort`

### DeepSeek 官方余额

- 底部状态行 `tok/s` 之后显示 `余额 ¥xx.xx`，点击看总额 / 充值 / 赠送 / 可用状态
- 仅当供应商是 DeepSeek 官方时显示，其它供应商不出现
- 60 秒缓存，失败静默

### 用量与上下文

- 「对话消息」那一行不再拿总占比冒充分项（改为「— 未拆分」并加说明）
- 滑块调整的上下文窗口现在真写进 patch（此前字段名不一致，等于白调）

### 其它

- 全新安装解包：PAX/GNU 长文件名支持 + 恒定内存（峰值 5.2 MB），失败自动清理重试
- 部署脚本默认保留用户数据（`--wipe` 才清空）

### 已知边界

- 视频输入不在 dsh 的模态模型内（只有 `text`/`image`），视频理解走内置抽帧工具
- 上下文分项明细 headless 模式不提供，只能给总量
- 本地 OCR 依赖系统 Vision 模型资产，不随包分发
