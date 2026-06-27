<p align="center"><a href="./README.md">简体中文</a> | <b>English</b></p>

# zhihu-distill

One-line summary: this Skill downloads a Zhihu user's answers, articles, and pins into Markdown, then filters, merges, and prepares the material for AI knowledge distillation.

## What this version can do

- Download a Zhihu user's answers, articles, and pins as Markdown files with metadata.
- Filter downloaded content by investment, technology, education, health, design, or custom keywords.
- Merge filtered content into one Markdown file ordered by articles, answers, then pins.
- Provide prompt templates for AI distillation into author profile, philosophy, methodology, opinion map, and practical recommendations.
- Work as a Codex Skill or as standalone Python scripts.

## Who it is for

- People who want to study a Zhihu creator's long-term public writing systematically.
- Users who need to turn scattered posts into research notes, knowledge-base material, or domain summaries.
- Users who already have legitimate access and want to automate repetitive copy-and-merge work.

## Usage example

Example input:

```bash
python3 scripts/zhihu_download.py --user example-user --output ./data
python3 scripts/zhihu_filter.py --input ./data/raw --output ./data/filtered --topic invest
python3 scripts/zhihu_merge.py --input ./data/filtered --output ./data/merged.md
```

Example output structure:

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

Use `merged.md` with the templates in `references/prompt_templates.md` for AI distillation.

## Quick start

Install dependencies:

```bash
python3 -m pip install httpx markdownify beautifulsoup4
```

Download a user's content:

```bash
python3 scripts/zhihu_download.py --user <user_token> --output ./data
```

`user_token` is the identifier in a Zhihu profile URL, such as `zhihu.com/people/<user_token>`.

The first run prompts for a Zhihu Cookie. Keep it only in the local output directory; this repository's `.gitignore` excludes `cookie.txt` and common generated outputs.

## Common uses

Filter by a built-in topic:

```bash
python3 scripts/zhihu_filter.py --input ./data/raw --output ./data/filtered --topic tech
```

Filter by custom keywords:

```bash
python3 scripts/zhihu_filter.py --input ./data/raw --output ./data/filtered --keywords "AI,machine learning,LLM"
```

Merge into a single Markdown file:

```bash
python3 scripts/zhihu_merge.py --input ./data/filtered --output ./data/merged.md
```

## Current limitations

- A valid Zhihu Cookie is required and must be refreshed when it expires.
- The scripts depend on Zhihu page and API behavior, so platform changes may require maintenance.
- Random delays make it suitable for careful archival, not high-frequency scraping.
- The repository prepares material for distillation; the final distillation report is produced by an AI workflow using the merged file.

## Security and privacy

- Only process content you are allowed to access and store, and follow Zhihu's platform rules.
- Do not commit Cookies, `.env` files, downloaded raw content, filtered output, or personal knowledge-base material.
- `.gitignore` excludes `cookie.txt`, `raw/`, `filtered/`, `distilled/`, `merged.md`, and other local outputs.

## Technical notes

- `scripts/zhihu_download.py` downloads answers, articles, and pins, then converts them to Markdown.
- `scripts/zhihu_filter.py` filters by topic or keyword list.
- `scripts/zhihu_merge.py` merges content while preserving type priority.
- `references/prompt_templates.md` contains distillation prompt templates.

## Roadmap

- Add stronger retry and resume support.
- Add reusable templates for final distillation reports.
- Add more topic keyword presets.

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
