# Telecom Coverage Optimization (geoskill-telecom-coverage-optimization)

> Simplified Okumura-Hata propagation with terrain and buildings to map coverage and blind spots for telecom planning

---

## 1. Overview

Estimates base-station coverage and blind spots using a simplified Okumura-Hata propagation model plus terrain/building clutter loss, supporting telecom network planning and blind-spot filling. Path loss is computed with the Hata empirical formula (including mobile-station height correction and urban/suburban/open-area empirical corrections); received signal level RSL = transmit power + antenna gain − path loss − clutter loss (additional dB from terrain relief and building height). For multiple base stations, the strongest signal is taken per pixel; RSL ≥ threshold is classified as covered, otherwise as a blind spot.

## 3. Quick Start

```bash
pip install -r requirements.txt
python geoskill-telecom-coverage-optimization.py --bbox 116 39 117 40 --synthetic --output-dir ./out
```

## 4. CLI Parameters

Run `python <skill>.py --help` for the full list. Common parameters:

| Parameter | Type | Description |
|---|---|---|
| `--bbox` | `float[4]` | WGS84 bounding box `min_lon min_lat max_lon max_lat` |
| `--input` | `path` | Local input file (GeoJSON/GeoTIFF/etc.) |
| `--output-dir` | `path` | Output directory (default `./output`) |
| `--synthetic` | `flag` | Use synthetic data instead of real input |
| `--quiet` | `flag` | Suppress non-essential stdout |

## 5. Input / Output

| File | Format | Description |
|---|---|---|
| `signal_strength.tif` | GeoTIFF | Best received signal level RSL (dBm) |
| `coverage_mask.tif` | GeoTIFF | Coverage mask (1 covered / 0 blind spot) |
| `towers.geojson` | GeoJSON | Base-station locations and parameters |
| `coverage_report.json` | JSON | Coverage rate / blind-spot rate / blind-spot filling suggestions |
| `output-manifest.json` | JSON | Run manifest |

## 6. Technical Principle

(see SKILL.md for details)

## 8. License

MIT License. See [`LICENSE`](./LICENSE) for full text.

---

> 中文完整版：[references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)
