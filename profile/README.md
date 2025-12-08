<div align="center">

<img src="https://raw.githubusercontent.com/alatticeio/lattice/main/docs/images/architecture.png" alt="Lattice Architecture" width="600" />

# Lattice

**Self-Hosted WireGuard Mesh · AI Agent Sandbox**
**自托管 WireGuard 覆盖网络 · AI 智能体安全沙箱**

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://github.com/alatticeio/lattice/blob/main/LICENSE)
[![Go Report Card](https://goreportcard.com/badge/github.com/alatticeio/lattice)](https://goreportcard.com/report/github.com/alatticeio/lattice)
[![Release](https://img.shields.io/github/v/release/alatticeio/lattice)](https://github.com/alatticeio/lattice/releases/latest)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/alatticeio/lattice/blob/main/CONTRIBUTING.md)

[**Website / 官网**](https://lattice.run) · [**Documentation / 文档**](https://lattice.run/docs) · [**Issues**](https://github.com/alatticeio/lattice/issues)

</div>

---

## Projects / 项目

| Project | Description |
|---------|-------------|
| [**lattice**](https://github.com/alatticeio/lattice) | Core — control plane, data plane, relay plane, and AI sandbox plane in one overlay networking platform. / 核心项目，四合一的覆盖网络平台。 |
| [**lattice-shim**](https://github.com/alatticeio/lattice-shim) | gVisor netstack ↔ WireGuard bridge library for zero-privilege AI agent sandboxing. / gVisor 网络栈与 WireGuard 桥接库。 |

---

## Two Core Pillars / 两大核心引擎

### Network Orchestration / 网络编排

Connect any device — servers, containers, IoT, Kubernetes pods — into an encrypted WireGuard overlay mesh. No firewall changes, no public IP exposure.
将任意设备连接成加密的 WireGuard 覆盖网格，无需修改防火墙，无需公网 IP。

| Capability / 能力 | Description / 描述 |
|---|---|
| **WireGuard Tunnel Automation** | Key distribution, rotation, and peer discovery are fully automated. / 密钥分发、轮换、Peer 发现全自动。 |
| **NAT Traversal** | Dual-stack ICE/STUN (IPv4 + IPv6), LRP relay fallback, works across symmetric NAT. / 双栈 ICE/STUN + LRP 中继自动回退。 |
| **Built-in IPAM** | Two-tier allocation (global pool → subnet → peer IP). / 两级 IP 分配。 |
| **Policy Engine** | Default-deny + label selectors + port-level rules; dual backend: iptables (Community) / eBPF TC (PRO). / 默认拒绝 + 标签选择器 + 端口级规则。 |
| **K8s Operator** | 13 CRDs for declarative network lifecycle management. / 13 个 CRD 声明式管理。 |
| **Web Dashboard** | Visual topology, policy editor, monitoring. / 可视化拓扑、策略编辑器、监控面板。 |
| **Multi-Workspace & RBAC** | Namespace isolation + cross-workspace peering + invitations. / 多工作区隔离与跨区对等。 |

### AI Agent Sandbox / AI 智能体安全

Give every AI agent a secure network identity — kernel-level isolation, natural-language-driven policy changes.
为每个 AI Agent 提供安全网络身份，内核级隔离，自然语言驱动的策略变更。

| Capability / 能力 | Description / 描述 |
|---|---|
| **AgentIdentity CRD** | Binds an AI agent to a WireGuard Peer with RBAC and sandbox mode. / AI Agent 与 WireGuard Peer 绑定，RBAC 权限控制。 |
| **Zero-Trust Enrollment** | Single-use token (TTL + usage limit) → auto-create Peer + identity → issue JWT. / 一次性注册令牌，自动创建身份。 |
| **Agent Isolation** | Tool-call enforcement: identity expiry check, namespace whitelist, tool whitelist. / 工具调用拦截：身份检查、白名单。 |
| **gVisor Sandbox (PRO)** | User-space kernel (runsc), zero privileges, no TUN, no eBPF. / 用户态内核，零特权，无需 TUN/eBPF。 |
| **MCP Server** | 14 tools for Claude Desktop / Cursor to manage networks via natural language. / 14 个工具，AI 助手自然语言管理网络。 |
| **Intent Engine (PRO)** | Natural language → LLM extracts CRD change plan → diff preview → approve → apply. / 意图引擎，自然语言 → CRD 变更计划 → 审批。 |

---

## Comparison / 对比

### Network Orchestration / 网络编排

| Capability | Lattice | Tailscale | Netbird | ZeroTier |
|---|---|---|---|---|
| Self-hosted / 自托管 | ✅ | ❌ (SaaS only) | ✅ | ✅ |
| Web Dashboard / 控制台 | ✅ | ✅ | ✅ | ✅ |
| K8s CRD Operator | ✅ (13 CRDs) | ✅ (limited) | ❌ | ❌ |
| eBPF policy / eBPF 策略 | ✅ (PRO) | ❌ | ❌ | ❌ |
| Policy TTL / 策略过期 | ✅ | ❌ | ❌ | ❌ |
| Cross-workspace / 跨区对等 | ✅ | ❌ | ❌ | ❌ |
| Built-in IPAM | ✅ | ✅ | ❌ | ❌ |

### AI Agent Sandbox / AI 智能体安全

| Capability | Lattice | Tailscale | Netbird | ZeroTier |
|---|---|---|---|---|
| Agent zero-trust enrollment / 零信任注册 | ✅ | ❌ | ❌ | ❌ |
| AgentIdentity CRD + RBAC | ✅ | ❌ | ❌ | ❌ |
| gVisor sandbox / 用户态沙箱 | ✅ (PRO) | ❌ | ❌ | ❌ |
| MCP Server / 自然语言管理 | ✅ | ❌ | ❌ | ❌ |
| Intent Engine / 意图引擎 | ✅ (PRO) | ❌ | ❌ | ❌ |
| Tool call audit / 审计日志 | ✅ | ❌ | ❌ | ❌ |

---

## Quick Start / 快速开始

```bash
# Docker (single command, no K8s required) / 一键部署
docker run -d \
  --name lattice-k3s \
  --privileged \
  -p 8080:8080 \
  ghcr.io/alatticeio/lattice-k3s:latest

# Install CLI / 安装 CLI
brew tap alatticeio/tap && brew install lattice

# Start agent / 启动 Agent
lattice init
lattice up
```

---

## Join Us / 加入我们

We're building the future of cloud-native overlay networking and AI agent security!
我们在构建云原生覆盖网络和 AI 智能体安全的未来！

- [Contribute / 参与贡献](https://github.com/alatticeio/lattice/blob/main/CONTRIBUTING.md)
- [Discussions / 讨论区](https://github.com/alatticeio/lattice/discussions)
- [Report Issues / 报告问题](https://github.com/alatticeio/lattice/issues)

## Contact / 联系我们

- Website：[lattice.run](https://lattice.run)
- Email：lauxinchi@gmail.com
- Twitter：[@alatticeio](https://twitter.com/alatticeio)
