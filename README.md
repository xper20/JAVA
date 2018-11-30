# JAVA의 특징
1. 쉽다 => API
2. OOP => 재사용성(캡슐화, 추상화(정보 은닉화), 상속, 다형성)
3. JVM(자바 가상머신)이 있어서 어떤 OS라도 사용가능하다.
4. 멀티 Thread를 제공한다
5. Memory(가비지 컬렉션)

# POJO(Plan Old Java Object)
- 순수한 값만을 가진 Object
- 특정 자바 모델이나 기능, 프레임워크 등을 따르지 않는 자바 오브젝트를 지칭하는 말로 대표적으로 스프링 프레임워크가 있다.

# 메모리 JVM
- Stack　: 지역변수, 메소드 실행	=> 가벼운 공간이라 사용 후 바로 삭제
- Heap 　　: 생성된 객체		=> 가비지 컬렉션이 삭제해줌

>String 객체에 경우<
<pre><code>String msg = "ABC"; 
msg += "DEF"; 
msg += "ZZZ"; 
System.out.println(msg);</code></pre>
100번지 : "ABC" + 200번지 : "DEF"
300번지 : “ABCDEF"
 
따라서 String 객체 같은 경우는 Heap 영역에 무리가 갈 수 있기 때문에 대입 연산자 같은 경우는 사용하지 않는 편을 추구한다.
때문에 StringBuffer 객체로 문자열을 안전하게 저장하여 무리가 가지 않게 한다.
