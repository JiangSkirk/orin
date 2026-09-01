# Orin

Orin is the **sidecar security gate** for [Echo](https://github.com/JiangSkirk/echo). Echo does the work. Orin stamps the passes. It is **not** a second Agent runtime.

- **Orin 2.0**: extracted `orin-guard` / `orin-proto` in [titan-agent](https://github.com/JiangSkirk/titan-agent) (`packages/orin-guard`, version 2.0.0). See [docs/ORIN_2_ARCHITECTURE.md](docs/ORIN_2_ARCHITECTURE.md).
- This tree may still hold a host-era `js/orin` + `js/orind` snapshot. That snapshot is not the standalone package.

[中文说明](#中文)

## Orin 2.0 kernel

| Piece | Role |
|-------|------|
| `GateKernel` | Issue / consume / freeze HMAC tickets; single-use; stored TTL |
| Conjunction | `private.read ∩ web.read ∩ egress.send` is unsatisfiable |
| `IFCEngine` | SECRET cannot egress |
| `ExecKernel` | Prefer argv; reject lexical bypass |
| `CredBroker` | Opaque tokens, never raw keys in the sandbox |
| `MCPGate` | Pin descriptors; no `--force` |

`echo-core` never imports `orin-guard`. A Host binds `GuardianSPI`.

PyPI is **not** published. Install from titan-agent (`uv sync` or path-install `./packages/orin-guard`).

## Host-era snapshot (this repo)

| Path | Role |
|------|------|
| `js/orin/` | In-process client snapshot (protocol, taint, policy, Stage A hooks) |
| `js/orind/` | Local daemon snapshot — Unix socket gatekeeper, not a second turn loop |
| `tests/orin/` | Stage A–C tests (many still need the Echo / titan-agent tree) |
| `docs/security/orin/` | Design and stage specs |

## Defaults (do not over-claim)

- `orin.enabled` defaults to **false**
- `orin.enforce` defaults to **false**
- Stage C cells / process split: **`not_implemented`**
- No TCC / Developer ID / notarization
- No independent FTO, clean-room, or third-party red-team sign-off
- MIT source / local RC. This is not a GitHub `stable` product tag

The runnable product is **titan-agent**: https://github.com/JiangSkirk/titan-agent

## License

MIT. See [`LICENSE`](LICENSE).

---

## 中文

Orin 是 Echo 的**旁路保安**，不是第二套回合运行时。

**Orin 2.0** 抽成 titan-agent 里的 `orin-guard` / `orin-proto`：GateKernel 单次票据、致命三件套结构不可满足、SECRET 不能出网。`echo-core` 不 import `orin-guard`。详见 [docs/ORIN_2_ARCHITECTURE.md](docs/ORIN_2_ARCHITECTURE.md)。

本仓库里的 `js/orin` 是宿主时代快照，不是独立 PyPI 包。默认关：`orin.enabled=false`，`orin.enforce=false`，Stage C 仍是 `not_implemented`。不要宣称 RCE 已收口，也不要打不含连字符的 `v*` 当 GitHub stable。

可运行的产品在 titan-agent：https://github.com/JiangSkirk/titan-agent
