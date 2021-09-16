# 1. Tcp /ip 흐름제어 (수현)
## 1.1TCP 3 & 4 way Hand Shake
1. TCP 연결할때 어떻게 연결이되는지 SYN과 ACK 관계로 설명해주세요.
    ``` 
    1. 클라이언트가 서버에게 SYN 플래그를 보냄(seq:1이라 가정)
    2. 서버는 클라이언트에게 SYN에대한 응답으로 ACK를 보냄과동시에 그후 연결초기화를 위한 SYN을 같이전송함(ack: 는 seq를 잘받았다는 의미로 2를 보냄, seq는 임의의숫자 10을보냄)
    3. 클라이언트는 SYN에대한 응답으로 ACK보냄
    ``` 
2. FIN WAIT1과 FIN WAIT2의 상태는 언제보이나요?
    ```
    FIN_WAIT1: 클라이언트가 FIN 플래그를 전송할때(ACK응답 못받았을때)
    FIN_WAIT2: 클라이언트가 FIN 플래그 전송에대한 ACK을 받았을때(ACK에대한 FIN 응답을 못받았을때)

    ```
3. passive close와 active close에 대해서 설명해주 세요. 
    ```
    active_close: FIN을 먼저 보내는쪽
    passive_close FIN Flag를 받는쪽
    ```
## 1.2 TCP/IP 흐름제어 혼잡제어
1. TCP 통신의 특징을 말씀해주세요
    ```
    1. 신뢰성이 있는 연결
     - 손실, 순서바뀜, 중복 ACK등이 없도록 보장함
    ```
2. TCP 통신이 가능하게 하는 TCP 대표적 기능이 무엇일까요?
    ```
    흐름제어, 혼잡제어
    ```
3. 흐름제어에 대해 설명해주세요
    ```
    송수신의 속도차이를 해결하기 위한 방법
    송신자가 수신자가 읽어들이는것에비해 너무 빠르면 수신자의 버퍼가 overflow난다. 이를 해결하는 법
    해결법: 
        - datalink층에서 해결법: stop-and -wait, go-back-N
        - datalink가 아닌곳에서 해법: receive window size를 전송해서 해결 가능한 만큼만 보내느 방법
    ```
2. 혼잡제어에 대해 설명해주세요.
    ```
    - packet 충돌등으로 패킷이 손실이나 잘못된 패킷이 왔을때에대해 전송 크기를 조절하여 전송하는것
    - Timeout, 중복 ACk감지시 혼잡자에 알고리즘 사용
    - 혼잡윈도(cwnd) 를 사용함
    - slow start: 2의 지수만큼 증가됨
    - 혼잡회피: cwnd=i인 느린시작임계치에 도달하면 혼잡 윈도 1씩 만증가
    - reno, cubic등이 혼잡제어 알고리즘에 속함
    ```
# 2. Udp 대칭키 공개키

# 3. Blocking non blocking 
1. Blocking과 non blocking에 대해서 설명해주세요. 
    ``` 
    1. Blocking : 함수 B는 내 할 일을 다 마칠 때까지 제어권을 가지고 있는다. A는 B가 다 마칠 때까지 기다려야 한다.
    2. Non-blocking : 함수 B는 할 일을 마치지 않았어도 A에게 제어권을 바로 넘겨준다. A는 B를 기다리면서도 다른 일을 진행할 수 있다.
    ``` 
2. Synchronous/Asynchronous에 대해서 설명해주세요. 
    ```
    Synchronous : 함수 A는 함수 B가 일을 하는 중에 기다리면서, 현재 상태가 어떤지 계속 체크한다.
    Asynchronous : 함수 B의 수행 상태를 B 혼자 직접 신경쓰면서 처리한다. (Callback)

    ```
3. Blocking I/O 와 Non-Blocking I/O의 차이를 설면해주세요. 
    ```
    I/O 작업이 진행되는 동안 user Process(Thread) 는 자신의 작업을 중단한 채 대기.
    Non-Blocking I/O 작업이 진행되는 동안 User Process의 작업을 중단하지 않음.

# 4. Http 로드밸런싱