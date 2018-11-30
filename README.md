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
- 정보은닉화
- 특정 자바 모델이나 기능, 프레임워크 등을 따르지 않는 자바 오브젝트를 지칭하는 말로 대표적으로 스프링 프레임워크가 있다.

# 메모리 JVM
- Stack: 지역변수, 메소드 실행	=> 가벼운 공간이라 사용 후 바로 삭제
- Heap: 생성된 객체		=> 가비지 컬렉션이 삭제해줌
- 상수풀(전역변수, static변수)
>static
- static 영역 위치
- static 키워드가 붙으면 오직 static 영역에 하나만 생성
	즉, class 내부에서 선언해도 stack과 heap에서는 절대 선언되지 않는다.)
- 생성 없이도 접근이 가능하다. ( heap과는 달라서 선언하지 않아도 됨, 따라서 객체간의 공유가 가능하다.)
<pre><code>class A(){ ... }
	A ref = new A();
	A ref2 = new A();
	ref2 = ref;
 </code></pre>
<div>
 <img width="250px" src="https://user-images.githubusercontent.com/39404179/49274879-084c1400-f4bd-11e8-9f54-7c9d44b4bbec.png">
</div>

>String 객체에 경우
<pre><code>String msg = "ABC"; 
msg += "DEF"; 
msg += "ZZZ"; 
System.out.println(msg);</code></pre>
100번지 : "ABC" + 200번지 : "DEF"
300번지 : “ABCDEF"
 
따라서 String 객체 같은 경우는 Heap 영역에 무리가 갈 수 있기 때문에 대입 연산자 같은 경우는 사용하지 않는 편을 추구한다.
때문에 StringBuffer 객체로 문자열을 안전하게 저장하여 무리가 가지 않게 한다.

<pre><code>for(int i = 0; [    ] ; i++) </code></pre>
- [    ] 안에는 ar.lenth를 사용하는 것을 권장하지 않는다.(배열의 크기값이 바로 보여지기 때문에)
- 자바5부터는 for(int i;    ; ar)로 쓰면 자동적으로 비교하기 때문에 .lenth 메서드를 쓰는 것이 아니라 효율적으로 연산 가능하다.(향상된 for문)

# 접근 제한자
- public : 모든 클래스에서 접근 가능
- protected: 자식 클래스에서만 접근 가능
- default : 같은 패키지에 소속된 클래스(정말 디폴트가 자료형이 아니고 말 그대로 아무것도 명시하지 않으면 기본적으로 적용되는 속성) 
- private : 모든 클래스에서 접근이 불가능하지만 내부 클래스에서는 접근이 가능하다.( 정보 은닉화 대표적인 예)

# 상속
## is'a 관계: extends 키워드를 사용하여 부모 클래스를 자식클래스가 확장하는 관계
<pre>
cf) is a 관계 메모리 구조
 Ex1_B ref = new Ex1_B();   => B ⊃ A
 </pre>
<div><img width="400px" src="https://user-images.githubusercontent.com/39404179/49278649-bf01c180-f4c8-11e8-9940-d88f48c83925.png"></div>
<pre>
this (　) = 현재클래스 내에 같은 생성자를 먼저 불러옴
super( ) = 생성자 안에서 부모클래스의 생성자를 불러옴 
          => 부모클래스 생성 -> 자식 클래스 생성
</pre>
- Has'a 관계: 하나의 클래스를 다른 클래스가 사용하기 위해서 주소를 참조하는 관계(A -> B)
<pre>
cf) has a 관계 메모리 구조
<code> B b = new B();
public class B {
    int bb = 2;
    A aRef;
public B(){
    aRef = new A();  
}
public class A {
    int aa = 10;
}</code></pre>
<div><img width="400px" src="https://user-images.githubusercontent.com/39404179/49278780-1e5fd180-f4c9-11e8-9b81-0a84f8b1c20b.png"></div>
====================================================================================================================================
## Association (연관관계): A가 B의 주소를 멤버필드에서 참조하는 관계 , 메서드로 B의 주소값을 인자값으로 전달 받는 형태 (CallByReference : 주소를 인자로 전달 받는 방식)
<div>
 <img  width="400px" src="https://user-images.githubusercontent.com/39404179/49274345-637d0700-f4bb-11e8-95f2-3f71da84fa09.png">
</div>
## Composition: A와 B라는 클레스가 있을 때 생성자를 새로 생성해서 아예 종속 시켜라
<div>
	<img width="400px" src="https://user-images.githubusercontent.com/39404179/49275976-629aa400-f4c0-11e8-9ddd-3bb04ed6a22f.png">
</div>


## 설계: 자식 클래스에 있는 공통된 기능을 부모 클래스에서 추상화된 개념으로 적는다.
<pre>
ex )　추상화 : drawSomething
   자식클래스의 공통기능이 기본 기능이 됨. (Base)
   Container = 속성을 다 포함하는 기본적인 객체 -> 부모클래스에 있어야 함
 ex)  Circle cir = new Circle();
      Rect rec = new Rect();
      Triangle tr = new Triangle();
</pre>
<div><img width="400px" src="https://user-images.githubusercontent.com/39404179/49279958-3553f300-f4cc-11e8-83ad-de4e4bf95c6b.png"></div>


## 오버라이딩(Overriding)
<pre>
   재정의 ( 자식클래스의 재정의 메서드가 우선 )
   부모의 기능을 자식이 고쳐서 사용
   부모 클래스의 메서드는 이름만 존재
   자식 클래스의 메서드 기능 담당
   [alt][insert] = overriding
   우선권이 자식한테 있음, 자식 꺼가 연산됨
ex) public static void main(String[] args) {
        Ex3_SubCar ref = new Ex3_SubCar();
        Ex3_SuperCar ref = new Ex3_SubCar();
    }
</pre>
<div><img width="400px" src="https://user-images.githubusercontent.com/39404179/49280136-b317fe80-f4cc-11e8-9be9-307e2677cd86.png"></div>
<pre>
=> 자식(SubCar)은 부모(SuperCar), 자식(SubCar) 모두 출력 가능 
   부모(SuperCar)는 부모(SUperCar)만 가능하지만
                    overriding했을 경우 자식의 값(SubCar)을 출력 가능

< Overriding사용하는 이유 >
 = 다형성을 위해서 overriding을 사용 한다.
   client가 부모를 통해서만 자식을 접근하면 client가 주문한 것만 볼 수 있음. 
   자식클래스의 정보의 은닉화를 위해서
</pre>
<div><img width="400px" src="https://user-images.githubusercontent.com/39404179/49280193-df337f80-f4cc-11e8-8d67-6a387530c844.png"></div>
<pre>
 cf) 만약에, stack:부모, heap:부모 만 하면 확장이 안 되므로 참조를 자주 해야 됨.
</pre>

- 추상 클래스
<pre>
추상화, 추상 메소드 (미완성된 메서드)
  => 추상메서드를 가진 클래스는 반드시 추상 클래스야 한다.
    : 추상메서드를 가진 추상 클래스를 상속받으면 
      자식 클래스는 무조건 추상메서드를 재정의 해야 한다. 
  => 추상메서드가 없어도 추상 클래스로 정의 될 수 있다.
    : 추상클래스는 new로 생성될 수 없고 반드시 자식 클래스로 생성
      추상클래스 안에서 새로운 객체를 생성할 수 없음
  => 추상클래스는 일반클래스가 가지는 속성을 모두 가진다.
  => 구체화 할 필요 없이 이름만 준다.
  => 일반 클래스는 강제성이 없음
     추상 클래스는 강제성이 있음
</pre>

# 오버로딩(Overloading)
- 각 메서드의 이름은 같고 인자 값이 다르다.(인자의 순서가 달라도 가능 (String s , int I -> int I , String s)
<pre><code>
    // 메소드 오버로딩: 메소드의 이름을 같게 해둠으로써
    // 메소드의 가독성과 일관성을 보장한다.
    public void draw(int r){
        System.out.println("지름이 "+r+"인 원을 그린다.");
    }
    public void draw(int w, int h){
        System.out.println("너비: "+w+", 높이: "+h+"인 사각형을 그린다.");
    }
    public void draw(String s, int i){
        System.out.println("String :"+ s+",int : "+i);
    }
    public void draw(int i,String s){
        System.out.println("int : "+i+",String :"+ s);
    }
    public void draw(int x, int y, int len){
        System.out.println("좌표 x: "+x+", 좌표 y: "+y);
        System.out.println("길이가 "+len+"인 선을 그린다.");
    }
</code></pre> 

# 오버라이딩(Overriding)
- 상속받아 같은 이름으로 씀

# 싱글톤 패턴 (디자인 패턴)
- static 메모리 구조 파악
- 싱글톤은 다른 소스에서 new로 생성하는 것을 막기위해 기본 생성자를 private으로 선언한다. 그리고 static 형태의 메서드에 객체를 생성하게 하고 그 안에 조건문으로 기존에 들어간 값이 없는지 검사하고 연결 상태인 것이 없다면 객체를 생성해 준다.
디자인 패턴 중 싱글톤은 무조건 객체를 하나만 생성하게 설계된 패턴이다.
<div>
	<img src="https://user-images.githubusercontent.com/39404179/49275791-d1c3c880-f4bf-11e8-80bb-00960c706c23.png">
</div>

# 생성자
 1) 생성자의 이름은 클래스의 이름과 동일해야 한다.
 2) 반환값이 없기 때문에 Return을 사용하지 않는다.
 3) 메서드에
 4) 기본 생성자는 생성하는 시점에서 실행 된다.(초기화 시에)
 
# 인자 전달방식 (Call by Value / Call by Address)
- Call by Value: 값을 인자로 전달받는 방식
- Call by Address: 주소 값을 인자로 전달받는 방식

# 배열
- 배열이란 하나의 값 또는 주소만을 가지고 있는 변수와 달리 여러개의 데이터를 가지고 있다는 차이점이 있다. 
- 배열의 선언
<pre>
  1. 변수 선언과 거의 비슷하며 여러 개의 데이터가 모여 있어 {}를 이용한다.
  2. 배열의 크기는 최초에 한번 설정되면 변경 불가능하다.
  ex) int[] arr = new int[5]
  
하나하나 뜯어보면
int[] => 자료형이 int형인 배열을 만들 것이다.
arr => 그 배열의 이름은 arr 이라고 할것이며
new => heap 영역에 새롭게 공간을 할당하여 만들것이고
int[5] => 5개의 데이터를 가지는 배열을 만들 것이다.
라는 뜻으로 해석할 수 있다.

자료를 넣을 때는
int arr[0] = 10;
int arr[1] = 20;
int arr[2] = 30;
int arr[3] = 40;
int arr[4] = 50;
처럼 하나하나 넣을수도 있고
int arr[] = {10, 20, 30, 40, 50};처럼 한번에 넣을수도 있다.

이렇게 자료형이 미리 정해져 있지 않고 사용자에게서 받을 경우가 있는데 이럴 때는 하나하나 받기보다는 for문을 쓰는 것이 유용하다.

ex)
Scanner scan = new Scanner(System.in); 
for(int I = 0; I <=arr.length ; I++){
	arr[i] = Integer.parseInt( scan.nextLine());
}
여기서 for문안에 .length 라는 메소드는 가급적 안쓰는 것이 좋은데
for(초기식;조건식;증감식)에서 조건식와 증감식은 for문이 한번 돌아갈 때 마다 실행되는 부분이므로 가급적 메소드를 호출하는 것은 피하는 것이 좋다. cpu가 할 일이 늘어 프로그램의 시간비용이 증가하기 때문이다. 같은 기능을 하는 프로그램이고, 정확도마저 둘이 같다면 시간은 줄일수록 좋다.
따라서
Scanner scan = new Scanner(System.in); 
int leng = arr.length;
for(int I = 0; I <= leng ; I++){
	arr[i] = Integer.parseInt( scan.nextLine());
}
으로 바꿔주는 것이 좋다.

jdk 5.0 버전 이후부터는 향상된 포문을 제공하는데
Scanner scan = new Scanner(System.in); 

for(int I  : arr){
	i = Integer.parseInt( scan.nextLine());
}
로 나타낼수 있다.
arr이라는 배열의 첫 값을 I 에게 할당하고 그 후 다음 값으로 계속해서 넘어가다가 arr이 끝나는 부분 즉 null값을 만난다면 for문을 탈출하도록 되어 있다.
arr 자리에 오는 것이 int 형 배열이 아니라 char 라면 int I 또한 char I로 바꿔주어야 한다.

<div><img width="400px" src="https://user-images.githubusercontent.com/39404179/49276162-02583200-f4c1-11e8-9ae1-01f53b4d95db.png"</div>


** String 변수는 char형 배열과 마찬가지이다.
그래서 String 형 1차원 배열은 char의 2차원 배열로 취급할수 있는데 그래서String형 배열을 다룰때는 주의가 필요하다.
ex)
	str[0]="Kosta188"; // 묵시적 생성 = static
        str[1]=new String("Kosta188"); // 명시적 생성 = heap
        str[2]=new String("Kosta188");
        str[3]="Kosta188";
     System.out.println("주소값 비교: "+(str[0]==str[3])); 
     System.out.println("주소값 비교: "+(str[1]==str[2]));

<div><img width="400px" src="https://user-images.githubusercontent.com/39404179/49276220-2fa4e000-f4c1-11e8-9c8a-e875050a1884.png"></div>

= str[0]일 때는 static에 null값이므로 kosta188생성해서 출력
  str[3]일 때는 static에 kosta 188이 이미 존재 하므로 static에 있는 kosta188을 불러오므로 주소값이 같음.
메모리 구조 5개 => str[0], str[3] = String
                   str[1] = String
                   str[2] = String
                   str[4] = String
</pre>


# WrapperClass
- 일반 자료 형을 내부적으로 품고 있는 객체를 제공해 주는 것
<pre>ex) int, boolean, double, ...
	Class Boolean { boolean };</pre>
- 일반 자료 형에 연관되는 메소드 기능을 가지고 있음
<pre>< 생성 방법 >
* AutoBoxing = 참조 자료형
Integer n = 10; => n이 100번지 생성 = WrapperClass로 생성
sout(n);
n.기능 => n.속성/메소드
* UnBoxing = 일반 자료형
Integer n = 10; => n이 100번지 생성 = WrapperClass로 생성
int n2 = n; 
sout(n2);
</pre>
<pre>
기본 자료형 =========> Wrapper 객체 = AutoBoxing ex) Integer n = new Integer(10);
   byte                      Byte
   short                     Short
    int                      Integer
   long                      Long
  float                       Float
 double                     Double
  char                     Character
boolean                     Boolean
  void      <===========    Void    = UnBoxing ex) int n2 = n.intValue( );
</pre>

<pre>
<div><img width="400px" src="https://user-images.githubusercontent.com/39404179/49278350-d7bda780-f4c7-11e8-9726-1dfb901e8c9f.png"></div>
= (1) 언박싱 (Unboxing)
    : Integer 참조 자료형을 int 일반 자료형으로 바꿔서 int ia 일반 자료형에 넣음
  (2) 오토언박싱 (Auto Unboxing)
    : Integer 참조 자료형을 int 일반 자료형으로 바꾸지 않고 int ib 일반 자료형에 넣음
     자동으로 int 일반 자료형으로 바꿔줌
  (3) 박싱 (Boxing)
    : 456를 Integer 참조 자료형으로 바꿔서 Integer ic 참조 자료형에 넣음 
  (4) 오토박싱 (Auto Boxing)
    : ia를 Integer 참조 자료형으로 바꾸지 않고 Integer iD 참조 자료형에 넣음
     자동으로 Integer 참조 자료형으로 바꿔줌
</pre>





cf) visual paradigm = - : private, + : public
