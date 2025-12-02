# 测试说明

## 功能改进
已完成对 Infinity2Chrome 书签导入功能的改进,现在支持从 `infinity` 文件夹中读取书签数据。

## 测试文件
项目中包含两个测试文件:

### 1. test-standard.json
标准格式的 Infinity 备份文件,包含:
- 4 个书签(百度、淘宝、知乎)
- 1 个文件夹
- 2 个页面

### 2. test-infinity-folder.json
包含 `infinity` 文件夹结构的备份文件,包含:
- 2 个书签(Google、GitHub)
- 1 个页面

## 手动测试步骤

### 测试标准格式
1. 打开 http://localhost:3000
2. 点击"选择文件"按钮
3. 选择 `test-standard.json` 文件
4. 验证:
   - ✅ 文件名显示为 "test-standard.json"
   - ✅ 显示统计信息: 总计 4, 网站 3, 应用 0, 文件夹 1
   - ✅ 可以看到所有书签
   - ✅ 可以切换到"页面 1"和"页面 2"查看不同页面的书签

### 测试 infinity 文件夹格式
1. 点击清除按钮(如果已导入其他文件)
2. 点击"选择文件"按钮
3. 选择 `test-infinity-folder.json` 文件
4. 验证:
   - ✅ 文件名显示为 "test-infinity-folder.json"
   - ✅ 显示统计信息: 总计 2, 网站 2, 应用 0, 文件夹 0
   - ✅ 可以看到 Google 和 GitHub 书签
   - ✅ 可以点击书签打开对应网站

### 测试导出功能
1. 导入任一测试文件后
2. 点击"导出到 Chrome 书签"按钮
3. 验证:
   - ✅ 下载了 `chrome_bookmarks.html` 文件
   - ✅ 文件包含正确的书签数据
   - ✅ 可以在 Chrome 书签管理器中导入该文件

### 测试错误处理
1. 创建一个无效的 JSON 文件
2. 尝试导入
3. 验证:
   - ✅ 显示错误信息
   - ✅ 可以展开查看调试信息
   - ✅ 调试信息显示文件的实际结构

## 支持的文件格式

### 格式 1: 标准格式
```json
{
  "data": {
    "site": {
      "sites": [[...]]
    }
  }
}
```

### 格式 2: infinity 文件夹格式
```json
{
  "infinity": {
    "data": {
      "site": {
        "sites": [[...]]
      }
    }
  }
}
```

### 格式 3: 简化格式
```json
{
  "site": {
    "sites": [[...]]
  }
}
```

### 格式 4: infinity 简化格式
```json
{
  "infinity": {
    "site": {
      "sites": [[...]]
    }
  }
}
```

## 调试功能

当导入失败时:
1. 错误信息会显示文件包含的顶层键
2. 可以展开"点击查看文件结构详情"查看完整的 JSON 结构
3. 控制台会输出详细的错误日志

## 开发者说明

### 修改的文件
- `components/sites-viewer.tsx` - 增强文件解析逻辑
- `.gitignore` - 添加测试文件忽略规则
- `IMPROVEMENTS.md` - 详细的改进文档

### 新增文件
- `test-standard.json` - 标准格式测试文件
- `test-infinity-folder.json` - infinity 文件夹格式测试文件
- `TESTING.md` - 本测试说明文档

### 关键改进
1. 支持多种文件格式
2. 智能数据提取
3. 详细的错误提示
4. 调试信息面板
5. 更好的用户体验
