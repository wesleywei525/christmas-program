# 画展导览网页使用说明

## 文件结构

请按以下方式组织你的文件：

```
exhibition/
├── exhibition_guide.Rmd    # R Markdown 主文件
├── images/                  # 画作照片文件夹
│   ├── painting01.jpg
│   ├── painting02.jpg
│   ├── painting03.jpg
│   └── ... (painting04.jpg 到 painting30.jpg)
├── audio/                   # 音频讲解文件夹
│   ├── painting01.mp3
│   ├── painting02.mp3
│   ├── painting03.mp3
│   └── ... (painting04.mp3 到 painting30.mp3)
└── exhibition_guide.html   # 生成的网页（Knit后产生）
```

## 使用步骤

### 1. 准备素材

**图片文件：**
- 格式：JPG 或 PNG
- 建议尺寸：宽度 1200-2000 像素（保持画作比例）
- 命名：painting01.jpg, painting02.jpg, ... painting30.jpg
- 放入 `images/` 文件夹

**音频文件：**
- 格式：MP3（推荐）或 M4A
- 录音建议：每段 2-4 分钟，清晰流畅
- 命名：painting01.mp3, painting02.mp3, ... painting30.mp3
- 放入 `audio/` 文件夹

### 2. 编辑 Rmd 文件

在 `exhibition_guide.Rmd` 中：
- 修改标题和作者信息
- 复制"作品 3"的代码块，粘贴 27 次（总共 30 个作品）
- 依次修改每个作品的：
  - 作品编号（01-30）
  - 画作标题
  - 文件名（painting01.jpg → painting30.jpg）
  - 创作时间、尺寸、媒介
  - 作品描述

### 3. 生成网页

在 RStudio 中：
1. 打开 `exhibition_guide.Rmd`
2. 点击 "Knit" 按钮（或按 Ctrl+Shift+K）
3. 等待生成完成
4. 会自动打开 `exhibition_guide.html` 预览

### 4. 测试

在本地浏览器中测试：
- 图片能否正常显示
- 音频能否播放
- 在手机浏览器中测试（重要！）
- 检查所有链接和文件路径

### 5. 部署上线

**方案 A：Netlify（推荐）**
1. 访问 https://app.netlify.com/drop
2. 将整个 `exhibition/` 文件夹拖入页面
3. 立即获得网址（如 https://random-name-123.netlify.app）
4. 可以自定义域名

**方案 B：GitHub Pages**
1. 在 GitHub 创建新仓库
2. 上传所有文件
3. 在仓库设置中启用 GitHub Pages
4. 获得网址：https://你的用户名.github.io/仓库名

**方案 C：Google Drive**
1. 上传整个文件夹到 Google Drive
2. 右键 `exhibition_guide.html` → 共享 → 获取链接
3. 注意：音频可能加载较慢

### 6. 生成二维码

获得网址后：
1. 访问 https://www.qr-code-generator.com/
2. 输入你的网址
3. 下载高清 PNG（建议 300 DPI）
4. 打印 30 份（或打印一份，复印 29 份）

## 特色功能

- **点击图片全屏**：观众可以点击画作查看大图
- **自适应设计**：手机、平板、电脑都能完美显示
- **音频预加载**：使用 `preload="metadata"` 加快加载速度
- **悬停效果**：鼠标悬停在画作上有轻微放大效果

## 高级定制（可选）

### 批量生成作品列表

如果你的作品信息在 Excel 或 CSV 中，可以用 R 代码批量生成：

```r
# 读取作品信息
paintings <- read.csv("paintings_info.csv")

# 生成 HTML 代码
for(i in 1:nrow(paintings)) {
  cat(sprintf('
<div class="painting">
<div class="painting-number">作品 %02d</div>
<h2 class="painting-title">%s</h2>
<img src="images/painting%02d.jpg" alt="%s" onclick="this.requestFullscreen()">
<audio controls preload="metadata">
  <source src="audio/painting%02d.mp3" type="audio/mpeg">
</audio>
<div class="painting-info">
<strong>创作时间：</strong>%s<br>
<strong>尺寸：</strong>%s<br>
<strong>媒介：</strong>%s
</div>
<div class="painting-description">
%s
</div>
</div>
---
', i, paintings$title[i], i, paintings$title[i], i, 
   paintings$date[i], paintings$size[i], 
   paintings$medium[i], paintings$description[i]))
}
```

### 修改样式

在 `<style>` 标签中可以修改：
- 颜色方案：修改 `color` 和 `background-color`
- 字体大小：修改 `font-size`
- 间距：修改 `margin` 和 `padding`
- 边框样式：修改 `border` 和 `border-radius`

## 故障排除

**问题：图片不显示**
- 检查文件路径是否正确（区分大小写）
- 确认图片在 `images/` 文件夹中
- 检查文件扩展名（.jpg 还是 .JPG）

**问题：音频无法播放**
- 确认音频格式为 MP3
- 检查文件大小（过大可能加载慢）
- 在不同浏览器中测试

**问题：手机上显示异常**
- 清除浏览器缓存
- 检查 CSS 中的响应式设计代码

## 联系支持

如有问题，随时问我！我可以帮你：
- 调整样式和布局
- 添加更多功能
- 解决技术问题
