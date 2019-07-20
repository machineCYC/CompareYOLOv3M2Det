# Compare YOLOv3 M2Det

## Environment

| os | nvidia-driver | cuda | cudnn | GPU |
| --- | --- | --- | --- |--- |
| ubuntu 18.04 (64) | 390.48 | 9.0 | 7.0 | GeForce 1060(6G) |

## M2Det

-

## YOLO

- YOLOv1
    - 將物件偵測的問題轉換成回歸問題，直接預測 bounding box 和類別的機率
    - 針對整張照片所能提供的資訊進行預測，與 sliding windows 和 region proposal 不太一樣。所以將背景預測成物體的機率就將對低 (與 Fast-R-CNN 相比)，但也導致 recall 下降。
    - 結構上是單一結構，因此可以 end-to-end 的訓練
    - loss function 則是將 localization error 和 classfication error 整合在一起，並透過不同權重來提升模型訓練時的穩定度
    - 針對較小的物件表現也相對不穩定，主要是因為小的物件 localization error 相對也較小

- YOLO2
    - 主要是針對 YOLOv1 較弱的部分進行加強 (localization 和 recall 相對 region propsal 比較差)
    - 新增 Batch Normailzation，取代 dropout，加速模型訓練和提升 mAP 2%
    - 訓練方式的調整，YOLOv1 預訓練時用 224*224，detection 使用 448*448。YOLOv2 則是從頭先訓練 224*224 一部分 epoch，在調整成 448*448，減緩圖片因為解析度轉換的 gap，因此提升 4% mAP
    - 移除最後的全連接層，新增 anchor，但也因為這樣 mAP 略為下降，但 recall 提高
    - 透過 kmaen 來決定 anchor 的比例，相對於用人為經驗來的好
    - 新增 passthrough layer (類似 ResNet)，將 26*26 的 fature map 和 13*13 的 fature map 做連接，提升較小 object 的偵測能力 (因為小物件可能在 pooling 的過程中就被稀釋了)
    - 在最後 fine tune detection 時，引入 Multi-Scale Training，也就是輸入圖像是動態的

- YOLOv3


## Summary

下列比較是基於 YOLOv3 和 M2Det paper 所公開的 pretrained model 來比較

- M2Det

  1. 這邊所使用的 M2Det 是 vgg512 版本
  2. train data 使用
  3. 測試影片結果及想法
  2. python 3367, GPU 3990 MiB

- YOLOv3

  1. 這邊所使用的 YOLOv3 是 320、416、608 版本


| Model | fps | excute time | total frame |
| --- | --- | --- | --- |
| YOLOv3-320 | 3.30 | 1813.016 | 5986 |
| YOLOv3-416 | 3.34 | 1790.327 | 5986 |
| YOLOv3-608 | 3.3 | 1813.77 | 5986 |
| M2Det | 7.38 | 810.64 | 5986 |

## Reference

- [測試影片連結](https://www.youtube.com/watch?v=yzFcXUO0HTA)

- [darknet](https://github.com/pjreddie/darknet)

- [YOLOv3 Source Code](https://github.com/iArunava/YOLOv3-Object-Detection-with-OpenCV)

- [M2Det Source Code](https://github.com/qijiezhao/M2Det)

- [YOLOv1 paper](https://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Redmon_You_Only_Look_CVPR_2016_paper.pdf)

- [YOLOv2 paper](http://openaccess.thecvf.com/content_cvpr_2017/papers/Redmon_YOLO9000_Better_Faster_CVPR_2017_paper.pdf)

- [YOLOv3 paper](https://pjreddie.com/media/files/papers/YOLOv3.pdf)