### 1주차 학습할 것

#### 공통 피드백

- 내용 정리시 이미지를 그냥 복사 하는 경우
- 그림은 직접 그려보는게 좋다
- 정 복잡한 그림이면 출처를 남기자
- 글은 되도록 인용하지 말 것
- 내용은 본인이 이해한대로 다시 적어야 한다
- 다른 사람의 과제 해결 내용을 볼 것 (서로 공부한 깊이가 다 다르다)

- [JVM](https://media.geeksforgeeks.org/wp-content/uploads/jvm-3.jpg) (출처: geeksforgeeks)

#### JVM이란 무엇인가

- Java Virtual Machine
- Java를 OS에 관계없이 실행해주는 프로그램 (cli: java app)
- JVM 자체는 OS에 종속적이다(Mac용 따로 Window용 따로..)

#### 컴파일 하는 방법

- 하위 버전에서 컴파일된 바이트 코드는 상위버전에서 실행 가능
- 상위 버전에서 컴파일된 바이트 코드는 하위버전에서 실행이 안된다
- (UnsupportedClassVersionError: XXX has been compiled by a more recent version of the Java Runtime...)
- 하지만 자바 컴파일시 옵션이 있다
- javac --help (자세한 옵션)

#### 실행하는 방법

- ../dir ~/Library/Java/JavaVirtualMachines/.../home/bin/java -source 1.8 -target 1.8
- 스프링 / 스프링 부트 등 프레임워크에서는 최소한의 버전 설정이 있다
- 일부 maven 플러그인 중에 호환 없이 그대로 컴파일되는 경우가 있다
- 기타 자바 관련 콘솔 명령
- javap : 디스어셈블러
- jdb : 디버거

#### 바이트코드란 무엇인가

- .java -> (javac) -> .class -> (jvm) -> process
- 바이트코드는 JVM 같은 가상머신이 이해할 수 있는 코드 (.class)
- (바이너리코드 : CPU가 이해할 수 있는 코드)

#### JIT 컴파일러는 무엇이며 어떻게 동작하는지

- java를 가지고 실행할 시점에 인트프리트 방식으로 (line by line) 변역 +
- 바이트코드를 기계어로 번역하여 실행
- JIT과 인터프리터는 동시에 실행 (JIT 스레드가 따로 돌고 있다)
- 코드 중 반복되는 코드라 판단되면 JIT 컴파일러가 기계어로 미리 캐싱 해놓고 반복하여 실행
- 중복해서 번역하는 비효율을 방지하기 위함

#### JVM 구성 요소

- [JVM구조](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FGhnRV%2FbtqB9Y0Ax1V%2FsnKN7iK04XGZXySMpujhWK%2Fimg.png) (출처: https://dailyheumsi.tistory.com/196)

##### 1. Class Loader : 바이트코드를 읽어서 메모리에 배치

- 로딩 : .class 읽어옴
- 링크 : 코드 내부 레퍼런스를 연결
- 초기화 : 클래스에 있는 static 값들 초기화

##### 2. Run time areas

- JVM이 프로그램을 수행하기 위해 OS로부터 별도로 할당받은 메모리 공간

- 메소드 : 클래스와 인터페이스의 정보를 처음 메모리에 올릴 때 초기화 되는 대상을 저장하기 위한 공간
- (클래스, 인터페이스, 메소드, 필드, static 변수 등)

- 힙 : 런타임시 동적으로 할당하여 사용되는 영역

- 스택 : 인스턴스 및 지역 변수 참조 주소들 저장
- (쓰레드마다 런타임 스택을 만들고, 스택 프레임을 쌓음)

- PC register : 스레드가 실행될 때 생성되는 공간으로 스레드마다 하나씩 존재
- (스레드가 어떤 부분을 어떤 명령으로 실행해야 할 것인가에 대한 것을 기록하는 부분)

- Native method stack : Java가 아닌 다른 언어로 작성된 코드를 위한 공간
- (바이트코드가 아닌 실제 수행할 수 있는 기계어로 작성된 프로그램을 실행시키는 영역)

##### 3. Execution Engine

- interpreter : 컴파일된 .class 바이트코드를 실행하는 역할

- JIT compiler

- GC : 더 이상 참조되지 않는 데이터를 알아서 정리(메모리 해제 free())

##### 4. Native Method Interface

#### JDK와 JRE의 차이

- JRE는 런타임에 필요한 것
- JDK는 JRE + (개발에 필요한 도구)
