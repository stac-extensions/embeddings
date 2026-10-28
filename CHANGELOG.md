# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- Embedding extension schema definitions for collection, item properties, asset fields, and extension-specific objects
  (`patch_layout`, `quantization`, `uncertainty`).
- Embedding-focused Item and Collection examples covering required `emb:model` and `emb:source-data` relations.

### Changed

- Embeddings assets are identified by the `embeddings` role instead of the `embeddings` asset key.
- Replaced `emb:chip_layout` with `emb:chip_size`, `emb:stride`, and `emb:grid_id`. `emb:grid_id` uses Grid Extension designations.
- Replaced `emb:quantization` with `emb:quantization_method` and `emb:original_data_type`.
- Renamed `emb:temporal_resolution` to `emb:temporal_period`, using ISO 8601 durations.
- Changed `emb:dimensions` from an integer to an array of integers (e.g. `[768]`).
- Updated to the latest [stac-extensions/template](https://github.com/stac-extensions/template).
- Replaced `requirements.md` with `best-practices.md`, removing outdated content.
- Collapsed field tables into a single table.
- Renamed relation types `emb:model` and `emb:decoder` to `emb:encoder_model` and `emb:decoder_model`. No relation types are required.
- Added `emb:grid` and `emb:quantization` relation types, replacing link objects inside the chip layout and quantization objects.
- Replaced template extension scaffolding with Embedding extension identity (`emb` prefix, embeddings schema identifier, and package metadata).
- Updated README to align with embedding requirements and link canonical STAC and STAC MLM specifications/schemas.
- Updated validator schema mapping to use the Embedding extension schema URL.

### Deprecated

### Removed

- `data_type` and `gsd` from the fields table; `data_type` is no longer required.
- `sci:publications`, `processing:datetime`, and `processing:version` from the fields table (see best practices).
- `emb:fit_for_use`, `emb:runtime_parameters`, `emb:preprocessing`, `emb:postprocessing`, `emb:energy`, and `emb:uncertainty`.
- `emb:source-data` relation type, in favor of `derived_from`.
- Template-specific field definitions and documentation (`template:*`).

### Fixed

- Example JSON formatting for validator lint compliance.

[Unreleased]: <https://github.com/stac-extensions/embeddings/compare/v0.0.1...HEAD>
