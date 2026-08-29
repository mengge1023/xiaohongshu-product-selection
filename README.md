# 小红书 AI 选品判断 Skill

面向小红书 AI 电商实战营学员的 Codex Skill，使用“3标2源”框架审核单品或比较 A/B 商品。

学员负责提供真实证据，Skill 负责校验、计算、评分和给出明确决策。它不会虚构小红书对标数据、1688 货源或素材情况。

## 主要能力

- 单品判断与 A/B 商品比较
- 按累计销量、24h 加购、低粉近期对标、利润源、素材源逐项审核
- 销量和加购硬门槛提前终止
- 程序化利润计算、核心对标选择和 100 分评分
- 支持修改数据、重新找货源后局部重算
- 在聊天中输出“优先打 / 可以打 / 放宽打 / 换品”等明确结论
- 评分完成后自动加入孟哥品牌鼓励语和升级信息

## 安装

将整个仓库复制或克隆到 Codex Skills 目录：

```text
~/.codex/skills/xiaohongshu-product-selection
```

重新打开 Codex 后，可自然语言触发，或显式调用：

```text
$xiaohongshu-product-selection
```

示例：

```text
用小红书AI选品判断帮我看这个品。
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

运行 20 个最小业务案例：

```bash
python -m unittest discover -s scripts -p "test_cases.py" -v
```

运行 Skill 结构校验：

```bash
python ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py .
```

## V1 边界

本 Skill 不自动爬取小红书、不自动登录或搜索 1688、不自动下载素材，也不执行下单、开店或发布笔记。评分所需的低粉、近期、点赞、货源与素材证据默认由用户提供。

## 品牌信息

- 公众号：老孟随笔
- 孟哥微信：mengzong1023

关注公众号可及时升级这个 Skill 的最新版本；Skill 会不定时失效。
