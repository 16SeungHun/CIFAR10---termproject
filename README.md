# CIFAR10데이터 셋으로 Image Classification하기

Baseline : 교수님의 resnet 코드<br/>

최종 top-1 acc : 98.22 % (시드 고정 전, epoch 71)<br/>
코딩환경 : Google colab<br/>
방법 : pytorch 공식 홈페이지를 많이 참조함<br/>

|테스트한 모델|
|------|
|ResNet-18|
|ResNet-34|
|ResNet-50|
|ResNet-101|
|**ResNet-152**|
|ResNeXt-50-32x8d|
|ResNeXt-101-32x8d|
|Wide ResNet-50-2|
|Wide ResNet-101-2|

|테스트한 Data Augmentation|
|------|
|RandomCrop(32, padding=4)|
|RandomHorizontalFlip|
|Resize(224, interpolation=2)|
|Normalize(mean=(0.485, 0.456, 0.406), std=(0.229, 0.224, 0.225)|
|CUTMIX기법|

|각종 parameters 값|
|------|
|optimizer : SGD, lr = 0.001, momentum=0.9, nesterov=True|
| (최대) epoch = 110 |
|lr_scheduler를 사용하여 step_size=7, gamma=0.1기법 사용|
|batchsize = 32|

