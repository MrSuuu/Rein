# 源码获取说明（GPL 合规）

本仓库分发的安装包（IPA）中包含以下 GPL 许可的组件：

| 组件 | 许可证 | 位置 |
|---|---|---|
| iSH | GPLv3（含 LICENSE.IOS 附加条款） | `Payload/DSH.app/helpers/ishd` |
| Theos / Logos | GPLv3 or later | `Payload/DSH.app/theos-min/` |
| Alpine 软件包（busybox 等） | 各自许可（多为 GPLv2） | `Payload/DSH.app/alpine-rootfs/` |
| radare2 | LGPLv3 | `Payload/DSH.app/reverse/` |

## 如何获取对应源码

**方式一（推荐，立即可得）**：上述组件均为未修改的上游版本，源码可从其官方仓库获取：

- iSH：https://github.com/ish-app/ish （版本与 `helpers/ishd` 内嵌一致）
- Theos：https://github.com/theos/theos
- Alpine aports：https://gitlab.alpinelinux.org/alpine/aports
- radare2：https://github.com/radareorg/radare2

**方式二（书面承诺）**：如需与本安装包完全对应的源码副本（含构建脚本），
请在本仓库提交 Issue 并注明版本号，我们将在 **3 年内**提供可下载的源码归档。

## 说明

- Rein 自有代码（主程序 `DSH`）为专有软件，不在上述源码范围内；
  主程序未链接 iSH / Theos / radare2 的代码，仅以独立可执行文件与数据目录形式随包分发。
- 若你是上述组件的权利人，认为本分发方式不符合许可要求，请通过 Issue 联系，我们会立即处理。
