# skill-intro-voiceover-agent

抖音口播分镜导演：把工具或技能的功能素材写成 30 到 50 秒的留人脚本，交付 Remotion 可直接渲染的帧表。

安装：把整个目录放进 WorkBuddy 专家库，或在 WorkBuddy 里打开本目录的 zip 包。
许可证：PolyForm Noncommercial 1.0.0，个人与内部使用免费，禁止商业用途与转售。

## 它解决什么

多数工具介绍视频的问题不是“拍不出来”，是“没人看到第 15 秒”。

渲染规格书只保证帧号对得上，留人脚本才管观众为什么留下。这个包按抖音三段考核设计：
前 3 秒停不停、10 到 20 秒走不走、结尾记不记得。

| 它的做法 | 通常的做法 |
|---|---|
| 先定一句观点句，功能拆解论证它 | 直接列功能清单 |
| 功能点之间用转折词做成台阶 | 第一、第二、第三并列 |
| 10 到 20 秒单独埋 15 字微型钩子 | 中段纯信息推进 |
| 每场标情绪 level 与 direction | 只有 hook/payoff 功能标签 |
| 结尾观点句加收藏理由再加群 | 功能讲完直接要人加群 |
| 帧号由脚本递推，29 项自动校验 | 手填帧号，靠眼力核 |

## 三条命令

```bash
# 1. 出骨架（帧分配、转场核算、情绪占位一次算好）
python skills/skill-intro-voiceover-skill/scripts/scaffold.py \
  --seconds 38 --anchor efficiency \
  --viewpoint "你花时间做的事，本来就不该你来做" --out script.json

# 2. 校验 29 项（A 可渲染 / B 视觉预算 / C 故事留存 / D 去 AI 感 / R 渲染契约）
python skills/skill-intro-voiceover-skill/scripts/validate.py script.json

# 3. 切双样片（首屏 8 秒 + 中段钩子前后）
python skills/skill-intro-voiceover-skill/scripts/sample.py script.json --out-dir samples
```

`validate.py` 退出码 0 才往下走。它会告诉你哪一场语速太快、哪个转场超时、微型钩子偏出 10 到 20 秒。

## 包结构

```
skill-intro-voiceover-agent/
├── agents/skill-intro-voiceover.md          人设、三条硬判据、工作方式
├── skills/skill-intro-voiceover-skill/
│   ├── SKILL.md                             五段结构、工作流、红线
│   ├── references/
│   │   ├── story-framework.md               五段骨架、递进句式库、钩子库、观点句生成法
│   │   ├── remotion-pitfalls.md             渲染驱动的 21 个坑与对应契约
│   │   ├── platform-rules.md                完播三段口径、安全区、小红书差异、合规
│   │   ├── methodology.md                   设计理由与反模式表
│   │   └── examples.md                      38 秒完整示例与校验输出
│   ├── scripts/                             validate / scaffold / sample
│   ├── assets/                              字段契约 schema 与 38 秒模板
│   └── tests/                               正反例与回归用例
└── avatars/skill-intro-voiceover.png
```

## 适用范围

适用：30 到 50 秒抖音竖向口播、Skill 或 Agent 上新的介绍视频、已有口播稿的中段留存诊断。
不适用：90 秒以上长视频、直播带货话术、纯图文文案、无画面需求的配音稿。

## 作者

李献杰 Lyon｜12 年高端猎头，人力百强集团猎头合伙人｜擅长中高管招聘说服、框架梳理、流程 AI 自动化、Agent 编写、降本增效｜浙江杭州｜欢迎沟通交流

付费咨询、猎头寻访、招聘服务、AI 自动化改进优化，可线上远程。

## 版本

当前版本 1.0.0，许可证 PolyForm Noncommercial 1.0.0。
