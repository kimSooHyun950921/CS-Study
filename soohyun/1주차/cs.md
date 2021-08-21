1. 멀티프로세싱이나 멀티스레드 환경에서 에서 생길 수 있는 문제점은 무엇일까요? 
    ```
    1. 경쟁상태가 발생 할 수 있음(자원이 다르게 변경될 수 있음) - 자원공유에대한 문제
    2. 데드락: 프로세스들이 자원을 할당받지못해 실행되지 못하는 상태
    ```

2. 데드락이 뭔지 설명해주세요
    ```
    프로세스나 스레드가 서로 자원을 가지고 놓지 않아 다음상태로 전이되지 못하는 상태
    ```
    ```c
    /* thread one runs in this function */
        public void *do work one(void *param){
            pthread mutex lock(&first mutex);
            pthread mutex lock(&second mutex);
            /**
            * Do some work
            */
            pthread mutex unlock(&second mutex);
            pthread mutex unlock(&first mutex);
            pthread exit(0);
            }
            /* thread two runs in this function */
            void *do work two(void *param)
            {
            pthread mutex lock(&second mutex);
            pthread mutex lock(&first mutex);
            /**
            * Do some work
            */
            pthread mutex unlock(&first mutex);
            pthread mutex unlock(&second mutex);
            pthread exit(0);
        }
    ```
3. 데드락이 왜발생하나요?
    ```
    - 아래 4가지 상황이 동시다발적으로 생성되면 발생할 수 있음
    1. 상호배제: 하나의자원은 한번에 하나의 프로세스 혹은스레드가 쓸 수 있을때
    2. Hold & Wait: 스레드가 하나의 자원을 붙잡고있는 상태에서 다른 자원을 얻으려고 하는 상태
    3. 비선점: 자원은 프로세스자체가 자발적으로 놓아주어야 하는경우(선점되지 않고)
    4. 순환 기다림: T0는 T1의 자원을 기다리고 있고 T1은 T2의 자원을 기다리는 형태로 순환적으로 프로세스가 각자원을 기다리는 경우

    ```

4. 데드락을 예방할수 있는 방법이 있을까요?
    ```
    1. 안전상태
    - 데드락이발생되지 않는 안전한 프로세스 실행 순서만들기
    2. 자원 할당 그래프알고리즘
    3. 은행원 알고리즘
        - 자원의 할당 여부를 결정하기 전에 미리 결정된 자원의 최대가능한 할당량을 시뮬레이션하여 안정상태의 여부를 검사한다. 대기중인 모든 활동의 교착상태 가능성을 조사하여 "안정상태" 여부를 검사확인하는 방법."
        출처: https://hoyeonkim795.github.io/posts/bankers/
    ```
    ```
    데드락을 다루는방법
    1. 데드락이 결고 발생하지 않는다고 가정하고 무시하기
        - 윈도우/리눅스같은 OS에서 사용됨
    2. 회피하거나 예방하는 프로토콜만들기
        - 커널개발자/애플리케이션 개발자들이 구현
        - 데드락회피방법:
            - 
        - 데드락 예방: 데드락 발생조건 4가지중 하나만 성립안하면됨
            - 상호배제: 공유가능하게 만든다(read-only), mutex-lock은 불가능
            - Hold&Wait: 다른 자원이 필요할때는 지금 가지고 있는자원을 해제하도록해야함
            기아상태를 가질수있고, 자원 유용성이 낮음
            - 비선점: 잡고있는자원을 암시적으로로 해제시킴
            - 순환대기: 임의의 자원을 요구하도록 함, 무조건 자기보다 작은 번호의 자원을 요구하도록함 
    3. 데드락 상태를 허락하고 탐지후 회복하는방법
        - 데이터베이스와같은 일부시스템에서 채택
    ```
5. 기아상태와 경쟁상태의 차이는 무엇을까요?
    ```
    - 경쟁상태: 같은데이터를 동시에 조작하여 순서에따라 다른결과가 나오는 상태 (동기화되지 않음) - 자원공유할때 나오는문제
    - 기아상태: 프로세스가 자원을 할당받지 못하는상태(프로세스 스케줄링)
    ```

6. 경쟁상태와 데드락의 차이는 무엇인가요?
    ```
    경쟁상태는 공유하는자원을 서로다른 프로세스가 변경하는 문제이고,
    데드락은 서로다른 프로세스가 자원을 할당받지 못하는 상태일때 상기는 문제이다.
    ```


7. 경쟁상태가 발생할 수 있는것을 실제 예제(프로그램언어등)에서 설명해주세요
    ```
    텍스트파일을 변경하려고할때 같은내용을 하나는 2로, 하나로 3으로 변경하려하면 실행순서에따라 결과는 2가되기도 하고 3이되기도한다.
    ```
8. 경쟁상태를 예방할 수 있는 방법이 어떤것이 있나요?
    ```
    세마포어와 뮤텍스, 모니터방법등이 있다.
    ```
9. 세마포어와 뮤텍스의 차이점은 무엇일까요?
    ```
    1. semapore: 이진세마포어가 mutex처럼 사용된다. 동시에 사용한 프로세스숫자를 s로하고 숫자를 하나씩 줄여가면서 숫자가 0이되면 대기한다(wait) 프로세스가 완료되면 s를 하나씩 증가시킨다.
    2. mutex: 단순히 critical section에 lock을 걸어 다른 프로세스가 진입하지 못하게하는것
    ```
10. 아래의 코드를 실행하면 count 값은 어떻게 나오나요? 
    ```java
    class Counter {
    int count=0;
    Counter() {
        Thread thread1 = new Thread(new Runnable() {
        @Override
        public void run() {
            count();
        }      
        });
        Thread thread2 = new Thread(new Runnable() {
        @Override
        public void run() {
            count();
        }      
        });
        thread1.start();
        thread2.start();
    }

    void count() {
        for(int i=0; i<100000; i++) {
        count++;
        }
    }
    }
    ```


    ``` 
    20000보다 작은 결과가 나온다.
    ```

11. 정상적으로 실행하려면 어떻게 바꿔야할까요?
    ```
    count를 하는곳에  lock을 걸어야합니다.
    자바 문법으로는 synchronized를 이용하거나, 스레드안전성 객체인 concurrent패키지를 이용하거나, immutable 객체로 만들면됩니다. 
    ```


