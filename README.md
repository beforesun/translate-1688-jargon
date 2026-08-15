# 1688 买家词 → 工厂黑话翻译 Skill

一个给 Codex 使用的中文采购 skill：把日常商品描述、零售名称、用途或图片线索，转换成适合 1688 检索的行业词、工厂搜索式和询盘话术。

它不会把猜测包装成专业参数。用户没提供克重、尺寸、材料或工艺时，这些信息会被标记为候选或待确认，而不是凭空写进商品描述。

## 能做什么

- 将买家口语拆成品类、材质、工艺、结构、规格和交易词
- 生成基础找货、行业精搜、库存尾货、找厂四类搜索式
- 使用三类工厂检索路径：
  - `面料名/原料名 + 工艺 + 品类`
  - `材质 + 尺寸/规格 + 尾货/库存`
  - `外贸单/库存 + 工厂/厂家`
- 提供服装/瑜伽裤、塑料收纳盒、手机壳候选词库
- 生成 MOQ、拿样、打样、OEM/ODM 等询盘话术
- 提醒核验所谓“源头工厂”“自产自销”“外贸原单”

## 安装

将 skill 目录复制到 Codex skills 目录：

```bash
git clone https://github.com/beforesun/translate-1688-jargon.git
cp -R translate-1688-jargon/skill/translate-1688-jargon ~/.codex/skills/
```

重新开启 Codex 会话后即可使用。

## 使用

```text
使用 $translate-1688-jargon，把“软乎乎、不掉毛的沙发毯”转换成 1688 搜索词。
```

```text
使用 $translate-1688-jargon，我要找高腰瑜伽裤的现货厂、库存尾货和 OEM 工厂。
```

默认输出包括：

1. 可能的行业品类词
2. 可直接复制到 1688 的多组搜索式
3. 拆词逻辑与候选属性
4. 需要确认的关键参数
5. 按需提供的供应商询盘话术

## 设计原则

搜索标签不是事实证明：标题包含“源头工厂、厂家直供、ODM、外贸原单”不代表卖家一定具有相应身份或授权。采购前应进一步核验主营类目、生产设备、样品一致性、MOQ、产能、验厂信息和开票主体。

## 目录

```text
skill/translate-1688-jargon/
├── SKILL.md
├── agents/openai.yaml
└── references/
    ├── category-lexicon.md
    └── translation-playbook.md
```

## License

MIT
