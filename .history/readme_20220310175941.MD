# Thumbnail Generation

Training and sampling script for generating thumbnails for the [**[2021 Visual News](https://github.com/FuxiaoLiu/VisualNews-Repository)** dataset](https://github.com/FuxiaoLiu/VisualNews-Repository).

## Installation

Git Clone this repository recursively.

```bash
git clone --recursive
```



Use the package manager [pip](https://pip.pypa.io/en/stable/) to install the package.

```bash
pip install -r requirements.txt
```
move into improved-diffusion directory and run the following command:
```bash
cd improved-diffusion
pip install -e .
pip install mpi4py


```
Move back to the root directory and run the following command:
```bash
cd ..
unzip sample.zip -d sample
```


## Training
Set environment variables:
```bash
%env MODEL_FLAGS= --image_size 64 --num_channels 128 --num_res_blocks 3
%env DIFFUSION_FLAGS=--diffusion_steps 4000 --noise_schedule linear
%env TRAIN_FLAGS=--lr 1e-4 --batch_size 32
%env OPENAI_LOGDIR = ./ckpt_model

```
Run Training:
```bash
python improved-diffusion/scripts/image_train.py --data_dir ./sample/ $MODEL_FLAGS $DIFFUSION_FLAGS $TRAIN_FLAGS
```

## PreProcessing and PostProcessing
```bash
pip install pytorch-fid 
```
Check out the pre&post-process+FID.ipynb notebook

## Sampling
Sample from the trained model:
```bash
python scripts/image_sample.py  --model_path ./ema_0.9999_050000.pt --num_samples 128 $MODEL_FLAGS $DIFFUSION_FLAGS
```

Check out sample.ipynb for more details.


## License
[MIT](https://choosealicense.com/licenses/mit/)