 # Nested Class
 - Java 네에서 클래스 변수
 
 
 # 외부 클래스(Outer Class)
 - 내부 클래스를 가지고 있는 클래스
 
 # 내부 클래스(Outer Class)
 - 클래스가 다른 클래스를 포함하는 경우 내부에 포함된 클래스의 명칭이다.
 - 내부 클래스의 객체를 생성하기 위해선 앞서 외부 클래스의 객체가 생성되어야 한다. 
 - 내부 클래스는 정의되는 위치에 따라 멤버 클래스와 지역 클래스로 나뉜다.

 # 익명 클래스(Anonymous Class)
 - 이건 Comparable, Comparator를 통해 이해함
 
 ## 목적
 - 파일 크기의 최소화, 보안, 성능 향상, 이벤트 처리 등을 쉽게 하기 위해 사용한다.
 - 자바 클래스 구조를 조직화하고 소스코드의 작성 효율을 높일 수 있고 캡슐화를 위해 사용한다.

 ## 멤버 클래스
 - 멤버 변수와 동일한 위치에 선언된 클래스 (멤버 변수 == 전역 변수)
 - static 예약어가 붙은 static 멤버와 instance 멤버로 나뉜다.(static을 붙이면 메모리에 바로 올라가기 때문에 모든 곳에서 동일하게 사용할 수 있다.)
 - 동일한 클래스 뿐만 아니라 다른 클래스에서도 접근 가능하다.
 - 클래스의 멤버 변수와 성격이 비슷하다.
 
 ## 지역 클래스
 - 메서드 내에 클래스가 정의되어 있는 경우
 - 지역 클래스(이름이 없는 클래스), 무명 클래스(이름이 없는 클래스)로 나닌다.
 - 활용 범위가 메서드 내부로 제한되는 특징을 가지고 있기에 클래스의 지역 변수와 성격이 비슷하다.

```java
package test;

import test.Outside.Inside;

// 1. instance 멤버 클래스
class Outside{
	public class Inside{
		int a = 10;
		
//		private int a = 10; --> getter setter 만들어 주지 않으면 접근 못 함
	}
}

// 2. static 멤버 클래스
class Outside2{
	static class StaticInside{
		 int b = 20;
//		private int b = 20; --> 마찬가지로 getter setter 만들어 주지 않으면 접근 못 함
	}
}

// 3. 지역 클래스
class Phone{
	void Name(){
		class Music{
			int c = 30;
//			private int c = 30;
		}
	}
}

// 4. 지역(무명) 클래스
abstract class Car{
	public abstract void engineOn();
	public abstract void engineOff();
}



public class TestJava {
	//5. TopLevelClass에서 사용하는 내부 클래스(전역변수처럼 사용)
	class InnerTest{
		private int e = 50;
	}
	
	static class InnerTest2{
		private int f = 60;
	}
	
	public static void main(String[] args) {
//		선언방법
		
		// 1. non-static inner class : 외부 클래스 객체 생성 후, 외부클래스.내부클래스. 객체명 = 외부객체명.new 내부클래스();
		Outside outer = new Outside();
		Outside.Inside inner = outer.new Inside();
		
		// 이렇게 사용하고 싶으면 외부 클래스를 import 해주어야 한다. 설령 import 한다 해도 외부객체명.new 클래스명();을 해주어야 하기 때문에 난 별로다.
		Inside inner2 = outer.new Inside();
		
		System.out.println(inner.a);
		System.out.println(inner2.a);
	
		
		
		// 2. static inner class : 외부클래스.내부클래스 객체명 = new 외부클래스.내부클래스();
		// 다른 식으로 객체화 하는 건 없나보다
		Outside2.StaticInside inner3 = new Outside2.StaticInside();
		
		System.out.println(inner3.b);
		System.out.println(inner3.b);
		
		
		// 5. 외부 클래스의 필드 내에서 쓰는 법
		// 5-1. non-static inner class : 외부 클래스 객체 생성 후, 외부클래스.내부클래스. 객체명 = 외부객체명.new 내부클래스();
		TestJava test = new TestJava();
		TestJava.InnerTest innerTest = test.new InnerTest();
		// 혹은 외부 클래스의 필드 이기 때문에 앞에 외부클래스를 생략해도 좋다.
		InnerTest innerTest2 = test.new InnerTest();
		
		System.out.println(innerTest.e);
		System.out.println(innerTest2.e);
		
		// 5-2. static inner class : 외부 클래스의 필드 내이고 static을 통해 메모리로 올라가서 일반 클래스의 객체를 생성하는 것 처럼 생성한다.
		InnerTest2 staticInnerTest = new InnerTest2();
		
		System.out.println(staticInnerTest.f);
		
		
		
//		번외
		
		// 이렇게 쓰고 싶으면 e를 static으로 선언해 주어야 한다. 외부 클래스는 static으로 사용하지 못한다 public, abstract, final 만 사용 가능
		//System.out.println(TestJava.InnerTest.e);
	}
}
```
