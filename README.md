<p align="center"><b>简体中文</b> | <a href="./README_en.md">English</a></p>

# zhihu-distill

一句话说明：这个 Skill 帮你把一个知乎用户的回答、文章和想法下载为 Markdown，再按主题筛选、合并，并整理成可供 AI 蒸馏的知识体系材料。

## 这个版本能做什么

- 从知乎用户主页批量下载回答、文章和想法，并保存为带元信息的 Markdown 文件。
- 按投资、科技、教育、健康、设计或自定义关键词筛选内容。
- 将筛选后的内容按文章、回答、想法顺序合并成一个可读的 Markdown 文件。
- 提供蒸馏提示词模板，帮助 AI 生成作者画像、核心理念、方法论、观点地图和实践建议。
- 可作为 Codex Skill 使用，也可以单独运行 Python 脚本。

## 适合谁

- 想系统研究某位知乎创作者长期内容的人。
- 想把分散回答整理成知识库、研究笔记或投资/行业观察材料的人。
- 已经有合法访问权限和有效 Cookie，需要把人工复制整理流程自动化的人。

## 使用示例

示例输入：

```bash
python3 scripts/zhihu_download.py --user example-user --output ./data
python3 scripts/zhihu_filter.py --input ./data/raw --output ./data/filtered --topic invest
python3 scripts/zhihu_merge.py --input ./data/filtered --output ./data/merged.md
```

示例输出结构：

```text
data/
├── raw/
│   ├── answers/
│   ├── articles/
│   ├── pins/
│   └── meta.json
├── filtered/
└── merged.md
```

`merged.md` 可以继续配合 `references/prompt_templates.md` 中的模板做 AI 蒸馏。

## 快速开始

安装依赖：

```bash
python3 -m pip install httpx markdownify beautifulsoup4
```

下载指定用户内容：

```bash
python3 scripts/zhihu_download.py --user <user_token> --output ./data
```

`user_token` 是知乎个人主页 URL 中的标识，例如 `zhihu.com/people/<user_token>`。

首次运行会提示输入知乎 Cookie。Cookie 只应保存在本地输出目录，仓库的 `.gitignore` 已排除 `cookie.txt` 和常见本地产物。

## 常见用法

按内置主题筛选：

```bash
python3 scripts/zhihu_filter.py --input ./data/raw --output ./data/filtered --topic tech
```

按自定义关键词筛选：

```bash
python3 scripts/zhihu_filter.py --input ./data/raw --output ./data/filtered --keywords "AI,机器学习,大模型"
```

合并为单个 Markdown：

```bash
python3 scripts/zhihu_merge.py --input ./data/filtered --output ./data/merged.md
```

## 当前限制

- 需要有效知乎 Cookie；Cookie 过期后需要重新获取。
- 脚本依赖知乎页面和接口结构，平台改版时可能需要维护。
- 下载速度有随机延迟，适合完整整理，不适合高频抓取。
- 蒸馏报告需要 AI 根据合并文件继续生成，本仓库只提供下载、筛选、合并和提示词模板。

## 安全与隐私说明

- 只处理你有权访问和保存的内容，并遵守知乎平台规则。
- 不要提交 Cookie、`.env`、下载原文、筛选产物或个人知识库材料到仓库。
- `.gitignore` 已排除 `cookie.txt`、`raw/`、`filtered/`、`distilled/`、`merged.md` 等本地产物。

## 技术实现

- `scripts/zhihu_download.py` 下载回答、文章和想法，并转换为 Markdown。
- `scripts/zhihu_filter.py` 按主题或关键词筛选内容。
- `scripts/zhihu_merge.py` 合并内容并保持类型优先级。
- `references/prompt_templates.md` 提供蒸馏提示词模板。

## Roadmap

- 增加更稳健的失败重试和下载进度恢复。
- 为蒸馏报告增加可复用输出模板。
- 增加更多主题关键词配置。

## License

[MIT](./LICENSE)

## Contributors

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/hankchn">
        <img src="https://github.com/hankchn.png" width="64" height="64" style="border-radius:50%;" alt="hankchn" />
        <br />
        <sub><b>hankchn</b></sub>
      </a>
      <br />
      <sub>Hank Yang</sub>
    </td>
    <td align="center">
      <a href="https://openai.com/codex">
        <img src="https://github.com/openai.png" width="64" height="64" style="border-radius:50%;" alt="Codex" />
        <br />
        <sub><b>Codex</b></sub>
      </a>
      <br />
      <sub>OpenAI Codex</sub>
    </td>
  </tr>
</table>
