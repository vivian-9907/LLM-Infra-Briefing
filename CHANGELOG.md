# Changelog

## Unreleased

- Added `config/experts.yml` for author, maintainer, lab and research-group signal weighting.
- Added `config/venues.yml` for conference, workshop and benchmark context.
- Added `config/tracked-repos.yml` so concrete GitHub repositories are maintained once with channel tags and source modes.
- Added training and kernel repositories such as Megatron-LM, DeepSpeed, TransformerEngine and CUTLASS to tracked GitHub release/activity coverage.
- Updated radar workflow and templates to report whether tracked repos, experts or venues were used.

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
