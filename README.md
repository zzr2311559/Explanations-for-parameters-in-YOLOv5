# Explanations-for-parameters-in-YOLOv5

## 1.IOU

IOU简单来说就是衡量监测框和标签框的重合程度，如图所示：

![image](https://raw.githubusercontent.com/zzr2311559/Explanations-for-parameters-in-YOLOv5/master/imgfile/IOU.jpg)

## 2.Precision & Recall

### (1) TP TN & FP FN

TP:True Positive

TN:True Negative

FP:False Positive

FN:False Negative

首字母T、F表示对象被检测器识别的正确与否

尾字母P、N表示对象被分为正样本或负样本

我们以一个简单案例来解释TP、TN、FP、FN

![image](https://raw.githubusercontent.com/zzr2311559/Explanations-for-parameters-in-YOLOv5/master/imgfile/flow%20graph.jpg)

对有12只狗和8只猫的数据集进行检测，目标是识别所有的狗

经过识别，我们得到了“10只狗”，但是实际上包括9只狗及1只猫。此时对原数据集而言，还剩下3只狗和7只猫

由于目标是检测所有的狗，那么得到的9只狗即是TP，1只猫被错误识别成了狗，它就是FP

剩下的3只狗根据期望应该被识别，但是却没有，它就是FN，而那7只猫没有被识别为狗，自然是TN

### (2) Precision

Precision = TP / (TP + FP)

Precision（精确度）指的是在检测器识别到的那一部分对象中，识别正确的对象占总对象的比例

对应于例子，就是9/10

### (3) Recall


Recall = TP / (TP + FN)

Recall（召回率）指的是在所有应该被检测到的对象中，识别正确的对象占总对象的比例

对应于例子，就是9/12

## 3. mAP

### (1) 计算AP（Average Precision）

首先，对检测器生成的预测框的置信度由高到低进行排序，再计算预测和实际标签框的IOU,若IOU >= 0.5,判断其为TP，若IOU < 0.5,判断其为FP

其次，分别设置一定的置信度阈值，无视所有的小于该阈值的预测框，据此得到多组Precision & Recall值（以下称PR值），制作P/R曲线，示例如下：

![image](https://raw.githubusercontent.com/zzr2311559/Explanations-for-parameters-in-YOLOv5/master/imgfile/PR%20graph.png)

最后，得到的蓝色部分即为AP值

### (2) 计算mAP（mean Average Precision）

AP是针对某一类而言的，mAP即是对所有类的AP求平均值
