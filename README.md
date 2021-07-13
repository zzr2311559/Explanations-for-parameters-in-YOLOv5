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

关于AP，其官方定义如下：
> Compute a version of the measured precision/recall curve with precision monotonically decreasing, by setting the precision for recall r to the maximum precision obtained for any recall r′ ≥ r.
Compute the AP as the area under this curve by numerical integration. No approximation is involved since the curve is piecewise constant.

本质上来说，AP表示不同召回率下的精度

![image](https://raw.githubusercontent.com/zzr2311559/Explanations-for-parameters-in-YOLOv5/master/imgfile/PR%20graph.png)

最后，得到的蓝色部分即为AP值

### (2) 计算mAP（mean Average Precision）

AP是针对某一类而言的，mAP即是对所有类的AP求平均值

此外我们经常见到的mAP是以mAP@0.5和mAP@0.5:0.95的形式出现的

对前者而言，0.5表示设置0.5为置信度阈值，对后者来说， 是以0.05为增量从0.5到0.95分别作阈值再取平均值，这可能是考虑到在0.5阈值下的表现不能代表总体表现，因此需要取多阈值下的平均值来整体反映模型的好坏
