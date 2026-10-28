# Best Practices

This document collects recommendations for describing embedding products with this extension.
It is non-normative.

- [Relationship to STAC MLM](#relationship-to-stac-mlm)
- [Embedding types](#embedding-types)
- [Common metadata](#common-metadata)
- [Related extensions](#related-extensions)
- [Uncertainty](#uncertainty)
- [Storage formats](#storage-formats)

## Relationship to STAC MLM

The [STAC MLM Extension](https://github.com/stac-extensions/mlm) describes the **model itself**: its architecture,
inputs, outputs, and available parameters. This extension describes the **embeddings produced** by running that model.
Link to the model with the `emb:encoder_model` relation type, ideally pointing to a STAC MLM Item.

## Embedding types

Geospatial embeddings fall into two categories (per [arXiv:2601.13134](https://arxiv.org/abs/2601.13134)):

| Type    | Description                                                | Typical Format |
| ------- | ---------------------------------------------------------- | -------------- |
| `pixel` | Dense, per-pixel embeddings preserving full spatial detail | COG, Zarr      |
| `chip`  | One embedding vector per spatial tile/chip                 | GeoParquet     |

The embedding type drives storage format, resolution, and cost trade-offs. A `pixel` product at 10m resolution for
Africa is \~38-77 TB; a `chip` product for the same area can be under 4 GB.

## Common metadata

Always provide [`data_type`](https://github.com/radiantearth/stac-spec/blob/master/commons/common-metadata.md#data-types)
for the stored embeddings (e.g. `float32`, `int8`), so that users can read them without inspecting the data.

Use [`gsd`](https://github.com/radiantearth/stac-spec/blob/master/commons/common-metadata.md#gsd) for the ground
sample distance or spatial extent per embedding, in meters.

For quantized embeddings, `data_type` is the stored (quantized) type. Use `emb:original_data_type` for the type
before quantization, and the [Raster Extension](https://github.com/stac-extensions/raster) `raster:scale` and
`raster:offset` fields for dequantization.

## Related extensions

Consider using these extensions alongside this one:

- [Processing Extension](https://github.com/stac-extensions/processing):
  - `processing:datetime` for when the embeddings were generated
  - `processing:version` for the source data processing baseline (e.g. Sentinel-2 processing baseline)
  - `processing:software` for the libraries and versions used to generate the embeddings
- [Scientific Extension](https://github.com/stac-extensions/scientific): `sci:doi`, `sci:citation`, and
  `sci:publications` for papers describing the model or embedding product
- [Projection Extension](https://github.com/stac-extensions/projection): CRS and geometry of pixel embeddings

## Uncertainty

Companion uncertainty data should be provided as a STAC Asset with the role `uncertainty`.

## Storage formats

- **Chip embeddings** are best stored in **GeoParquet**, with one geometry and one embedding array per row.
- **Pixel embeddings** are best stored in **COG** or **Zarr**, with embedding dimensions as bands or array variables.
- **Embed the CRS in every data file**, not only in STAC metadata or external documentation.
  Implicit CRS assumptions are a major source of integration bugs.
- **Use cloud-native formats** (COG, GeoParquet, GeoZarr) to allow efficient range-request access without full downloads.
