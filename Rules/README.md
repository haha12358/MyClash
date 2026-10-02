# 规则文件

`update_rules` 工作流负责生成并提交以下文件：

| 输入                                                                                                         | 输出                                          | 触发条件                             |
| ------------------------------------------------------------------------------------------------------------ | --------------------------------------------- | ------------------------------------ |
| [HaGeZi PRO mini Adblock](https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/pro.mini.txt) | `hagezi-pro.mini.list`、`hagezi-pro.mini.mrs` | 每天 UTC 22:30（北京时间次日 06:30） |
| `direct.list`                                                                                                | `direct.mrs`                                  | 列表推送到 `main` 后                 |
| `proxy.list`                                                                                                 | `proxy.mrs`                                   | 列表推送到 `main` 后                 |

也可以在 GitHub Actions 中手动运行 `update_rules`，一次更新全部文件。生成结果有变化时自动提交，无变化时不创建提交。

`direct.list` 和 `proxy.list` 使用 mihomo `domain` 文本格式，每行一个域名：`example.com` 精确匹配，`+.example.com` 匹配域名及其子域名。请修改 `.list` 源文件，`.mrs` 文件由工作流生成。

mihomo 不支持转换空规则集。空列表（或仅包含空行、`#` 注释的列表）会跳过转换并删除该列表已有的 `.mrs`，避免旧规则继续生效；填入规则后会自动生成。目前 `proxy.list` 为空，因此首次运行只会生成 `direct.mrs`。

HaGeZi 的 `||example.com^` 会转换为 `+.example.com`，去除注释、去重并排序，再使用 mihomo 官方 `convert-ruleset domain text` 命令生成 MRS。遇到不支持的 Adblock 语法或空规则集时，工作流会失败并保留仓库中已有的生成文件。

转换逻辑直接包含在工作流中。每次运行通过 GitHub Releases API 获取 mihomo 最新正式版，下载其 Linux amd64 compatible 版本，不使用预发布版或固定版本号。

定时任务需将工作流合入默认分支后生效；仓库需要允许 GitHub Actions 写入内容。如果分支保护禁止机器人直接提交，需要调整相应的仓库设置。
