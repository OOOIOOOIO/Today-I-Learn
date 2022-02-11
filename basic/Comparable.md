# Comparable

- &nbsp;Comparable, Comparator 두 인터페이스는 객체를 비교할 수 있도록 만든다. primitive 타입(int, double, byte, ...)의 경우
부등호를 이용해 쉽게 변수를 비교할 수 있다. 하지만 객체는 사용자가 기준을 정해주지 않는 이상 어느 객체가 더 높은 우선순위를
갖는지 알 지 못한다. 따라서 이러한 문제점을 해결하기 위해 나온 개념이 Comparable과 Comparator이다.<br>

- &nbsp;객체에 Arrays.sort 혹은 Collections.srot를 입맛에 맞게 사용하기 위해선 Comparable에서는 comparTo를,omparator에서는 compare를
반드시 재정의 해주어야 한다. 왜냐하면 sort의 작동 방식에서 Comparable과 Comparator을 사용하기 때문이다.<br>

- &nbsp;Comparable은 인터페이스이다. Comparable 안에는 compareTo라는 추상메소드를 "하나" 가지고 있다.
인터페이스 안에 있는 메소드는 무조건 추상 메소드이기 때문에 재정의(overriding)를 해주어야 한다. 

-Comparable은 자기 자신(this)과 파리미터로 들어오는 객체를 비교한다.


# 코드
```java
package util;

import java.util.*;

// Comparable 예시
class Student implements Comparable<Student> { // 클래스이름
	int age;			// 나이
	int classNumber;	// 학급
	
	public Student() {;}
	
	Student(int age, int classNumber) {
		this.age = age;
		this.classNumber = classNumber;
	}
	
	@Override
	public int compareTo(Student o) { // 클래스이름 객체
    
		// 자기 자신의 age가 o의 age보다 크다면 양수
		if(this.age > o.age) { // 자기 자신이기 때문에 this / 파라미터의 객체이기 때믄에 o
			return 1;
		}
		// 자기 자신의 age와 o의 age가 같다면 0
		else if(this.age == o.age) {
			return 0;
		}
		// 자기 자신의 age가 o의 age보다 작다면 음수
		else {
			return -1;
		}
		/* return this.age - o.age; --> 이런식으로 하면 더 좋을 듯하지만 치명적인 함정이 있다.
		 * 	바로 int의 범위이다. int의 범위는 -2^31 ~ 2^31승이다.
		 * 이렇게 - 혹은 + 만으로 comparTo를 구현할 경우
		 * int의 범위 혹은 primitive 형의 범위를 넘어갈 수 있다. 이 때 underflow, overflow가 발생하게 된다.  
		 * 주어진 범위의 하한선을 넘는 것을 underflow
		 * 주어진 범위의 상한선을 넘는 것을 overflow라고 한다. 
		 */
	}
}


public class Comparable_O {
	public static void main(String[] args) {
		Student a = new Student(17,2);
		Student b = new Student(10,3);
		
		int result = a.compareTo(b);
		
		if(result > 0) System.out.println("a객체가 b객체보다 큽니다");
		
		else if(result == 0) System.out.println("a객체와 b객체가 같습니다");
		
		else System.out.println("a객체보다 b객체가 큽니다");
		
		
//		번외
//		이런식으로도 쓸 수 있다. 사실 이런 덩그러니  쓰기는 힘든 것 같다. this 자기 자신을 넣기가 힘듬
//		익명 클래스를 사용할 경우(추상메소드 재정의)
		Comparable<Integer> com = new Comparable<Integer>() {
			
			@Override
			public int compareTo(Integer o) {
				// TODO Auto-generated method stub
				return 0;
			}
		};
		
		
//		바로 사용하는 경우도 가능하다. Comparator는 안되는데 신기하다.
		Comparable<Integer> com2 = null;
		com2 = 3;
		System.out.println(com2.compareTo(4));
		
	
	}
}
```
