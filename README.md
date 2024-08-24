# VoxFormer: A Camera & Occupancy Network based Voxelized Scene Reconstruction


## Introduction
Autonomous vehicles (AVs) require comprehensive 3D scene understanding for effective planning and mapping. Semantic Scene Completion (SSC) aims to infer the complete 3D geometry and semantics of a scene from limited 2D perspectives captured by vehicle cameras. This project, based on the KITTI dataset, focuses on developing an efficient version of VoxFormer, a state-of-the-art model for SSC. Our goal is to optimize the VoxFormer architecture to reduce computational demands while maintaining high performance.

## Dataset
The KITTI dataset consists of real-world data captured from a vehicle equipped with stereo cameras and a 64-beam LiDAR sensor. It includes:
- RGB images
- 3D point clouds
- Detailed annotations with 3D bounding boxes for objects

## Baseline Results
The baseline results were obtained using the following models:
- MonoScene
- VoxFormer-T

The performance metrics used are Intersection over Union (IoU) and Mean Intersection over Union (mIoU). Our results demonstrate that VoxFormer-T achieves higher performance compared to MonoScene, particularly in short-range scenarios crucial for autonomous driving.

## Methodology

### Overview
The methodology for improving the VoxFormer model for SSC involves optimizing the architecture to handle complex 3D scene reconstructions with reduced computational resources. The enhanced version, termed "VoxFormer S," aims to maintain high performance while significantly reducing the memory footprint and computational demands.

### Depth-based Query Proposal
- Depth prediction is achieved using the MobileStereoNet model.
- The resulting depth map is back-projected to generate a 3D point cloud.
- This point cloud is converted into a binary voxel grid map, focusing on occupied voxels and ignoring empty spaces.

### Transformer-based 3D Scene Reconstruction
- Features are extracted from the occupied voxels and allowed to attend to corresponding image observations.
- Voxels not proposed by the initial depth-based query are associated with a learnable mask token.
- The complete set of voxels undergoes processing via self-attention mechanisms for comprehensive reconstruction and per-voxel semantic segmentation.

### Architectural Modifications
- **Model Simplification**: VoxFormer S processes only one image at a time, reducing computational load.
- **Training Optimization**: Streamlined training process with fewer epochs and a smaller sample size.
- **Memory Management**: Data accessed directly from storage using memory mapping techniques, beneficial for large datasets.

### Feature Extractor Modifications
- **MobileNet Adoption**: Incorporates MobileNet, utilizing depth-wise separable convolutions to reduce parameters.
- **Parameter Efficiency**: MobileNet has five times fewer parameters compared to ResNet, making the model faster and less resource-intensive.

## Detailed Performance Analysis
The performance of various SSC models is evaluated using IoU and mIoU metrics across different thresholds. Our optimized VoxFormer model shows competitive results at lower thresholds but exhibits a decline at higher thresholds, indicating areas for further refinement.

## Future Work
- Enhance results by harnessing computational power of the Sol supercomputer or AWS.
- Conduct thorough comparative analysis with other methodologies.
- Extend analysis to different 3D object detection models such as VoxelFormer, TPV Former, and SegFormer.
- Focus on further improving model accuracy for better performance.

## Conclusion
Developing an efficient variant of the VoxFormer model posed significant challenges. Through architectural optimizations, this project demonstrated the potential to achieve competitive performance with reduced computational and memory requirements, crucial for deployment on resource-constrained autonomous vehicle systems. This work paves the way for improved autonomous capabilities by optimizing resource-intensive models, showcasing the scope for innovation in developing efficient algorithms for safe self-driving operations.

## References
1. VoxFormer: Sparse Voxel Transformer for Camera-based 3D Semantic Scene Completion - Yiming Li, Zhiding Yu, Christopher Choy, Chaowei Xiao, Jose M. Alvarez, Sanja Fidler, Chen Feng, and Anima Anandkumar. CVPR, 2023.
2. 3D-R2N2: A Unified Approach for Single and Multi-view 3D Object Reconstruction - Christopher B. Choy, Danfei Xu, JunYoung Gwak, Kevin Chen, and Silvio Savarese. ECCV, 2016.
3. Multi-view Supervision for Single-view Reconstruction via Differentiable Ray Consistency - Shubham Tulsiani, Tinghui Zhou, Alexei A. Efros, and Jitendra Malik. CVPR, 2017.
4. A Point Set Generation Network for 3D Object Reconstruction from a Single Image - Haoqiang Fan, Hao Su, and Leonidas J. Guibas. CVPR, 2017.
5. KinectFusion: Real-time Dense Surface Mapping and Tracking - Richard A. Newcombe, Shahram Izadi, Otmar Hilliges, et al. ISMAR, 2011.
6. PCN: Point Completion Network - Wentao Yuan, Tejas Khot, David Held, Christoph Mertz, and Martial Hebert. 3DV, 2018.
7. Implicit Functions in Feature Space for 3D Shape Reconstruction and Completion - Julian Chibane, Thiemo Alldieck, and Gerard Pons-Moll. CVPR, 2020.
8. 3D Shape Generation and Completion through Point-Voxel Diffusion - Linqi Zhou, Yilun Du, and Jiajun Wu. ICCV, 2021.
9. Shape Completion using 3D-Encoder-Predictor CNNs and Shape Synthesis - Angela Dai, Charles Ruizhongtai Qi, and Matthias Nießner. CVPR, 2017.
10. Image Segmentation using Deep Learning: A Survey - Shervin Minaee, Yuri Boykov, Fatih Porikli, et al. TPAMI, 2022.
11. Deep Learning for 3D Point Clouds: A Survey - Yulan Guo, Hanyun Wang, Qingyong Hu, et al. TPAMI, 2020.
12. Semantic Scene Completion from a Single Depth Image - Shuran Song, Fisher Yu, Andy Zeng, et al. CVPR, 2017.
13. Lightweight Multiscale 3D Semantic Completion - Luis Roldao, Raoul de Charette, and Anne Verroust-Blondet. 3DV, 2020.
14. Sparse Single Sweep LiDAR Point Cloud Segmentation via Learning Contextual Shape Priors from Scene Completion - Xu Yan, Jiantao Gao, Jie Li, et al. AAAI, 2021.
15. MonoScene: Monocular 3D Semantic Scene Completion - Anh-Quan Cao and Raoul de Charette. CVPR, 2022.
