# epub-beautify

EPUB 美化工具：目录识别与装饰、卷章分级打标、弹注识别、12 套风格预设 × 4 种目录形式（含竖排右翻古籍）、全书底纹/配色。无损模式：只增类与元素、不改不删源书内容，幂等重跑零变化。

从 [PoxenStudio/mybooks](https://github.com/PoxenStudio/mybooks) 的 `epub_beautify` 工具箱插件提取（revision `0.2.0`，见 `webserver/toolbox/epub_beautify.py` 的 `info()`），目录结构与原仓一致，上游 PR 见 PoxenStudio/mybooks#73。

## 布局

```text
webserver/toolbox/epub_beautify.py        工具入口（依赖 mybooks 框架：BaseTool/CoreAPI，见下）
webserver/toolbox/utils/epub_beautify_lib.py   独立核心（仅标准库依赖）
webserver/toolbox/utils/chapter_patterns.py    章节标题正则
webserver/toolbox/utils/styles/                预设 CSS/纸样纹理（presets.json + textures/）
app/src/pages/toolbox/epub_beautify.vue   前端（Nuxt 2 + Vuetify 2，需 mybooks app）
webserver/resources/toolbox/epub_beautify.png  工具图标
tests/test_epub_beautify_core.py           核心单测（170 个，standalone 无依赖）
```

## 运行测试

```bash
python -m pytest tests/test_epub_beautify_core.py -q
```

核心库与测试**不依赖** mybooks/calibre，可独立运行（168/170；另 2 个用例覆盖
框架耦合的 `EpubBeautifyTool` 工具类，需 mybooks 运行时 + calibre，仅在原仓跑）。`epub_beautify.py`（工具入口）与 `.vue`（前端）需 mybooks 框架，仅作源码归档。
