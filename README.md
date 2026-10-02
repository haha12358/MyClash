# MyClash 使用说明

适用于 mihomo 内核客户端。使用前请关闭客户端的 DNS 覆写。

## 选择版本

精简版适合日常使用；全量版提供更多服务分流选项。

| 版本   | 覆写脚本                                                                                           | 配置文件                                                                                                       |
| ------ | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| 精简版 | [Script.js](https://raw.githubusercontent.com/haha12358/MyClash/main/Script/Script.js)             | [mihomoConfigLite.yaml](https://raw.githubusercontent.com/haha12358/MyClash/main/Config/mihomoConfigLite.yaml) |
| 全量版 | [mihomoScript.js](https://raw.githubusercontent.com/haha12358/MyClash/main/Script/mihomoScript.js) | [mihomoConfig.yaml](https://raw.githubusercontent.com/haha12358/MyClash/main/Config/mihomoConfig.yaml)         |

## 方式一：覆写机场订阅

1. 在客户端导入机场订阅。
2. 打开该订阅的脚本覆写设置，通过上表链接导入脚本，或复制脚本内容粘贴。
3. 启用覆写并更新订阅，然后选择需要使用的节点或策略组。

脚本用于覆写机场提供的配置。[Bettbox](https://github.com/appshubcc/Bettbox) 支持通过图形界面调整脚本选项。

## 方式二：使用配置文件

1. 下载上表中的配置文件。
2. 将 `proxy-providers` → `provider1` → `url` 中的空字符串替换为机场订阅地址。
3. 将修改后的文件导入客户端，启用配置并更新订阅。
4. 在“默认代理”中选择节点或地区，在各服务策略组中按需调整分流。

机场有专用 DNS 或 hosts 设置时，使用配置文件需手动补入对应设置，可优先选择脚本覆写方式。
