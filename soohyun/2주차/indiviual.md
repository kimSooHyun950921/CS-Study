[ 이력서&포트폴리오](https://drive.google.com/file/d/1xlU8eKT5xGJPb8Opg8dUOg_FgC_Yf7Bo/view?usp=sharing)
1. 본직무에 지원한 이유는?
    ```
    학교에서 많은 프로젝트를 진행하면서 최적의 솔루션을 찾는방법이 매력적이였다. 
    ```

2. 딥러닝이 많이 나오고 있는데 머신러닝을 사용해야하는 이유는 뭔가요?
    ```
    딥러닝은 모든 문제에서 해결수단이 될수없다. 예를들어 단순 linear regression을 푸는 문제는 머신러닝이 좋다고 생각한다.
    딥러닝(우리가 생각하는 NN으로)으로 문제를 해결했을때, ML으로 해결했다면 1분만에 풀리는 문제를 NN으로 GD방식으로 했을때는 weight를 찾는데 24시간이 넘게걸렸다.  따라서 이미지처리나 자연어와같이 고차원적인 문제를 푸는 방식이 아닌, 데이터를 이용해서 분류하는 방법은 머신러닝이 훨씬 최적이라고 생각한다.
    ```

3. 알고있는 metric에 대해 설명 해보세요
    ```
    1. confusion matrix:
        TP: Positive라고 예측한것이 맞은것
        FP: Positive라고 예측한것이 틀린것
        FN: Negative라고 예측한것이 틀린것
        TN: Negative라고 예측한것이 맞은것
    2. 정확도:  전체 예측한것중에 TP+TN의 비율
    3. precision: 맞았다고 예측한것중에 실제로 맞은것(TP/TP+FP)
    4. recall: 실제 맞은것중에 맞았다고 예측한것(TP/TP+FN)
    5. f1 score: precision과 recall을 조화평균한것
    6. roc curve의 AUC: Falce positive Rate이 변할때 True Positive이 어떻게 변하는지 나타내는곡선

    ```

4. 설명지표에대해서 각각은 언제 사용하는 것이 좋을까요?
    ```
    1. 실제데이터에서 예측데이터가 얼마나 같은지 판단하기때문에 모델성능예측에서는 가장 많이 사용된다.
    2. precision은 P를 잘못예측하면(FP) 문제가생기는경우(스팸메일 필터)
    3. recall은: Negative로 잘못예측하면 문제가 생기는경우(암 환자 발생)
    4. precision과 recall은 trade-off 관계에 있을경우 모두 가장 높은지점을 찾는경우
    5. ROC curve: 2진 분류할때 쓰인다. TPR/FPR로 나타내며 이면적이 넓으면 정확도가 높다.
    ```

5. 각각의 지표를 어떻게 높일 수 있을까요?
    ```
    1. precison을 높이려면 FP를 낮추면 된다. 확실한경우만 제외하고 모두 Negative로 예측하면 된다.
    2. recall을 높이려면 FN을 낮추면 된다. Positve가 많게 예측하면 된다.
    3. precison과 recall의 
    4. RoC 커브는 ?

    ```

6. 데이터 전처리를 해야하는 이유는 무엇일까요?
```
데이터값이 NaN값이 많거나, 각 feature마다 단위가 다르면 
정확도가 잘못측정될 수 있다. 특히 regression 과같은 알고리즘은
특히나 값이 영향을 많이 받기때문에 값에대한 영향을 줄이려면
전처리가 필요하다.
```

