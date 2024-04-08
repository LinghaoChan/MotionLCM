# MotionLCM: Real-time Controllable Motion Generation via Latent Consistency Model


Author list 

links

## 🤩 Abstract

> xxx

## 📢 News

- **[2024/04/08]** upload paper and release code.

## 👨‍🏫 Quick Start

This section provides a quick start guide to set up the environment and run the demo. The following steps will guide you through the installation of the required dependencies, downloading the pretrained models, and preparing the datasets. 

<details>
  <summary><b> 1. Conda environment</b></summary>


```
conda create python=3.10 --name motionlcm
conda activate motionlcm
```

Install the packages in `requirements.txt` and install [PyTorch 1.13.1](https://pytorch.org/).

```
pip install -r requirements.txt
```

We test our code on Python 3.10.12 and PyTorch 1.13.1.

</details>

<details>
  <summary><b> 2. Dependencies</b></summary>

Run the script to download dependencies materials:

```
bash prepare/download_glove.sh
bash prepare/download_t2m_evaluators.sh
bash prepare/perpare_t5.sh
```

</details>

<details>
  <summary><b> 3. Pretrained models</b></summary>


Run the script to download the pretrained models:

```
bash prepare/download_pretrained_models.sh
```

The folders `experiments_t2m` and `experiments_control` store pretrained models for text-to-motion and motion control respectively.

</details>


<details>
  <summary><b> 4. (Optional) Download manually</b></summary>



Visit the [Google Driver](https://drive.google.com/drive/folders/1SIhb6srXWS0PNvZ2fs40QiE3Rk764u6z?usp=sharing) to download the previous dependencies and models.

</details>

<details>
  <summary><b>5. Prepare the datasets</b></summary>

Please refer to [HumanML3D](https://github.com/EricGuo5513/HumanML3D) for text-to-motion dataset setup. Copy the result dataset to our repository:
```
cp -r ../HumanML3D/HumanML3D ./datasets/humanml3d
```

</details>


<details>
  <summary><b>6. Folder Structure</b></summary>


After the whole setup pipeline, the folder structure will look like:

```
MotionLCM
├── configs
├── datasets
│   ├── humanml3d
│   │   ├── new_joint_vecs
│   │   ├── new_joints
│   │   ├── texts
│   │   ├── Mean.npy
│   │   ├── Std.npy
│   │   ├── ...
│   └── humanml_spatial_norm
│       ├── Mean_raw.npy
│       └── Std_raw.npy
├── deps
│   ├── glove
│   ├── sentence-t5-large
│   └── t2m
├── experiments_control
│   └── motionlcm_humanml
│       └── motionlcm_humanml.ckpt
├── experiments_t2m
│   ├── mld_humanml
│   │   └── mld_humanml.ckpt
│   └── motionlcm_humanml
│       └── motionlcm_humanml.ckpt
├── ...
```


</details>

## 🎬 Demo


MotionLCM provides two main functionalities: text-to-motion and motion control. The following commands demonstrate how to use the pretrained models to generate motions based on the provided prompts and lengths.

<details>
  <summary><b>Text-to-Motion (using provided prompts and lengths in `demo/example.txt`) </b></summary>

```
python demo.py --cfg configs/motionlcm_t2m.yaml --example demo/example.txt --plot
```
</details>

<details>
  <summary><b>Text-to-Motion (using prompts from HumanML3D test set)</b></summary>

```
python demo.py --cfg configs/motionlcm_t2m.yaml --plot
```
</details>

<details>
  <summary><b>Motion Control (using prompts and trajectory from HumanML3D test set)</b></summary>

```
python demo.py --cfg configs/motionlcm_control --plot
```

The outputs will be stored in `${cfg.TEST_FOLDER} / ${cfg.NAME} / demo_${timestamp}` (`experiments_t2m_test/motionlcm_humanml/demo_2024-04-06T23-05-07`).

</details>



## 🚀 Train your own models

We provide the training guidance for both text-to-motion and motion control tasks. The following steps will guide you through the training process.

<details>
  <summary><b>1. Important args in the config yaml</b></summary>


The parameters required for model training and testing are recorded in the corresponding YAML file (e.g., `configs/motionlcm_t2m.yaml`). Below are some of the important parameters in the file:

- `${FOLDER}`: The folder for the specific training task (i.e., `experiments_t2m` and `experiments_control`).
- `${TEST_FOLDER}`: The folder for the specific testing task (i.e., `experiments_t2m_test` and `experiments_control_test`).
- `${NAME}`: The name of the model (e.g., `motionlcm_humanml`). `${FOLDER}`, `${NAME}`, and the current timestamp constitute the training output folder (for example, `experiments_t2m/motionlcm_humanml/2024-04-06T23-05-07`). The same applies to `${TEST_FOLDER}` for testing.
- `${TRAIN.PRETRAINED}`: The path of the pretrained model.
- `${TEST.CHECKPOINTS}`: The path of the testing model.


</details>


<details>
  <summary><b>2. Train MotionLCM and ControlNet</b></summary>

#### 2.1. Ready to train MotionLCM model

Please first check the parameters in `configs/motionlcm_t2m.yaml`. Then, run the following command:

```
python -m train_motionlcm --cfg configs/motionlcm_t2m.yaml
```

#### 2.2. Ready to train motion ControlNet

Please update the parameters in `configs/motionlcm_control.yaml`. Then, run the following command:

```
python -m train_motion_control --cfg configs/motionlcm_control.yaml
```

</details>


<details>
  <summary><b>3. Evaluate the model</b></summary>


Text-to-Motion: 

```
python -m test --cfg configs/motionlcm_t2m.yaml
```

Motion Control:

```
python -m test --cfg configs/motionlcm_control.yaml
```

</details>


## 📊 Results

We provide the quantitative and qualitative results in the paper. 

## 🌹 Acknowledgement

We would like to thank the authors of the following repositories for their excellent work: 


## 📜 Citation

If you find this work useful, please consider citing our paper:

```bash
@inproceedings{motionlcm,
  title={MotionLCM: Real-time Controllable Motion Generation via Latent Consistency Model},
  author={xxx},
  booktitle={xxx},
  year={2024}
}
```