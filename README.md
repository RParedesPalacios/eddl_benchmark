# Eddl benchmarks results
The results were obtained using the following configuration:
* EDDL version: 0.7.1
* Pytorch version: 1.6.0
* Keras version: 2.4.3
* Keras backend: tensorflow
* Tensorflow version: 2.2.0
* GPU model: Nvidia GeForce GTX 1050Ti
* CPU model: Intel(R) Core(TM) i7-7700HQ 2.80GHz
* Graphics and accuracy results obtained executing on GPU
## Detected anomalies
### Time
* PyEDDL usually lasts a bit more than EDDL. However, with VGGs in CPU, that increase is abnormaly huge (more than double).
* In Resnet50 with batchnorm in CPU PyEDDL lasts less than EDDL. This may be circumstantial as it was tested only in one epoch.
* The time increase due to BatchNorm is much greater in EDDL than in Keras or Pytorch.
* EDDL times are quite competitive in Resnets but much worse than Keras and Pytorch in VGGs.
* EDDL and PyEDDL last more with batchnorm than without it in CPU with VGGs.

### Accuracy
* EDDL converges slower than Keras and Pytorch without batchnorm, specially in VGGs.
* With VGG16, it doesn't reach the same accuracy as Keras and Pytorch. With VGG19 it didn't reach it neither, but using HeUniform instead of GlorotUniform as initializer seemed to solve the problem.
* In general, Pytorch's test accuracy is more stable and a bit higher than Keras and EDDL when using batchnorm.

## Cifar10
### VGGs
#### VGG16
|Without batchnorm|Keras|Pytorch|EDDL|PyEDDL|
|-----------------|----------|-----------|------|------|
|Train accuracy (%)|99.2|99.2|98.9|-|
|Test accuracy (%)|77.4|77.9|74.6|-|
|GPU Time per epoch (s)|62|77|146|147|
|CPU Time per epoch (s)|1313|887|3107|6966|


|With batchnorm|Keras|Pytorch|EDDL|PyEDDL|
|------------- | ---------- | ----------- |------|------|
|Train accuracy (%)|99.1|99.1|99.3|-|
|Test accuracy (%)|71.7|76.2|76.4|-|
|GPU Time per epoch (s)|68|81|204|204|
|CPU Time per epoch (s)|1375|956|2846|7962|


#### VGG19
|Without batchnorm*|Keras|Pytorch|EDDL|PyEDDL|
|------------- | ---------- | ----------- |------|------|
|Train accuracy (%)|98.7|98.7|98.9|-|
|Test accuracy (%)|66.0|65.5|68.2|-|
|GPU Time per epoch (s)|76|129|190|193|
|CPU Time per epoch (s)|1703|1262|3872|8992|

\* This experiment used HeUniform as weight initializer insted of GlorotUniform. GlorotUniform was the initializer for all the other experiments.


|With batchnorm|Keras|Pytorch|EDDL|PyEDDL|
|------------- | ---------- | ----------- |------|------|
|Train accuracy (%)|98.4|98.8|98.8|-|
|Test accuracy (%)|59.9|59.7|61.0|-|
|GPU Time per epoch (s)|81|135|260|264|
|CPU Time per epoch (s)|1809|1352|3838|8628|


### Resnets

#### Resnet18
|Without batchnorm|Keras|Pytorch|EDDL|PyEDDL|
|------------- | ---------- | ----------- |------|------|
|Train accuracy (%)|99.0|98.7|98.7|-|
|Test accuracy (%)|67.6|66.4|67.3|-|
|GPU Time per epoch (s)|25|62|36|37|
|CPU Time per epoch (s)|1234|456|932|1191|


|With batchnorm|Keras|Pytorch|EDDL|PyEDDL|
|------------- | ---------- | ----------- |------|------|
|Train accuracy (%)|98.7|98.5|98.4|-|
|Test accuracy (%)|64.0|65.7|64.8|-|
|GPU Time per epoch (s)|26|64|49|52|
|CPU Time per epoch (s)|1244|485|1207|1373|


#### Resnet34
|Without batchnorm|Keras|Pytorch|EDDL|PyEDDL|
|------------- | ---------- | ----------- |------|------|
|Train accuracy (%)|98.7|98.8|98.7|-|
|Test accuracy (%)|66.6|67.8|66.1|-|
|GPU Time per epoch (s)|44|103|65|67|
|CPU Time per epoch (s)|2125|834|1674|2073|


|With batchnorm|Keras|Pytorch|EDDL|PyEDDL|
|------------- | ---------- | ----------- |------|------|
|Train accuracy (%)|98.1|98.2|98.2|-|
|Test accuracy (%)|66.4|65.5|60.4|-|
|GPU Time per epoch (s)|46|107|89|93|
|CPU Time per epoch (s)|2140|895|2119|2301|


#### Resnet50
|Without batchnorm|Keras|Pytorch|EDDL|PyEDDL|
|------------- | ---------- | ----------- |------|------|
|Train accuracy (%)|98.7|98.6|98.7|-|
|Test accuracy (%)|68.4|68.1|66.4|-|
|GPU Time per epoch (s)|47|89|75|79|
|CPU Time per epoch (s)|1995|706|1684|2204|


|With batchnorm|Keras|Pytorch|EDDL|PyEDDL|
|------------- | ---------- | ----------- |------|------|
|Train accuracy (%)|97.1|97.1|97.6|-|
|Test accuracy (%)|61.3|63.1|61.9|-|
|GPU Time per epoch (s)|52|97|132|143|
|CPU Time per epoch (s)|2044|835|2622|2468|

### Plots
![Results plot](results/vgg16_nobn.png)
![Results plot](results/vgg16_bn.png)
![Results plot](results/vgg19_nobn.png)
![Results plot](results/vgg19_bn.png)
![Results plot](results/resnet18_nobn.png)
![Results plot](results/resnet18_bn.png)
![Results plot](results/resnet34_nobn.png)
![Results plot](results/resnet34_bn.png)
![Results plot](results/resnet50_nobn.png)
![Results plot](results/resnet50_bn.png)
