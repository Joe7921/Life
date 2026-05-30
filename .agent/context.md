# Life: Fate's Line of Defense - 命运极速割草动作游戏

## 当前开发阶段：Batch 1-5 基础架构及黑白卡机制重构完毕

### 已完成的宏观计划
1. **废弃旧体系 (Batch 1/5)**：彻底摒弃了旧的 11 张静态 Buff 字典（`playerObj.buffs`），并清理了 `TAROT_CARDS_POOL` 无用代码。
2. **引入 OOP 体系 (Batch 1/2)**：实装了 `CARD_DICTIONARY` (7张核心卡，白/黑双极) 和 `CardEffect` 子类结构。
3. **物理与渲染解耦重构 (Batch 2)**：
   - 弹道逻辑：加入 `knockback`、`sineWave`、`drawAsBall` 等。
   - 属性控制：`Player.recalcStats()` 作为全量数据源，统一管理活跃效果的叠加。
4. **底层事件翻新 (Batch 3/4)**：
   - **AI导演抽卡 (`getThreeRandomCards`)**：动态黑牌生成概率（前3次0%，4-6次15%，7次以后25%+递增）。
   - **底牌熔铸 (`triggerUltimateDivinationSettlement`)**：根据卡槽黑牌数(isBlack)决定底牌：0-2黑=星辰(引力漩涡)，3-6黑=审判(激光)，7-9黑=世界(越界穿梭)。
   - **流血替换 (`resolveBleedingReplacement`)**：丢弃白牌扣生命上限，丢弃黑牌强制刷精英（惩罚者）。
   - **动态物理环境重构**：如死神黑牌 (`deathBlackActive`) 激活时怪物生成定时器减半，上限翻倍；月亮黑牌 (`moonBlackActive`) 压缩 Canvas 遮罩至 150px 加上乱线涂鸦盲区。
   - **UI 与碰撞全面换血**：彻底清除了所有关于旧版 `buffs` 的判断（包含皇帝光环、恋人伤害、游戏结算 UI 等）。
5. **本地验证 (Batch 5)**：
   - 运行 `vite build` 通过无报错验证，确保替换过程中的废弃代码清理并未破坏 JavaScript 引擎的词法解析。

### 遗留工作 (待下一步执行)
目前无技术遗留问题。底层架构重塑已完工。

## 宏观方向确认要求
等待人工决策验证完毕后，是否继续推进 **“动态音效响应系统”**，或是 **“异构怪物集群调度引擎 (Enemy Director)”**？
