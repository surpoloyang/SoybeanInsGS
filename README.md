# SoybeanInsGS: A high-precision and data-efficient point cloud instance segmentation pipeline for mature soybean plants via cross-view instance tracking and instance-aware 3D Gaussian Splatting 


## Results
### Rendered Images
<img width="1000" alt="image" src='media/result.gif'>

### Cross-view Instance Tracking
<img width="1000" alt="image" src='media/CVIT.png'>

### Point Cloud Instance Segmentation
<img width="1000" alt="image" src='media/ins_seg.png'>

## Installation
```shell
conda create --name soybeaninsgs -y python=3.10
conda activate soybeaninsgs
pip install torch==2.2.2 torchvision==0.17.2 --index-url https://download.pytorch.org/whl/cu118
pip install rfdetr

pip install plyfile==0.8.1
pip install tqdm scipy wandb opencv-python scikit-learn lpips hdbscan dearpygui
pip install "numpy<2"

pip install submodules/diff-gaussian-rasterization --no-build-isolation
pip install submodules/simple-knn --no-build-isolation
```

## Data Preparation:
We typically support data prepared as COLMAP format.


```
data/
├── scene_1                     # scene_1, scene_2, ... are different scenes (different soybean plants)
│   ├── images                  # images, images_2, images_4, and images_8 are the original images with different downsampling rates (1, 2, 4, and 8)
│   ├── images_2
│   ├── images_4
│   ├── images_8
│   ├── object_mask             # cross-view instance tracking results(gray), which are used as the supervision for training the instance-aware 3D Gaussian Splatting model
│   ├── rf_detr_mask            # cross-view instance tracking results(gray), for backup
│   ├── rf_detr_mask_visual     # cross-view instance tracking results(visual), which are used for visualization
│   ├── raw_rf_detr_mask        # RF-DETR results(gray), for cross-view instance tracking
│   └── sparse                  # COLMAP results
├── scene_2
│   ├── images
│   ├── images_2
│   ├── images_4
│   ├── images_8
│   ├── object_mask
│   ├── rf_detr_mask
│   ├── rf_detr_mask_visual
│   ├── raw_rf_detr_mask
│   └── sparse
├── ...

```