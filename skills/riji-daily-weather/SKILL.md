# 每日天气填写

## 目标

每天自动读取日记中的位置信息，获取当地天气并填入日记的 Evening 区域。

## 使用时机

- 定时任务每天 21:00 执行
- 用户手动触发更新天气

## 输入

- `diary_date`: 日期（默认今天）

## 工作流程

### Step 1: 读取日记文件

路径格式：
```
~/Library/Mobile Documents/iCloud~md~obsidian/Documents/riji/daily/YYYY-MM-DD.md
```

### Step 2: 提取位置

从 "Location：" 行提取位置（可能是中文或英文城市名）

### Step 3: 获取天气

调用天气 API 获取：
- mintempC: 最低温度
- maxtempC: 最高温度
- weatherDesc: 天气状况

### Step 4: 填入日记

在 Evening 区域的 "Weather：" 后填入格式：
```
X°C-X°C 晴/雨/多云
```

### Step 5: 返回结果

- 成功：返回填入的天气信息
- 失败：返回错误信息

## 定时任务配置

```json
{
  "name": "riji-daily-weather",
  "schedule": "0 21 * * *",
  "tz": "Asia/Shanghai",
  "delivery": "announce"
}
```

## 注意事项

- 如果位置为空，跳过
- 如果 API 限速（429），记录错误但不要中断
- 极端天气需要附带提醒
