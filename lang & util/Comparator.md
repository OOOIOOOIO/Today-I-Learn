# Comparator

- &nbsp;Comparable, Comparator 두 인터페이스는 객체를 비교할 수 있도록 만든다. primitive 타입(int, double, byte, ...)의 경우
부등호를 이용해 쉽게 변수를 비교할 수 있다. 하지만 객체는 사용자가 기준을 정해주지 않는 이상 어느 객체가 더 높은 우선순위를
갖는지 알 지 못한다. 따라서 이러한 문제점을 해결하기 위해 나온 개념이 Comparable과 Comparator이다. Comparator는 import java.util을
해주어야 사용 가능하다.<br>

- &nbsp;객체에 Arrays.sort 혹은 Collections.srot를 입맛에 맞게 사용하기 위해선 Comparable에서는 comparTo를,Comparator에서는 compare를
반드시 재정의 해주어야 한다. 왜냐하면 sort의 작동 방식에서 Comparable과 Comparator을 사용하기 때문이다.<br>


	<Comparator> 	: 	Interface Comparator<T> 	/	java.util --> import 필요 
	
 
- &nbsp;Comparator 또한 인터페이스이다. Comparator 안에는 compare과 equals라는 추상메소드를 "두개" 가지고 있다. Comparator 안에는 많은 메소드들이 있지만 추상메소드로 선언된 것은 저 둘 뿐이다. 
compare과 달리 equals는 오브젝트 타입만 비교 가능하다.<br>


 

# 코드
```java
package util;

import java.util.*;

// Comparator 일반적 예시 
class Student2 implements Comparator<Student2>{
	int age;
	int classNumber;
	
	public Student2() {;}
	
	public Student2(int age, int classNumber) {
		this.age = age;
		this.classNumber = classNumber;
	}
	
	@Override
	public int compare(Student2 o1, Student2 o2) {
		// o1의 학급이 o2의 학급보다 크다면 양수 --> 내림차순
		if(o1.classNumber > o2.classNumber) {
			return 1;
		}
		// o1의 학급이 o2의 학급과 같다면 0
		else if(o1.classNumber == o2.classNumber) {
			return 0;
		}
		// o1의 학급이 o2의 학급보다 작다면 음수 --> 오름차순
		else {
			return -1;
		}
		
//		return o1.classNumber - o2.classNumber;
		/* --> 이런식으로 하면 더 좋을 듯하지만 치명적인 함정이 있다.
		 * 	바로 int의 범위이다. int의 범위는 -2^31 ~ 2^31승이다.
		 * 이렇게 - 혹은 + 만으로 comparTo를 구현할 경우
		 * int의 범위 혹은 primitive 형의 범위를 넘어갈 수 있다. 이 때 underflow, overflow가 발생하게 된다.  
		 * 주어진 범위의 하한선을 넘는 것을 underflow
		 * 주어진 범위의 상한선을 넘는 것을 overflow라고 한다. 
		 */
	}
}


public class Comparator_O{
	// 익명 클래스를 이용하는 방법2 (main함수 밖에서 static으로 선언)
	public static Comparator<Student2> comp2 = new Comparator<Student2>() {

		@Override
		public int compare(Student2 o1, Student2 o2) {

			return o1.classNumber - o2.classNumber;
		}
	};
	
	
	
	public static void main(String[] args) {
		/* Comaparator를 사용하기 위해선 이렇게 객체를 일일히 선언해주어야 하며 사실 a.com~ b.com~을 쓰든
		 상관이 없다. 이 뜻은 일관성이 없다는 말이 된다. 그래서 Compartor를 쓸 때는 익명 클래스를 자주 사용한다.*/
		
		// 익명 클래스를 이용하는 방법 1 (main함수 안에서 non-static으로 선언)
		Comparator<Student2> comp1 = new Comparator<Student2>() {
			@Override
			public int compare(Student2 o1, Student2 o2) {
				
				return o1.classNumber -o2.classNumber;
			}
		};
		
		
		// 일반적으로 일일히 선언하는 방법
		Student2 a = new Student2(10, 2);
		Student2 b = new Student2(20, 4);
		Student2 c = new Student2(30, 6);
		
		// a.compare(a, c) : a객체와는 상관없이 b와 c객체를 비교한다. 
		// 자기 자신과는 상관이 없으므로 a.compare(a, c)도 문제 없이 실행된다.
//		int result = a.compare(b, c);
		
		
		// 익명 클래스를 이용하는 법
		// 익명 클래스를 이용하더라도 비교할 객체는 필요하다!
		int result = a.compare(b, c); // 기본
		int result2 = comp1.compare(b, c); // 익명클래스1
		int result3 = comp2.compare(b, c); // 익명클래스2
		
		System.out.println(result);
		System.out.println(result2);
		System.out.println(result3);
		
		
		//비교하기
		if(result > 0) System.out.println("b객체가 c객체보다 큽니다");
		
		else if(result == 0) System.out.println("b객체와 c객체가 같습니다");
		
		else System.out.println("b객체보다 c객체가 큽니다");
		
		
//		번외
//		Comparator는 Comparable과 달리 익명 클래스를 이용해서 compare 메서드를 override 해주어야만 
//		작동하는 것 같다. Comparator<Integer> com = null; 로 초기화 후 com.compare 해봤는데
//		java.lang.NullPointerException 이 뜬다. static으로 해 주어도 뜬다.
		
	}
}
```
