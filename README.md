# Rein for iOS

把 DeepSeek dsh 装进 iPhone：**聊天、终端、插件市场、视觉/媒体工具**，全部在本机跑，不依赖电脑。

[![下载 Rein.ipa](https://img.shields.io/badge/%E4%B8%8B%E8%BD%BD-Rein.ipa%20%C2%B7%20281MB-2ea44f?style=for-the-badge&logo=apple)](https://github.com/MrSuuu/Rein/releases/latest/download/Rein.ipa)
[![版本](https://img.shields.io/badge/%E7%89%88%E6%9C%AC-0.2.2%20Preview-blue?style=flat-square)](https://github.com/MrSuuu/Rein/releases)
[![要求](https://img.shields.io/badge/%E8%A6%81%E6%B1%82-iOS%2015--17%20%C2%B7%20TrollStore-lightgrey?style=flat-square)](#安装)

> 点上面的绿色按钮直接下载安装包；打不开就到 [Releases](https://github.com/MrSuuu/Rein/releases) 页面下 `Rein.ipa`。

---

## 安装

1. 手机先装好 [TrollStore](https://github.com/opa334/TrollStore)（iOS 15–17）
2. 下载 `Rein.ipa`
3. 用 TrollStore 打开 → Install

首次启动会解包运行时（约 640MB，30 秒左右），期间显示「正在解包运行时（N 秒）」属正常现象。
建议可用空间留 2GB 以上。

## 装完先导入 SDK（只在编译插件时需要）

安装包**不含 Apple SDK**——SDK 许可禁止再分发，需要你自己从 Xcode 里取一份：

1. Mac 上打开
   `/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/`
2. 把 `iPhoneOS.sdk` 拷到「文件」App → 我的 iPhone → Rein
3. App 内：工具台 → 组件管理 → 导入 SDK（zip 也可以）
4. 支持 16.5 / 17.0 / 26.5 多份共存，随时切换

不导入也能用：聊天、终端、视觉工具、图片/视频处理、表格、`git_lite` 都不依赖 SDK。

## 能做什么

| 模块 | 说明 |
|---|---|
| 聊天 | 原生界面、深浅色自适应、轨迹面板、用量统计 |
| 终端 | 内置 Alpine 环境，可跑 `apk` / `git` / `python` |
| 插件市场 | 直接装 npm 上的 dsh 插件，装/卸都通 |
| 看图 | 离线 OCR（中英）、画面分类、条码、主色 |
| 看视频 | 抽帧、逐帧识别、裁剪、压缩、转 GIF、拼接 |
| 图片 | 批量缩放 / 转格式 / 加文字水印 |
| 表格 | 读写出 `.xlsx` |
| 开发 | `git_lite` 本地版本管理、`deb_publish` 发到本地源 |
| 编译 | 内置 Theos + clang-16 + ldid + dpkg-deb，手机上直接打 deb |
| 诊断 | 逐项自检 + 真编译测试，出错能看到完整日志 |

不配任何 API 也能跑：视觉走 Apple Vision 离线识别，生图退化为本地渲染。
配了多模态 / 生图 API 后，`vision_describe` / `image_generate` 会自动升级。

## 模型能力：按服务端真实数据来

装什么模型就用什么模型，不再一刀切当纯文本。

- **图像输入** — 读 `/models` 的 `input_modalities` 自动声明。
  DeepSeek 官方 V4.1-Flash 原生多模态，装上直接能读图；自建网关没返回能力时，
  可在「供应商 → 模型」里手动打开「允许图片输入」
- **思考档位** — 只显示当前模型真实支持的档（`effort.supported_levels`），
  并写进运行时配置真正生效；换模型时自动落到可用档
- **上下文窗口** — 用服务端 `context_window`（官方是 1M），也可在用量面板手动覆盖
- **DeepSeek 官方余额** — 底部状态行 `tok/s` 后面显示 `余额 ¥xx`，点开看充值 / 赠送明细；
  只有官方供应商才显示

## JIT 说明

纯 TrollStore（未越狱）设备默认没有 JIT，App 会自动降级到 `--jitless`——能跑，但慢一些。
想恢复满速，可用 StikDebug 之类的工具给 App 开 JIT，重启后自动走 JIT 路径。

## 系统要求

- iOS 15.0 – 17.x（arm64 / arm64e）
- 已越狱，或用 TrollStore 侧载
- 空闲存储 ≥ 2GB

## 已知限制

- 预览版，UI 仍在调整
- 上下文**分项**占比拿不到（headless 只给总量），面板里标「—」表示未拆分
- 视频理解走内置抽帧工具，不是模型原生视频输入（dsh 的模态只有 text/image）
- 效果图生成需要外接生图 API，手机端不跑扩散模型

## 致谢

感谢 **DeepSeek 官方** 提供 dsh 运行时与模型能力 —— Rein 的原生外壳就是围绕它做的。

## 反馈

问题、建议都欢迎开 [Issue](https://github.com/MrSuuu/Rein/issues)。
