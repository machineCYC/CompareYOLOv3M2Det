# Compare YOLOv3 M2Det

## Environment

| os | nvidia-driver | cuda | cudnn | GPU |
| --- | --- | --- | --- |--- |
| ubuntu 18.04 (64) | 390.48 | 9.0 | 7.0 | GeForce 1060(6G) |

## Summary

下列比較是基於 YOLOv3 和 M2Det paper 所公開的 pretrained model 來比較

- M2Det

  1. 這邊所使用的 M2Det 是 vgg512 版本

- YOLOv3

  1. 這邊所使用的 YOLOv3 是 320 版本


| Model | parameter size | fps | excute time | total frame|
| --- | --- | --- | --- |--- |--- |--- | ---|
| YOLOv3-320 |  | 3.30 | 1813.016 | 5986 |
| YOLOv3-416 |  |  |  |  |
| YOLOv3-608 |  | 3.3 | 1813.77 | 5986 |
| M2Det | | 8 |  | |

## Reference

- [darknet](https://github.com/pjreddie/darknet)

- [YOLOv3 Source Code](https://github.com/iArunava/YOLOv3-Object-Detection-with-OpenCV)

- [M2Det Source Code](https://github.com/qijiezhao/M2Det)