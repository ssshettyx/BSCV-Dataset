<div align="center">

<h1>BitStream-Corrupted Video Recovery:</br >A Novel Benchmark Dataset and Method</h1>

<div>
    <a href='' target='_blank'>Tianyi Liu*<sup>1</sup></a>&emsp;
    <a href='' target='_blank'>Kejun Wu*<sup>1</sup></a>&emsp;
    <a href='https://wangyintu.github.io/' target='_blank'>Yi Wang<sup>2</sup></a>&emsp;
    <a href='' target='_blank'>Wenyang Liu<sup>1</sup></a>&emsp;
    <a href='' target='_blank'>Kim-Hui Yap<sup>1</sup></a>&emsp;
    <a href='' target='_blank'>Lap-Pui Chau<sup>2</sup></a>
</div>
<div>
    <sup>1</sup>Nanyang Technological University&emsp;
    <sup>2</sup>The Hong Kong Polytechnic University
</div>

<div>
    <strong>NeurIPS 2023</strong>
</div>

<p align="center">
    <a href='https://arxiv.org/abs/2309.13890'>
      <img src='https://img.shields.io/badge/Paper-arXiv-green?style=plastic&logo=arXiv&logoColor=green' alt='Paper arXiv'>
    </a>
</p>

<p align="center"> (This page is under continuous update and construction..) </p>

---

</div>


## Update
**2023.12.18:** Our code and model are publicly available in the [method](https://github.com/LIUTIGHE/BSCV-Dataset/edit/main/README.md#824) part.

**2023.09.22:** 🎉 We are delight to announce that our paper has been accepted by **NeurIPS 2023** Dataset and Benchamrk Track, ~~we will upload the preprint version soon~~ the preprint version is available at [arXiv](https://arxiv.org/abs/2309.13890)!

**2023.08.30:** We additionally presented some performance comparisons in video form, which highlights the advantage of our method in recovering long-term and large area corruptions.

**2023.08.29:** We shared our proposed video recovery method and evaluation results in the [method](https://github.com/LIUTIGHE/BSCV-Dataset/edit/main/README.md#824) part. The training and testing code will release soon.

**2023.08.24:** **1).** New YouTube-VOS&DAVIS branches is available with tougher parameter adjustments and corruption ratios. **2).** New subset with higher resolutions in 1080P and 4K is included. **3).** H.265 protocol is supported.

## Table of Contents

- [Dataset](#dataset)
    - [Property](#property)
    - [Download](#download)
    - [Extraction](#extraction)
    - [Extension](#extension)
- [Method](#method)
- [Experimental Setup](#experimental-setup)

## Dataset

![Tesear](assets/Fig/teaser.png)

For each video in YouTubeVOS&DAVIS subset, under various parameter setting, we provide differently corrupted videos (from left to right: ``(P, L, S) = (1/16, 0.4, 2048), (1/16, 0.4, 4096), (1/16, 0.2, 4096), (2/16, 0.4, 4096)``, and **additional** ``(1/16, 0.4, 8192), (1/16, 0.8, 4096), (4/16, 0.4, 4096)`` branches , respectively. The explanation of the parameter will be explained below/in paper.).

<div align="center">
<table>
  <tr>
    <td><img src="assets/GIF/bmx-bumps_142048.gif" alt="GIF 1" width="220"/></td>
    <td><img src="assets/GIF/bmx-bumps_144096.gif" alt="GIF 2" width="220"/></td>
    <td><img src="assets/GIF/bmx-bumps_124096.gif" alt="GIF 3" width="220"/></td>
    <td><img src="assets/GIF/bmx-bumps_244096.gif" alt="GIF 4" width="220"/></td>
  </tr>
</table>
<table>
  <tr>
    <td><img src="assets/GIF/camel_142048.gif" alt="GIF 1" width="220"/></td>
    <td><img src="assets/GIF/camel_144096.gif" alt="GIF 2" width="220"/></td>
    <td><img src="assets/GIF/camel_124096.gif" alt="GIF 3" width="220"/></td>
    <td><img src="assets/GIF/camel_244096.gif" alt="GIF 4" width="220"/></td>
  </tr>
</table>
<table>
  <tr>
    <td><img src="assets/GIF/mascot_142048.gif" alt="GIF 1" width="220"/></td>
    <td><img src="assets/GIF/mascot_144096.gif" alt="GIF 2" width="220"/></td>
    <td><img src="assets/GIF/mascot_124096.gif" alt="GIF 3" width="220"/></td>
    <td><img src="assets/GIF/mascot_244096.gif" alt="GIF 4" width="220"/></td>
  </tr>
</table>
<table>
  <tr>
    <td><img src="assets/GIF/tennis_142048.gif" alt="GIF 1" width="220"/></td>
    <td><img src="assets/GIF/tennis_144096.gif" alt="GIF 2" width="220"/></td>
    <td><img src="assets/GIF/tennis_124096.gif" alt="GIF 3" width="220"/></td>
    <td><img src="assets/GIF/tennis_244096.gif" alt="GIF 4" width="220"/></td>
  </tr>
</table>
---

</div>

### Features
- Flexible video resolution setting (480P, 720P, 1080P, 4K)
- Realistic video degradation caused by bitstream corruption.
- Unpredictable error pattern in various degree.
- With about 30K video clips and 3.5M frames, 50% frames have corruption.
- ...

### Download
For dataset downloading, please check this [link](https://entuedu-my.sharepoint.com/:f:/g/personal/liut0038_e_ntu_edu_sg/Egn7Xygv7UJBilL9z3nFo_4Bm5LdeoXCv-uiDo3qANsmTw?e=fMU9gZ) (Extension for higher resolution, more parameter combination, and uploading are in progress).

### Extraction
We have seperated the dataset into training and testing set and for each branch in YouTube-VOS & DAVIS.
YouTube-UGC 1080P subset and Videezy4K 4K subset is currently constructed for testing.
After downloading the ``.tar.gz`` files, please firstly restore the original ``.tar.gz`` files, unzipping the archives and formatting the folders by
```
$ bash format.sh
```

After the data preparation, ffmpeg encoded orignial (GT) video bitstream is provided in the ``_144096`` branch with folder name ``GT_h264`` and its decoded frame sequence with corruption is provided in the folder named ``GT_JPEGImages``.
We also provide the h264 bitstreams of each video and their decoded frame sequence as commonly used video dataset.
Additionally, the mask sequence which is used for corruption region indication is provided in the ``masks`` folder in each branch, the files are structured as following:
```
BSCV-Dataset
|-scripts                         # Codes for dataset construction
|-YouTube-VOS&DAVIS
| |-train_144096                    # Branch_144096
|  |-GT_h264
|    |-##########.h264            # H.264 video bitstream with original id in YouTube-VOS dataset
|    |-...                        # 3,471 bitstream files in total
|  |-GT_JPEGImages
|    |-##########                 # Corresponding video ID
|      |-00000.jpg                # Decoded frame sequence with different length
|      |-...
|    |-...                        # 3,471 frame sequence folder in total
|  |-BSC_h264                     # Corresponding corrupted bitstream
|    |-##########_2.h264          
|    |-...                        
|  |-BSC_JPEGImages               # Corresponding decoded corrupted frame sequence
|    |-##########
|      |-00000.jpg              
|      |-...
|    |-...
|  |-masks                        # Corresponding mask sequence
|    |-##########
|      |-00000.png
|      |-...
|    |-...         
|  |-Diff                         # The binary difference map for mask geneartion by morphological operations
|    |-##########
|      |-00000.png
|      |-...
|    |-...
| |-train_142048                    # The following branch has the same structure, without GT data only
|  |-BSC_h264
|  |-BSC_JPEGImages
|  |-masks       
|  |-Diff      
| |...
|-YouTube-UGC-1080P
| |-FHD
| |-FHD_124096
|  |-GT_h264       
|  |-GT_JPEGImages
|  |-BSC_h264
|  |-BSC_JPEGImages
|  |-masks       
|  |-Diff
| |...
|-Videezy4K-4K
| |-QHD
|  |-GT_h264       
|  |-GT_JPEGImages
|  |-BSC_h264
|  |-BSC_JPEGImages
|  |-masks       
|  |-Diff
```

### Extension
We adopt FFmpeg as our video codec, please refer to the official guide line for your ffmpeg installation.

We proposed a parameter model for generating bitstream corruption and therefore causing arbitrarily corrupted videos, even additional branches. 
![Param_Model](extend_fig.png)

You can use the provided program with your parameter combination to generate arbitrary branches based on the GOP size 16 as our setting, by the following commands, e.g.
```
python corrpt_Gen.py --prob 1 --pos 0.4 --size 4096 
```
Please use integer for ``prob`` and ``size``, and float for ``pos`` due to the limitation of our current experimental setting. 
If you want to adjust the GOP size, please refer to FFmpeg's instruction to recoding the frame sequence in folder ``GT_JPEGImages`` of branch ``_144096``.

PS: It seems the working principle is different between Linux and Windows version of FFmpeg since we have some practical lost-frame error in decoding on Linux but the same bitstream is fine on Windows. So we recommend using FFmpeg on windows to deal with the lost frame issue if you are generating new branches. 

## Method

We propose a recovery framework based on end to end video inpainting method while leveraging the partial contents in the corrupted region, and we achieved better recovery quality compared with existing SOTA video inpainting methods.
![Method](assets/Fig/overview.png)

## Experiments

### Dependencies and Installation
```bash
$ git clone https://github.com/LIUTIGHE/BSCV-Dataset.git
$ conda create -n BSCVR python=3.7
$ conda activate BSCVR
$ pip install torch==1.10.1+cu111 torchvision==0.11.2+cu111 -f https://download.pytorch.org/whl/cu111/torch_stable.html
$ pip install -r requirements.txt
```

### Prepare Pre-trained models
Download our pretrained models from this [link](https://entuedu-my.sharepoint.com/:f:/g/personal/liut0038_e_ntu_edu_sg/EvdxcFMZjsBDvWQxcXnj3AYBHDcVa5-jacK4szujTd6cqw?e=QfZgjX) to the ```/checkpoints``` folder.

### Quick Test
```bash
python test.py --width 854 --height 480 --type BSCVR_S --ckpt ./checkpoints/BSCVR_S.pth --video /path_to_frame_sequence --mask /path_to_mask_sequence --framestride 50
```
The results will be saved in the ```result``` foldedr, please indicate the width and height of the input video, and adjust ```--framestride``` to reduce the VRAM occupancy or improve inference efficiency.

## Results
![Tab](assets/Fig/quant_eval.png)
![Vis](assets/Fig/qual_eval.png)
More visualized performance comparisons of recovery results in video form are illustrated below

**Under 240P Resolution:** From left to right, top to down is Corrupted Video, Mask Input, STTN, FuseFormer, E2FGVI-HQ, BSCVR-S(Ours), BSCVR-P(Ours), and Ground Truth, in sequence.

<p align="center">
  <img src="assets/GIF/lady-running_input.gif" alt="Image 1" width="200" height="113"/>
  <img src="assets/GIF/lady-running_mask.gif" alt="Image 2" width="200" height="113"/>
  <img src="assets/GIF/lady-runningbsctrain_sttn.gif" alt="Image 3" width="200" height="113"/>
  <img src="assets/GIF/lady-runningbsctrain_fuseformer.gif" alt="Image 4" width="200" height="113"/>
  <img src="assets/GIF/lady-runningbsctrain_e2fgvi.gif" alt="Image 5" width="200" height="113"/>
  <img src="assets/GIF/lady-runningbsctrain_BSCVI_S.gif" alt="Image 6" width="200" height="113"/>
  <img src="assets/GIF/lady-runningbsctrain_BSCVI_P.gif" alt="Image 7" width="200" height="113"/>
  <img src="assets/GIF/lady-running_gt.gif" alt="Image 8" width="200" height="113"/>
</p>

<p align="center">
  <img src="assets/GIF/8ba5691030_input.gif" alt="Image 1" width="200" height="113"/>
  <img src="assets/GIF/8ba5691030_mask.gif" alt="Image 2" width="200" height="113"/>
  <img src="assets/GIF/8ba5691030bsctrain_sttn.gif" alt="Image 3" width="200" height="113"/>
  <img src="assets/GIF/8ba5691030bsctrain_fuseformer.gif" alt="Image 4" width="200" height="113"/>
  <img src="assets/GIF/8ba5691030bsctrain_e2fgvi.gif" alt="Image 5" width="200" height="113"/>
  <img src="assets/GIF/8ba5691030bsctrain_BSCVI_S.gif" alt="Image 6" width="200" height="113"/>
  <img src="assets/GIF/8ba5691030bsctrain_BSCVI_P.gif" alt="Image 7" width="200" height="113"/>
  <img src="assets/GIF/8ba5691030_gt.gif" alt="Image 8" width="200" height="113"/>
</p>

<p align="center">
  <img src="assets/GIF/trucks-race_input.gif" alt="Image 1" width="200" height="113"/>
  <img src="assets/GIF/trucks-race_mask.gif" alt="Image 2" width="200" height="113"/>
  <img src="assets/GIF/trucks-racebsctrain_sttn.gif" alt="Image 3" width="200" height="113"/>
  <img src="assets/GIF/trucks-racebsctrain_fuseformer.gif" alt="Image 4" width="200" height="113"/>
  <img src="assets/GIF/trucks-racebsctrain_e2fgvi.gif" alt="Image 5" width="200" height="113"/>
  <img src="assets/GIF/trucks-racebsctrain_BSCVI_S.gif" alt="Image 6" width="200" height="113"/>
  <img src="assets/GIF/trucks-racebsctrain_BSCVI_P.gif" alt="Image 7" width="200" height="113"/>
  <img src="assets/GIF/trucks-race_gt.gif" alt="Image 8" width="200" height="113"/>
</p>

**Under Original 480/720P Resolution:** From left to right, top to down is Corrupted Video, Mask Input, Ground Truth, Pretrained E2FGVI-HQ, BSCV-trained E2FGVI-HQ, BSCVR-S(Ours), in sequence.

<p align="center">
  <img src="assets/GIF/heli-landing_input.gif" alt="Image 1" width="272" height="153"/>
  <img src="assets/GIF/heli-landing_mask.gif" alt="Image 2" width="272" height="153"/>
  <img src="assets/GIF/heli-landing_gt.gif" alt="Image 3" width="272" height="153"/>
  <img src="assets/GIF/heli-landingpretrain_e2fgvi.gif" alt="Image 4" width="272" height="153"/>
  <img src="assets/GIF/heli-landingbsctrain_e2fgvi.gif" alt="Image 5" width="272" height="153"/>
  <img src="assets/GIF/heli-landingbsctrain_BSCVI_S.gif" alt="Image 6" width="272" height="153"/>
</p>

<p align="center">
  <img src="assets/GIF/horse-jump_input.gif" alt="Image 1" width="272" height="153"/>
  <img src="assets/GIF/horse-jump_mask.gif" alt="Image 2" width="272" height="153"/>
  <img src="assets/GIF/horse-jump_gt.gif" alt="Image 3" width="272" height="153"/>
  <img src="assets/GIF/horse-jumppretrain_e2fgvi.gif" alt="Image 4" width="272" height="153"/>
  <img src="assets/GIF/horse-jumpbsctrain_e2fgvi.gif" alt="Image 5" width="272" height="153"/>
  <img src="assets/GIF/horse-jumpbsctrain_BSCVI_S.gif" alt="Image 6" width="272" height="153"/>
</p>

<p align="center">
  <img src="assets/GIF/jug-selfie_input.gif" alt="Image 1" width="272" height="153"/>
  <img src="assets/GIF/jug-selfie_mask.gif" alt="Image 2" width="272" height="153"/>
  <img src="assets/GIF/jug-selfie_gt.gif" alt="Image 3" width="272" height="153"/>
  <img src="assets/GIF/jug-selfiepretrain_e2fgvi.gif" alt="Image 4" width="272" height="153"/>
  <img src="assets/GIF/jug-selfiebsctrain_e2fgvi.gif" alt="Image 5" width="272" height="153"/>
  <img src="assets/GIF/jug-selfiebsctrain_BSCVI_S.gif" alt="Image 6" width="272" height="153"/>
</p>

---

For additional comparison with non-end-to-end methods, our preliminary evaluation result is
| Method | PSNR $\uparrow$ | SSIM $\uparrow$ | LPIPS $\downarrow$ | VFID $\downarrow$ | Runtime |
| ------ | ------ | ------ | ------ | ------ | ------ |
| FGT[2] | **31.5407** | 0.8967 | 0.0486 | 0.3368 | ~1.97 |
| ECFVI[1] | 20.8676 | 0.7692 | 0.0705 | 0.3019 | ~2.24 |
| **BSCVR-S (Ours)** | 28.8288 | ***0.9138*** | ***0.0399*** | **0.1704** | **0.172** |
| **BSCVR-P (Ours)** | ***29.0186*** | **0.9166** | **0.0391** | ***0.1730*** | ***0.178*** |

Performance comparisons of recovery results in video form are illustrated below, from left to right, top to down is Corrupted Video, Mask Input, Ground Truth, FGT, ECFVI, and Our method in sequence.

<p align="center">
  <img src="assets/GIF/mascot_input.gif" alt="Image 1" width="272" height="153"/>
  <img src="assets/GIF/mascot_mask.gif" alt="Image 2" width="272" height="153"/>
  <img src="assets/GIF/mascot_gt.gif" alt="Image 6" width="272" height="153"/>
  <img src="assets/GIF/mascotpretrain_FGT.gif" alt="Image 3" width="272" height="153"/>
  <img src="assets/GIF/mascotpretrain_ECFVI.gif" alt="Image 4" width="272" height="153"/>
  <img src="assets/GIF/mascotbsctrain_BSCVI_S.gif" alt="Image 5" width="272" height="153"/>
</p>

<p align="center">
  <img src="assets/GIF/walking_input.gif" alt="Image 1" width="272" height="153"/>
  <img src="assets/GIF/walking_mask.gif" alt="Image 2" width="272" height="153"/>
  <img src="assets/GIF/walking_gt.gif" alt="Image 6" width="272" height="153"/>
  <img src="assets/GIF/walkingpretrain_FGT.gif" alt="Image 3" width="272" height="153"/>
  <img src="assets/GIF/walkingpretrain_ECFVI.gif" alt="Image 4" width="272" height="153"/>
  <img src="assets/GIF/walkingbsctrain_BSCVI_S.gif" alt="Image 5" width="272" height="153"/>
</p>

<p align="center">
  <img src="assets/GIF/tennis_input.gif" alt="Image 1" width="272" height="153"/>
  <img src="assets/GIF/tennis_mask.gif" alt="Image 2" width="272" height="153"/>
  <img src="assets/GIF/tennis_gt.gif" alt="Image 6" width="272" height="153"/>
  <img src="assets/GIF/tennispretrain_FGT.gif" alt="Image 3" width="272" height="153"/>
  <img src="assets/GIF/tennispretrain_ECFVI.gif" alt="Image 4" width="272" height="153"/>
  <img src="assets/GIF/tennisbsctrain_BSCVI_S.gif" alt="Image 5" width="272" height="153"/>
</p>

These video form presentations well highlight the advantages of our model in recovering long-term video sequences and large-area error patterns caused by bitstream corruptions.

<!--
<p align="center">
  <img src="assets/GIF/mascot_input.gif" alt="Image 1" width="160" height="88"/>
  <img src="assets/GIF/mascot_mask.gif" alt="Image 2" width="160" height="88"/>
  <img src="assets/GIF/mascotpretrain_FGT.gif" alt="Image 3" width="160" height="88"/>
  <img src="assets/GIF/mascotpretrain_ECFVI.gif" alt="Image 4" width="160" height="88"/>
  <img src="assets/GIF/mascotbsctrain_BSCVI_S.gif" alt="Image 5" width="160" height="88"/>
  <img src="assets/GIF/mascot_gt.gif" alt="Image 6" width="160" height="88"/>
</p>

<p align="center">
  <img src="assets/GIF/walking_input.gif" alt="Image 1" width="160" height="88"/>
  <img src="assets/GIF/walking_mask.gif" alt="Image 2" width="160" height="88"/>
  <img src="assets/GIF/walkingpretrain_FGT.gif" alt="Image 3" width="160" height="88"/>
  <img src="assets/GIF/walkingpretrain_ECFVI.gif" alt="Image 4" width="160" height="88"/>
  <img src="assets/GIF/walkingbsctrain_BSCVI_S.gif" alt="Image 5" width="160" height="88"/>
  <img src="assets/GIF/walking_gt.gif" alt="Image 6" width="160" height="88"/>
</p>

<p align="center">
  <img src="assets/GIF/tennis_input.gif" alt="Image 1" width="160" height="88"/>
  <img src="assets/GIF/tennis_mask.gif" alt="Image 2" width="160" height="88"/>
  <img src="assets/GIF/tennispretrain_FGT.gif" alt="Image 3" width="160" height="88"/>
  <img src="assets/GIF/tennispretrain_ECFVI.gif" alt="Image 4" width="160" height="88"/>
  <img src="assets/GIF/tennisbsctrain_BSCVI_S.gif" alt="Image 5" width="160" height="88"/>
  <img src="assets/GIF/tennis_gt.gif" alt="Image 6" width="160" height="88"/>
</p>
-->


## Citation
If you find our paper and/or code helpful, please consider citing:
```
@article{liu2023bitstream,
  title={Bitstream-Corrupted Video Recovery: A Novel Benchmark Dataset and Method},
  author={Liu, Tianyi and Wu, Kejun and Wang, Yi and Liu, Wenyang and Yap, Kim-Hui and Chau, Lap-Pui},
  journal={arXiv preprint arXiv:2309.13890},
  year={2023}
}
```


