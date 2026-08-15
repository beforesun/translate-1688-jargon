<div align="center">

# 🏭 1688 买家词 → 工厂黑话翻译器

**你以为自己在找货，其实可能连“厂里的叫法”都没搜对。**

把「瑜伽裤」「收纳盒」「手机壳」这类买家词，转换成 1688 更容易检索的材质、工艺、结构、产业带、库存与代工关键词。

适用于 **Codex · Claude Code · OpenClaw · Hermes Agent · 其他 Agent Skills 兼容客户端**

[快速安装](#安装) · [查看示例](#效果示例) · [工作原理](#它是怎么翻译的) · [安全边界](#它不会为了显得专业而胡编)

</div>

---

## 为什么需要它？

1688 最反直觉的地方是：普通人按“用途和感受”描述商品，工厂却按“原料、工艺、结构和生产方式”描述商品。

你搜商品名，像在逛商场；你搜行业词，才更像在进仓库。

| 你会搜索 | Skill 帮你继续拆成 |
|---|---|
| 瑜伽裤 | 锦氨、双面磨毛、无缝针织、高腰、库存尾货、OEM |
| 收纳盒 | PP/ABS、注塑、分格、一体成型、周转盒、开模 |
| 手机壳 | PC/TPU、素材壳、精孔注塑、内置磁圈、外贸库存、ODM |

但这些术语不是固定答案。Skill 会区分“用户已经确认的属性”和“值得尝试的搜索分支”，避免凭一个商品名就编出克重、尺寸和材料。

## 效果示例

### 输入

```text
高腰瑜伽裤
```

### 输出思路

```text
基础找货：高腰 女士 瑜伽裤
材质分支：锦氨 高腰 瑜伽裤
工艺分支：无缝针织 高腰 健身裤
库存分支：高腰 瑜伽裤 库存尾货
找厂分支：瑜伽服 OEM 加工厂

待确认：成分比例、克重、织法、是否磨毛、裆部结构、尺码段、首单数量
```

它不会因为“280g”“双面磨毛”听起来专业，就擅自认定你的商品一定具有这些属性。

### 再看两个例子

| 买家输入 | 可尝试的行业搜索路径 |
|---|---|
| 内衣收纳盒 | `PP 注塑 分格整理盒` · `塑料收纳盒 注塑加工厂` · `内衣整理盒 库存尾货` |
| 防摔手机壳 | `TPU 软胶 全包防摔壳` · `PC TPU 复合保护壳` · `手机壳 注塑加工 OEM` |

## 它是怎么翻译的？

Skill 会把一句买家描述拆成六层信息：

```text
核心品类 → 材质/面料 → 生产工艺 → 结构/款式 → 尺寸规格 → 供货方式
```

然后从六条供应链路径生成搜索式：

1. **找生产现货**：`面料名/原料名 + 工艺 + 品类`
2. **找库存尾货**：`材质 + 尺寸/规格 + 尾货/库存`
3. **找代工工厂**：`外贸单/库存 + 工厂/厂家 + OEM/ODM`
4. **找产业带**：`候选产地 + 品类 + 工艺/厂家`
5. **去溢价标签**：移除“网红、ins、轻奢、专用”，回到基础工业品名
6. **以图搜款再拆词**：从图片结果提取重复行业词，再进行二次文字搜索

默认会提供：

- 基础找货词
- 行业精搜词
- 库存/尾货词
- 加工/找厂词
- 候选属性与待确认参数
- 可复制的供应商询盘话术
- 真工厂核验清单与拿样避坑提醒

## 安装

本仓库采用开放的 `SKILL.md + references/` 结构。Skill 不依赖 API、脚本或特定操作系统。

### Codex

个人安装：

```bash
git clone https://github.com/beforesun/translate-1688-jargon.git ~/.codex/skills/translate-1688-jargon
```

使用：

```text
使用 $translate-1688-jargon，把“软乎乎、不掉毛的沙发毯”转换成 1688 搜索词。
```

### Claude Code

安装为个人 Skill：

```bash
git clone https://github.com/beforesun/translate-1688-jargon.git ~/.claude/skills/translate-1688-jargon
```

也可以放到项目的 `.claude/skills/translate-1688-jargon/`。调用：

```text
/translate-1688-jargon 帮我把“抽屉收纳盒”变成找厂搜索词
```

### OpenClaw

从 GitHub 直接安装到当前 workspace：

```bash
openclaw skills install git:beforesun/translate-1688-jargon@main
```

安装给所有本地 Agent：

```bash
openclaw skills install git:beforesun/translate-1688-jargon@main --global
```

调用：

```text
$translate-1688-jargon 把“磁吸手机壳”翻译成 1688 工厂词
```

### Hermes Agent

Hermes 支持从 `SKILL.md` URL 安装：

```bash
hermes skills install https://raw.githubusercontent.com/beforesun/translate-1688-jargon/main/SKILL.md --name translate-1688-jargon --now
```

也可以手动安装完整目录：

```bash
git clone https://github.com/beforesun/translate-1688-jargon.git ~/.hermes/skills/ecommerce/translate-1688-jargon
```

调用：

```text
/translate-1688-jargon 帮我找 PP 注塑收纳盒的库存厂
```

### 其他 Agent Skills 客户端

如果客户端支持 `SKILL.md` / [Agent Skills](https://agentskills.io/) 结构，通常只需把本仓库放进它的 skills 目录。通用个人目录可使用：

```bash
git clone https://github.com/beforesun/translate-1688-jargon.git ~/.agents/skills/translate-1688-jargon
```

具体的优先级和调用语法以客户端文档为准。

## 推荐提示词

### 只要搜索词

```text
把“冰箱保鲜盒”转换成 1688 搜索词。分别给我基础找货、材料工艺、库存尾货和找厂四组，不要解释。
```

### 找源头货源

```text
我要采购 500 个透明首饰盒。使用 1688 黑话拆解材质、工艺、结构和供货方式，给搜索词、待确认参数和询盘话术。
```

### 看图找货

```text
根据这张商品图片，先列出能观察到的结构与表面特征，再给 3 组可能的 1688 行业词。无法确认的材质不要当事实。
```

### 批量转换

```text
把下面 20 个商品整理成表格：日常说法、行业词、库存搜索式、找厂搜索式、待确认参数。
```

### 产业带与平替路径

```text
我要找保温杯货源。请给行业词、常见产业带候选、库存搜索式和工厂核验问题；不要把产业带或“源头工厂”标签当成真实性证明。
```

## 它不会为了显得专业而胡编

有些“黑话翻译器”会把一个模糊商品名直接扩写成：

```text
280g 锦纶双面磨毛无缝……
PP 塑料 30×20cm 外贸尾货……
PC 硬壳 6.7寸 ODM 源头工厂……
```

问题是：用户根本没提供这些参数。

本 Skill 遵守三条底线：

1. **精确参数必须有依据**：未知的克重、尺寸、型号、材料和等级只作为候选。
2. **搜索标签不是身份证明**：`源头工厂`、`自产自销`、`外贸原单`、`ODM` 都可能只是标题营销词。
3. **不承诺神奇差价**：行业词能改变检索结果，但不能保证便宜多少，也不能“彻底过滤”中间商。

找到候选供应商后，还应核验主营类目、生产设备、材料牌号、样品一致性、MOQ、日产能、验厂资料与开票主体。

## Skill 内容

```text
.
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── category-lexicon.md
    ├── sourcing-playbook.md
    └── translation-playbook.md
```

- `SKILL.md`：跨 Agent 的核心工作流与输出规范
- `category-lexicon.md`：服装、塑料收纳、手机壳等高频类目候选词
- `translation-playbook.md`：拆词公式、交易术语、示例和质量校验
- `sourcing-playbook.md`：产业带候选、去标签搜索、以图搜款、供应商核验和拿样话术

## 贡献

欢迎提交 Issue 或 PR，尤其欢迎补充新的类目词典。建议每个术语同时说明：

- 适用类目
- 对应材料或工艺
- 容易混淆的说法
- 哪些参数必须向供应商确认

## License

[MIT](LICENSE)

如果这个 Skill 帮你少翻了几页分销货，欢迎点个 ⭐。
