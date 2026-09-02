# 🚀 Neuroweave 完整搜索和 Tag 系统使用指南

## ✨ 功能特性

### 已集成的功能：

✅ **Pagefind 全文搜索** - 快速搜索所有文章内容  
✅ **Tag 系统** - `/tags/[tag]` 动态路由  
✅ **三种内容类型** - translations（翻译）、overviews（概述）、conversations（访谈）  
✅ **搜索 + Tag 组合** - 支持全文搜索和 Tag 过滤同时使用  
✅ **现代化 UI** - Modal 弹窗式搜索界面  
✅ **MIT License** - 基于 Astro Cactus 主题改进（已署名）  

---

## 🔍 搜索功能详解

### 1. **Pagefind 全文搜索**

**位置**: 所有列表页面顶部搜索按钮

**工作原理**:
- 点击搜索按钮打开 Modal
- 输入关键词实时搜索文章标题、内容、摘要
- 支持按 `Ctrl+K` / `Cmd+K` 快捷键打开
- 按 `Esc` 关闭搜索

**代码位置**: [src/components/Search.astro](src/components/Search.astro)

**自定义选项**:
```astro
new PagefindUI({
  baseUrl: import.meta.env.BASE_URL,
  bundlePath: import.meta.env.BASE_URL.replace(/\/$/, "") + "/pagefind/",
  element: "#pagefind",
  showImages: false,  // 是否显示图片
});
```

### 2. **Tag 过滤系统**

**位置**: 列表页面右侧边栏

**工作原理**:
- 点击 Tag 按钮过滤该 tag 的文章
- 显示每个 tag 对应的文章数量
- "全部" 按钮重置过滤

**三个列表页面**:
- `/reading/translations` - NW 翻译
- `/reading/overviews` - NW 概述  
- `/reading/conversations` - NW 访谈

### 3. **Tag 页面**

**位置**: `/tags/[tag]`

**功能**:
- 显示该 tag 下所有文章（跨越所有内容类型）
- 显示相关 tag 和文章数
- 返回导航链接

**示例 URL**:
- `/tags/神经多样性`
- `/tags/自雇`
- `/tags/博物馆`

---

## 📝 如何添加新文章

### 步骤 1: 复制模板

根据内容类型选择模板：
- **翻译**: `src/content/articles/TEMPLATE-translations.md`
- **概述**: `src/content/articles/TEMPLATE-overviews.md`

### 步骤 2: 编辑 Frontmatter

```markdown
---
title: "你的文章标题"
date: "2026-09-01"
author: "你的名字或团队"
tags: ["标签1", "标签2", "标签3"]
excerpt: "这是文章摘要，显示在列表页。"
type: "translations"    # 或 overviews, conversations
---
```

**字段说明**:
- `title`: 文章标题（必需）
- `date`: 发布日期 YYYY-MM-DD（必需）
- `author`: 作者名称（可选）
- `tags`: 标签数组（可选，用于搜索和过滤）
- `excerpt`: 摘要（会显示在列表）
- `type`: 内容类型（必需：translations/overviews/conversations）

### 步骤 3: 编写内容

使用 Markdown 格式：
```markdown
## 主标题

这是段落文本。

### 子标题

- 列表项 1
- 列表项 2

[链接文本](https://example.com)

> 引用文本
```

### 步骤 4: 保存文件

- 位置: `src/content/articles/`
- 文件名: `my-article-title.md`（使用英文和连字符）
- 文件名会作为 URL slug

**自动生成的 URL**:
- 文章详情: `/reading/article/my-article-title`
- Tag 页面: `/tags/标签名`

---

## 🎯 搜索和过滤的工作流程

### 使用场景 1: 搜索特定关键词

1. 打开任何列表页面（translations/overviews/conversations）
2. 点击搜索按钮或按 `Ctrl+K`
3. 输入关键词（如"ADHD"、"自雇"等）
4. Pagefind 实时返回匹配的文章
5. 点击结果跳转到文章详情

### 使用场景 2: 按 Tag 浏览

1. 打开列表页面
2. 右侧边栏点击某个 Tag（如"神经多样性"）
3. 文章列表自动过滤到该 Tag 的文章
4. 点击 Tag 标签访问 `/tags/[tag]` 页面

### 使用场景 3: 组合搜索和过滤

1. 打开列表页面
2. 先点击 Tag 过滤（如"工作"）
3. 再在搜索框输入关键词（如"自雇"）
4. 文章既要匹配 Tag 又要匹配关键词

### 使用场景 4: 浏览所有同 Tag 的文章

1. 在任何文章详情页，点击文章下方的 Tag
2. 跳转到 `/tags/[tag]` 页面
3. 查看该 Tag 下所有文章（跨越所有内容类型）
4. 侧边栏可快速切换到其他 Tag

---

## 🔧 文件结构

```
src/
├── components/
│   ├── Search.astro                    # Pagefind 搜索组件
│   └── ...
├── content/articles/
│   ├── TEMPLATE-translations.md        # 翻译模板
│   ├── TEMPLATE-overviews.md           # 概述模板
│   ├── neurodivergent-self-employment.md
│   ├── museum-neurodivergent-accessibility.md
│   └── invisible-disabilities-sunflower.md
├── pages/
│   ├── reading/
│   │   ├── translations.astro          # NW 翻译列表
│   │   ├── overviews.astro             # NW 概述列表
│   │   ├── conversations.astro         # NW 访谈列表
│   │   └── article/[slug].astro        # 文章详情
│   └── tags/
│       └── [tag].astro                 # Tag 页面
└── ...
```

---

## 🎨 Tag 最佳实践

### Tag 命名规范

✅ **推荐**:
- 中英文混合: `["ADHD", "神经多样性", "自雇"]`
- 相关性强: `["博物馆", "包容性", "无障碍"]`
- 不过于具体: 用 `"工作"` 而非 `"远程工作"`

❌ **避免**:
- 标点符号: `"ADHD/ADD"` 改为 `["ADHD", "ADD"]`
- 过长: `"关于神经发散者在职场中面临的挑战"` 改为 `["工作", "神经多样性", "挑战"]`
- 同义重复: 不要同时用 `"翻译"` 和 `"translation"`

### Tag 管理建议

1. **保持一致性** - 同一概念用同一 Tag
2. **保持简洁** - 每篇文章 3-5 个 Tag
3. **跨内容类型** - Tag 在所有内容类型中通用
4. **定期审核** - 检查类似或重复的 Tag

---

## 🔐 构建和部署

### 本地开发

```bash
# 安装依赖
pnpm install

# 启动开发服务器
pnpm dev

# 注意：Pagefind 搜索在开发环境禁用
# 在搜索框会提示需要生产构建
```

### 生产构建

```bash
# 构建网站
pnpm build

# Pagefind 索引会自动生成到 dist/pagefind/

# 本地预览生产构建
pnpm preview
```

---

## 📌 已知事项

- **Pagefind 仅在生产构建可用** - 开发环境搜索框会提示
- **搜索索引** - 每次构建时自动重建
- **Tag 页面跨类型** - 一个 Tag 可能包含 translations、overviews、conversations 的文章

---

## 📄 许可证信息

本项目基于 Astro Cactus 主题改进，采用 MIT License。

**原项目**:
- 名称: Astro Cactus
- 链接: https://github.com/chrismwilliams/astro-theme-cactus
- 中文版: https://github.com/zouzonghao/Astro-theme-Cactus-zh_CN
- 许可证: MIT

**改进内容**:
- 集成 Pagefind 全文搜索
- 创建 Tag 动态路由
- 支持多内容类型（translations/overviews/conversations）
- 改进搜索 UI 和交互

---

## 💡 常见问题

**Q: 我的文章在列表中看不到？**  
A: 检查 frontmatter 中的 `type` 字段是否正确且不包含 "TEMPLATE"

**Q: Pagefind 搜索不工作？**  
A: 确保在生产构建中（`pnpm build && pnpm preview`），开发环境不支持

**Q: 如何修改 Tag？**  
A: 直接编辑 markdown 文件的 `tags` 字段，系统会自动更新

**Q: 能否删除文章？**  
A: 直接删除对应的 markdown 文件即可

**Q: 搜索结果为空？**  
A: 确保关键词与文章标题、内容或摘要匹配

---

## 🚀 后续优化方向

- [ ] 搜索高亮显示
- [ ] 按日期排序选项
- [ ] Tag 云可视化
- [ ] 搜索历史记录
- [ ] 相关文章推荐

---

**最后更新**: 2026-09-01
**作者**: Neuroweave 开发团队
