# Multimodal screenshot assistant

Screenshot and text query in, grounded answers out—coding help

## Setup

### Install dependenices

Install [uv](https://github.com/astral-sh/uv), then:

```bash
cd multimodal-screen-assistant   # repository root
uv venv
source .venv/bin/activate
uv pip install -r requirements.txt
```
### Download the weights 
cd model
git clone https://huggingface.co/jingyaogong/siglip2-base-p16-ve
cd ../
git clone git@hf.co:jingyaogong/minimind-3v-pytorch
git clone git@hf.co:jingyaogong/minimind-3v
cd ./out
ln -s ../minimind-3v-pytorch/*.pth . 

### Download the dataset 

cd ../dataset
git clone git@hf.co:datasets/jingyaogong/minimind-v_dataset
ln -s ./minimind-v_dataset/*.parquet . 
cd ../

## Quick Start  

### load_from='model': 加载原生PyTorch权重, load_from='其他路径': 加载transformers格式
python eval_vlm.py --load_from model --weight sft_vlm

### 或使用transformers格式模型
python eval_vlm.py --load_from minimind-3v

## Training

### Pretrain

python train_pretrain_vlm.py --epochs 4 --from_weight llm

### SFT

python train_sft_vlm.py --epochs 2 --from_weight pretrain_vlm

## Inference 

### Test SFT
python eval_vlm.py --weight sft_vlm

### Test Pretrain
python eval_vlm.py --weight pretrain_vlm
