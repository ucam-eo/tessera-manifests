# GeoTessera Registry

This repository contains the data registry files for the [GeoTessera Python
library](https://github.com/ucam-eo/geotessera), which provides access to
geospatial embeddings from the [Tessera geospatial foundation model](https://github.com/ucam-eo/tessera).

## Contents

The registry is organized into two main categories:

### Embeddings Registry (`registry/embeddings/`)

Contains checksum files for geospatial embedding tiles organized by year (2017-2024) and geographic regions. Each file lists the available embedding tiles for a specific year and geographic region with their SHA256 checksums.

**File format:** `embeddings_{year}_lon{longitude}_lat{latitude}.txt`

Each registry file contains entries in the format:
```
{year}/grid_{lon:.2f}_{lat:.2f}/grid_{lon:.2f}_{lat:.2f}.npy {sha256_hash}
{year}/grid_{lon:.2f}_{lat:.2f}/grid_{lon:.2f}_{lat:.2f}_scales.npy {sha256_hash}
```

The embeddings are organized in a 0.1-degree grid system where:
- `.npy` files contain quantized embeddings (128 channels)
- `_scales.npy` files contain dequantization scales
- Final embeddings are computed as: `embedding * scales`

### Landmasks Registry (`registry/landmasks/`)

Contains checksum files for landmask TIFF files that define land/water boundaries for each grid tile, organized by geographic regions.

**File format:** `landmasks_lon{longitude}_lat{latitude}.txt`

Each registry file contains entries in the format:
```
grid_{lon:.2f}_{lat:.2f}.tiff {sha256_hash}
```

## Usage

These registry files are automatically used by the GeoTessera Python library to:
1. Discover available embedding tiles for a region of interest
2. Verify data integrity through checksum validation
3. Cache downloaded data locally using Pooch

## Data Access

The actual embedding and landmask data files are hosted at `https://dl-2.tessera.wiki/` and automatically downloaded by the GeoTessera library as needed.

## GeoTessera Library

To use these embeddings in your projects, install the GeoTessera Python library:

```bash
pip install geotessera
```

See the [main repository](https://github.com/ucam-eo/geotessera) for documentation and examples.
