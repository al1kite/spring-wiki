# 좋은 객체 지향 설계의 5가지 원칙(SOLID)

## SOLID
클린코드로 유명한 로버트 마틴이 좋은 객체 지향 설계의 5가지 원칙을 정리
- SRP: 단일 책임 원칙(single responsibility principle)
- OCP: 개방-폐쇄 원칙 (Open/closed principle)
- LSP: 리스코프 치환 원칙 (Liskov substitution principle)
- ISP: 인터페이스 분리 원칙 (Interface segregation principle)
- DIP: 의존관계 역전 원칙 (Dependency inversion principle)

### SRP 단일 책임 원칙
Single responsibility principle
- 한 클래스는 하나의 책임만 가져야 한다.
- 하나의 책임이라는 것은 모호하다.
  - 클 수 있고, 작을 수 있다.
  - 문맥과 상황에 따라 다르다.
- 중요한 기준은 변경이다. 변경이 있을 때 파급 효과가 적으면 단일 책임 원칙을 잘 따른 것
- 예) UI 변경, 객체의 생성과 사용을 분리

계층 등이 잘 나뉘어져 있는 이유는 단일 책임 원칙을 지키려 함이라고 보면 된다.
범위를 너무 작게 하면 빈이 너무 잘게 쪼개지고 크게 하면 책임이 많아져 단일 책임 원칙이 깨질 수 있기에
이 책임이라는 범위를 적절하게 잘 조절하는 것이 객체 지향 설계의 묘미이다. 
변경이 있을 시 하나의 클래스, 지점만 고치면 단일 책임 원칙을 잘 따르는 것이라 할 수 있다.

### OCP 개방-폐쇄 원칙
Open/closed principle
- 소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다
- 이런 거짓말 같은 말이? 확장을 하려면, 당연히 기존 코드를 변경?
- 다형성을 활용해보자
- 인터페이스를 구현한 새로운 클래스를 하나 만들어서 새로운 기능을 구현
- 지금까지 배운 역할과 구현의 분리를 생각해보자

결국 다형성을 잘 활용하면 개방폐쇄 원칙을 지킬 수 있다.
인터페이스를 구현하는 새로운 클래스를 하나 만드는 건 기존 코드를 변경하는 것이 아니다.
지금까지 배운 역할-구현을 생각해보면 소프트웨어를 확장에는 열려있으나 변경에는 닫혀있게 할 수 있다.

**문제점**
- MemberService 클라이언트가 구현 클래스를 직접 선택
  - MemberRepository m = new MemoryMemberRepository(); //기존 코드
  - MemberRepository m = new JdbcMemberRepository(); //변경 코드
- 구현 객체를 변경하려면 클라이언트 코드를 변경해야 한다.
- 분명 다형성을 사용했지만 OCP 원칙을 지킬 수 없다.
- 이 문제를 어떻게 해결해야 하나?
- 객체를 생성하고, 연관관계를 맺어주는 별도의 조립, 설정자가 필요하다.

클라이언트가 기존 코드를 변경해야 한다는 문제가 발생한다. 이 문제를 해결하려면 별도로 조립해주는 생성자가 필요하고,
이걸 스프링 컨테이너가 해준다. 이 원칙을 지키기 위해 DI, IOC 컨테이너가 필요한 것.

### LSP 리스코프 치환 원칙
Liskov substitution principle
- 프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다
- 다형성에서 하위 클래스는 인터페이스 규약을 다 지켜야 한다는 것, 다형성을 지원하기 위한 원칙, 인터페이스를 구현한 구현체는 믿고 사용하려면, 이 원칙이 필요하다.
- 단순히 컴파일에 성공하는 것을 넘어서는 이야기
- 예) 자동차 인터페이스의 엑셀은 앞으로 가라는 기능, 뒤로 가게 구현하면 LSP 위반, 느리더라도 앞으로 가야함

단순 컴파일 단계를 말하는게 아닌 인터페이스 규약을 맞춰야 한다. 기능적으로 보장을 해줘야 한다는 이야기. 


### ISP 인터페이스 분리 원칙
Interface segregation principle
- 특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다
- 자동차 인터페이스 -> 운전 인터페이스, 정비 인터페이스로 분리
- 사용자 클라이언트 -> 운전자 클라이언트, 정비사 클라이언트로 분리
- 분리하면 정비 인터페이스 자체가 변해도 운전자 클라이언트에 영향을 주지 않음
- 인터페이스가 명확해지고, 대체 가능성이 높아진다

기능을 맞게 적당한 크기로 인터페이스도 쪼개는게 중요하다는 의미. 
덩어리가 작으면 그 기능만 구현하는 그에 맞는 구현체를 구현하기 수월해진다.

### DIP 의존관계 역전 원칙
Dependency inversion principle
- 프로그래머는 “추상화에 의존해야지, 구체화에 의존하면 안된다.” 의존성 주입은 이 원칙을 따르는 방법 중 하나다.
- 쉽게 이야기해서 구현 클래스에 의존하지 말고, 인터페이스에 의존하라는 뜻
- 앞에서 이야기한 역할(Role)에 의존하게 해야 한다는 것과 같다. 객체 세상도 클라이언트가 인터페이스에 의존해야 유연하게 구현체를 변경할 수 있다! 구현체에 의존하게 되면 변경이 아주 어려워진다.

제일 중요한 원칙이 OCP와 DIP. 앞서 이야기한 역할에 의존하라는 것과 같은 의미.
대체 가능성이 있도록 역할과 구현이 철저하게 분리되도록 시스템을 설계해 시스템도 언제든 갈아끼워질 수 있도록 해야한다.

그런데 OCP에서 설명한 MemberService는 인터페이스에 의존하지만, 구현 클래스도 동시에 의존한다.
- MemberService 클라이언트가 구현 클래스를 직접 선택
- MemberRepository m = new MemoryMemberRepository();
- DIP 위반

의존한다는 건 내가 그 코드에 대해 안다 라는 의미. 알기만 하면 다 의존한다 보면 된다.
여기서 MemberService는 MemberRepository 뿐만 아니라 MemoryMemberRepository 까지 알아야 하기에 
다른 걸로 바꾸려 할 때 코드를 변경해야 한다. MemberService 클라이언트가 MemberRepository를 직접 선택하고 있고,
직접 의존하고 있는 것, 이는 DIP를 위반하는 행위이다. 추상화에 의존해야지 구체화에 의존해야 하지만, 추상화와 구체화에
모두 의존하고 있어 DIP를 위반하고 있다.

따라서 MemberService는 MemberRepository 인터페이스에만 의존하도록 설계해야한다.


정리
- 객체 지향의 핵심은 다형성
- 다형성 만으로는 쉽게 부품을 갈아 끼우듯이 개발할 수 없다.
- 다형성 만으로는 구현 객체를 변경할 때 클라이언트 코드도 함께 변경된다.
- **다형성 만으로는 OCP, DIP를 지킬 수 없다.**
- 뭔가 더 필요하다

다형성만으로는 클라이언트의 코드 변경을 막을 수는 없다. 무언가 더 필요한 상황.