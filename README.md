# license-plate-detect-recoginition-pytorch
深度学习车牌检测与识别，检测结果包含车牌矩形框和4个角点，基于pytorch框架运行，
主程序是detect_rec_img.py，运行程序前需要确保您的机器安装了pytorch

车牌识别模块，可以更换成crnn网络做识别，也可以更换到传统图像处理方法分割字符后逐个字符识别，
在这个车牌检测和识别系统里，我觉得最重要的是前面的车牌检测与矫正模块，因为如果前面没做好，
那么后面输入到车牌识别模块里的图片是一个倾斜的车牌，这时候输出结果就出错了。

对于车牌检测，也可以使用图像分割的思想，例如使用UNet语义分割网络，分割出车牌，
二值化然后查找连通域，计算4个顶点

# 补充

运行步骤：

测试

`python detect_rec_img.py  --cfg Resnet50  --imgpath imgs/18.jpg`      or

`python detect_rec_img.py  --cfg mobilenet0.25  --imgpath imgs/18.jpg`

所需权重文件主要包括mnet_plate.pth与Resnet50_epoch_40.pth两个不同模型所训练的车牌定位与关键点检测，选择一个即可如上代码所示，my_lprnet_model.pth为车牌号码识别的权重文件。

训练主要是训练mnet_plate.pth与Resnet50_epoch_40.pth两个模型权重，可以在Plate-Landmarks-detection文件中进行训练，需要下载[ccpd数据集](https://blog.csdn.net/LuohenYJ/article/details/117752120)，这个文件用法见下面链接。

license-plate-detector文件是利用mobilenet训练ccpd数据集得到的mnet_plate.pth模型权重，这个模型是车牌定位

[https://gitee.com/zeusees/license-plate-detector](https://gitee.com/zeusees/license-plate-detector)

Plate-Landmarks-detection文件是利用基于mobilenet训练的mnet_plate.pth权重或者基于resnet50训练的Resnet50_epoch_40.pth模型权重进行车牌定位与关键点检测

https://github.com/Fanghc95/Plate-Landmarks-detection

LPRNet_Pytorch文件是进行车牌号码识别的模型用于生成Final_LPRNet_model.pth  

[https://github.com/sirius-ai/LPRNet_Pytorch](https://github.com/sirius-ai/LPRNet_Pytorch)

主文件是利用mnet_plate.pth的车牌定位与关键点检测与基于Final_LPRNet_model.pth网络的车牌号码识别

[https://github.com/hpc203/license-plate-detect-recoginition-pytorch](https://github.com/hpc203/license-plate-detect-recoginition-pytorch)

license-plate-detect-recoginition-opencv，将mnet_plate.pth与LPRNet转换为onnx部署进行测试

[https://github.com/hpc203/license-plate-detect-recoginition-opencv](https://github.com/hpc203/license-plate-detect-recoginition-opencv)

