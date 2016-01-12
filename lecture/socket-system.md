# 소켓 시스템  

## 네트워크 프로그래밍  
- 일반적으로 클라이언트-서버 모델은 네트워크 서비스를 제공하는 서비스 제공자와 서비스 이용자 사이의 관계를 표현  
  - 여기서 서비스를 제공하는 프로그램을 서버 프로세스, 서버와 연결을 시도해 서비스를 제공받는 프로그램을 클라이언트 프로세스라고 한다.  
  
### 연결형 서비스  
- 소켓  
  - 네트워크 통신을 위한 소프트웨어 교신점  
  - 두 개의 독립 프로세스가 네트워크를 통해 통신하려면 논리적인 연관 관계를 맺어주는 소켓이 필요  

#### 서버의 동작  
- 서버 프로세스는 다수의 클라이언트에게 제공되는 Well-known 포트로 자신의 소켓 주소를 설정한 후에 클라이언트의 연결 요청에 대기  
- 클라이언트 요구에 따라 연결이 설정되면 서버 프로세스가 제공하는 서비스가 시작  
- 서버 프로세스의 동작은 여러 클라이언트들에게 반복적으로 이루어짐  
- 서버의 동작 과정  
  - 서비스 교신점(호스트의 IP 주소, 포트 번호) 공개
  - 클라이언트로부터 발생하는 서비스 요구 대기
  - 클라이언트에 서비스 제공
  - 해당 클라이언트에 서비스 제공 완료
  - 2단계로 이동  

#### 클라이언트의 동작  
- 원하는 서비스를 제공하는 서버 확인  
- 해당 서버와 연결 시도  
- 서버에 서비스 요청  
- 서버에 서비스 요구 완료  

![TCP를 이용한 통신 절차](http://dbscthumb.phinf.naver.net/3578_000_1/20141023224533900_KC1PW3WD1.jpg/ka8_174_i1.jpg?type=w431_fst&wm=N)  

### 비연결형 서비스  
- 비연결형 서비스에서는 connect()와 accept() 함수로 연결을 설정하는 과정이 생략  
- 데이터 송수신을 위한 send(), recv() 함수 대신, sendto(), recvfrom() 함수를 사용  
- 전송 데이터마다 수신자의 포트 번호를 함께 전송  

![UDP를 이용한 통신 절차](http://dbscthumb.phinf.naver.net/3578_000_1/20141023224536183_HL3QYYF5A.jpg/ka8_175_i1.jpg?type=w431_fst&wm=N)  


## 요약  
1. 프로세스 사이의 통신을 지원하는 포트 주소는 프로토콜의 종류에 따라 달라진다. 대표적인 예는 호스트 내부의 프로세스끼리 통신하는 유닉스 도메인과 서로 다른 호스트 사이에서 통신하는 인터넷 도메인이다.

2. socket() 함수로 소켓을 생성하고, bind() 함수로 소켓 주소를 부여할 수 있다.

3. TCP를 사용하려면 connect()와 accept() 함수를 이용해 연결을 설정하고, send()와 recv() 함수를 이용해 데이터를 송수신한다.

4. 비연결형 서비스를 제공하는 UDP에서는 sendto()와 recvfrom() 함수를 사용해 데이터를 송수신한다.

5. 호스트 주소 INADDR_ANY는 서버 프로세스가 실행되는 호스트의 IP 주소를 의미한다.

6. IP 주소와 포트 주소의 표현과 관련해 프로그램 개발 환경에서 개발자에게 다양한 변환 함수를 제공한다.

7. 클라이언트-서버 모델에서 서버 프로세스는 클라이언트보다 먼저 실행되어 accept() 함수에서 대기하고, 클라이언트 프로세스의 connect() 함수와 만나 연결이 설정된다.