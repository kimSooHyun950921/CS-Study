1. 데드락이 뭔지 설명해주세요

2. 데드락이 왜발생하나요?

3. 데드락을 예방할수 있는 방법이 있을까요?

4. 기아상태와 경쟁상태의 차이는 무엇을까요?

5. 경쟁상태와 데드락의 차이는 무엇인가요?

6. 멀티프로세싱이나 멀티스레드 환경에서 에서 생길 수 있는 문제점은 무엇일까요? 

7. 경쟁상태가 언제 발생하나요?

8. 경쟁상태가 발생할 수 있는것을 실제 예제(프로그램언어등)에서 설명해주세요

8. 경쟁상태를 예방할 수 있는 방법이 어떤것이 있나요?

9. 경쟁상태를 예방할 수 있는 알고리즘을 설명해주세요

10. 아래의 코드를 실행하면 어떻게 나오나요? 
정상적으로 실행하려면 어떻게 바꿔야할까요?
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

