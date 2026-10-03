# Deploy Guide — PAX_TRANSFORMER
**Stack:** Python 3.11, PyTorch 2.10+, Flash Attention 2, CUDA, AIOSS_FORMAT | Air-gap capable

## Prerequisites
Anticloud core stack installed. PAX 27B weights (pax-27b-q4.gguf). AIOSS_FORMAT.

## Install
```bash
pip install anticloud-pax-transformer
```

## AIOSS Integration
```bash
aioss init --module PAX_TRANSFORMER --output ./pax_transformer.aioss
```

## Air-Gap
```bash
pip download -r requirements.txt -d ./wheels/
pip install --no-index --find-links ./wheels/ -r requirements.txt
```

## PAX Harness Wiring
```python
from anticloud_pax import PAXHarness
harness = PAXHarness(model_path="./pax-27b-q4.gguf", module="PAX_TRANSFORMER",
                     aioss_chain="./pax_transformer.aioss",
                     classification="L5_NARROW_L2_GENERAL")
```

## Verification
```bash
aioss verify --chain ./pax_transformer.aioss --verbose
python -m pax_transformer.tests.smoke
```
