> The output data is available at (in an anonymous fashion) at https://figshare.com/s/23463d715d6001627332

- This data includes prompts, model responses, post-processes responses, and results.

## Getting Started
1. Prepare a virtual environment:
```bash
conda create -n dcot python=3.10
conda activate dcot
pip install -r requirements.txt
```

2. Download the training data
> Link to the input data https://figshare.com/s/ec0249df13f7b1fc69c3
- This zip files includes training, dev, test sets and our **DCoT dataset.**
- Create a folder called `data` and download the contents of this link in that folder
## Usage


### Training


```bash
$ python training_script.py \
    --train \
    --base_model_path YOUR_MODEL_PATH/models--llama-2-hf/7B \
    --lora_path YOUR_LORA_OUTPUT_PATH/ \
    --train_path data/dcot_collection/cot9_dataset.json \
    --epochs 3\
    --training_batch_size 4 \
    --ccot \
    --seed 0
```

### Evaluation

```bash
$ python evaluation.py \
    --base_model_path YOUR_MODEL_PATH/models--llama-2-hf/7B \
    --lora_path YOUR_LORA_OUTPUT_PATH/ \
    --min_cots 1 \
    --max_cots 4 \
```

### Remarks on Phi 1.5 and 2
vLLM is not compatible with Phi 1.5 and Phi 2 with lora. Therefore, to evaluate with lora you need to merge the lora weights on the base model first. See `merge_weights.py` to see how to do it. Then, you can run the evaluation as follows

```bash
$ python evaluation.py \
    --base_model_path YOUR_PATH_TO_PHI_MERGED_MODEL \
    --postprocess_responses \
    --min_cots 1 \
    --max_cots 4 \
```

## Disclaimer

> This repository contains experimental software and is published for the sole purpose of giving additional background details on the respective publication. 