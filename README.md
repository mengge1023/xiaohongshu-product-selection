# 爆不爆｜孟哥AI选品裁判

> 选品别靠猜，链接丢进来，马上告诉你爆不爆。

面向小红书 AI 电商实战营学员的 WorkBuddy Skill，使用“3标2源”框架审核单品或比较 A/B 商品。

本 Skill 面向腾讯 WorkBuddy：学员提供小红书商品/笔记链接，Skill 使用现有轻量能力读取公开证据，再负责校验、计算、评分和给出明确决策。采购价与采购端单件运费无法从公开网页可靠取得，必须由用户直接提供。

## 主要能力

- 单品判断与 A/B 商品比较
- 自动读取小红书商品页和笔记页的公开字段
- 电脑端缺少24h加购按正常边界留空，先给出其余已核字段；不因此反复抓取或要求后台权限
- 采购价与采购端单件运费直接由用户提供，不浪费时间抓取货源网页
- 自动搜索并核验同款低粉近期对标，保留来源链接与抓取时间
- 按累计销量、24h 加购、低粉近期对标、利润源、素材源逐项审核
- 销量和加购硬门槛提前终止
- 程序化利润计算、核心对标选择和 100 分评分
- 支持修改数据、重新找货源后局部重算
- 在聊天中输出“优先打 / 可以打 / 放宽打 / 换品”等明确结论
- 评分完成后自动加入孟哥品牌鼓励语和升级信息

## 安装

当前正式版：**v1.3.1**（版本唯一记录在 `VERSION`）。[下载 WorkBuddy 安装包](https://github.com/mengge1023/xiaohongshu-product-selection/releases/download/v1.3.1/bao-bu-bao-workbuddy-v1.3.1.zip) · [更新记录](CHANGELOG.md) · [读不到数据的排查指引](references/workbuddy-troubleshooting.md)。

下载ZIP后，在 WorkBuddy 的技能页选择“添加技能 → 上传技能”，上传整个ZIP并确认启用。也可直接向 WorkBuddy 发送：

```text
请从 https://github.com/mengge1023/xiaohongshu-product-selection/releases/download/v1.3.1/bao-bu-bao-workbuddy-v1.3.1.zip 下载并全局安装或更新爆不爆技能。安装后读取技能目录里的 VERSION，确认是1.3.1，并告诉我实际安装位置。
```

将完整仓库打包上传到腾讯 WorkBuddy 的“添加技能 → 上传技能”，或复制到 WorkBuddy Skills 目录（macOS：`~/.workbuddy/skills/xiaohongshu-product-selection`）。更新后新建一个任务再测试，避免旧会话沿用旧规则。公开商品页优先使用 WorkBuddy 已有的“网页获取”能力，不把手动打开某个浏览器、安装扩展或单独购买小红书 API 当成默认前置条件。若需要自动搜索小红书站内对标，请启用已有的小红书连接器、MCP 或相关 Skill，并完成必要登录授权；采购数据仍由用户直接提供。

兼容 Codex 时也可复制到：

```text
~/.codex/skills/xiaohongshu-product-selection
```

重新打开 Codex 后，可自然语言触发，或显式调用：

```text
$xiaohongshu-product-selection
```

示例：

```text
用“爆不爆”帮我看这个品。
```

```text
帮我比较 A、B 两个商品，哪个更值得测试？
```

## 目录

```text
xiaohongshu-product-selection/
├── SKILL.md
├── agents/openai.yaml
├── config/thresholds.json
├── references/
└── scripts/
```

评分阈值集中在 `config/thresholds.json`，业务说明与品牌尾注位于 `references/`，确定性计算和测试位于 `scripts/`。

## 验证

运行业务阈值与网页价格解析检查：

```bash
python -m unittest discover -s scripts -p "test_*.py" -v
```

运行 Skill 结构校验：

```bash
python ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py .
```

## V1 边界

本 Skill 只做只读自动取证，不执行下单、收藏、关注、评论、私信、开店或发布笔记。它不会为补充页面字段安装浏览器、下载 Chrome、修改代理或反复调试；每个商品最多读取两次；基础字段缺失才补证一次，缓存不算新的核验。仍失败时说明具体缺口，用户无法补充则保留未知。24h加购缺失不影响其他字段读取，但仍不生成缺项的完整总分。采购数据始终由用户提供。

## 品牌信息

- 公众号：老孟随笔
- 孟哥微信：mengzong1023

关注公众号可及时升级这个 Skill 的最新版本；Skill 会不定时失效。
