# 每日日记生成

## 目标

每天自动生成当天的日记模板文件，基于模板替换日期变量。

## 使用时机

- 定时任务每天 00:00 执行
- 用户手动触发生成今天日记

## 输入

- `vault_path`: Obsidian vault 路径（默认：~/Library/Mobile Documents/iCloud~md~obsidian/Documents/riji）
- `template_path`: 模板文件路径

## 工作流程

### Step 1: 检查日记是否已存在

```bash
FILE_PATH="$VAULT_PATH/daily/$(date +%Y-%m-%d).md"
if [ -f "$FILE_PATH" ]; then
    echo "日记已存在"
    exit 0
fi
```

### Step 2: 从模板生成

```bash
sed -e "s/{{date:YYYY-MM-DD}}/$(date +%Y-%m-%d)/g" \
    -e "s/{{date:dddd}}/$(date +%A)/g" \
    "$TEMPLATE_PATH" > "$FILE_PATH"
```

### Step 3: 返回结果

- 成功：返回生成的文件路径
- 失败：返回错误信息

## 定时任务配置

```json
{
  "name": "riji-daily-diary",
  "schedule": "0 0 * * *",
  "script": "generate-lifeos-daily.sh",
  "delivery": "announce"
}
```

## 注意事项

- 确保 LANG=en_US.UTF-8 以获取英文星期
- 检查文件是否已存在，避免覆盖
