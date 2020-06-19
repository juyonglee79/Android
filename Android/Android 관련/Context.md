# Context



## 1. context 란?

> Interface to global information about an application environment. This is an abstract class whose implementation is provided by the Android system. It allows access to application-specific resources and classes, as well as up-calls for application-level operations such as launching activities, broadcasting and receiving intents, etc.
>
> 어플리케이션 환경에 관한 글로벌 정보를 접근하기 위한 인터페이스. Abstract 클래스이며 실재 구현은 안드로이드 시스템에 의해 제공된다. Context 를 통해, 어플리케이션에 특화된 리소스나 클래스에 접근할 수 있을 뿐만 아니라, 추가적으로, 어플리케이션 레벨의 작업 - Activity 실행, Intent 브로드캐스팅, Intent 수신 등, 을 수행하기 위한 API 를 호출 할 수도 있다.

Context  는 크게 두 가지 역할을 수행하는 Abstract 클래스다.

- 어플리케이션에 관하여 시스템이 관리하고 있는 정보에 접근하기 

- 안드로이드 시스템 서비스에서 제공하는 API 를 호출 할 수 있는 기능

  

인터페이스가 제공하는 API 중, getPackageName(), getResource() 등의 메서드들이 첫 번째 역할을 수행하는 대표적인 메서드입니다. 보통 get 이라는 접두어로 시작하는 메서드이다. 그 외에, startActivity() 나 bindService() 와 같은메서드들이 두 번째 역할을 수행하기 위한 메서드라고 할 수 있습니다.



## 2. context 타입

### Application

실행중인 어플리케이션 프로세스는 Singletone instances 이다.
Activity이나 Service에서는 getApplication() 메소드를 통해 getApplicationContext()로 Context를 얻어 올 수 있다.
프로세스내 동일한 instanees를 받게 된다.

### Activity/Service

ContextWrapper를 상속받아 구현한 Context이며 메소드로 Context를 얻어 오면 기본 Context로 구성되어 있다.
프레임워크는 Activity또는 Service가 실행 될때 기본 Context에다 필요한 정보를 warp한다.
실행시 고유한 Context를 가지게 된다.

### BroadcaseReceiver

위의 2가지와 다르게 자기자신이 Context자체는 아니다.
하지만 onRecevie()시 Context를 가져올 수 있는데, 이때의 Context는 ReveiverRestrictedContext이며 두가지 기능 registerReceiver()와 bindService()를 사용 할 수 없다.
리시버가 브로드캐스트를 처리 할때마다 새로운 Context가 생성 된다.



## 3. context 종류

### LoginActivity.this

LoginActivity.this 는 Acitivity를 상속받은 자신의 클래스를 참조하지만 Activity 또한 Context class를 상속받으므로 activity context를 제공하는데 사용될 수 있다.

### getApplication()

getApplication()은 Application 객체를 참조하지만 Application 클래스는 Context 클래스를 상속받으므로 application context를 제공하는데 사용될 수 있다.

### getApplicationContext()

getApplicationContext()는 application context를 제공한다.

### getBaseContext()

getBaseContext()는 activity context를 제공한다.

