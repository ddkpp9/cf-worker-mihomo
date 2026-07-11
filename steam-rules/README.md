# Steam Mihomo MRS 规则

本目录通过 GitHub Actions 自动把文本规则转换为 Mihomo 可用的 `.mrs` 文件。

## 生成文件

- `ruleset/steam-domain.mrs`：Steam 域名规则
- `ruleset/steam-ip.mrs`：Steam IP 网段规则

## Raw 下载地址

```text
https://raw.githubusercontent.com/ddkpp9/cf-worker-mihomo/main/steam-rules/ruleset/steam-domain.mrs
https://raw.githubusercontent.com/ddkpp9/cf-worker-mihomo/main/steam-rules/ruleset/steam-ip.mrs
```

## Mihomo 配置示例

```yaml
rule-providers:
  steam-domain:
    type: http
    behavior: domain
    format: mrs
    url: "https://raw.githubusercontent.com/ddkpp9/cf-worker-mihomo/main/steam-rules/ruleset/steam-domain.mrs"
    path: ./ruleset/steam-domain.mrs
    interval: 86400

  steam-ip:
    type: http
    behavior: ipcidr
    format: mrs
    url: "https://raw.githubusercontent.com/ddkpp9/cf-worker-mihomo/main/steam-rules/ruleset/steam-ip.mrs"
    path: ./ruleset/steam-ip.mrs
    interval: 86400
```

在 `rules:` 中引用：

```yaml
rules:
  - RULE-SET,steam-domain,Steam
  - RULE-SET,steam-ip,Steam,no-resolve
  - MATCH,节点选择
```

请把示例中的 `Steam` 和 `节点选择` 替换成配置里实际存在的策略组名称。

## 更新规则

只需要修改以下源文件并提交到 `main` 分支：

```text
steam-rules/rules/steam-domain.list
steam-rules/rules/steam-ip.list
```

GitHub Actions 会自动下载最新版 Mihomo、生成 MRS，并把生成结果提交回仓库。
