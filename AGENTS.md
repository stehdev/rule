# Agent Guidelines for Rule Configuration Repository

## Overview
This repository contains network proxy configuration files for various clients (mihomo, singbox, shadowrocket, zijian) and includes Python/Go code for AI-based smart routing. Repository is primarily in Chinese.

## Build/Test Commands
- **Python scripts**: `python config/mihomo/AI/train_flexible.py` (main ML training script)
- **Go compilation**: `go build config/mihomo/AI/transform.go` (feature transform utilities)
- **No automated tests found** - manual validation required for config files

## Code Style Guidelines

### Python (ML/AI modules)
- Use type hints: `def load_data(file_path: str) -> Optional[pd.DataFrame]`
- Chinese comments for user-facing messages, English for technical docs
- Standard imports: pandas, numpy, lightgbm, sklearn
- Constants in UPPERCASE: `DATA_FILE = 'smart_weight_data.csv'`
- Error handling with try/except and informative logging

### Go (LightGBM integration)
- Package naming: lowercase single words (`package lightgbm`)
- Struct fields: PascalCase with JSON tags (`FeatureIndices []int`)
- Error handling: return error as last value
- Constants: CamelCase (`StandardScalerTransform`)
- Comprehensive error validation and logging

### Configuration Files
- YAML: snake_case keys, proper indentation
- JSON: camelCase for compatibility
- File naming: descriptive with version/purpose (`config_tun_zijian.json`)

## File Conventions
- `/config/`: organized by client type (mihomo, singbox, etc.)
- Python scripts in `/AI/` subdirectories
- Configuration templates with clear naming patterns