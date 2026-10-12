# Rules4AI

美国主流 AI 服务（OpenAI、Anthropic、xAI Grok、Google Gemini、Perplexity、Copilot、Meta AI）的 **Clash / Surge 分流规则集**。

GitHub Actions 每天 **北京时间 03:00** 自动运行：重新拉取各家的域名和 IP 段，只要有变化就提交。

## 规则列表

<!-- RULES:START -->
| Ruleset | Description | Domains | IP | Surge | Clash |
| --- | --- | ---: | ---: | --- | --- |
| **OpenAI** | OpenAI: ChatGPT, Sora, Codex, OpenAI API | 20 | 0 | [RULE-SET](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Surge/OpenAI.list) · [DOMAIN-SET](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Surge/OpenAI_Domain.list) | [classical](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Clash/OpenAI.yaml) · [domain](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Clash/OpenAI_Domain.yaml) |
| **Anthropic** | Anthropic: Claude, Claude Code, Claude API | 9 | 3 | [RULE-SET](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Surge/Anthropic.list) · [DOMAIN-SET](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Surge/Anthropic_Domain.list) | [classical](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Clash/Anthropic.yaml) · [domain](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Clash/Anthropic_Domain.yaml) · [ipcidr](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Clash/Anthropic_IP.yaml) |
| **xAI** | xAI: Grok, Grok API | 4 | 1 | [RULE-SET](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Surge/xAI.list) · [DOMAIN-SET](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Surge/xAI_Domain.list) | [classical](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Clash/xAI.yaml) · [domain](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Clash/xAI_Domain.yaml) · [ipcidr](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Clash/xAI_IP.yaml) |
| **Gemini** | Google: Gemini, AI Studio, NotebookLM, DeepMind, Jules, Antigravity | 46 | 0 | [RULE-SET](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Surge/Gemini.list) · [DOMAIN-SET](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Surge/Gemini_Domain.list) | [classical](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Clash/Gemini.yaml) · [domain](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Clash/Gemini_Domain.yaml) |
| **Perplexity** | Perplexity AI | 5 | 0 | [RULE-SET](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Surge/Perplexity.list) · [DOMAIN-SET](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Surge/Perplexity_Domain.list) | [classical](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Clash/Perplexity.yaml) · [domain](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Clash/Perplexity_Domain.yaml) |
| **Copilot** | Microsoft Copilot and GitHub Copilot | 10 | 0 | [RULE-SET](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Surge/Copilot.list) · [DOMAIN-SET](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Surge/Copilot_Domain.list) | [classical](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Clash/Copilot.yaml) · [domain](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Clash/Copilot_Domain.yaml) |
| **MetaAI** | Meta AI and Llama | 2 | 0 | [RULE-SET](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Surge/MetaAI.list) · [DOMAIN-SET](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Surge/MetaAI_Domain.list) | [classical](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Clash/MetaAI.yaml) · [domain](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Clash/MetaAI_Domain.yaml) |
| **AI** | All vendors above combined | 96 | 4 | [RULE-SET](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Surge/AI.list) · [DOMAIN-SET](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Surge/AI_Domain.list) | [classical](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Clash/AI.yaml) · [domain](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Clash/AI_Domain.yaml) · [ipcidr](https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Clash/AI_IP.yaml) |
<!-- RULES:END -->

`AI` 是以上所有厂商的合集，一条规则全部覆盖。

## 文件格式

| 文件 | 用途 |
| --- | --- |
| `Surge/<Name>.list` | Surge `RULE-SET`（域名 + `IP-CIDR,...,no-resolve`） |
| `Surge/<Name>_Domain.list` | Surge `DOMAIN-SET`（仅域名，匹配更快；不含关键字和 IP） |
| `Clash/<Name>.yaml` | Clash / mihomo rule-provider，`behavior: classical` |
| `Clash/<Name>_Domain.yaml` | mihomo rule-provider，`behavior: domain`（不含关键字和 IP） |
| `Clash/<Name>_IP.yaml` | mihomo rule-provider，`behavior: ipcidr`（仅当该厂商有 IP 段时生成） |

想要完整覆盖就用 classical / RULE-SET；`_Domain` + `_IP` 组合匹配更快，但会丢掉少量 `DOMAIN-KEYWORD` 规则。

## 使用方法

### Surge

```ini
[Rule]
RULE-SET,https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Surge/AI.list,AI
# 或者按厂商分开：
# RULE-SET,https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Surge/OpenAI.list,US
# RULE-SET,https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Surge/Anthropic.list,US
# DOMAIN-SET,https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Surge/Gemini_Domain.list,US
```

### Clash / mihomo

```yaml
rule-providers:
  AI:
    type: http
    behavior: classical
    format: yaml
    url: https://raw.githubusercontent.com/Maverick3a1/Rules4AI/main/Clash/AI.yaml
    path: ./ruleset/AI.yaml
    interval: 86400

rules:
  - RULE-SET,AI,AI
```

## 数据来源

| 类型 | 来源 |
| --- | --- |
| 域名 | [v2fly/domain-list-community](https://github.com/v2fly/domain-list-community)（`openai`、`anthropic`、`xai`、`google-deepmind`、`perplexity`、`github-copilot`），去掉标记为 `@ads` / `@cn` 的条目 |
| 域名 | [`config/vendors.jsonc`](config/vendors.jsonc) 中手工维护的补充条目 |
| IP | [RIPEstat](https://stat.ripe.net/) 查询各厂商自有 ASN 实际宣告的网段：OpenAI `AS401864`、Anthropic `AS399358` / `AS400243` / `AS401551`、xAI `AS400297` |
| IP | [Anthropic IP 地址文档](https://platform.claude.com/docs/en/api/ip-addresses) 中的 *Inbound* 段（出站 IP 和已停用的 IP 不收录） |

每次生成时还会做这些处理：

- 校验域名 / CIDR 格式，被上级后缀覆盖的条目自动去重，IP 段自动合并；
- 过于宽泛的后缀（如 `google.com`、`googleapis.com`、`azureedge.net`、`x.com`）会被拒绝，避免把无关流量带进去，列表见 `global_deny_suffix`；
- 上游 regexp 规则 Clash 和 Surge 无法通用，所以跳过；
- **防误删**：某个数据源拉取失败，或者某个规则集一次缩水超过 50%，就保留上一版文件，并在 Actions 里给出警告；
- 只在规则内容真正变化时才重写文件，所以文件头里的 `UPDATED` 就是规则最后一次变化的时间。

## 本地运行

只依赖 Python 3.9+ 标准库：

```bash
python3 scripts/build.py
```

## 添加厂商或规则

编辑 [`config/vendors.jsonc`](config/vendors.jsonc)：

```jsonc
{
  "name": "Example",                 // 输出文件名
  "description": "Example AI",
  "sources": [
    {"type": "v2fly", "list": "example"},   // v2fly 数据文件名
    {"type": "asn", "asn": 12345}           // 通过 RIPEstat 查询宣告网段
  ],
  "domain_suffix": ["example.ai"],
  "domain": ["api.example.com"],
  "domain_keyword": [],
  "ip_cidr": [],
  "exclude": []                      // 要从结果中删除的条目
}
```

推送到 `main` 后会自动触发重新生成。也可以在 Actions 页面手动运行 **Update rulesets**。

## License

[MIT](LICENSE)
