# skill-intro-voiceover-agent

引流视频分镜导演：把功能素材或履历写成 30 到 90 秒的 `production.json`，三条时间线一次给全，再导出剪辑软件能直接用的素材包。

安装：把整个目录放进 WorkBuddy 专家库，或在 WorkBuddy 里打开本目录的 zip 包。
许可证：PolyForm Noncommercial 1.0.0，个人与内部使用免费，禁止商业用途与转售。

## 它解决什么

多数工具介绍视频的问题不是“拍不出来”，是“没人看到第 15 秒”。

渲染规格书只保证帧号对得上，留人脚本才管观众为什么留下。这个包按抖音三段考核设计：
前 3 秒停不停、10 到 20 秒走不走、结尾记不记得。

| 它的做法 | 通常的做法 |
|---|---|
| 先定一句观点句，功能拆解论证它 | 直接列功能清单 |
| 三个时间线分开改，靠锚点对齐 | 一份稿，动效写死绝对帧，改字就崩 |
| 10 到 20 秒单独埋 15 字微型钩子 | 中段纯信息推进 |
| 每场标情绪与运动预算 | 只有 hook/payoff 功能标签 |
| 数字入场按叙事段切换 | 全程小窗，或干脆没有人物 |
| 九组 46 项自动校验 | 手填帧号，靠眼力核 |
| 导出 SRT、分镜表、渲染参数 | 稿子丢给剪辑，再从零对时间轴 |

## 四条命令

```bash
# 1. 出骨架（三条时间线、帧分配、转场核算一次算好）
python skills/skill-intro-voiceover-skill/scripts/scaffold.py \
  --type agent_skill --viewpoint "你花时间做的事，本来就不该你来做" \
  --seconds 38 --out production.json

# 2. 校验九组 46 项
python skills/skill-intro-voiceover-skill/scripts/validate.py production.json

# 3. 切双样片（首屏 8 秒 + 中段钩子前后）
python skills/skill-intro-voiceover-skill/scripts/sample.py production.json --out-dir samples

# 4. 导出剪辑素材包（SRT、分镜表、渲染参数、落地指南）
python skills/skill-intro-voiceover-skill/scripts/export_edit_pack.py production.json --out-dir edit-pack
```

个人介绍把 `--type` 换成 `personal_intro`，`--seconds 60`，会自动带出数字人调度表。

`validate.py` 退出码 0 才往下走。它会告诉你哪一场语速太快、哪个锚点解析不了、微型钩子偏出 10 到 20 秒。

## 三条时间线

| 线 | 字段 | 改它影响什么 |
|---|---|---|
| A 口播 | `scriptTimeline[]` | 只改文案，动效跟着锚点走 |
| B 动效 | `motionTimeline[]` | 只改卡点，不碰文案 |
| C 数字人 | `avatarTimeline[]` | 只改人物调度，不动前两条 |

动效靠五种锚点挂到口播上：场景首帧、重读词、场景结束前、固定偏移、口播停顿。
依赖 TTS 时序的锚点标 `resolve_after_tts: true`，配音后重算，不写死。

## 剪辑怎么落地

`references/editing-toolchain.md` 给三条路径，按“批量、人物、改稿频率”选：

| 路径 | 工具 | 什么时候用 |
|---|---|---|
| A 代码渲染 | Remotion | 批量出、改数据重渲、动效精确落帧 |
| B 人工剪辑 | 剪映专业版 / Premiere / 达芬奇 | 一次性、现场改口播 |
| C 数字人 | HeyGen / 腾讯智影 / 硅基智能 | 个人介绍要真人出镜 |

时长、帧数、字数、场景数四者必须同时成立：38 秒对应 1140 帧、145 到 160 字、11 到 13 场。

## 包结构

```
skill-intro-voiceover-agent/
├── agents/skill-intro-voiceover.md          人设、三条硬判据、三条时间线
├── skills/skill-intro-voiceover-skill/
│   ├── SKILL.md                             工作流、输出契约、红线
│   ├── references/
│   │   ├── story-framework.md               两类内容的五段骨架、句式库、记忆点三件套
│   │   ├── editing-toolchain.md             剪辑与生成工具选型、时长设置
│   │   ├── remotion-pitfalls.md             渲染驱动的 26 个坑
│   │   ├── platform-rules.md                完播口径、安全区、小红书差异、合规
│   │   ├── methodology.md                   设计理由与反模式表
│   │   └── examples.md                      38 秒完整示例
│   ├── scripts/                             validate / scaffold / sample / export_edit_pack
│   ├── assets/                              production.schema.json 与 38 秒模板
│   └── tests/                               三份正反例与回归用例
└── avatars/skill-intro-voiceover.png
```

## 适用范围

适用：30 到 90 秒抖音竖向口播、Skill 或 Agent 上新的介绍视频、个人履历短视频、已有稿的中段留存诊断。
不适用：90 秒以上长视频、直播带货话术、纯图文文案、无画面需求的配音稿。

## 作者

李献杰 Lyon｜12 年高端猎头，人力百强集团猎头合伙人｜擅长中高管招聘说服、框架梳理、流程 AI 自动化、Agent 编写、降本增效｜浙江杭州｜欢迎沟通交流

付费咨询、猎头寻访、招聘服务、AI 自动化改进优化，可线上远程。

## 版本

当前版本 2.0.0，许可证 PolyForm Noncommercial 1.0.0。
