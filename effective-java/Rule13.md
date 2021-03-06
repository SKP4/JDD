#Rule13. 클래스와 멤버의 접근권한은 최소화하라.
잘설계된 모듈과 그렇지 못한 모듈을 구별 짓는 가장 중요한 속성 하나는 모듈 내부의 데이터를 비롯한 구현 세부사항을 다른 모듈에 잘 감추느냐의 여부
-> 잘 설계된 모듈은 구현 세부사항을 전부  API뒤쪽에 감춘다. 정보은닉과 캡슐화라는 용어로 알려져 있음

정보은닉 : 의존성을 낮춰서, 각자 개별적으로 개발하고 시험하고 최적화하고 이해하고 변경할 수 있도록 한다는 사실에 기초함
개발 속도가 높아짐. 각각의 모듈을 병렬적으로 개발할 수 있기 때문
효과적인 성능 튜닝이 가능
프로파일링이 용이함
소프트웨어의 재사용 가능성이 높아짐
다른 소프트웨어 개발에도 유용하게 쓰일 수 있음

접근제어 메커니즘은 클래스와 인터페이스, 그리고 그 멤버들의 접근권한을 규정함
해당  개체가 선언된 위치와 권한 수정자에 의해 결정됨
원칙 : 각 클래스와 멤버는 가능한 한 접근 불가능하도록 만들기

최상위 레벨 클래스와 인터페이스에 부여할 수 있는 접근 권한은 package-private와 public 두가지다.
public:  전역적 개체가 된다.
public을 안붙이면: 해당 패키지 안에서만 유효
최상위 레벨 클래스나 인터페이스는 가능한 package-private로 선언해야 함
-> API의 일부가 아니라 구현 세부사항에 속하게 되므로, 다음번 릴리스에 클라이언트 코드를 깨뜨릴 걱정 없이 자유로이 변경하거나 삭제하거나, 대체할 수 있다.

최상위레벨 package-private클래스의 접근 권한을 낮추는 것보다 public 클래스의 접근권한을 낮추는 것이 더 중요.
최상위 package-private클래스는 이미 구현 세부사항일 뿐이지만, public클래스는 해당 패키지 API의 일부이기 때문.

+ pirave : 최상위 레벨 클래스 내부에서만 접근이 가능
+ package-private: 같은 패키지 내의 아무 클래스나 사용할 수 있다.
+ protected : 선언된 클래스 및 그 하위 클래스만 사용
+ public: 어디에서도 사용이 가능

메서드의 접근 권한을 줄일 수 없는 경우 :  상위 클래스 멤서드를 재정의할 때는 원래 메서드의 접근 권한보다 낮은 권한을 설정할 수 없다.

객체 필드는 절대로 public으로 선언하면 안됨
-> 비-final필드나 변경가능 객체에 대한 final참조 필드를 public으로 선언하면, 필드에 저장될 값을 제한할 수 없게 됨

변경가능 public필드를 가진 클래스는 다중 스레드에 안전하지 않다.
-> 필드가 변경될 때 특정한 동작이 실행되도록 할수 없기 때문

public static final배열 필드를 두거나, 배열 필드를 반환하는 접근자(accessor)를 정의하면 안됨
->길이가 0이 아닌 배열은 언제나 변경이 가능하기 때문
