##  Thread

### 1.1 안드로이드에서의 스레드

스레드란 쉽게 말해 여러작업을 같이 하기 위한 기능이라고 생각하면 된다. 예를 들어 음악을 들으면서 SNS를 할 수 있는 것처럼 말이다.

어플리케이션은 성능향상을 위해 멀티 스레드를 많이 사용하지만, UI를 업데이트 할 때는 단일 스레드 모델이 적용된다. 멀티 스레드로 UI를 업데이트 하면 동일한 UI자원을 사용할 때 *교착 상태, *경합 상태 등 여러 문제가 발생할 수 있다. 따라서 UI업데이트는 메인스레드에서만 허용한다.

######  

### 1.2 Thread, 왜 사용해요?

메인스레드 만으로 구현하게 된다면, 사용자는 해당 작업이 끝날 때까지 멈춰있는 화면을 보고만 있어야한다. 오랜 시간동안 UI관련 작업이 처리되지 못하면 결국 *ANR 에러가 발생한다. 그러면 어플리케이션은 정지된다.

안드로이드 3.0 버전부터 통신 클래스 내 전송이나 수신과 관련된 메소드는 메인 스레드에서 사용하지 못하도록 의도적으로 막아버렸다.

 EX) 메인 스레드에서 소켓클래스의 conntect() 메소드를 호출하면 'NetworkOnMainThreadException' 이 발생한다.

위와같은 네트워크 통신기능이나 데이터 검색, 빈번하게 사용하는 파일의 로드과 같이 시간이 걸리는 작업들은 사용자가 기다리지 않도록 하기 위하여 여분의 스레드를 사용해야 한다. (멀티스레드)

안드로이드 앱을 제대로 개발하기 위해서는 멀티 스레드를 이용하는 것은 필수적이라 할 수 있다.

### 1.3 Thread, 직접 만들어보자

스레드를 구현하는 방법은 2가지가 있다. 하나는 **Thread**를 이용하는 것이고, 나머지 하나는 **Runnable**을 이용하는 것이다.

#### 1.3.1 Thread를 상속받아 구현하기

```kotlin
public class TaeiimThread extends Thread {
    @Override
    public void run() {
        super.run();
        // Do something..
    }
}
// 스레드 실행
TaeiimThread thread = new TaeiimThread();
thread.start();
```

#### 1.3.2. Runnable 인터페이스 구현

Runnable 인터페이스를 상속받은 후, run() 메소드에 원하는 작업을 하도록 구현하면 된다.

완성된 클래스를 생성한 후, Thread 클래스의 생성자에 인수로 전달한다.

```kotlin
public class TaeiimRunnable implements Runnable {
    @Override
    public void run() {
        // Do something,, 
    }
}
// 사용하기 
TaeiimRunnable myRunnable = new TaeiimRunnable();
Thread thread = new Thread(myRunnable);
thread.start();
```

#### 1.3.3. Thread VS. Runnable

Thread와 Runnable 은 몇가지 차이점이 있다.

1. **Thread는 상속(Extends)을 받는 것이며 Runnable은 인터페이스**로서 구현하는 것이 큰 차이점이다.

   자바는 다중 상속이 불가능하기 때문에 Thread를 상속받게 되은 클래스는 다른 클래스를 상속 받을 수가 없지만 Runnable은 인터페이스이기 때문에 implements만 하면 되고 다른 필요한 클래스를 상속 받을 수 있다.

2. **Thread는 재사용 불가능, Runnable 가능**

   스레드는 일회용이다. 따라서 한 번 사용한 스레드는 재사용할 수 없다. 재사용시 'IllegalThreadStateException' 이 발생한다. 즉, 하나의 스레드에 대해 start()가 한 번만 호출될 수 있다. 하지만, Runnable로 구현한 경우 재사용 가능하다.

**용어정리**

###### * 교착상태(dead lock): 두 개 이상의 작업이 서로 상대방의 작업이 끝나기 만을 기다리고 있기 때문에 결과적으로 아무것도 완료되지 못하는 상태

###### * 경합상태(race condition) : 두 개 이상의 프로세스가 공통 자원을 병행적으로 읽거나 쓸 때, 공용데이터에 대한 접근이 어떤 순서에 따라 이루어졌는지에 따라 그 실행 결과가 달라지는 상황

###### * ANR : 안드로이드에서는 어떤 작업을 요청하고 5초간의 응답이 없을 때 강제종료 여부를 묻는 다이얼로그를 발생시킨다. 이 다이얼로그를 **ANR**(Application not responding) 메시지 라고 한다.