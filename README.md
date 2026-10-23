# CFB Wainwright fire: full Copernicus satellite data

Raw, unmodified Copernicus Sentinel exports covering the Oct. 17, 2026 fire at CFB Wainwright, Alberta, kept in full so anyone can check the analysis in the [CFB Wainwright fire archive](https://github.com/primerogueinc/cfb-wainwright-fire-archive).

Every file is exactly as exported from [Copernicus Browser](https://browser.dataspace.copernicus.eu/). Each folder has a `manifest.json` with the SHA-256 of every file, the frame and pixel size, whether the export covers three reference points (the fire's origin, the Range 2 point and the road head), a haze check, and small previews.

## Sentinel-2

| Date | Level | Format | Files | Usable | Why | Folder |
|---|---|---|---|---|---|---|
| 2026-10-04 | L1C | TIFF | 23 | Yes | About 10 m pixels, clear | [`sentinel-2/2026-10-04/L1C_tiff/`](sentinel-2/2026-10-04/L1C_tiff/) |
| 2026-10-16 | L1C | JPG | 23 | Preview only | JPG, not georeferenced | [`sentinel-2/2026-10-16/L1C_jpg/`](sentinel-2/2026-10-16/L1C_jpg/) |
| 2026-10-16 | L2A | TIFF | 23 | No | Haze or thin cloud over the fire area | [`sentinel-2/2026-10-16/L2A_tiff/`](sentinel-2/2026-10-16/L2A_tiff/) |
| 2026-10-19 | L2A | TIFF | 23 | Yes | About 10 m pixels, clear | [`sentinel-2/2026-10-19/L2A_tiff/`](sentinel-2/2026-10-19/L2A_tiff/) |
| 2026-10-21 | L1C | TIFF | 17 | No | Fire area outside the swath | [`sentinel-2/2026-10-21/L1C_tiff/`](sentinel-2/2026-10-21/L1C_tiff/) |
| 2026-10-21 | L2A | TIFF | 17 | No | Fire area outside the swath | [`sentinel-2/2026-10-21/L2A_tiff/`](sentinel-2/2026-10-21/L2A_tiff/) |

**Usable** means the export covers all three reference points, at least 95% of the fire area (52.74-52.80°N, 110.85-110.96°W) has data, and the blue band shows no haze. Unusable exports are kept because a documented gap is part of the record.

**Levels.** L2A is surface reflectance (atmospherically corrected); L1C is top-of-atmosphere reflectance. Do not mix them in before-and-after comparisons.

**Coverage pattern.** Full coverage of the fire comes from one orbit track, imaged about 18:39 UTC every five days, alternating Sentinel-2B and 2C: Oct. 4, 9, 14, 19, 24, 29. Other dates (such as Oct. 21) are neighbouring tracks whose swath edge falls east of the fire.

## First-analysis exports

[`first-analysis-exports/`](first-analysis-exports/) holds the exports used in the first analysis (Oct. 20-21), each folder with its own ABOUT.md: Oct. 4 (pre-fire baseline), Oct. 16, checks showing no acquisition on Oct. 17 and 18, the Oct. 19 L1C, and Sentinel-3 OLCI.

## Adding an export

```
python3 scripts/ingest.py path/to/Browser_images.zip
```

The script sorts files by date and level, checks coverage and haze, writes the manifest and previews, and copies the raw files in unchanged. Exports should be TIFF (32-bit float), Raw bands B01-B12 and B8A plus the scene classification map, over about 52.69-52.84°N, 110.66-111.02°W, at 10 m.

## Licence

Scripts and documentation: MIT (see LICENSE). Satellite data: Copernicus Sentinel data are free and open under the [Copernicus data policy](https://sentinels.copernicus.eu/documents/247904/690755/Sentinel_Data_Legal_Notice); credit "Contains modified Copernicus Sentinel data [2026]" when reusing.

Maintained by Prime Rogue Inc.
