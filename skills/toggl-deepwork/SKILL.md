# toggl-deepwork

自动获取 Toggl Track 中今天的 Deep Work 时间并写入 riji daily 日记。

## 使用场景
- 每天晚上同步昨天的 Deep Work 时间到日记
- 手动触发获取 Deep Work 统计数据

## 数据获取步骤

### 1. 打开 Toggl 报表页面
使用 browser 工具打开：https://toggl.com/app/reports/detailed

### 2. 筛选条件
- **日期**：选择今天（或者昨天，取决于执行时间）
- **项目**：technology development
- **标签**：deepwork

### 3. 统计时长
汇总所有符合条件的时间条目，计算总时长。

### 4. 写入日记
**⚠️ 注意：是 Obsidian 的 riji/daily 日记，不是 memory 文件夹！**

写入到 riji daily 日记的 Evening 部分：

路径：`~/Library/Mobile Documents/iCloud~md~obsidian/Documents/riji/daily/YYYY-MM-DD.md`

在 `Deep work：` 字段填写统计结果，格式：
```
Deep work：X小时X分钟
```

## 输出格式
```
今日 Deep Work 总计：X小时X分钟 (HH:MM)
- 09:21-10:03: X分钟
- 10:11-12:17: X小时X分钟
```

## 注意事项
- 需要保持浏览器登录状态（使用 profile="user" 或默认 profile）
- Deep Work 标签为 "deepwork"，项目为 "technology development"
- 如果是 cron 任务自动执行，使用 browser 默认 profile 即可
