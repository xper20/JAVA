# JAVA의 특징
1. 쉽다 => API
2. OOP => 재사용성(캡슐화, 추상화(정보 은닉화), 상속, 다형성)
3. JVM(자바 가상머신)이 있어서 어떤 OS라도 사용가능하다.
4. 멀티 Thread를 제공한다
5. Memory(가비지 컬렉션)

# POJO(Plan Old Java Object)
- 순수한 값만을 가진 Object
- 상속 받지 않는다.
- 기본 생성자만을 사용한다.
- 값만을 위한 기능만을 가지고 있다.
- UML과 DI시키지 않는다.
- Setter / Getter
- 특정 자바 모델이나 기능, 프레임워크 등을 따르지 않는 자바 오브젝트를 지칭하는 말로 대표적으로 스프링 프레임워크가 있다.

# 메모리 JVM
- Stack　: 지역변수, 메소드 실행	=> 가벼운 공간이라 사용 후 바로 삭제
- Heap 　　: 생성된 객체		=> 가비지 컬렉션이 삭제해줌

>String 객체에 경우
<pre><code>String msg = "ABC"; 
msg += "DEF"; 
msg += "ZZZ"; 
System.out.println(msg);</code></pre>
100번지 : "ABC" + 200번지 : "DEF"
300번지 : “ABCDEF"
 
따라서 String 객체 같은 경우는 Heap 영역에 무리가 갈 수 있기 때문에 대입 연산자 같은 경우는 사용하지 않는 편을 추구한다.
때문에 StringBuffer 객체로 문자열을 안전하게 저장하여 무리가 가지 않게 한다.

<pre><code>for(int i = 0; [    ] ; i++) </code><pre>
- [    ] 안에는 ar.lenth를 사용하는 것을 권장하지 않는다.(배열의 크기값이 바로 보여지기 때문에)
- 자바5부터는 for(int i;    ; ar)로 쓰면 자동적으로 비교하기 때문에 .lenth 메서드를 쓰는 것이 아니라 효율적으로 연산 가능하다.(향상된 for문)

# 접근 제한자
- public : 모든 클래스에서 접근 가능
- protected: 자식 클래스에서만 접근 가능
- default : 같은 패키지에 소속된 클래스(정말 디폴트가 자료형이 아니고 말 그대로 아무것도 명시하지 않으면 기본적으로 적용되는 속성) 
- private : 모든 클래스에서 접근이 불가능하지만 내부 클래스에서는 접근이 가능하다.( 정보 은닉화 대표적인 예)

# 참조 관계
- Has ‘ a 관계 : 하나의 클래스를 다른 클래스가 사용하기 위해서 주소를 참조하는 관계
- Association (연관관계) : A가 B의 주소를 멤버필드에서 참조하는 관계 , 메서드로 B의 주소값을 인자값으로 전달 받는 형태 (CallByReference : 주소를 인자로 전달 받는 방식)
<div>
 <img src="https://user-images.githubusercontent.com/39404179/49274345-637d0700-f4bb-11e8-95f2-3f71da84fa09.png">
</div>
