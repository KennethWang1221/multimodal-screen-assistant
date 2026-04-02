# Multimodal Screenshot Assistant

Screenshot + text query in, grounded answer out.

## Setup

### 1) Install dependencies

Install [uv](https://github.com/astral-sh/uv), then run:

```bash
cd multimodal-screen-assistant
uv venv
source .venv/bin/activate
uv pip install -r requirements.txt
```

### 2) Download model weights

```bash
cd model
git clone https://huggingface.co/jingyaogong/siglip2-base-p16-ve
cd ..
git clone git@hf.co:jingyaogong/minimind-3v-pytorch
git clone git@hf.co:jingyaogong/minimind-3v
cd out
ln -s ../minimind-3v-pytorch/*.pth .
cd ..
```

### 3) Download dataset

```bash
cd dataset
git clone git@hf.co:datasets/jingyaogong/minimind-v_dataset
ln -s ./minimind-v_dataset/*.parquet .
cd ..
```

## Quick Start

Use native PyTorch weights:

```bash
python eval_vlm.py --load_from model --weight sft_vlm
```

Use Transformers-format weights:

```bash
python eval_vlm.py --load_from minimind-3v
```

## Training

### Pretrain

```bash
python trainer/train_pretrain_vlm.py --epochs 4 --from_weight llm
```

### SFT

```bash
python trainer/train_sft_vlm.py --epochs 2 --from_weight pretrain_vlm
```

## Inference

Test SFT checkpoint:

```bash
python eval_vlm.py --weight sft_vlm
```

Test pretrain checkpoint:

```bash
python eval_vlm.py --weight pretrain_vlm
```
