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

- Updated to the latest [stac-extensions/template](https://github.com/stac-extensions/template).
- Collapsed field tables into a single table.
- Renamed relation types `emb:model` and `emb:decoder` to `emb:encoder_model` and `emb:decoder_model`. No relation types are required.
- Added `emb:grid` and `emb:quantization` relation types, replacing link objects inside the chip layout and quantization objects.
- Replaced template extension scaffolding with Embedding extension identity (`emb` prefix, embeddings schema identifier, and package metadata).
- Updated README to align with embedding requirements and link canonical STAC and STAC MLM specifications/schemas.
- Updated validator schema mapping to use the Embedding extension schema URL.

### Deprecated

### Removed

- `emb:source-data` relation type, in favor of `derived_from`.
- Template-specific field definitions and documentation (`template:*`).

### Fixed

- Example JSON formatting for validator lint compliance.

[Unreleased]: <https://github.com/stac-extensions/embeddings/compare/v0.0.1...HEAD>
