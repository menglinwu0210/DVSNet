# DVSNet
The major contributors of this repository include [Yu-Shuan Xu](https://github.com/SUSean), [Hsuan-Kung Yang](https://github.com/hellochick), [Tsu-Jui Fu](https://github.com/yesray0216), and Chun-Yi Lee.
## Introduction
Dynamic Video Segmentation Network (DVSNet) framework is presented to strike a balance between quality and efficiency for semantic video segmentation.
The DVSNet framework consists of two convolutional neural networks: a segmentation network (e.g., [DeepLabv2](https://arxiv.org/abs/1606.00915)) and a flow network (e.g.,[FlowNet2](https://arxiv.org/abs/1612.01925)).
The former generates highly accurate semantic segmentations, but is deeper and slower.
The latter is much faster than the former, but its output requires further processing to generate less accurate semantic segmentations.
And DVSNet exploits a decision network (DN) to determine which frame regions should be forwarded to which paths based on a metric called **expected confidence score**.
The useage of DN proposed an adaptive key frame scheduling policy to adaptively adjust the update period of key frames at runtime.

[**Demo Video**](https://goo.gl/szDUm8)

## Disclaimer
This is a modified implementation for DVSNet based on Tensorflow. Please notes that there are some differences to the original implementation:
(1) Data I/O and Image Preprocessing times are included when calculating fps. (2) It use NHWC data formate rather than NCHW data formate in the original implementation.
These differences cause lower fps than reported in the paper.

## Requirements
### Checkpoint
Create checkpoint directory and get restore checkpoint from [Google Drive](https://goo.gl/ELcxmf)(270 MB).
### pip install
```
pip install tensorflow-gpu==1.4  # for Python 2.7 and GPU
pip install opencv-python
pip install Pillow
pip install scipy
```

## Inference
To get segmented results of vedio frames:
```
python inference.py --data-dir=cityscape_video_dir --data-list=cityscape_video_list
```
List of Args:
```
--data-dir:     Path to the directory containing the dataset.
--data-list:    Path to the file listing the images in the dataset.
--restore-from: Where restore model parameters from.
--save_dir:     Where to save segmented output.
--num-steps:    Number of images in the video.
--overlap:      Overlapping size.
--target:       Confidence score threshold.
--dynamic:      Whether to dynamically adjust target
```
Inference time including time of Data I/O and Image Preprocessing: 0.1\~0.05s (10\~20fps)  
With Intel Xeon E5-2620 CPUs and  NVIDIA GTX 1080 Ti GPU

## Citation
```
@inproceedings{xu2018dvsnet,
    author = {Yu-Shuan Xu and Hsuan-Kung Yang and Tsu-Jui Fu and Chun-Yi Lee},
    title = {Dynamic Video Segmentation Network},
    booktitle = {IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
    year = 2018
}

@article{chen2017deeplab,
    author = {L.-C. Chen and G. Papandreou and I. Kokkinos and K. Murphy and A. L. Yuille},
    title = {Deeplab: Semantic image segmentation with deep convolutional nets, atrous convolution, and fully connected {CRFs}},
    journal = {IEEE Trans. Pattern Analysis and Machine Intelligence (TPAMI)},
    year = 2017
}
@inproceedings{ilg2017flownet2,
    author = {E. Ilg and N. Mayer and T. Saikia and M. Keuper and A. Dosovitskiy and T. Brox},
    title = {FlowNet 2.0: Evolution of Optical Flow Estimation with Deep Networks},
    booktitle = {IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
    year = 2017
}
```
## Reference Code
DeepLabv2 tensorflow model : [tensorflow-deeplab-resnet](https://github.com/DrSleep/tensorflow-deeplab-resnet)  
FlowNet2 tensorflow model : [flownet2-tf](https://github.com/sampepose/flownet2-tf)