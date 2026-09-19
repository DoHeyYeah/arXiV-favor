# Usage

This repository collects daily arXiv papers for 3D Vision and Dexterous
Manipulation, driven by GitHub Actions.

## How it works

- `.github/workflows/cv-arxiv-daily.yml` runs `daily_arxiv.py` once a day
  (UTC 00:00), searches arXiv with the keywords defined in `config.yaml`,
  and commits the results to `README.md` and `docs/`.
- `.github/workflows/update_paper_links.yml` runs every Monday with
  `--update_paper_links` to refill missing code links in the stored data.

## Configuration

All search topics, filters and output paths live in `config.yaml`:

- `keywords`: each topic has a list of `filters`, which are combined with
  `OR` into a single arXiv query.
- `manual_papers`: manually collected papers as arXiv ids, grouped by topic.
  They are merged into the daily output together with the keyword results.
  A topic here that is not in `keywords` (e.g. `Favorites`) gets its own
  section.
- `max_results`: how many papers to fetch per topic per run.
- `publish_readme` / `publish_gitpage` / `publish_wechat`: which outputs to
  generate.

## Run locally

```bash
pip install -r requirements.txt
python daily_arxiv.py --config_path config.yaml
```
