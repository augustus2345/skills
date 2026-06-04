# 我的 Claude Skills 集合

个人维护的 Claude Code skills。每个 skill 独立放在自己的目录里，**本仓库是单一事实来源**（source of truth）。

## Skills

| Skill | Description | Use when |
|---|---|---|
| [hecaitou-style](./hecaitou-style/) | 用和菜头（公众号"槽边往事"作者）的结构与节奏写中文随笔，叙述者设定为 25 岁 | 写第一人称中文随笔、读后感、生活观察 |
| [he-tongxue-video](./he-tongxue-video/) | 根据"想法.md"生成何同学风格的两份产出：视频文稿（旁白）+ 视频脚本（分镜） | 拿到视频选题想法，要生成可拍摄的完整脚本 |

## How to use

本仓库文件是**权威版本**。`$HOME\.claude\skills\` 里的本地副本可随时丢弃/重建。

### 安装单个 skill

PowerShell 5.1（Windows）：

```powershell
Copy-Item -Recurse -Force F:\skills\<skill-name> $HOME\.claude\skills\
```

例如：

```powershell
Copy-Item -Recurse -Force F:\skills\hecaitou-style $HOME\.claude\skills\
```

### 推荐：用 junction 双向实时同步

```powershell
New-Item -ItemType Junction -Path $HOME\.claude\skills\<skill-name> -Target F:\skills\<skill-name>
```

junction 让两边指向同一份文件，改一边另一边即时同步。Claude Code 加载 `.claude/skills/` 的行为完全不变。

## Adding a new skill

1. 在仓库根下创建 kebab-case 命名的目录，例如 `my-new-skill/`
2. 写 `SKILL.md`，frontmatter 至少包含：
   - `name`：与目录名一致
   - `description`：单行，包含 "适用于…" 和 "NOT for:" 子句
3. （可选）添加 `examples.md`、`references.md`、`assets/` 等同目录下的辅助文件
4. 在本 README 的 Skills 表格里加一行
5. 提交并推送：

   ```powershell
   git -C F:\skills add .
   git -C F:\skills commit -m "Add <skill-name> skill"
   git -C F:\skills push
   ```

## 约定

- 所有 skill **平铺在顶层**，不分组、不嵌套
- `SKILL.md` 必须大写（Linux/macOS 加载器大小写敏感）
- 每个 skill 自包含，不跨 skill 共享文件
- `name` 字段 = 目录名（kebab-case）
- frontmatter 不加 `version` / `tags` / `author`（加载器不读这些；git 历史承担）
- 推荐章节顺序：适用场景 → 核心原则 → 流程 → 自检清单 → 参考范文
