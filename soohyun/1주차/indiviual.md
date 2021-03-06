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



1. 앙상블(Ensemble) 기법에 대해서 설명해주세요
    ```
    정답: 여러개의 분류기를 생성하고, 그 예측을 결함합으로써 보다 정확한 예측을 도출하는 기법을 말한다.

    다양한 방법이 있다.

    보팅(Voting): 각기 다른 예측기를 통해 결과를 예측하고 가장 다수 예측기가 선택한 결과를 투표하는 방법

    배깅(Bagging): 모두 같은 예측기를 통해 결과를 예측하고 다수결 투표 혹은 평균값 집계한다. 과적합(Overfitting) 방지에 효과적이다. 대표적인 배깅 방식으로 랜덤포레스트가 있다.

    부스팅(Boosting): 여러개의 분류기가 순차적으로 학습을 수행한다. 이전 분류기가 잘못된 예측을 하면 다음 분류기에서 잘 예측하도록 틀린 데이터에 대해서 가중치를 부여하며 학습과 예측을 진행한다. 계속해서 분류기에게 가중치를 부스팅하며 학습을 진행하기에 부스팅 방식이라고 불린다. 예측 성능이 뛰어나 앙상블 학습을 주도한다. 대표적인 방식으로는 XGBoost, LigthGBM이 있다.

    * 보통 배깅 방식에 비해 성능이 좋지만, 속도가 느리고 과적합이 발생할 가능성이 존재하므로 상황에 따라 적절히 사용해야한다.
    ```
 

2. 머신러닝 관점에서 파라미터와 하이퍼파라미터에 대해서 말씀해주세요

    ```
    정답:

    파라미터: 매개변수라고 생각하면 된다. 모델 내부에서 정의되는 값이다. 예를 들어 선형 회귀에서 다양한 데이터에 의해서 선형 기울기가 선정될 때 그 값은 사용자가 정의한 값이 아닌 모델이 만들어낸 값이다.

    하이퍼파라미터: 사용자가 정의한 값이다. 대표적으로 Learning rate나 SVM의 C의 값이다. 사용자가 직접 정의하는 모든 값이 다 하이퍼파라미터이다. 정확한 값은 없다. 대체적으로 휴리스틱한 접근을 통해서 만들어진다.
    ```
 

3. 알고있는 활성화 함수를 설명해주세요. 또한 활성화 함수를 사용하는 이유는 무엇인가요?
    ```
        정답: 

        sigmoid, tanh, relu, softmax를 알고 있다.
    ```
 

4. XOR 문제를 어떻게 해결할 수 있나요?(손으로 그려보세요)
    ```
    ```
 

5. Overfitting을 방지하기 위한 방법에 대해서 아는대로 설명해주세요

    ```
    정답:
    nomalization, dropout 기법을 사용할 수 있습니다.
    ```

 

6. Convolution neural network에 대해서 layer 별로 설명해주세요
    ```
    ```

 
7. softmax 함수는 무엇이고, 언제 사용하나요?
    ```
    정답

    여러 종류의 피쳐에 대한 값을 큰 값은 더 크게, 작은 값은 상대적으로 더 작게 만들어주는 역할을 합니다.

    softmax를 거치면 결과의 총합이 1이 되는 연산입니다.
    ```
 

8. OnehotEncoding은 언제 사용하나요?

    ```정답
    범주형 데이터에 대한 학습을 진행할 때 보통 사용합니다.
    ```

 

9. epoch과 batch에 대해서 설명해주세요

    ```
    상황: 1만개의 데이터를 처리하는 batch단위가 1000개이고 epoch 값이 50이다.

    이 경우에 학습의 흐름이 어떻게 진행되나요?
    ```

 
10. Gradient Vanishing 문제가 무엇이고, 어떻게 해결할 수 있나요?

    ```
        정답: 큰 범주의 데이터셋을 0~1 사이의 작은 범주르 꾸겨넣기 작업을 여러번 하기 때문에 기울기 값이 사라지는 문제이다. 해결방법은 normalization, 활성화함수를 sigmoid -> relu로 바꾸면서 해결할 수 있다.

        sigmoid는 모든 값을 0~1 사이의 값으로 넣어주어서, 해당 연산을 계속하게되면 기울기가 0의 방향으로 수렴하는 문제가 발생한다. 이후 최초 입력값에 대해서 출력값이 거의 영향을 받지 않게 된다. 그래서 relu 연산으로 사용한다. relu는 max(0,x)를 의미한다. 값이 0 이상이 될 수도 있다.
    ```

 
11. Nomalization 하는 이유는?
    ```
    인풋의 범주가 정규화 되어있지 않으면 learning rate를 작게 해야 학습이 진행된다.
    ```

12. 머신러닝과 딥러닝의 차이점은?
    ```
    ```

13. 머신러닝을 3가지로 분류한다면?
    ```
    ```
14. Cross validation이란?
    ```
    ```

15. gradient descent에 대해서 가능한 자세하게 설명한다면?
    ```
    ```

16. 모델의 성능 평가 지표에는 무엇이 있는가?
    ```
    ```

17. 하이퍼파라미터 튜닝은 어떻게 할 수 있을까?
    ```
    ```

18. normalization과 regularization의 차이는?
    ```
    ```

19. batch normalization이란? 어떻게 동작하는가?
    ```
    ```

20. Max Pooling을 하는 이유는?
    ```
    ```

21. Global Average pooling이란?
    ```
    ```
22. SVM이란?
    ```
    ```
23. overfitting이란?
    ```
    ```
24. CNN의 장점은?
    ```
    ```

25. 로지스틱 회귀란? 언제 로지스틱 회귀를 사용할 수 있을까?
    ```
    ```

26. Local Minima를 해결하는 방법은?
    ```
    ```

27. gradient vanishing이 생기는 이유는? 이를 해결할 수 있는 방법은 무엇이 있을까?
    ```
    ```

    


 

 - 출처: https://datacodingschool.tistory.com/106
 - https://butter-shower.tistory.com/184