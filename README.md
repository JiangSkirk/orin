# Orin

Orin is the **sidecar security gate** for [Echo](https://github.com/JiangSkirk/echo) (JS Agent). Echo does the work. Orin stamps the passes.

This repository publishes the Orin / `orind` source as its own GitHub tree. It is **not** a second Agent runtime, and it is **not** a standalone install yet: the client still types against Echo leases, and some cells still import Echo's OS sandbox.

[中文说明](#中文)

## What this is

| Path | Role |
|------|------|
| `js/orin/` | In-process client (protocol, taint, policy, Stage A hooks) |
| `js/orind/` | Local daemon — Unix socket gatekeeper, not a second turn loop |
| `tests/orin/` | Orin / Stage A–C tests (many still need the Echo tree) |
| `docs/security/orin/` | Design and stage specs |

## Defaults (do not over-claim)

- `orin.enabled` defaults to **false**
- `orin.enforce` defaults to **false**
- Stage C cells / process split: **`not_implemented`** — see [`docs/security/orin/ORIN_STAGE_C_CLOSEOUT.md`](docs/security/orin/ORIN_STAGE_C_CLOSEOUT.md)
- No TCC / Developer ID / notarization
- No independent FTO, clean-room, or third-party red-team sign-off
- MIT source / local RC. This is not a GitHub `stable` product tag

The runnable product is **Echo**: https://github.com/JiangSkirk/echo

## License

MIT. See [`LICENSE`](LICENSE).

---

## 中文

Orin 是 Echo（JS Agent）的**旁路保安**，不是第二套回合运行时。

本仓库把 `js/orin`、`js/orind` 和对应测试/设计文档单独放到 GitHub 上，方便当一个项目看。它目前**还不能脱离 Echo 独立安装**：租约类型和部分沙箱仍来自 Echo。

默认关：`orin.enabled=false`，`orin.enforce=false`，Stage C 官方裁决是 `not_implemented`。不要宣称 RCE 已收口，也不要打不含连字符的 `v*` 当 GitHub stable。

可运行的产品在 Echo 仓库：https://github.com/JiangSkirk/echo
