## Faster R-CNN

## Dependencies
* lxml
* matplotlib
* numpy
* tqdm
* torch==1.10.1
* torchvision==0.10.1
* pycocotools
* Pillow

## Code organization
代码框架主要如下：

* `train_fasterrcnn_res50_fpn.py`, `train_FCOS_res50_fpn.py`训练的主体文件
* `predict_FCOS.py`,`predict_fasterrcnn.py` 用于输出目标检测结果，并以图片形式保存在test_images文件夹中
* `proposals.py` 用于绘制第一阶段的proposal
* `my_dataset.py`, `my_transform.py` VOC2012数据集的读取与预处理
* `backbone` 训练时用到的backbone，主要是resnet50系列
* `network_files` Faster R-CNN和FCOS模型，结构与pytorch官方一致
* `save_weights` 存放模型参数pth文件
* `test_images` 保存目标检测结果以及proposals结果
* `train_utils` 训练与验证的主要代码
* `pascal_voc_classes.json` 保存VOC2012类别，无需改动


## Run experiments
### 准备数据与预训练模型
* 下载代码至本地 
* Pascal VOC2012 train/val数据集下载地址：http://host.robots.ox.ac.uk/pascal/VOC/voc2012/VOCtrainval_11-May-2012.tar 并解压到当前文件夹
* MobileNetV2: https://download.pytorch.org/models/mobilenet_v2-b0353104.pth 下载后重命名为`mobilenet_v2.pth`，然后放到`bakcbone`文件夹下
* 训练好的模型参数 链接: https://pan.baidu.com/s/19CVbWoJkBN1ASLLRY2pG4g?pwd=33gb (提取码: 33gb)，下载后将文件覆盖save_weights文件夹

### 目标检测
* 选择不在VOC2012数据集中，但拥有其类别的三张测试图像进行目标检测：
* 测试图像已存放在test_images中，命名为test1.jpg,test2.jpg,test3.jpg,目标检测结果图片名称为 f'{net}_test.jpg'

运行下列代码可以使用训练好的模型直接在测试图像上进行目标检测
```
python predict_fasterrcnn.py
python predict_FCOS.py
```
### Proposal
* 选择四张数据集中的图片，显示Fasterrcnn第一阶段的proposals:
运行下列代码可以使用训练好的模型进行proposal绘制，并保存在test_images中，命名为proposal1.jpg,proposal2.jpg,proposal3.jpg,proposal4.jpg
```
python proposals.py
```

### 训练模型
运行下列代码可以训练Faster R-CNN 和 FCOS
```
python train_fasterrcnn_res50_fpn.py
python train_FCOS_res50_fpn.py
```



