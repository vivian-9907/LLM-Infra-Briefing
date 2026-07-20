# Changelog

## v0.6 - Lightweight infra briefing baseline

- Renamed the project to LLM Infra Briefing.
- Generalized the skill into two channels: `quantization` and `ai-infra`.
- Added channel-specific profiles, full topic maps, research maps and output templates.
- Added shared sources, watchlist and radar rubric configuration.
- Switched regular radar runs to read lightweight profiles by default and expand full topics only when needed.

## Maintenance Notes

- Keep generated reports under `outputs/<channel>/radar/`; reports are ignored by git.
- Keep `.gitkeep` files so the expected output directories exist in fresh clones.
- Review `config/watchlist.yml` periodically so query expansion stays high-signal instead of becoming a broad news list.
