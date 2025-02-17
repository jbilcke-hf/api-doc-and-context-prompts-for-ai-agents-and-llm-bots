<summary>Training command</summary>

TODO: LTX does not do too well with the disney dataset. We will update this to use a better example soon.

```bash
#!/bin/bash
export WANDB_MODE="offline"
export NCCL_P2P_DISABLE=1
export TORCH_NCCL_ENABLE_MONITORING=0
export FINETRAINERS_LOG_LEVEL=DEBUG

GPU_IDS="0,1"

DATA_ROOT="/path/to/video-dataset-disney"
CAPTION_COLUMN="prompt.txt"
VIDEO_COLUMN="videos.txt"
OUTPUT_DIR="/path/to/output/directory/ltx-video/ltxv_disney"

ID_TOKEN="BW_STYLE"

# Model arguments
model_cmd="--model_name ltx_video \
  --pretrained_model_name_or_path Lightricks/LTX-Video"

# Dataset arguments
dataset_cmd="--data_root $DATA_ROOT \
  --video_column $VIDEO_COLUMN \
  --caption_column $CAPTION_COLUMN \
  --id_token $ID_TOKEN \
  --video_resolution_buckets 49x512x768 \
  --caption_dropout_p 0.05"

# Dataloader arguments
dataloader_cmd="--dataloader_num_workers 0"

# Diffusion arguments
diffusion_cmd="--flow_weighting_scheme logit_normal"

# Training arguments
training_cmd="--training_type lora \
  --seed 42 \
  --batch_size 1 \
  --train_steps 3000 \
  --rank 128 \
  --lora_alpha 128 \
  --target_modules to_q to_k to_v to_out.0 \
  --gradient_accumulation_steps 4 \
  --gradient_checkpointing \
  --checkpointing_steps 500 \
  --checkpointing_limit 2 \
  --enable_slicing \
  --enable_tiling"

# Optimizer arguments
optimizer_cmd="--optimizer adamw \
  --lr 3e-5 \
  --lr_scheduler constant_with_warmup \
  --lr_warmup_steps 100 \
  --lr_num_cycles 1 \
  --beta1 0.9 \
  --beta2 0.95 \
  --weight_decay 1e-4 \
  --epsilon 1e-8 \
  --max_grad_norm 1.0"

# Miscellaneous arguments
miscellaneous_cmd="--tracker_name finetrainers-ltxv \
  --output_dir $OUTPUT_DIR \
  --nccl_timeout 1800 \
  --report_to wandb"

cmd="accelerate launch --config_file accelerate_configs/uncompiled_2.yaml --gpu_ids $GPU_IDS train.py \
  $model_cmd \
  $dataset_cmd \
  $dataloader_cmd \
  $diffusion_cmd \
  $training_cmd \
  $optimizer_cmd \
  $miscellaneous_cmd"

echo "Running command: $cmd"
eval $cmd
echo -ne "-------------------- Finished executing script --------------------\n\n"
```

</details>

Here we are using two GPUs. But one can do single-GPU training by setting `GPU_IDS=0`. By default, we are using some simple optimizations to reduce memory consumption (such as gradient checkpointing). Please refer to [docs/training/optimizations](./docs/training/optimization.md) to learn about the memory optimizations currently supported.
