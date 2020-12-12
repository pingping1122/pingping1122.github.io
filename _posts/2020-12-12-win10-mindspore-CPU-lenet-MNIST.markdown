---
layout: post
title:  "Win10上MindSpore(CPU)用Lenet网络训练MNIST"
date:   2020-12-12 10:20:08 +0800
categories: jekyll update
---




本文是在windows10上安装了CPU版本的Mindspore,并在mindspore的master分支基础上使用LeNet网络训练MNIST数据集，实践已训练成功，此文为记录过程中的出现问题；
（据说此时mindspore的r0.7版本上是直接执行成功的）
 
 - Windows10 
 - Miniconda 4.8.3
 - Python 3.7.7
 - MindSpore master  [mindspore的gitee地址](https://gitee.com/mindspore/mindspore?_from=gitee_search)
 


【1】首先使用conda activate mindspore 进入mindspore虚拟环境

【2】再切入mindspore中lenet网络的train.py所在目录 `D:\gitee\mindspore\model_zoo\official\cv\lenet` 

![mindspore的lenet网络训练文件所在位置](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_mindspore_cpu_lenet_mnist/train.py.png)

【3】执行训练 `python train.py --device-target=CPU`  （因为代码里默认使用的训练设备为Ascend，需要手动设置 `--device_target`为`CPU`）

 - **问题一  No module named 'mindspore.dataset.vision'**
 
 ![No module named mindspore.dataset.vision](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_mindspore_cpu_lenet_mnist/bug1-mindspore.dataset.vision.png)

报错：文件  `D:\gitee\mindspore\model_zoo\official\cv\lenet\src\dataset.py` 引入模块`import mindspore.dataset.version.c_transforms as CV` 错误;

原因：查看发现系统 miniconda3的mindspore环境中 在\dataset 和 \version文件夹中还有一层 \transforms 

![dataset和version中还有一层transform层](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_mindspore_cpu_lenet_mnist/transform.png)
**解决：修改dataset.py 文件中模块引用的位置；**

```
import mindspore.dataset.transforms.vision.c_transforms as CV
from mindspore.dataset.transforms.vision import Inter
```

保存文件重新执行命令 `python train.py --device-target=CPU`


 - **问题二  ImportError: cannot import name 'set_seed' from 'mindspore.common'**

![ImportError: cannot import name set_seed from mindspore.common](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_mindspore_cpu_lenet_mnist/bug2-set_seed.png)
报错：文件train.py中导入set_seed模块出错

原因： `C:\Users\86183\miniconda3\envs\mindspore\Lib\site-packages\mindspore\common\__init__.py`  文件中没有set_seed模块（也即common文件下没有set_seed.py文件）

**解决：在train.py 中将以下两条语句注释掉**

```
from mindspore.common import set_seed

set_seed(1)
```

 保存文件重新执行命令 `python train.py --device-target=CPU`

 - **问题三  ValueError: The folder ./Data\train does not exist or permission denied!**
 
 ![ValueError: The folder ./Data\train does not exist or permission denied!](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_mindspore_cpu_lenet_mnist/bug3-Data_train_file_not_exist.png)

原因：/Data/train 文件不存在

**解决：在`D:\gitee\mindspore\model_zoo\official\cv\lenet\` 下新建Data目录，并在Data目录下新建train和test文件夹**

![缺少Data目录](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_mindspore_cpu_lenet_mnist/data.png)

重新执行命令 `python train.py --device-target=CPU`

 - **问题四 RuntimeError: Currently dateset sink mode is not supported when the device target is CPU**

![RuntimeError: Currently dateset sink mode is not supported when the device target is CPU](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_mindspore_cpu_lenet_mnist/bug4-RuntimeError.png)
原因：数据下沉模式是针对asic芯片做的优化 默认是开启的，CPU不支持这种模式

**解决：改为执行命令  `python train.py --device_target=CPU --dataset_sink_mode=False`**


 - **问题五：  Unexpected error. There is no valid data matching the dataset API MnistDataset.Please check file path or dataset API validation first.**

![Unexpected error. There is no valid data matching the dataset API MnistDataset.Please check file path or dataset API validation first.](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_mindspore_cpu_lenet_mnist/bug5-download_MNIST.png)

原因：脚本没有自动下载MNIST数据集，需要自己手动下载

**解决：手动下载MNIST数据集[MNIST数据集下载地址](http://yann.lecun.com/exdb/mnist/)**

MNIST数据目录结构：

![MNIST数据集目录结构](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_mindspore_cpu_lenet_mnist/MNIST_data_Set.png)

将`t10k-labels-idx1-ubyte.gz` 和`t10k-images-idx3-ubyte.gz` 解压到 问题三新建的Data/test 目录下

将`train-labels-idx1-ubyte.gz` 和`train-images-idx3-ubyte.gz` 解压到 问题三新建的Data/test 目录下

![MNIST的test数据集](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_mindspore_cpu_lenet_mnist/data_test.png)

![MNIST的train数据集](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_mindspore_cpu_lenet_mnist/data_train.png)

重新执行`python train.py --device_target=CPU --dataset_sink_mode=False`

 - **问题六  InferImplBiasAddGrad] BiasAddGrad input y backprop, dim should >= 2, while 1.**

![ InferImplBiasAddGrad BiasAddGrad input y backprop, dim should 2, while 1.](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_mindspore_cpu_lenet_mnist/bug6-InferImplBiasAddGrad.png)

**解决：在train.py中添加语句 `is_grad=False`, 变成下面这样**

```
    net_loss = nn.SoftmaxCrossEntropyWithLogits(sparse=True, reduction="mean",is_grad=False)
```


再度执行命令 `python train.py --device_target=CPU --dataset_sink_mode=False` ， 训练成功；

![训练10个epoch](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_mindspore_cpu_lenet_mnist/train_success.png)

验证准确率： `python eval.py --ckpt_path="ckpt/checkpoint_lenet-10_1875.ckpt" --device_target=CPU`

```
============== Starting Testing ==============
============== {'Accuracy': 0.9844751602564102} ==============
```

![验证准确性](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_mindspore_cpu_lenet_mnist/eval_accuracy.png)


