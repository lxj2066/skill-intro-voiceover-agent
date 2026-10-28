# CHANGELOG

## 2.0.0

技术层重写为双时间线，新增个人介绍分支与剪辑落地。判据 29 项扩到 46 项，主版本升级。

**三条时间线**
- `scriptTimeline[]` 只放会被念出来的字，`voiceover_pure` 是唯一 TTS 字段。
- `motionTimeline[]` 用五种锚点挂到口播，不再写绝对帧。
- `avatarTimeline[]` 独立调度数字人，三档模式跟着叙事段走。
- 依赖 TTS 的锚点强制 `resolve_after_tts: true`，两阶段解析。

**两类内容**
- `agent_skill`：观点句、功能递进、中段钩子、收藏暗示、粉丝群。
- `personal_intro`：人设句、记忆点三件套、合作接口三项、数字人调度。
- 新增 D 组事实判据：数字进 `claims.source`，角色进 `role_tag`，极限词拦截。

**九组 46 项**
A 6 / B 8 / C 7 / D 3 / E 3 / F 4 / G 4 / H 6 / I 5。未启用数字人时 F 组跳过，不虚增分母。

**交付**
- 新增 `export_edit_pack.py`：tts.txt、captions.srt、storyboard.csv、remotion-props.json、remotion-notes.md、edit-guide.md。
- 新增 `references/editing-toolchain.md`：Remotion、剪映、数字人三条路径与时长对照。
- `scaffold.py` 支持两类内容与平台切换，微型钩子前定长。
- 安全区改为抖音上 100 下 200、小红书 3:4 下 120。

**校验**
- 三份用例：38 秒工具稿 42/42、60 秒个人稿 46/46、反例命中 11 项。
- 渲染坑从 21 条补到 26 条。

## 1.0.0

首版。把一份“渲染规格书”级的抖音口播提示词，升级成带确定性判据的完整包。

**故事层升级（原提示词的五条审计结论已全部落地为可执行检查）**
- 新增观点句：`meta.viewpoint` 必填，必须在观点回扣段原句出现，C1 项校验。
- 功能点从并列改递进：相邻功能场必须有转折词，C2 项校验。
- 10 到 20 秒新增 `midpoint_hook` 场景，15 字内，单独成场，C3/C7 项校验。
- 新增情绪曲线：每场 `level` 与 `direction`，必须有一次回落，C4 与 B5 到 B8 项校验。
- 结尾改三段式：观点回扣加收藏理由加粉丝群，C5 项校验。

**渲染层补强（原提示词未覆盖的引擎现实）**
- fps 改为变量，帧号由秒派生，禁止硬编码。
- 新增起帧递推契约：下一场起帧 = 上一场起帧 + 上一场时长 − 转场时长。手填必错。
- 转场时长上限改为相邻场景的一半，符合 TransitionSeries 要求。
- 第 0 帧必须有效：`first_frame_visible` 必填，抖音拿它当封面。
- TTS 文本与字幕高亮分离，`voiceover_text` 禁 markdown。
- 新增语速预算，3.2 到 8.0 字每秒，防稿子念不完。
- 新增字幕安全区校验，每行 16 字、最多 2 行。

**交付层**
- `scripts/validate.py`：A/B/C/D/R 五组 29 项校验，退出码 0/1，附 `--selftest` 正反例。
- `scripts/scaffold.py`：四种锚点的帧骨架，开箱即过校验。
- `scripts/sample.py`：首屏 8 秒与中段钩子双样片，帧号重基到 0。
- `assets/script.schema.json`：字段契约；`assets/voiceover-template.json`：38 秒模板。
- `references/remotion-pitfalls.md`：21 个渲染坑与对应契约。

**已知未覆盖**
- 不评估画面美不美，只保证不越界、不超预算。
- 不预测播放量。
- 平台权重为行业复盘口径，非官方公告，需按自己账号复核。
