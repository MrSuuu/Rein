# 第三方组件与许可

Rein 内置下列第三方组件。各组件的版权归其作者所有，按各自许可证使用。

| 组件 | 许可证 | 在包内的位置 | 获取源码 |
|---|---|---|---|
| DeepSeek dsh 运行时 | MIT | `runtime-app.tgz` | 随包附带许可声明；上游 npm `@deepseek-ai/dsh-*` |
| Node.js | MIT | `node22` | https://github.com/nodejs/node |
| pnpm | MIT | `pnpm/` | https://github.com/pnpm/pnpm |
| iSH（Linux 内核模拟） | **GPLv3**（附 `LICENSE.IOS` 附加条款） | `helpers/ishd` | https://github.com/ish-app/ish |
| Alpine Linux rootfs | 各软件包各自许可（busybox 为 GPLv2 等） | `alpine-rootfs/` | https://gitlab.alpinelinux.org/alpine/aports |
| Theos（makefiles / Logos） | **GPLv3 or later** | `theos-min/`（含 LICENSE.md） | https://github.com/theos/theos |
| radare2 | LGPLv3 | `reverse/`（含 `share/licenses`） | https://github.com/radareorg/radare2 |
| Python 3 | PSF License | `python-runtime/` | https://www.python.org |
| OLLVM（基于 LLVM） | Apache-2.0 with LLVM Exceptions | `ollvm/` | https://github.com/obfuscator-llvm/obfuscator |
| Rein 自身代码 | 专有 | 主程序 `DSH` | 不公开 |

## 关于 GPL 组件的说明

`helpers/ishd` 是 iSH 的独立可执行文件（不含 Rein 自有代码），**Rein 主程序未链接任何 GPL 代码**。
`theos-min/`、`alpine-rootfs/`、`reverse/` 均以独立文件/数据形式随包，不与主程序静态链接。

按 GPL 要求，上述组件的完整对应源码可通过 `SOURCE-OFFER.md` 中的方式获取。

## 商标声明

- "DeepSeek"、"dsh" 为其权利人商标。本项目为第三方客户端，**与 DeepSeek 官方无隶属或背书关系**。
- "Apple"、"iPhone"、"iOS"、"Xcode" 为 Apple Inc. 商标。本项目非 Apple 官方产品。
- "TrollStore" 为其作者商标，本项目仅说明安装方式，未捆绑该工具。
