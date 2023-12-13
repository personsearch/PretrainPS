# PretrainPS


## Introduction

This is the implementation for [Divide and Conquer: Hybrid Pre-training for Person Search](https://arxiv.org/submit/5292080/view).

[comment]: <> (![demo image]&#40;demo/arch.jpg&#41;)


## License

This project is released under the [Apache 2.0 license](LICENSE).


## Installation

This project is developed upon [MMdetection](https://github.com/open-mmlab/mmdetection), please refer to [install.md](docs/install.md) to install MMdetection.

We utilized mmcv=1.3.9, pytorch=1.7.0


## Dataset

Download [CUHK-SYSU](https://github.com/ShuangLI59/person_search) and [PRW](https://github.com/liangzheng06/PRW-baseline).

[comment]: <> (We provide coco-style annotation in [demo/anno]&#40;demo/anno&#41;.)

[comment]: <> (For CUHK-SYSU, change the path of your dataset and the annotaion file in the [config file]&#40;configs/_base_/datasets/cuhk_detection_1000.py&#41; L3, L38, L43, L48)

[comment]: <> (For PRW, change the paths in these config files: [config1]&#40;configs/fcos/prw_base_focal_labelnorm_sub_ldcn_fg15_wd1-3.py&#41; [config2]&#40;configs/fcos/prw_dcn_base_focal_labelnorm_sub_ldcn_fg15_wd7-4.py&#41;)



## Experiments
  1. Pre-training

   ```bash
   sh run_train.sh
   ```

  2. format our pretrained model
   ```bash
   sh tools/format_epoch_weights_for_pretraining.sh
   ```

  3. Fine-tuning
     
   ==>on PRW (eg. ROI-AlignPS method):
   Change the paths in L127 and L128 in [test_results_prw.py](tools/test_results_prw.py)
     
   ```bash
   sh run_train_alignps.sh
   ```


   ==>on CUHK-SYSU (e.g. ROI-AlignPS method):
   Change the paths in L59 and L72 in [test_results.py](tools/test_results.py)

    
   ```bash
   sh run_train_alignps.sh
   ```

  4. Test
     
   ==>on PRW (e.g. ROI-AlignPS method):
    
   ```bash
   sh run_test_roi_prw.sh
   ```

   ==>on CUHK-SYSU (e.g. ROI-AlignPS method):

   ```bash
   sh run_test_roi.sh
   ```


## Performance

|Dataset|Model|mAP|Rank1| Config | Link |
|-----|-----|------|-----|------|-----|
|CUHK-SYSU|ROI-AlignPS| 95.3%|95.8%|[cfg](https://github.com/daodaofr/AlignPS/blob/master/configs/fcos/fcos_center-normbbox-centeronreg-giou_r50_caffe_fpn_gn-head_dcn_4x4_1x_cuhk_reid_1500_stage1_fpncat_dcn_epoch24_multiscale_focal_x4_bg-2_lconv3dcn_sub_triqueue_dcn0.py)| [model](https://drive.google.com/file/d/1hZZAYuYNaKR1CefWx-92x88q8W7Pls9f/view?usp=share_link)| 
|CUHK-SYSU|ROI-AlignPS+ours|95.4%|96.0%|[cfg](https://github.com/daodaofr/AlignPS/blob/master/configs/fcos/fcos_center-normbbox-centeronreg-giou_r50_caffe_fpn_gn-head_dcn_4x4_1x_cuhk_reid_1500_stage1_fpncat_dcn_epoch24_multiscale_focal_x4_bg-2_lconv3dcn_sub_triqueue.py)| [model](https://drive.google.com/file/d/1PBgVGNGvyWE6NQwMM6GlSFy1Cru5Ep8W/view?usp=share_link)| 
|PRW|ROI-AlignPS| 51.8%|85.5%|[cfg](https://github.com/daodaofr/AlignPS/blob/master/configs/fcos/prw_base_focal_labelnorm_sub_ldcn_fg15_wd1-3.py)| [model](https://drive.google.com/file/d/14K3EUknoBnOR9hII4GywdtkIrhL32Yjh/view?usp=share_link)| 
|PRW|ROI-AlignPS+ours|54.5%|87.6%|[cfg](https://github.com/daodaofr/AlignPS/blob/master/configs/fcos/prw_dcn_base_focal_labelnorm_sub_ldcn_fg15_wd7-4.py)| [model](https://drive.google.com/file/d/1SBXzjZp_LHTQr-Hwo3-bPMVyT8wGrgLO/view?usp=share_link)| 
|PoseTrack21|ROI-AlignPS| 59.1%|82.1%|[cfg](https://github.com/daodaofr/AlignPS/blob/master/configs/fcos/prw_base_focal_labelnorm_sub_ldcn_fg15_wd1-3.py)| [model](https://drive.google.com/file/d/1PBgVGNGvyWE6NQwMM6GlSFy1Cru5Ep8W/view?usp=share_link)| 
|PoseTrack21|ROI-AlignPS+ours|63.6%|87.1%|[cfg](https://github.com/daodaofr/AlignPS/blob/master/configs/fcos/prw_dcn_base_focal_labelnorm_sub_ldcn_fg15_wd7-4.py)| [model](https://drive.google.com/file/d/1hZZAYuYNaKR1CefWx-92x88q8W7Pls9f/view?usp=share_link)| 



## Pretrained Model
you can run the following commend to install: ([ref](https://pypi.org/project/psvis/1.6.0/))
   ```bash
   pip install psvis
   ```
and load the model as:
   ```bash
   from psvis.models.backbones import resnet
   resnet50 = resnet.__dict__['resnet50'](pretrained=True)
   ```
or you can download pretrained models from:
[resnet50](https://drive.google.com/file/d/1yf26ngXQP0Mwrlp6z2lPSxTfSEfYV5Da/view?usp=share_link)
[resnet18](https://drive.google.com/file/d/1yf26ngXQP0Mwrlp6z2lPSxTfSEfYV5Da/view?usp=share_link)
[shufflenet_v1](https://drive.google.com/file/d/14K3EUknoBnOR9hII4GywdtkIrhL32Yjh/view?usp=share_link)

## Citation

If you use our pretrained model or benchmark in your research, please cite this project.

```

@inproceedings{tian2024pretrainps,
  title={Divide and Conquer: Hybrid Pre-training for Person Search},
  author={Yanling Tian, Di Chen, Yunan Liu, Jian Yang, Shanshan Zhang},
  booktitle={AAAI},
  year={2024}

}

```

