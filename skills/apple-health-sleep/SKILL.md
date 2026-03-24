# apple-health-sleep

自动读取 Apple Health 睡眠数据并写入 riji daily 日记。

## 使用场景
- 每天早上同步昨天的睡眠数据到日记
- 手动触发同步睡眠数据

## 数据源路径
- Apple Health 睡眠数据：`~/Library/Mobile Documents/iCloud~md~obsidian/Documents/riji/apple health/`
- riji daily 日记：`~/Library/Mobile Documents/iCloud~md~obsidian/Documents/riji/daily/`

## 操作步骤

### 1. 确定日期
- 默认读取**昨天**的睡眠数据（因为通常是早上执行）
- 如果手动指定，则读取指定日期

### 2. 读取 Apple Health 睡眠数据
读取 `apple health` 文件夹中对应日期的 .md 文件，提取：
- Total Sleep（总睡眠时间）
- Deep（深睡）
- REM
- Core（核心睡眠）
- Awake（清醒时间）

### 3. 写入 riji daily 日记
找到 `### 🛏 Sleep Record` 部分，填写以下字段：
```
- Total Sleep: {总睡眠时间}
- Deep: {深睡时间}
- REM: {REM睡眠时间}
- Core: {核心睡眠时间}
- Awake: {清醒时间}
```

**注意**：只填写模版中已有的字段，不要添加新字段。

### 4. 日期格式
- Apple Health 文件名格式：`YYYY-MM-DD.md`（例：2026-03-24.md）
- riji daily 文件名格式：`YYYY-MM-DD.md`

## 示例输出
```
### 🛏 Sleep Record
- Total Sleep: 7h 12m
- In Bed: 
- Deep: 38m
- REM: 1h 45m
- Core: 4h 48m
- Awake: 54m
- Bedtime:
- Wake up time:
- Night urination times：
```

## 注意事项
- 只填写模版中已有的字段
- 不要添加额外的活动数据（如步数、心率等）
- 如果某天没有睡眠数据，跳过该日期
