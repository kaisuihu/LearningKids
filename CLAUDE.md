# 小朋友的学习乐园

单文件 HTML 网页游戏（~500KB），字母 + 数学 + 汉字 + 拼音 + 组词 + 自然拼读 + 闪示训练，适合幼儿互动学习。

## 七大模块

### 字母大冒险
- 18 关，4 阶段：大写认读 → 小写认读 → 大小写配对 → 混合挑战
- 无尽挑战模式（按错题加权出题），题数可选（5/10/15/20/26）
- 目标字母隐藏开关（👁️），每个选项下方独立 🔊 发音按钮
- 英文发音 `"Capital A"` / `"Small a"`，rate 0.75
- 错题集本地存储（localStorage key: `letter_adventure_errors`）

### 数学小天才
- 6 个分类卡片：10以内 / 凑十拆十法 / 20以内 / 50以内 / 100以内 / 九九乘法表
- 乘除法含网格可视化（行列标注 + 🔊 题目朗读）
- 得分/计时双模式：得分模式答错提示答案后跳题；计时模式答错只说"不对"、不跳题
- 两种模式均显示错题回顾（同一题多次错误合并显示）
- 题数持久化（localStorage key: `math_qty`、`endless_qty`）

### 汉字小英雄
- 3500 字内联，7 个阶段映射为 4 个级别（幼儿园/一二/三四/五六年级）
- 165 条富文本元数据保留在 CHAR_META 查找表
- 默认不自动发声，孩子主动点击听发音后选拼音
- 搜索：汉字/拼音（支持去声调）/组词，不匹配英文释义
- 收藏 + 进度跟踪，题数 5/10/15/20（localStorage key: `char_qty`、`char_bookmarks`）

### 组词训练
- 4 个年级段，~130 个常见两字词
- 看目标汉字选正确组词，干扰项为目标字+随机字拼凑的假词
- 题数跟随 `char_qty`

### 拼音小能手
- 声母韵母学习区（23 声母 + 24 韵母），Tab 切换，汉字代表音发音
- 游戏：简易模式（声母+韵母）/ 完整模式（含声调）
- `parsePinyin(py)` 解析引擎，题数 5/10/15/20（localStorage key: `pinyin_qty`）

### 自然拼读（Phonics）
- 1090 个单词内联，7 个年级（K~6），61 个拼读规律
- **地图页**：搜索 + 规律下拉筛选（AND 组合），教学/小测 Tab
- **拼读教学**：按年级展示单词卡片（音标/含义/规律标签），🔊 发音，⭐ 收藏，进度跟踪
- **音标学习**：48 个国际音标，6 类分组，例词 + 完整音标（目标 IPA 高亮），TTS 限制提示
- **小测**：得分/计时双模式，看单词选音标 / 看音标选单词，题数 5/10/15/20
- 收藏面板 + 错题集（按年级分组），均支持点击展开单词详情卡片
- 所有交互用 data 属性 + 事件委托，innerHTML 重建后事件不丢失
- localStorage keys: `phonics_qty`、`phonics_errors`、`phonics_bookmarks`、`phonics_progress`

### 闪示训练
- 数字/字母快速闪现，train 瞬时记忆和注意力
- **数字模式**：数字记忆（1-6位）+ 算式运算（加减乘除，10/20/50/100 以内）
- **字母模式**：1-6 个大写/小写/混合字母
- 速度 0.2s~3.0s 可调（默认 0.5s），滑块 + 实时数值
- **看谁记性好**（辨识模式）：闪现后从 4 个选项中选出看到的
- **火眼金睛**（排序模式）：逐个闪现后按顺序点击（仅多内容可用）
- 得分/计时双模式，5/10/15/20 题数
- 排序模式：位置指示器 + 连续错 3 次跳题
- completion：Canvas 纸屑 + 错题回顾
- 所有交互用 data 属性 + 事件委托
- localStorage keys: `flash_qty`/`flash_speed`/`flash_type`/`flash_digit_mode`/`flash_digit_length`/`flash_calc_op`/`flash_calc_range`/`flash_letter_count`/`flash_letter_case`/`flash_mode`/`flash_errors`

## 关键全局变量
- `gameState` / `mathState` / `charState` / `wordState` / `pyState` / `phState` / `flashState`
- `LEVELS` / `MATH_LEVELS` / `CHINESE_CHARS` / `CHAR_GRADES` / `WORD_BANK`
- `PHONICS_WORDS` / `PHONICS_PATTERNS` / `PHONICS_GRADES` / `IPA_DATA`
- `PY_INITIALS` / `PY_FINALS` / `PY_TONES` / `parsePinyin(py)`

## 技术要点
- **纯单文件**，零外部依赖，~500KB，V1.0.4
- Web Speech API：英文 `lang='en-US'`，中文 `lang='zh-CN'`
- 所有答题模块均用 data 属性 + 事件委托，避免 inline onclick 引号转义问题
- 子元素用 `max-width` 约束，不用 `width:100%`，flex 居中自然生效
- 音色选择器已隐藏，Canvas 五彩纸屑，首页 ? 帮助弹窗 + 📋 更新日志弹窗
- 首页浏览器建议（Chrome/Edge）+ 版本号 + 硬编码更新时间

## localStorage keys 汇总
- `letter_adventure_errors` / `math_qty` / `endless_qty`
- `char_qty` / `char_bookmarks`
- `pinyin_qty`
- `phonics_qty` / `phonics_errors` / `phonics_bookmarks` / `phonics_progress`
- `flash_qty` / `flash_speed` / `flash_type` / `flash_digit_mode` / `flash_digit_length`
- `flash_calc_op` / `flash_calc_range` / `flash_letter_count` / `flash_letter_case`
- `flash_mode` / `flash_errors`
- `preferred_voices`（已隐藏）

## Git 仓库
- **本地路径**: `D:\CC_Projects\zzPersonal\learning-kids`
- **GitHub 远程**: `git@github.com:kaisuihu/LearningKids.git`（SSH）
- **GitHub 用户名**: kaisuihu
- **主分支**: `master`
- **SSH 密钥**: `id_ed25519`（已配置，认证正常）

## 开发规范
1. **题数选项**：所有答题任务必须提供 5/10/15/20，未指定时先询问
2. **答题模式**：得分模式（答错提示+跳题）/ 计时模式（答错只说"不对"+停留），均显示错题记录（同题合并）
3. **完成反馈**：按正确率分级（100%/≥90%/≥80%/≥60%/<60%），对应不同纸屑+语音+鼓励语
4. **版本号更新**：更新帮助弹窗 → 更新版本号+硬编码时间 → 更新日志弹窗（内容由用户提供）
5. **避免 width:100%**：子元素用 max-width；用 data 属性+事件委托替代 inline onclick