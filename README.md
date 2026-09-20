# Reverse Skill

网络安全技能路由包：**44 个**逆向 / 渗透 / CTF / 移动 / 固件 / 云安全场景技能，含全局路由与工具自举。

## 安装

### Codex

```bash
# 把仓库放到本地插件目录
git clone https://github.com/kingmaozi/reverse-skill.git ~/plugins/reverse-skill

# 注册到 personal marketplace（~/.agents/plugins/marketplace.json）
python3 - <<'PY'
import json, pathlib
p = pathlib.Path.home() / ".agents/plugins/marketplace.json"
data = json.loads(p.read_text(encoding="utf-8"))
if not any(e["name"] == "reverse-skill" for e in data["plugins"]):
    data["plugins"].append({
        "name": "reverse-skill",
        "source": {"source": "local", "path": "./plugins/reverse-skill"},
        "policy": {"installation": "AVAILABLE", "authentication": "ON_INSTALL"},
        "category": "逆向技能",
    })
    p.write_text(json.dumps(data, indent=2, ensure_ascii=True) + "\n", encoding="utf-8")
PY

codex plugin add reverse-skill@personal
```

装好后用 `codex debug prompt-input` 可以确认 `reverse-skill:<技能名>` 已进入技能目录；新开一个会话即可使用。

Codex 会递归扫描 skills/ 目录下的 SKILL.md，因此 44 个顶层技能、reverse-skill-router，以及 pentest-tools/src-hunter、reverse-engineering/dsl-vm-reverse 这类嵌套技能都会注册。skills/ 里同时放着 config/、ops/、scripts/、tests/、references/、field-journal/ 六个支撑目录，它们是路由脚本和证据链的依赖：scripts/master-route.sh 按 skills/config/routing.json 定位路由表，技能正文用 ../field-journal/ 引用先例记录。这些目录没有 SKILL.md，不是技能本身，Codex 会自动跳过。

### MiniMax Code

插件 → 导入 → 从 Git 仓库导入，粘贴本仓库地址：

```
https://github.com/kingmaozi/reverse-skill
```

## 技能范围

- 二进制逆向：IDA / Ghidra / radare2 / Binary Ninja / 二进制差分 / Go & Rust 逆向 / macOS Mach-O / .NET
- 移动与固件：APK 逆向 / 移动端逆向 / 固件渗透 / 硬件接口（UART/JTAG）/ 射频 SDR
- 攻防链路：攻击链编排 / Pwn / 补丁差分利用 / EDR 绕过 / 免杀与规避
- 渗透与后渗透：内网渗透工具链 / Windows AD / 云与 K8s / 数据库安全 / 身份联邦
- 蓝队与调研：威胁狩猎 / 威胁情报 / 数字取证 / 邮件安全 / 供应链安全 / LLM 安全
- 辅助：协议逆向 / 浏览器扩展逆向 / 厚客户端 / CTF 靶场 / 图表与文档生成

## 上游与许可

- 上游：[zhaoxuya520/reverse-skill](https://github.com/zhaoxuya520/reverse-skill)（MIT），本仓库为 MiniMax Code 适配版
- 本仓库许可：MIT（见 [LICENSE](LICENSE)）
- 例外：`CTF-Sandbox-Orchestrator` 相关部分为 GPL-3.0

## 说明

全部技能仅供**授权范围内**的安全测试、CTF 学习与防御研究使用。
