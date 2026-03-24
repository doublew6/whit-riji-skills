# ticktick-tasks

自动获取滴答清单 (dida365.com) 中今天未完成的任务并写入 riji daily 日记。

## 使用场景
- 每天晚上同步今天的未完成任务到日记
- 手动触发获取未完成任务列表

## 数据获取步骤

### 1. 打开滴答清单网页版
使用 browser 工具打开：https://dida365.com/

### 2. 查看今天任务
- 点击左侧"今天"选项
- 查看未完成的任务列表
- 记录任务名称

### 3. 写入日记
**⚠️ 注意：是 Obsidian 的 riji/daily 日记，不是 memory 文件夹！**

写入到 riji daily 日记的 Evening 部分：

路径：`~/Library/Mobile Documents/iCloud~md~obsidian/Documents/riji/daily/YYYY-MM-DD.md`

在 `TickTick：` 字段填写未完成任务列表：
```
TickTick:
- 任务1
- 任务2
- ...
```

## 输出格式
```
今天未完成任务（共X个）：
- nut
- apple
- quant
- reading
- ...
```

## 注意事项
- 需要保持浏览器登录状态（使用 profile="user" 或默认 profile）
- 中国区使用的是 dida365.com（不是 ticktick.com）
- 滴答清单 = TickTick 中国区版本
- 收集箱中的任务即为未完成任务
