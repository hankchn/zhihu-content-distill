<h1 align="center">zhihu-distill 🧪</h1>

<p align="center">
  <a href="README.md">简体中文</a> | <strong>English</strong> | <a href="README_ar.md">العربية</a>
</p>

<p align="center">
  A CodeBuddy Skill for bulk downloading Zhihu user profiles and AI-powered knowledge distillation.
</p>

---

Given a Zhihu user link, it automatically downloads all answers, articles, and pins, saves them as Markdown files, and generates a structured knowledge distillation report.

## ✨ Features

- **Bulk Download** — Automatically crawl all answers, articles, and pins from a Zhihu user profile, converting to clean Markdown
- **Topic Filtering** — Built-in keyword libraries for investment/tech topics, with support for custom keywords
- **Content Merging** — Merge content into a single document by priority (Articles > Answers > Pins)
- **AI Distillation** — Structured prompt templates to guide AI in generating in-depth knowledge reports

## 🚀 Installation

Use as a CodeBuddy Skill:

```bash
unzip zhihu-distill.zip -d ~/.codebuddy/skills/
```

Or use the scripts independently:

```bash
pip install httpx markdownify beautifulsoup4
```

## 📖 Usage

1. **Download**: `python3 scripts/zhihu_download.py --user <user_token> --output ./data`
   - `user_token` is the identifier in the Zhihu profile URL: `zhihu.com/people/<user_token>`
   - On first run, you'll be prompted to enter your Zhihu Cookie (obtain from browser DevTools)

2. **Filter**:
   ```bash
   # Use built-in investment topic
   python3 scripts/zhihu_filter.py --input ./data/raw --output ./data/filtered --topic invest
   # Use custom keywords
   python3 scripts/zhihu_filter.py --input ./data/raw --output ./data/filtered --keywords "AI,machine learning,LLM"
   ```

3. **Merge**: `python3 scripts/zhihu_merge.py --input ./data/filtered --output ./data/merged.md`

4. **AI Distillation**: Send the merged file to AI in batches, using templates from `references/prompt_templates.md` to generate reports.

## 📁 Project Structure

```
zhihu-distill/
├── SKILL.md                    # CodeBuddy Skill definition
├── scripts/
│   ├── zhihu_download.py       # Download script
│   ├── zhihu_filter.py         # Filter script
│   └── zhihu_merge.py          # Merge script
├── references/
│   └── prompt_templates.md     # Distillation prompt templates
├── .gitignore
├── LICENSE
└── README.md
```

## ⚠️ Notes

- Requires a valid Zhihu Cookie (expires periodically, needs refresh)
- Built-in random delays (1.5-3s) to avoid triggering anti-crawl mechanisms
- Cookie file (`cookie.txt`) is excluded in `.gitignore`

## 📄 License

MIT
