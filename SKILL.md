---
name: geoskill-telecom-coverage-optimization
description: 'Simplified Okumura-Hata propagation with terrain and buildings to map coverage and blind spots for telecom planning'
---

# 通信覆盖优化 | Telecom Coverage Optimization

Estimates base station coverage and blind spots using a simplified Okumura-Hata propagation model plus terrain/building clutter losses, serving telecom network planning and gap-filling (blind-spot filling).

Path loss is computed with the Hata empirical formula (including mobile-station height correction and urban/suburban/open-area empirical corrections); received signal level RSL = transmit power + antenna gain − path loss − clutter loss (additional dB from terrain relief and building height). For multiple base stations, the strongest signal is selected per pixel; RSL ≥ threshold is classified as covered, otherwise as a blind spot.

## Dependencies / 依赖

```bash
pip install 'numpy' 'rasterio' 'scipy'
```

## Usage / 使用方法

### Basic Usage

```bash
python geoskill-telecom-coverage-optimization.py --bbox 116.0 39.0 117.0 40.0 [other parameters]
```

### Example 1 (synthetic scene, offline)

```bash
python geoskill-telecom-coverage-optimization.py --bbox 116 39 117 40 --synthetic --output-dir ./out
```

### Example 2 (real terrain/building (DEM/building height))

```bash
python geoskill-telecom-coverage-optimization.py --input terrain.tif --output-dir ./out
```

### Example 3 (suburban environment + 900 MHz)

```bash
python geoskill-telecom-coverage-optimization.py --input terrain.tif --environment suburban --frequency 900 --output-dir ./out
```

### Example 4 (stricter coverage threshold)

```bash
python geoskill-telecom-coverage-optimization.py --input terrain.tif --threshold -95 --output-dir ./out
```

### Example 5 (raise transmit power to assess coverage improvement)

```bash
python geoskill-telecom-coverage-optimization.py --input terrain.tif --tx-power 46 --gain 18 --output-dir ./out
```

## Output / 输出

| File | Format | Description |
|---|---|---|
| `signal_strength.tif` | GeoTIFF | Best received signal level RSL (dBm) |
| `coverage_mask.tif` | GeoTIFF | Coverage mask (1 covered / 0 blind spot) |
| `towers.geojson` | GeoJSON | Base station locations and parameters |
| `coverage_report.json` | JSON | Coverage rate / blind-spot rate / gap-filling recommendations |
| `output-manifest.json` | JSON | Run manifest |

## Data Source / 数据源 / Source

Multi-band GeoTIFF with band order DEM / building height. Alternatively, use `--synthetic` to generate physically consistent simulated data (fully offline).

## Privacy / 隐私声明 / Privacy

- Runs offline by default; `--synthetic` mode requires no network at all.
- All processing is performed locally; no user data is uploaded.

## License / License

MIT

---

> 中文完整版：需要时再读 [references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)，不要默认全量加载。
