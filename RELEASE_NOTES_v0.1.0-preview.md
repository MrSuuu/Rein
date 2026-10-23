## Rein for iOS · 0.1.0 Preview

首个公开预览版。iPhone 上原生跑 dsh：聊天、终端、插件市场、视觉/媒体工具，全部本机执行。

### 新增

- **启动页**：海洋渐变背景 + 星辰环绕动画 + 彩虹进度条，底部实时显示正在加载的阶段
- **工具台**（侧栏新入口）：一页看清内置能力与运行状态，可直达输出目录
- **内置视觉与媒体工具（15 个，随包自带）**
  - `image_report` / `image_ocr`：OCR（中英）、画面分类、条码、主色
  - `video_frames` / `video_report`：抽帧、逐帧识别合成时间轴
  - `video_trim` / `video_compress` / `video_gif` / `video_concat`
  - `image_batch`：批量缩放 / 转格式 / 文字水印
  - `xlsx_read` / `xlsx_write`：读写 Excel（报价表、材料清单）
  - `git_lite`：本地版本管理（真实 git 对象格式，不依赖 git 二进制）
  - `deb_publish`：deb → 本地 Sileo 源，自动更新 Packages
  - `web_fetch` / `web_search`：网页正文抓取与搜索
- **诊断页**新增「视觉工具」一行：medialib / 插件挂载状态一目了然

### 修复

- 编译测试报 `framework not found Foundation`：包内 `iPhoneOS16.5.sdk` 是残缺副本，已重新打包并在构建时加完整性校验
- 点设置等二级页偶发无响应：导航层级改为独立全屏模态，与抽屉彻底解耦
- 左侧栏四角不圆：`clipsToBounds` 没裁到背景层
- 输入框顶部多余白线：移除 1pt 镜面高光，改为 0.5pt 主题色细边
- 启动页在浅色模式白茫茫：背景渐变曾被 `return` 提前跳过

### 说明

- 不配置任何 API 也能用：视觉走 Apple Vision 离线识别，生图退化为本地渲染
- 配置多模态 / 生图 API 后，`vision_describe` / `image_generate` 会自动升级为真看图 / 真生图

### 已知限制

- 预览版，界面仍在调整
- 效果图生成需要外接生图 API，手机端不跑扩散模型

### 安装

需要 TrollStore。下载下方 `Rein_174.ipa` → 用 TrollStore 打开安装。
首次启动解包运行时约 30 秒。
