# Neuroweave 文章管理系统使用指南

## 📋 文件结构

```
src/
├── content/articles/          # 所有文章存放位置
│   ├── TEMPLATE-translations.md     # Translations 模板
│   ├── TEMPLATE-overviews.md        # Overviews 模板
│   ├── neurodivergent-self-employment.md
│   ├── museum-neurodivergent-accessibility.md
│   └── invisible-disabilities-sunflower.md
│
└── pages/reading/
    ├── translations.astro      # NW 翻译列表页面
    ├── overviews.astro         # NW 概述列表页面
    └── article/[slug].astro    # 文章详情页面（动态路由）
```

## 🚀 如何添加新文章

### 步骤 1：复制模板
选择你要添加的内容类型：
- **翻译文章**：复制 `TEMPLATE-translations.md`
- **概述**：复制 `TEMPLATE-overviews.md`

### 步骤 2：编辑 Frontmatter
```markdown
---
title: "你的文章标题"
date: "2026-09-01"
author: "你的名字或团队名"
tags: ["标签1", "标签2", "标签3"]
excerpt: "这是文章摘要，会显示在列表页面。"
type: "translations"    # 或 "overviews"
---
```

**Frontmatter 字段说明：**
- `title`: 文章标题（必需）
- `date`: 发布日期，格式 YYYY-MM-DD（必需）
- `author`: 作者名称（可选）
- `tags`: 标签数组，用于分类和搜索（可选）
- `excerpt`: 文章摘要，会显示在列表页（可选）
- `type`: 内容类型：`"translations"` 或 `"overviews"`（必需）

### 步骤 3：编写文章内容
使用 Markdown 格式编写文章内容。支持：
- `## 标题`, `### 小标题`
- 有序/无序列表
- 引用 `> 引用文本`
- 代码块 (使用 `````)
- 链接 `[文本](URL)`
- 等所有标准 Markdown 格式

### 步骤 4：保存文件
将文件保存到 `src/content/articles/` 目录，文件名将自动作为文章 URL slug 使用。

**命名约定：**
- 使用英文和连字符：`my-article-title.md`
- 避免空格和特殊字符
- 文件名会直接用在 URL 中

## 🏷️ Tag 系统

### 如何使用 Tag
1. **分类**：Tag 用于对文章进行分类
2. **搜索**：用户可以点击 Tag 过滤相关文章
3. **灵活添加**：添加任何你认为合适的 Tag，系统会自动识别

### Tag 示例
```yaml
tags: ["ADHD", "神经多样性", "工作"]
tags: ["博物馆", "包容性", "无障碍"]
tags: ["隐形障碍", "向日葵计划", "认可"]
```

## 🔍 搜索和过滤功能

- **搜索栏**：实时搜索文章标题和摘要
- **Tag 按钮**：点击 Tag 过滤相关文章
- **组合使用**：可同时使用搜索和 Tag 过滤

## 📄 页面说明

### NW 翻译 (`/reading/translations`)
- 显示所有 `type: "translations"` 的文章
- 支持搜索和 Tag 过滤
- 实时搜索文章内容

### NW 概述 (`/reading/overviews`)
- 显示所有 `type: "overviews"` 的文章
- 支持搜索和 Tag 过滤
- 结构与 Translations 相同

### 文章详情 (`/reading/article/[slug]`)
- 显示完整的 Markdown 文章内容
- 展示文章元信息（日期、作者）
- 显示相关 Tag（可点击回到列表过滤）
- 有"返回"链接回到列表页

## ✨ Markdown 内容样式示例

```markdown
## 主要标题

这是普通段落文本，会自动获得适当的行距和字体。

### 小标题

#### 更小的标题

**粗体文本** 和 *斜体文本*

#### 列表

有序列表：
1. 第一项
2. 第二项
3. 第三项

无序列表：
- 项目 A
- 项目 B
- 项目 C

#### 引用

> 这是一个引用
> 可以多行

#### 代码

`行内代码`

```python
# 代码块
def hello():
    print("Hello, World!")
```

#### 链接

[Neuroweave 网站](https://neuroweave.com)
```

## 🎨 自动功能

这个系统会自动：
- ✅ 从 Markdown 文件提取 Frontmatter
- ✅ 解析并显示所有 Tag
- ✅ 生成文章列表（按日期倒序）
- ✅ 计算每个 Tag 的文章数量
- ✅ 支持实时搜索和过滤
- ✅ 生成文章详情页面
- ✅ 处理 Markdown 格式化

## 🔗 URL 规则

添加文件后，自动生成的 URL：
- 文件：`src/content/articles/my-article.md`
- 详情页 URL：`/reading/article/my-article`

## 💡 Tips

1. **Frontmatter 缩进**：确保 YAML 缩进正确（2 个空格）
2. **日期格式**：必须是 `YYYY-MM-DD` 格式
3. **Tag 多样性**：同时使用中英文 Tag 可以增加搜索灵活性
4. **摘要**：好的摘要让用户快速理解文章内容
5. **文件名**：使用小写字母和连字符，避免特殊字符

## 📝 完整示例

```markdown
---
title: "神经发散与创意：一个新的视角"
date: "2026-09-01"
author: "Neuroweave 翻译团队"
tags: ["神经多样性", "创意", "认知差异"]
excerpt: "探讨神经发散如何影响创意思维，以及为什么这是一个值得庆祝的优势。"
type: "translations"
---

## 神经发散与创意

神经发散人士常常展现出独特的创意能力...

### 不同的思维方式

ADHD 个体可能...

### 创意优势

许多成功的艺术家、设计师和创新者...
```

## 🆘 常见问题

**Q: 我的文章没有出现在列表中？**
A: 检查 frontmatter 中的 `type` 字段是否正确（"translations" 或 "overviews"）

**Q: 搜索不工作？**
A: 搜索会检查文章标题和摘要。确保你的 `excerpt` 字段包含相关关键词。

**Q: 如何编辑已有的文章？**
A: 直接编辑 markdown 文件，保存即可自动更新。

**Q: 可以删除文章吗？**
A: 是的，直接删除对应的 markdown 文件即可。
