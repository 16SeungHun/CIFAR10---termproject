# CIFAR10데이터 셋으로 Image Classification하기

Baseline : 교수님의 resnet 코드<br/>

최종 top-1 acc : 98.22 % (시드 고정 전, epoch 71)<br/>
코딩환경 : Google colab<br/>
방법 : pytorch 공식 홈페이지를 많이 참조함<br/>

**사용한 기법은 진하게 글자 표시되어있음**<br/>

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
|**RandomCrop(32, padding=4)**|
|**RandomHorizontalFlip**|
|**Resize(224, interpolation=2)**|
|**Normalize(mean=(0.485, 0.456, 0.406), std=(0.229, 0.224, 0.225)**|
|CUTMIX기법|

|각종 parameters 값|
|------|
|**optimizer : SGD, lr = 0.001, momentum=0.9, nesterov=True**|
| **(최대)epoch = 110**|
|**lr_scheduler를 사용하여 step_size=7, gamma=0.1기법 사용**|
|**batchsize = 32**|

1. data augmentation 방법중, CUTMIX를 사용해서 훈련시켜 봤는데, 생각보다 비약적으로 정확도가 올라가지 않아서 사용하지 않았습니다.<br/>
2. class로 하나하나 코드를 짜서 하는 것 보다 pretreined된 model을 불러와서 transfer learning을 진행했을 때 정확도가 대략 6% 이상 향상되었습니다.<br/>
3. Resize기법을 사용했을 때 정확도가 8% 이상 향상되었습니다.<br/>
4. ResNet 모델들 중 152가 정확도가 가장 높아서 152를 사용했습니다.<br/>
5. ResNext50(85.35%) < ResNext101(86.29%) <= wide ResNet101(87.25%) < ResNet-152(98.22%) 순으로 정확도가 높았습니다.<br/>
6. mean값과 std값도 두가지 경우로 비교해봤습니다. 보통 많이 사용하시는<br/>
mean=(0.4914, 0.4824, 0.4467), std=(0.2471, 0.2436, 0.2616)보다 <br/>
mean=(0.485, 0.456, 0.406), std=(0.229, 0.224, 0.225)의 정확도가 조금 더 높게 나왔습니다.<br/>
7. Resize를 동일하게 사용하고 RandomCrop와 RandomHorizontalFlip의 사용 유무도 비교해봤습니다.<br/>
사용했을 때 최대 98.22%를 기록하였고, 사용하지 않았을 때 98.07%를 기록했습니다.<br/>
8. batchsize를 32와 16 두가지로 비교했을 때, 16보다 32가 훨씬 정확도가 높게 나왔습니다.<br/>
9. np.random.seed(3)로 고정시켜 훈련했습니다.<br/>

#결론
RenNet-152가 가장 성능이 좋았음. Transfer learning 성능 좋음. 마지막 1 layer 제외하고 freeze 하여 사용. data augmentaion resize 성능 종음. pretrained model 사용.<br/>
mean=(0.485, 0.456, 0.406), std=(0.229, 0.224, 0.225) 사용. resize를 단독으로 사용하는 것 보다는 RandomCrop와 RandomHorizontalFlip를 같이 써주니 약간의 성능 향상.


