# 🐠 小鱼冲冲冲（Fishy Go Go Go!）

A fun underwater math adventure game for kids!

《小鱼冲冲冲》是一款结合 **数学练习、海底冒险、角色成长和魔法战斗** 的儿童教育游戏。

玩家控制一条可爱的小鱼，在海底游泳、收集食物、躲避障碍物，并通过回答数学题获得魔法值（MP），使用魔法击败敌人，获得经验值（EXP），不断升级和进化。

## 🎮 Play Game

**Game URL:**

https://mrsealgame.github.io/kids-games/fishy-go-go-go.html

**HTML File:**

`fishy-go-go-go.html`

游戏基于 HTML5 Canvas 和 JavaScript 开发，无需安装，使用浏览器即可运行。

---

# 1. Game Overview

## 1.1 Core Gameplay

游戏采用横向自动卷轴（Side-scrolling）模式。

- 玩家小鱼位于屏幕左侧，面向右方。
- 海底物品、障碍物和敌人从右向左移动。
- 玩家通过点击或拖动屏幕控制小鱼游动。
- 小鱼需要收集食物、回血瓶，同时躲避危险障碍物。
- 玩家通过回答减法题获得 MP。
- 拥有 MP 时，小鱼可以自动攻击进入攻击范围的敌人。
- 击败敌人获得 EXP。
- EXP 达到升级要求后，小鱼升级。
- 每升 3 级，小鱼进化为新的外观。
- 随着关卡推进，海底环境、敌人和障碍物逐渐改变。

## 1.2 Game Objective

玩家需要：

1. 尽可能长时间生存。
2. 回答数学题积累魔法。
3. 击败敌人获得经验。
4. 提升等级，进化小鱼。
5. 探索不同海底区域。
6. 挑战越来越强的敌人。

**Game Over Condition:**

当 HP ≤ 0 时，游戏结束。

---

# 2. Player Controls

## 2.1 Movement

游戏采用自动卷轴机制。

- 小鱼不会因为玩家不操作而停止游戏。
- 海底场景持续向左移动。
- 玩家点击水面任意位置，小鱼向该位置游动。
- 按住并拖动可以持续调整目标位置。
- 小鱼通过平滑动画移动，而不是瞬间传送。

### Movement Direction

| Character | Direction |
|---|---|
| Player Fish | ➡️ Face Right |
| Enemy Fish | ⬅️ Face Left |
| Scrolling Objects | ⬅️ Move Left |

## 2.2 Swimming Sound

点击水面控制小鱼游动时，播放短促、可爱的水泡音效。

## 2.3 Pause

游戏提供暂停按钮。

暂停时：

- 小鱼停止移动。
- 所有物品停止移动。
- 敌人停止移动。
- 关卡计时暂停。
- 不允许答题或攻击。

点击继续后恢复游戏。

---

# 3. Player Attributes

玩家拥有四种主要属性：

| Attribute | Description |
|---|---|
| ❤️ HP | Health Points |
| ⭐ EXP | Experience Points |
| ✨ MP | Magic Points |
| ⚔️ ATK | Attack Power |

## 3.1 HP — Health Points

HP 表示小鱼的生命值。

初始状态：

`HP: 5 / 5`

HP 减少：

- 碰到障碍物。
- 与敌人发生碰撞。

HP 增加：

- 收集回血瓶。
- 升级时恢复全部 HP。

当 HP = 0 时，游戏结束。

### HP Display

使用红色进度条和数字。

例如：

❤️ HP ███████░░░ 7 / 10

HP 变化时显示浮动数字：

- `−1 HP`
- `−2 HP`
- `+2 HP`

受到伤害时，小鱼短暂闪烁，并获得短暂的无敌保护时间，避免一次碰撞连续扣血。

## 3.2 MP — Magic Points

MP 用于发动魔法攻击。

初始状态：

`MP: 0 / 3`

### MP Rules

| Action | MP Change |
|---|---|
| Correct Math Answer | +1 MP |
| Wrong Math Answer | −1 MP |
| Magic Attack | −1 MP |
| Level Up | Restore to Max MP |

MP 不允许低于 0，也不能超过 Max MP。

### MP Display

使用紫色进度条和数字。

例如：

✨ MP ██████░░░░ 6 / 10

MP 变化时显示：

- `+1 MP`
- `−1 MP`

### Magic Appearance

当 MP > 0：

- 小鱼周围出现紫色魔法光环。
- 小鱼身上出现魔法闪光。
- 小鱼上方出现 ⚡ 标志。

当 MP = 0：

- 魔法光环消失。
- 小鱼恢复普通外观。

## 3.3 EXP — Experience Points

EXP 用于升级。

EXP 来源：

| Action | EXP |
|---|---|
| Eat Food | +1 |
| Defeat Normal Enemy | +2 |
| Defeat Advanced Enemy | +3 ~ +20 |

EXP 达到 Max EXP 时升级。

### EXP Display

使用黄色进度条和数字。

例如：

⭐ EXP █████░░░░░ 5 / 10

获得 EXP 时显示浮动文字：

`+1 EXP`

`+5 EXP`

## 3.4 ATK — Attack Power

ATK 决定每次魔法攻击造成的伤害。

攻击力随小鱼等级增加。

**ATK 不显示进度条。**

攻击力提升主要通过小鱼进化后的外观和魔法效果体现。

### ATK Formula

```javascript
ATK = 1 + Math.floor((level - 1) / 3);
```

| Level | ATK |
|---|---|
| 1–3 | 1 |
| 4–6 | 2 |
| 7–9 | 3 |
| 10–12 | 4 |
| 13–15 | 5 |
| 16–18 | 6 |

---

# 4. Level System

Level 表示玩家小鱼的成长等级。

Level 和 Stage 是两个独立系统。

- **Level**：决定玩家属性和外貌。
- **Stage**：决定海底环境和游戏难度。

## 4.1 Level Progression

初始等级：

`Level 1`

升级需要达到对应的 EXP 要求。

### Attribute Growth

| Level | Max HP | Max MP | EXP Required | ATK |
|---|---|---|---|---|
| 1 | 5 | 3 | 8 | 1 |
| 2 | 6 | 4 | 10 | 1 |
| 3 | 7 | 5 | 12 | 1 |
| 4 | 8 | 6 | 14 | 2 |
| 5 | 9 | 7 | 16 | 2 |
| 6 | 10 | 8 | 18 | 2 |
| 7 | 11 | 9 | 20 | 3 |
| 8 | 12 | 10 | 22 | 3 |
| 9 | 13 | 11 | 24 | 3 |
| 10 | 14 | 12 | 26 | 4 |

### Formulas

```javascript
maxHP = 4 + level;

maxMP = 2 + level;

maxEXP = 6 + level * 2;

ATK = 1 + Math.floor((level - 1) / 3);
```

## 4.2 Level Up

升级时：

1. Level +1。
2. Max HP +1。
3. Max MP +1。
4. 下一等级所需 EXP +2。
5. HP 恢复至 Max HP。
6. MP 恢复至 Max MP。
7. 每 3 级提升 ATK。
8. 每 3 级改变小鱼外貌。

升级时播放：

- 闪光动画
- 星星特效
- 升级音效

并显示：

`✨ Level Up!`

## 4.3 Fish Evolution

每 3 级进化一次。

| Level | Appearance | Evolution |
|---|---|---|
| 1–3 | 🐠 | Baby Fish |
| 4–6 | 🐟 | Growing Fish |
| 7–9 | 🐡 | Strong Fish |
| 10–12 | 🦈 | Shark Warrior |
| 13–15 | 🐉 | Dragon Fish |
| 16+ | 🐲 | Legendary Dragon |

进化后：

- 小鱼外貌改变。
- 魔法攻击力提高。
- 保留原有移动方式。
- 小鱼仍然面向右方。

---

# 5. Math System

数学题用于获取 MP。

## 5.1 Default Math Difficulty

默认使用：

**10 以内减法**

例如：

`8 − 3 = ?`

屏幕下方显示三个数字选项：

`3`　`5`　`7`

每次只显示一道数学题。

不显示数学难度选择。

## 5.2 Correct Answer

答对后：

- MP +1。
- 播放正确音效。
- 显示 `+1 MP`。
- 自动生成下一道题。

## 5.3 Wrong Answer

答错后：

- MP −1。
- 播放错误音效。
- 显示 `−1 MP`。
- 保留当前题目，让玩家重新选择。

不需要显示错误文字或改变选项颜色。

## 5.4 MP Limit

如果 MP 已达到 Max MP：

- 玩家仍然可以答题。
- MP 不超过上限。

---

# 6. Combat System

## 6.1 Automatic Magic Attack

小鱼拥有 MP 时，可以自动攻击前方敌人。

攻击条件：

1. MP > 0。
2. 敌人位于小鱼前方。
3. 敌人进入攻击范围。
4. 攻击冷却结束。

### Attack Parameters

| Parameter | Value |
|---|---|
| MP Cost | 1 |
| Base Attack Range | 265 px |
| Attack Cooldown | 0.55 seconds |
| Damage | Player ATK |

## 6.2 Enemy HP

每个敌人拥有独立 HP。

敌人头顶显示血条。

例如：

`HP: 5 / 5`

受到攻击：

`HP: 3 / 5`

再次攻击：

`HP: 1 / 5`

直到 HP = 0，敌人才会被击败。

## 6.3 Attack Animation

魔法攻击时：

- 小鱼向前发射紫色魔法。
- 魔法飞向敌人。
- 敌人受到攻击。
- 敌人头顶显示伤害数字。
- 敌人 HP Bar 减少。

## 6.4 Enemy Defeat

敌人 HP = 0：

- 敌人消失。
- 播放击败音效。
- 增加 EXP。
- 显示浮动 EXP 奖励。

---

# 7. Enemy System

敌人全部使用海洋生物。

敌人从右向左游动，**头部朝左**。

| Enemy | Unlock Stage | HP | Collision Damage | EXP Reward |
|---|---|---|---|---|
| 🐟 Normal Fish | 1 | 1 | 1 | 2 |
| 🐠 Fast Fish | 4 | 3 | 1 | 3 |
| 🐡 Armored Fish | 7 | 5 | 2 | 5 |
| 🦈 Shark | 10 | 8 | 3 | 8 |
| 🐙 Octopus Boss | 13 | 15 | 4 | 15 |
| 🦑 Giant Squid | 16 | 20 | 5 | 20 |

### Enemy Rules

- 所有敌人拥有独立 HP。
- 所有敌人头顶显示 HP Bar。
- 敌人 HP 不会因为被攻击一次就自动归零。
- 只有 HP = 0 才会被击败。
- 敌人未被击败时继续移动。
- 玩家与敌人碰撞会损失 HP。
- 不同敌人拥有不同 EXP 奖励。

---

# 8. Obstacles

障碍物必须与敌人有明确视觉区别。

**障碍物使用非生物物体或自然现象。**

不使用水母和海胆作为障碍物。

| Obstacle | Unlock Stage | HP Damage |
|---|---|---|
| 🪨 Rock | 1 | −1 |
| 🪸 Sharp Coral | 4 | −2 |
| 💎 Crystal | 7 | −3 |
| 🌀 Whirlpool | 10 | −4 |
| ☄️ Volcanic Rock | 13 | −5 |
| ⚡ Energy Trap | 16 | −6 |

## 8.1 Rock

普通石头。

- 向左移动。
- 碰撞造成 1 HP 伤害。

## 8.2 Sharp Coral

尖锐珊瑚。

- 造成 2 HP 伤害。
- 出现在珊瑚海及之后的区域。

## 8.3 Crystal

尖锐水晶。

- 造成 3 HP 伤害。
- 出现在水晶洞穴及之后的区域。

## 8.4 Whirlpool

漩涡。

- 造成 4 HP 伤害。
- 靠近时会轻微影响小鱼移动方向。

## 8.5 Volcanic Rock

火山石。

- 造成 5 HP 伤害。
- 出现在海底火山区域。

## 8.6 Energy Trap

能量陷阱。

- 造成 6 HP 伤害。
- 出现在神秘深海区域。

---

# 9. Stage System

Stage 决定海底区域和难度。

## 9.1 Stage Progression

每 24 秒进入下一关。

```javascript
stageDuration = 24;
```

每 3 关切换海底区域。

| Stage | Region | Theme |
|---|---|---|
| 1–3 | 阳光浅海 | Sunny Shallows |
| 4–6 | 珊瑚花园 | Coral Garden |
| 7–9 | 水晶洞穴 | Crystal Cave |
| 10–12 | 暗流海域 | Strong Currents |
| 13–15 | 海底火山 | Underwater Volcano |
| 16+ | 神秘深海 | Mysterious Deep Sea |

## 9.2 Environment Design

### 🌊 Stage 1–3：阳光浅海

**Visual Design**
- 浅蓝色海水
- 阳光照射
- 沙地
- 海草
- 气泡

**Obstacles**
- Rock

**Enemies**
- Normal Fish

### 🪸 Stage 4–6：珊瑚花园

**Visual Design**
- 蓝绿色海水
- 彩色珊瑚
- 贝壳
- 海底植物

**New Obstacle**
- Sharp Coral

**New Enemy**
- Fast Fish

### 💎 Stage 7–9：水晶洞穴

**Visual Design**
- 深蓝色海水
- 发光水晶
- 岩石洞穴
- 蓝紫色光线

**New Obstacle**
- Crystal

**New Enemy**
- Armored Fish

### 🌪️ Stage 10–12：暗流海域

**Visual Design**
- 深青色海水
- 水流纹路
- 漂浮岩石
- 漩涡

**New Obstacle**
- Whirlpool

**New Enemy**
- Shark

### 🌋 Stage 13–15：海底火山

**Visual Design**
- 深红色环境光
- 火山岩
- 熔岩裂缝
- 火山喷发气泡

**New Obstacle**
- Volcanic Rock

**New Enemy**
- Octopus Boss

### ✨ Stage 16+：神秘深海

**Visual Design**
- 深紫色海水
- 发光植物
- 神秘遗迹
- 魔法光点

**New Obstacle**
- Energy Trap

**New Enemy**
- Giant Squid

## 9.3 Difficulty Scaling

随着 Stage 增加：

- 物品移动速度增加。
- 障碍物生成间隔缩短。
- 解锁更危险的障碍物。
- 解锁 HP 更高的敌人。

### Movement Speed

```javascript
speed = 145 + Math.min(stage, 25) * 11;
```

敌人移动速度：

```javascript
enemySpeed = speed * 1.15;
```

### Spawn Interval

```javascript
spawnInterval =
  random(0.85, 1.5) *
  Math.max(0.57, 1 - stage * 0.025);
```

---

# 10. Collectible Items

## 10.1 Food

🦐 Food

- 收集后 EXP +1。
- 立即消失。
- 播放收集音效。
- 显示 `+1 EXP`。

## 10.2 Health Potion

🧪 Health Potion

- 收集后恢复 HP。
- 默认恢复 2 HP。
- 不超过 Max HP。
- 显示 `+2 HP` 或实际恢复数值。

---

# 11. User Interface

## 11.1 Top HUD

屏幕顶部显示：

- ❤️ HP Bar + 数字
- ⭐ EXP Bar + 数字
- ✨ MP Bar + 数字
- ⭐ Player Level
- 🌊 Current Stage
- 🗺️ Current Region

不显示 ATK Bar。

## 11.2 Bottom Math Panel

屏幕底部显示：

- 当前减法题
- 三个数字答案按钮

例如：

**8 − 3 = ?**

`3`　`5`　`7`

## 11.3 Floating Feedback

所有属性变化都显示浮动数字。

| Event | Feedback | Color |
|---|---|---|
| Damage | −1 HP | Red |
| Heal | +2 HP | Green |
| Correct Answer | +1 MP | Purple |
| Wrong Answer | −1 MP | Purple |
| Food | +1 EXP | Yellow |
| Enemy Defeated | +5 EXP | Yellow |
| Enemy Hit | −2 HP | Red |

浮动数字：

1. 从角色或目标附近出现。
2. 向上移动。
3. 逐渐透明。
4. 自动消失。

## 11.4 Pause and Restart

游戏提供：

- ⏸ Pause
- ▶ Resume
- 🔄 Restart

不提供游戏难度选择或数学难度选择。

---

# 12. Sound Effects

游戏使用 Web Audio API 生成音效。

| Event | Sound |
|---|---|
| Swimming | Bubble sound |
| Correct Answer | Happy high-pitched sound |
| Wrong Answer | Low-pitched sound |
| Food Collected | Reward sound |
| HP Lost | Damage sound |
| HP Recovered | Healing sound |
| Magic Attack | Magic sound |
| Level Up | Celebration sound |
| Stage Change | Transition sound |

浏览器可能要求用户先与页面交互，才能播放音效。

---

# 13. Visual Design

## 13.1 Overall Style

游戏采用：

- Cute
- Colorful
- Child-friendly
- Underwater fantasy
- Bright and clear visuals

## 13.2 Visual Requirements

- 不显示网格。
- 不使用覆盖整个游戏画面的半透明遮罩。
- 正常游戏时保持背景清晰。
- 小鱼与敌人方向正确。
- 魔法光环只围绕玩家小鱼。
- 敌人血条清晰可见。
- 障碍物与敌人视觉上容易区分。

## 13.3 Character Direction

玩家：

➡️ Face Right

敌人：

⬅️ Face Left

## 13.4 Canvas Rendering

游戏使用 HTML5 Canvas。

支持高分辨率屏幕，通过 `devicePixelRatio` 调整 Canvas 绘制分辨率。

---

# 14. Game State

游戏主要维护以下状态：

```javascript
{
  level,
  stage,
  hp,
  mp,
  exp,
  playerPosition,
  enemies,
  obstacles,
  collectibles,
  spawnTimer,
  attackTimer,
  invulnerabilityTimer,
  paused,
  gameOver
}
```

## 14.1 Game Initialization

开始游戏时：

- Level = 1
- Stage = 1
- HP = 5
- MP = 0
- EXP = 0
- ATK = 1

游戏立即生成初始物品，避免海底画面长时间空白。

## 14.2 Game Loop

游戏循环负责：

1. 更新关卡计时。
2. 更新小鱼位置。
3. 生成新物品。
4. 移动物品和敌人。
5. 检测碰撞。
6. 检测自动魔法攻击。
7. 更新 HP、EXP、MP。
8. 检查升级条件。
9. 更新动画。
10. 绘制游戏画面。

---

# 15. Technical Requirements

## Technology

- HTML5
- CSS3
- JavaScript
- Canvas 2D API
- Web Audio API

## Deployment

游戏采用单个 HTML 文件，可直接部署到 GitHub Pages。

无需：

- Backend
- Database
- Login
- External API

## File Structure

```text
kids-games/
│
├── README.md
│
├── index.html
│
└── fishy-go-go-go.html
```

---

# 16. Future Enhancements

以下功能属于未来扩展，不代表当前版本已经实现。

### Boss Battles
- 每 5 关出现特殊 Boss。
- Boss 拥有更多 HP。
- Boss 可以使用特殊攻击。

### New Magic Skills
- Fire Magic
- Ice Magic
- Lightning Magic

### Special Rewards
- Temporary Shield
- Double EXP
- Extra MP

### Game Progress
- Save highest level
- Save highest stage
- Track defeated enemies

### Achievements
- Defeat 10 enemies
- Reach Level 10
- Complete 20 math questions
- Survive 10
