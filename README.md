# Rein for iOS

把 DeepSeek dsh 装进 iPhone 的原生外壳：**聊天、终端、插件市场、视觉/媒体工具**，全部在本机跑，不依赖电脑。

> 当前版本：**0.2.2-preview**（预览版，功能可用但仍在迭代）

## 安装（TrollStore）

1. 手机需已安装 [TrollStore](https://github.com/opa334/TrollStore)（iOS 15–17，支持你的设备）
2. 下载下方 Release 里的 `Rein_x.ipa`
3. 用 TrollStore 打开 IPA → Install

首次启动会解包运行时（约 640MB），需要 30 秒左右并占用约 1.5GB 空间。

## 装完先做一件事：导入 SDK

安装包**不含 Apple SDK**（SDK 许可禁止再分发），编译插件前要自己导入一份：

SDK 由 Apple 随 Xcode 提供，**我们不能代为分发**，请从自己的 Xcode 里取：

1. Mac 上打开路径：
   `/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/`
2. 把其中的 `iPhoneOS.sdk` 文件夹拷到「文件」App → 我的 iPhone → Rein
3. App 内：工具台 → 组件管理 → 导入 SDK → 选中这个文件夹（也可以先压成 zip 再导入）
4. 支持多份共存（16.5 / 17.0 / 26.5 都可以导入，随时切换）

> 没有 Xcode 也能从其他来源获取，但请自行确认许可，我们不对第三方来源负责。

不导入也能用：聊天、终端、视觉工具、图片/视频处理、表格、git_lite 都不依赖 SDK。

## 这一版有什么

- **原生聊天界面**：玻璃质感卡片、深浅色自适应、轨迹面板
- **侧边抽屉**：会话列表 + 插件市场 / 文件 / 终端 / 设置 / 诊断 / 工具台
- **内置视觉与媒体工具**（15 个，随包自带，无需安装）
  - 看图：OCR（中英）、画面分类、条码、主色报告
  - 看视频：抽帧、逐帧识别生成时间轴、裁剪、压缩、转 GIF、拼接
  - 图片：批量缩放 / 转格式 / 文字水印
  - 表格：读写 `.xlsx`（报价表、材料清单）
  - 开发：`git_lite`（本地版本管理）、`deb_publish`（deb → 本地源）
  - 上网：网页正文抓取、搜索
- **诊断页**：逐项自检 + 真编译测试（Theos / clang / SDK / ldid / dpkg-deb）
- **插件系统**：dsh 插件市场可直接装 npm 上的插件

不配置任何 API 也能用：视觉工具走 Apple Vision 离线识别，生图退化为本地渲染。
配置多模态/生图 API 后，`vision_describe` / `image_generate` 会自动升级为真看图 / 真生图。

## 模型能力与余额

- **图像输入**：按服务端 `/models` 返回的 `input_modalities` 自动声明。
  DeepSeek 官方 V4.1-Flash 是原生多模态，装上就能直接读图；
  自建网关若未返回能力，可在「供应商 → 模型」里手动打开「允许图片输入」
- **思考档位**：只显示当前模型真实支持的档（来源 `effort.supported_levels`），并写入 patch 真正生效
- **上下文窗口**：模型行显示的窗口来自服务端 `context_window`，也可在用量面板里手动覆盖
- **DeepSeek 官方余额**：底部状态行 `tok/s` 之后显示 `余额 ¥xx`，点开看充值/赠送明细
  （仅官方供应商显示，其它供应商不出现）

## 关于 JIT

纯 TrollStore（未越狱）设备默认没有 JIT，App 会自动检测并降级到 `--jitless` 模式——能跑，但会慢一些。
想恢复满速，可用 StikDebug 之类的工具给 App 开 JIT，重启后自动走 JIT 路径。

## 系统要求

- iOS 15.0 – 17.x（arm64 / arm64e）
- 已越狱或用 TrollStore 侧载
- 空闲存储 ≥ 2GB

## 已知限制

- 预览版，UI 仍在调整
- 设备上没有 git 二进制，`git_lite` 只做本地版本（推送需另配）
- 效果图生成需外接生图 API，手机端不跑扩散模型

## 致谢

感谢 **DeepSeek 官方** 提供 dsh 运行时与模型能力 —— Rein 的原生外壳就是围绕它做的。

## 反馈

提 Issue 即可，附上机型 / iOS 版本 / 复现步骤；诊断页可以一键导出状态。
