## Generic 이해하기!! 정복하기!!

### Generic 이란?

제네릭(Generic)은 직역하자면 '일반적인'이라는 뜻이다.
'데이터 형식에 의존하지 않고, 하나의 값이 여러 다른 데이터 타입들을 가질 수 있도록 하는 방법'이다.
<br>
<br>
기본적으로 ArrayList같은 것을 생성 할때 어떻게 생성을 하죠?
객체<타입> 객체명 = new 객체<타입>(); 이런식으로 사용을 하게 된다.

```java
ArrayList<Integer> list1 = new ArrayList<Integer>();
ArrayList<String> list2 = new ArrayList<Integer>();

LinkedList<Double> list3 = new LinkedList<Double>():
LinkedList<Character> list4 = new LinkedList<Character>();
```

제네릭(Generic)은 클래스 내부에서 지정하는 것이 아닌 외부에서 사용자에 의해 지정되는 것을 의미한다. 한마디로 특정(Specific) 타입을 미리 지정해주는 것이 아닌 필요에 의해 지정할 수 있도록 하는 일반(Generic) 타입이라는 것이다.

## 장점

1. 제네릭을 사용하면 잘못된 타입이 들어올 수 있는 것을 컴파일 단계에서 방지할 수 있다.
2. 클래스 외부에서 타입을 지정해주기 때문에 따로 타입을 체크하고 변환해줄 필요가 없다. 즉, 관리기가 편하다.
3. 비슷한 기능을 지원하는 경우 코드의 재사용성이 높아진다.

## 사용방법

| 타입 | 설명    |
| ---- | ------- |
| T    | Type    |
| E    | Element |
| K    | Key     |
| V    | Value   |
| N    | Number  |

1. 클래스 및 인터페이스 선언

```java
public class ClassName <T> { ... }
public Interface InterfaceName <T> { ... }

타입을 2개로 설정
public class ClassName <T, K> { ... }
public Interface InterfaceName <T, K> { ... }

public class HashMap <K, V> { ... }
```

```java
public class ClassName <T, K> { ... }

public class Main {
	public static void main(String[] args) {
		ClassName<String, Integer> a = new ClassName<String, Integer>();
	}
}
```

-   객체를 생성할 때 구체적인 타입을 명시해주어야 한다
-   위 예시라면 T는 String이 되고, K는 Integer가 된다.
-   이 때 주의해야 할 점은 타입 파라미터로 명시할 수 있는 것은 참조 타입(Reference Type)밖에 올 수 없다. 즉, int, double, char 같은 primitive type은 올 수 없다는 것이다. 그래서 int형 double형 등 primitive Type의 경우 Integer, Double 같은 Wrapper Type으로 쓰는 이유가 바로 위와같은 이유다.

```java
public class ClassName <T> { ... }

public class Student { ... }

public class Main {
	public static void main(String[] args) {
		ClassName<Student> a = new ClassName<Student>();
	}
}
```

-   사용자가 정의한 클래스도 타입으로 올 수 있다는 것이다.

---

2. 제네릭 클래스

```java
// 제네릭 클래스
class ClassName<E> {

	private E element;	// 제네릭 타입 변수

	void set(E element) {	// 제네릭 파라미터 메소드
		this.element = element;
	}

	E get() {	// 제네릭 타입 반환 메소드
		return element;
	}

}

class Main {
	public static void main(String[] args) {

		ClassName<String> a = new ClassName<String>();
		ClassName<Integer> b = new ClassName<Integer>();

		a.set("10");
		b.set(10);

		System.out.println("a data : " + a.get());
		// 반환된 변수의 타입 출력
		System.out.println("a E Type : " + a.get().getClass().getName());

		System.out.println();
		System.out.println("b data : " + b.get());
		// 반환된 변수의 타입 출력
		System.out.println("b E Type : " + b.get().getClass().getName());

	}
}

a data : 10
a E Type : java.lang.String
b data : 10
b E Type : java.lang.Integer
```

---

제네릭을 2개 쓰고 싶다면

```java
// 제네릭 클래스
class ClassName<K, V> {
	private K first;	// K 타입(제네릭)
	private V second;	// V 타입(제네릭)

	void set(K first, V second) {
		this.first = first;
		this.second = second;
	}

	K getFirst() {
		return first;
	}

	V getSecond() {
		return second;
	}
}

// 메인 클래스
class Main {
	public static void main(String[] args) {

		ClassName<String, Integer> a = new ClassName<String, Integer>();

		a.set("10", 10);


		System.out.println("  fisrt data : " + a.getFirst());
		// 반환된 변수의 타입 출력
		System.out.println("  K Type : " + a.getFirst().getClass().getName());

		System.out.println("  second data : " + a.getSecond());
		// 반환된 변수의 타입 출력
		System.out.println("  V Type : " + a.getSecond().getClass().getName());
	}
}

first data : 10
K E Type : java.lang.String
second data : 10
V E Type : java.lang.Integer
```

---

3. 제네릭 메서드

```java
public <T> T genericMethod(T o) {	// 제네릭 메소드
		...
}

[접근 제어자] <제네릭타입> [반환타입] [메소드명]([제네릭타입] [파라미터]) {
	// 텍스트
}
```

```java
// 제네릭 클래스
class ClassName<E> {

	private E element;	// 제네릭 타입 변수

	void set(E element) {	// 제네릭 파라미터 메소드
		this.element = element;
	}

	E get() {	// 제네릭 타입 반환 메소드
		return element;
	}

	<T> T genericMethod(T o) {	// 제네릭 메소드
		return o;
	}


}

public class Main {
	public static void main(String[] args) {

		ClassName<String> a = new ClassName<String>();
		ClassName<Integer> b = new ClassName<Integer>();

		a.set("10");
		b.set(10);

		System.out.println("a data : " + a.get());
		// 반환된 변수의 타입 출력
		System.out.println("a E Type : " + a.get().getClass().getName());

		System.out.println();
		System.out.println("b data : " + b.get());
		// 반환된 변수의 타입 출력
		System.out.println("b E Type : " + b.get().getClass().getName());
		System.out.println();

		// 제네릭 메소드 Integer
		System.out.println("<T> returnType : " + a.genericMethod(3).getClass().getName());

		// 제네릭 메소드 String
		System.out.println("<T> returnType : " + a.genericMethod("ABCD").getClass().getName());

		// 제네릭 메소드 ClassName b
		System.out.println("<T> returnType : " + a.genericMethod(b).getClass().getName());
	}
}

a data : 10
a E Type : java.lang.String
b data : 10
b E Type : java.lang.Integer
<T> returnType : java.lang.Integer
<T> returnType : java.lang.String
<T> returnType : ClassName
```

-   a객체의 ClassName의 E 제네릭 타입은 String으로 모두 변환된다.
-   b객체의 ClassName의 E 제네릭 타입은 Integer으로 모두 변환된다.
-   genericMethod()는 파라미터 타입에 따라 T 타입이 결정된다.

    -   그럼 위와같은 방식이 왜 필요한가? 바로 '정적 메소드로 선언할 때 필요'하기 때문이다.

-   static 은 무엇인가? 정적이라는 뜻이다. static 변수, static 함수 등 static이 붙은 것들은 기본적으로 프로그램 실행시 메모리에 이미 올라가있다.

---

```java
class ClassName<E> {

	/*
	 * 클래스와 같은 E 타입이더라도
	 * static 메소드는 객체가 생성되기 이전 시점에
	 * 메모리에 먼저 올라가기 때문에
	 * E 유형을 클래스로부터 얻어올 방법이 없다.
	 */
	static E genericMethod(E o) {	// error!
		return o;
	}

}

class Main {

	public static void main(String[] args) {

		// ClassName 객체가 생성되기 전에 접근할 수 있으나 유형을 지정할 방법이 없어 에러남
		ClassName.getnerMethod(3);

	}
}
```

-   제네릭이 사용되는 메소드를 정적메소드로 두고 싶은 경우 제네릭 클래스와 별도로 독립적인 제네릭이 사용되어야 한다는 것이다.

---

```java
// 제네릭 클래스
class ClassName<E> {

	private E element; // 제네릭 타입 변수

	void set(E element) { // 제네릭 파라미터 메소드
		this.element = element;
	}

	E get() { // 제네릭 타입 반환 메소드
		return element;
	}

	// 아래 메소드의 E타입은 제네릭 클래스의 E타입과 다른 독립적인 타입이다.
	static <E> E genericMethod1(E o) { // 제네릭 메소드
		return o;
	}

	static <T> T genericMethod2(T o) { // 제네릭 메소드
		return o;
	}

}

public class Main {
	public static void main(String[] args) {

		ClassName<String> a = new ClassName<String>();
		ClassName<Integer> b = new ClassName<Integer>();

		a.set("10");
		b.set(10);

		System.out.println("a data : " + a.get());
		// 반환된 변수의 타입 출력
		System.out.println("a E Type : " + a.get().getClass().getName());

		System.out.println();
		System.out.println("b data : " + b.get());
		// 반환된 변수의 타입 출력
		System.out.println("b E Type : " + b.get().getClass().getName());
		System.out.println();

		// 제네릭 메소드1 Integer
		System.out.println("<E> returnType : " + ClassName.genericMethod1(3).getClass().getName());

		// 제네릭 메소드1 String
		System.out.println("<E> returnType : " + ClassName.genericMethod1("ABCD").getClass().getName());

		// 제네릭 메소드2 ClassName a
		System.out.println("<T> returnType : " + ClassName.genericMethod2(a).getClass().getName());

		// 제네릭 메소드2 Double
		System.out.println("<T> returnType : " + ClassName.genericMethod2(3.0).getClass().getName());
	}
}

a data : 10
a E Type : java.lang.String

b data : 10
b E Type : java.lang.Integer

<E> returnType : java.lang.Integer
<E> returnType : java.lang.Integer
<T> returnType : ClassName
<T> returnType : java.lang.Double

```
-   제네릭 메소드는 제네릭 클래스 타입과 별도로 지정된다는 것을 볼 수 있다.

---
4. 제한된 Generic과 와일드 카드
```java
<K extends T>	// T와 T의 자손 타입만 가능 (K는 들어오는 타입으로 지정 됨)
<K super T>	// T와 T의 부모(조상) 타입만 가능 (K는 들어오는 타입으로 지정 됨)
 
<? extends T>	// T와 T의 자손 타입만 가능
<? super T>	// T와 T의 부모(조상) 타입만 가능
<?>		// 모든 타입 가능. <? extends Object>랑 같은 의미
```
※ 주의사항 <br>
K extends T와 ? extends T는 비슷한 구조지만 차이점이 있다.
'유형 경계를 지정'하는 것은 같으나 경계가 지정되고 K는 특정 타입으로 지정이 되지만, ?는 타입이 지정되지 않는다는 의미다.

```java
 - Number와 이를 상속하는 Integer, Short, Double, Long 등의
 - 타입이 지정될 수 있으며, 객체 혹은 메소드를 호출 할 경우 K는
 - 지정된 타입으로 변환이 된다.
<K extends Number>
 
 - Number와 이를 상속하는 Integer, Short, Double, Long 등의
 - 타입이 지정될 수 있으며, 객체 혹은 메소드를 호출 할 경우 지정 되는 타입이 없어
 - 타입 참조를 할 수는 없다.
<? extends T>	// T와 T의 자손 타입만 가능
```

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbpS4Bp%2FbtqLcTploFp%2FcTEkLdHVPZW5lnKOvtbS91%2Fimg.png" width="500"><br>

```java
<K extends T>, <? extends T>

<T extends B>	// B와 C타입만 올 수 있음
<T extends E>	// E타입만 올 수 있음
<T extends A>	// A, B, C, D, E 타입이 올 수 있음
 
<? extends B>	// B와 C타입만 올 수 있음
<? extends E>	// E타입만 올 수 있음
<? extends A>	// A, B, C, D, E 타입이 올 수 있음
```
 - extends 뒤에 오는 타입이 최상위 타입으로 한계가 정해지는 것이다.
---
 대표적인 예로는 제네릭 클래스에서 수를 표현하는 클래스만 받고 싶은 경우가 있다. 대표적인 Integer, Long, Byte, Double, Float, Short 같은 래퍼 클래스들은 Number 클래스를 상속 받는다.

즉,  Integer, Long, Byte, Double, Float, Short 같은 수를 표현하는 래퍼 클래스만으로 제한하고 싶은 경우 다음과 같이 쓸 수 있다.
```java
public class ClassName <K extends Number> { ... }

public class ClassName <K extends Number> { 
	... 
}
 
public class Main {
	public static void main(String[] args) {
 
		ClassName<Double> a1 = new ClassName<Double>();	// OK!
 
		ClassName<String> a2 = new ClassName<String>();	// error!
	}
}

```
- Integer는 Number 클래스를 상속받는 클래스라 가능하지만, String은 Number클래스와는 완전 별개의 클래스이기 때문에 에러(Bound mismatch)를 띄운다.
---
```java
<K super T>, <? super T>

<K super B>	// B와 A타입만 올 수 있음
<K super E>	// E, D, A타입만 올 수 있음
<K super A>	// A타입만 올 수 있음
 
<? super B>	// B와 A타입만 올 수 있음
<? super E>	// E, D, A타입만 올 수 있음
<? super A>	// A타입만 올 수 있음
```

```java
public class ClassName <E extends Comparable<? super E>> { ... }
 ```
- 특히 PriorityQueue(우선순위 큐), TreeSet, TreeMap 같이 값을 정렬하는 클래스 만약 여러분이 특정 제네릭에 대한 자기 참조 비교를 하고싶을 경우 대부분 공통적으로 위와 같은 형식을 취한다.

```java
public class SaltClass <E extends Comparable<E>> { ... }
 
public class Student implements Comparable<Student> {
	@Override
	public int compareTo(Person o) { ... };
}
 
public class Main {
	public static void main(String[] args) {
		SaltClass<Student> a = new SaltClass<Student>();
	}
}
```
- 이렇게만 쓴다면 E extends Comparable<E> 까지만 써도 무방하다.
즉, SaltClass의 E 는 Student 이 되어야 하는데, <br> Comparable<Student> 의 하위 타입이어야 하므로 거꾸로 말해 Comparable을 구현해야한다는 의미인 것이다.

- 그러면 왜 Comparable<E> 가 아닌 <? super E> 일까?<br>
잠깐 설명했지만, super E는 E를 포함한 상위 타입 객체들이 올 수 있다고 했다.

- 만약에 위의 예제에서 학생보다 더 큰 범주의 클래스인 사람(Person)클래스를 둔다면 어떻게 될까? 한마디로 아래와 같다면?
```java
public class SaltClass <E extends Comparable<E>> { ... }	// Error가능성 있음
public class SaltClass <E extends Comparable<? super E>> { ... }	// 안전성이 높음
 
public class Person {...}
 
public class Student extends Person implements Comparable<Person> {
	@Override
	public int compareTo(Person o) { ... };
}
 
public class Main {
	public static void main(String[] args) {
		SaltClass<Student> a = new SaltClass<Student>();
	}
}
```
- 쉽게 말하면 Person을 상속받고 Comparable 구현부인 comparTo에서 Person 타입으로 업캐스팅(Up-Casting) 한다면 어떻게 될까?

- 만약 <E extends Comparable<E>>라면 SaltClass<Student> a 객체가 타입 파라미터로 Student를 주지만, Comparable에서는 그보다 상위 타입인 Person으로 비교하기 때문에 Comparable<E>의 E인 Student보다 상위 타입 객체이기 때문에 제대로 정렬이 안되거나 에러가 날 수 있다.

- 그렇기 때문에 E 객체의 상위 타입, 즉 <? super E> 을 해줌으로써 위와같은 불상사를 방지할 수가 있는 것이다.

- 즉, <E extends Comparable<? super E>> 는 쉽게 말하자면 E 타입 또는 E 타입의 슈퍼클래스가 Comparable을 의무적으로 구현해야한다는 뜻으로 슈퍼클래스타입으로 Up Casting이 발생하더라도 안정성을 보장받을 수 있다.

---
이 긴 내용을 한 마디로 정의하자면 이렇다.

"E 자기 자신 및 조상 타입과 비교할 수 있는 E"